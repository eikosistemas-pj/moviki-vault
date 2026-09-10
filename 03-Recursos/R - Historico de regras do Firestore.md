---
type: recurso
status: referencia
area: A3 - Dados e Regras
tags: [regra-firestore, dados]
atualizado: 2026-09-10
---

# R — Histórico de regras do Firestore

Substitui a antiga `R - Historico de regras v7 a v15`, cujo nome envelhecia a cada
publicação. **Este nome não muda mais.**

⚠️ **A verdade é o Console do Firebase.** Esta tabela é derivada.

| Versão | Data | O que mudou |
| --- | --- | --- |
| v7 | 26/08 | Coleção `newsletter` + os 4 campos da Fase 2b no `negocioValido` |
| v8 | 26/08 | Métricas por negócio + resumo de avaliações |
| v9 | 26/08 | `expiraEm` (TTL) — **exigia** o campo na criação |
| v10 | 26/08 | `expiraEm` volta a ser **opcional** na criação |
| v11 | 26/08 | Teto de campos alterados vira 3 **só** quando o documento ainda não tem `expiraEm` |
| v12 | 26/08 | `metricas/{uid}/dias` ganhou `|| isAdmin()` no read |
| v13 | 27/08 | Coleção `conversas` + subcoleção `mensagens`. Aditiva. |
| v14 | 27/08 | Os 4 campos do robô e o valor `'bot'` em `conversaCampos` |
| v15 | 27/08 | Coleção `vik_memoria/{uid}` |
| v16 | 28/08 | `configuracoes/sistema` destravado — o `hasOnly` saiu, a validação virou de TIPO |
| v17 | 31/08 | Campo `capa` no `negocioValido` |
| v18 | 02/09 | `aulasVistas` e `aulasEm` no update de `parceiros/{uid}` |
| v19 | 03/09 | Auditoria: `create` do resumo de avaliações fechado para anônimo · comentário limitado a 300 · teto de R$ 5.000 no pedido de saque |
| **v20** | **03/09** | **Coleção `parceiros_publicos/{slug}` — `read: true`, `write: false`. Publicada.** |
| v21 | 05/09 | Campo `aceiteConduta {versao, em}` opcional no update de `parceiros/{uid}`, com forma fechada |
| **v22** | **10/09** | **Campo `videos` no `negocioValido` — lista de `{url, titulo}`, no máximo 6. É a que está publicada.** |

## Por que a v20 existe

A página `moviki.com.br/v/{apelido}` precisa ler algo público para confirmar, na frente
do comerciante, que aquela pessoa é parceira.

**Ler `parceiros/{uid}` está fora de questão: a CHAVE PIX mora naquele documento.**
Regra do Firestore libera o documento **inteiro ou nada** — não existe "libera só estes
campos". Abrir aquela coleção entregaria a chave Pix de todo parceiro a qualquer
visitante.

Então o robô copia, para uma coleção separada, só o que pode ser visto por estranho:
`slug · nome · arroba · desde · treinado · ativo · espelhoEm`. Dinheiro, e-mail e uid
não atravessam. O número de seguidores também não — é dado do parceiro, não credencial
dele.

`write: if false` cobre create, update **e** delete. Quem grava é o Admin SDK do
`moviki-robo` (`lib/espelhoParceiro.js`), que ignora regras — mesmo padrão de
`comissoes`, `pontos` e `vik_memoria`. É isso que impede um parceiro de se declarar
"treinado" ou de reativar sozinho um cadastro suspenso.

Detalhe completo em [[R - Verificacao publica de parceiro]].

## Por que a v21 existe

O **Guia CONAR 2026** trata conteúdo comissionado como publicidade e põe sobre o **anunciante** o dever de informar o divulgador das normas e de monitorar o que ele publica, sob risco de responsabilização **solidária**. Todo parceiro daqui é comissionado.

A videoaula P10 ensina; **este campo registra que o dever de informar foi cumprido**, com versão e data — visualização de vídeo não é prova. A versão fica na chave para o dia em que o compromisso mudar: quem aceitou a 1.0 não conta como tendo aceitado a 2.0, e o painel volta a pedir.

O campo entrou **opcional** e com **forma fechada** (`hasOnly(['versao','em'])`, tamanhos limitados), para não virar depósito de texto qualquer dentro do cadastro do parceiro. Dinheiro, status e slug continuam fora do `hasOnly`: o máximo que um parceiro esperto consegue forjando o campo é liberar os próprios botões de copiar link e baixar crachá — e, ao forjar, grava a declaração de que se comprometeu, **contra ele, não a favor**.

**Ordem obrigatória:** regras antes do `parceiro.html`. Sem o campo no `hasOnly`, o botão "Li e concordo" responde "Não deu certo" para sempre. Mesma armadilha da v18.

## Por que a v22 existe

A página pública ganhou uma faixa de **vídeos** acima da galeria de fotos: o lojista cola o link de um vídeo que ele já postou (YouTube/Shorts, Instagram Reels, TikTok). O Moviki **não hospeda vídeo nenhum** — 30 s de vídeo pesa 15 a 20 MB contra 200 KB de uma foto, e sairia da banda do Storage a cada visita.

`videos` é opcional e limitado a 6 — o teto existe para o documento não estourar e para a faixa não virar rolagem infinita. **A regra não entra dentro de cada item:** regra do Firestore não lê mapa dentro de lista. O filtro de domínio (sempre `https`, só as três redes) é feito no painel ao colar e **de novo** no `404.html` ao publicar, que é quem joga o link dentro de um `href`.

**Ordem obrigatória:** publicar antes do `index.html` `2026-09-10-videos`. `negocioValido` usa `hasOnly` — sem `videos` na lista, **todo** "Salvar tudo" do painel é negado, não só o vídeo. Mesma armadilha da v17.

## As regras de ouro que nasceram deste histórico

**Da v16 —** `hasOnly` em coleção que **só admin** escreve é segurança de mentira: não
barra ninguém que já não estivesse barrado e quebra o painel a cada campo novo. Validar
**TIPO**, nunca conjunto fechado. E `allow write` cobre delete, onde `request.resource`
é **nulo** — a expressão erra e nega. Separar `create, update` de `delete` sempre.

**Da v18 —** publicar a regra **ANTES** do arquivo, quando o arquivo passa a gravar
campo novo. Sem `aulasVistas` no `hasOnly`, o parceiro assistia, a barra andava, e ao
recarregar voltava do zero. **Escrita negada pelas regras falha CALADA.**

**Da v19 —** **regra não é tela.** Todo limite que a tela impõe — tamanho de texto,
valor máximo, "só um por vez" — precisa existir também na regra. Quem chama o Firestore
direto não passa pela sua tela.

**Da v20 —** **documento que mistura dado público com dado sensível pede ESPELHO em
coleção separada.** Não existe meio-termo em regra do Firestore. E a ordem continua
sendo regra: aqui a inversão não quebra nada, só faz a página de verificação dizer
"não existe parceiro" para todo mundo — mentira na tela do comerciante, que é
exatamente o que aquela página existe para evitar.

**Da v21 —** campo que guarda um **compromisso jurídico** entra com forma fechada, não como texto livre. E o que prova o cumprimento de um dever é o **registro do aceite**, com versão e data — nunca o log de que a pessoa viu um vídeo.

**Da v22 —** **regra do Firestore não valida item dentro de lista.** Quando o dado é uma lista de objetos, a regra só garante tipo e tamanho; o que valida cada item é o HTML, e por isso essa validação é **duplicada** — ao gravar e ao publicar. Link que o usuário digita e que vira `href` sem lista fechada de domínios é `javascript:` executando na página do cliente dele.

**Da entrega da v22 —** **antes de entregar qualquer regra, pedir a ATUAL a ele.** O `.txt` guardado no Project estava na v19 enquanto o ar já tinha v20 e v21: a primeira versão da entrega foi montada sobre a v19 e **teria apagado as duas**. O Console é a verdade; arquivo salvo não é prova.

## Cópias publicadas guardadas no Project

`claude/moviki-regras-firestore-PUBLICADAS-v9.txt` · `v10` · `v11` · `v12` · `v13` ·
`v17` · `v18` · `v19` · `v20` · **`claude/moviki-regras-firestore-v22.txt`**

⚠️ **A v21 não tem cópia isolada no Project.** Ela está inteira dentro do arquivo da v22, que é aditivo e traz o cabeçalho de cada versão desde a v14.

Regras do **Storage** desde 27/08: `claude/moviki-regras-storage-v1.txt`.

## Estados que toda regra nova precisa cobrir

1. Documento **antigo**, sem o campo.
2. Documento **em transição**, ganhando o campo. **É onde tudo quebra.**
3. Documento **novo**, já com o campo.

## Ligações

[[A3 - Dados e Regras]] · [[R - Colecoes do Firestore]] · [[R - Regras de ouro]] · [[R - Verificacao publica de parceiro]] · [[P14 - Verificacao de parceiro]] · [[ARQ - Auditoria de seguranca 03092026]] · [[ARQ - Conduta do divulgador no ar]] · [[ARQ - Galeria de videos na pagina publica]]
