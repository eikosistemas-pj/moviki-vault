---
type: recurso
status: referencia
area: A3 — Dados e Regras
tags: [regra-firestore, dados]
atualizado: 2026-09-03
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

## Cópias publicadas guardadas no Project

`claude/moviki-regras-firestore-PUBLICADAS-v9.txt` · `v10` · `v11` · `v12` · `v13` ·
`v17` · `v18` · `v19` · **`v20`**

Regras do **Storage** desde 27/08: `claude/moviki-regras-storage-v1.txt`.

## Estados que toda regra nova precisa cobrir

1. Documento **antigo**, sem o campo.
2. Documento **em transição**, ganhando o campo. **É onde tudo quebra.**
3. Documento **novo**, já com o campo.

## Ligações

[[A3 - Dados e Regras]] · [[R - Colecoes do Firestore]] · [[R - Regras de ouro]] · [[R - Verificacao publica de parceiro]] · [[P14 - Verificacao de parceiro]] · [[ARQ - Auditoria de seguranca 03092026]]
