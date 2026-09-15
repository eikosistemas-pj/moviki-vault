---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, seguranca, firestore, regras, cota, regra-de-ouro, armadilha]
atualizado: 2026-09-15
---

# A sessao da live passa a ser do servidor — 15/09/2026

Fase 1 do achado **A4** de [[P35 - Auditoria de seguranca do Modo Live]], que
fecha de uma vez **A2, A3, B1, B2, B3 e B6** — e entrega a **cota de 2 lives do
teste gratis** decidida em [[P34 - Travas contra abuso do teste gratis]].

Entrega: `moviki-sessao-live-15092026.zip` — **regras v24 + 6 arquivos**.

---

## 1. A divisao que resolve

| Documento | Quem escreve | O que guarda |
| --- | --- | --- |
| `negocios/{uid}/estado/live` | **lojista** (como sempre) | titulo, sacola, destaque, oferta, cupom, brinde — **conteudo** |
| `live_sessoes/{uid}` | **so o Admin SDK** | `ativa`, `whep`, `inicioEm`, `pulsoEm`, `limiteMin`, `entradaId`, `encerradaPor` — **autoridade** |

A pagina publica passa a decidir "esta no ar" e **de onde vem o video** pela
colecao nova. O `moviki/api/live.js` **continua sem poder de escrita** — a conta
de servico dele e so-leitura de proposito, e segue assim: ele chama o robo com
segredo compartilhado.

## 2. A REGRA DE OURO que nasceu aqui, e que quase custou a correcao inteira

> **Regra do Firestore nao tem "deny".** Quando varios `match` casam com o mesmo
> caminho, o acesso e concedido se **qualquer um** permitir. Um `match`
> especifico com `allow write: if false` **nao tira** o que um curinga acima ja
> concedeu.

O desenho original punha a sessao em `negocios/{uid}/estado/liveSessao`. Dentro
de `negocios/{uid}` existe `match /{documento=**}` com escrita para o dono —
**a trava teria virado enfeite**, e o lojista continuaria podendo se declarar no
ar. Por isso a colecao e da **raiz**, onde o curinga nao alcanca.

**De quebra:** a lista de lives no ar vira consulta simples, sem
`collectionGroup` e **sem indice novo no Console**.

## 3. O que cada peca faz

- **`moviki-robo/lib/livesessao.js` (NOVO)** — as quatro portas: `live_abrir`
  (servidor->servidor, com `LIVE_SEGREDO`), `live_pulso`, `live_fechar` e
  `live_adm_fechar`. Entra como **etapa do `api/pontos.js`**, como o
  `lib/checkout.js`, por causa do teto de funcoes da Vercel.
- **O pulso deixou de ser escrita do navegador e virou batida no servidor.** E
  la que o **teto de 60/180 min passa a existir de verdade**: antes era so o
  relogio da tela, e um `nivel.limiteMin=99999` no console fazia a live de uma
  hora durar doze.
- **`moviki/api/live.js`** — depois de conferir plano, bloqueio, beta, aceite e
  termos, abre a sessao no robo. **Falha fechada:** robo mudo, live nao comeca.
- **`moviki-app/eikoadm01.html`** — o encerramento pelo dono passa a chamar
  `live_adm_fechar`. **Sem isso o botao de encerrar pararia de funcionar**, porque
  o estudio deixou de olhar o campo antigo.
- **Cota do teste gratis:** 2 lives, com **carencia de 15 minutos** — reabrir
  dentro dela nao consome cota. Sem a carencia, uma queda de 4G na feira gastaria
  a cota inteira e o lojista ficaria sem teste por causa do sinal. E o estudio
  mostra "esta e a sua live 1 de 2": trava e gatilho de assinatura ao mesmo tempo.

## 4. Regras v24 — tres mudancas

Geradas **sobre o texto copiado do Console** (a v23 estava mesmo publicada;
confirmado em 15/09), letra por letra. Conferido: **chaves 75/75, parenteses
550/550, profundidade final zero**.

1. `live_sessoes/{uid}` — leitura publica, **escrita negada para todos**,
   inclusive dono e admin.
2. `live_cota/{uid}` — leitura so admin, escrita negada.
3. **`liveNoAr(uid)` passa a ler `live_sessoes`.**

⚠️ **O item 3 nao e cosmetico.** O campo `ativa` de `estado/live` passa a ser
sempre `false`. Se a funcao continuasse lendo de la, **o chat da live pararia
para todo visitante, calado** — ele escreve, a regra nega, a tela diz "Nao foi".
`exists()` antes do `get()` porque, sem o documento, `get()` derruba a regra com
erro em vez de negar.

## 5. Ordem de upload

| # | O que |
| --- | --- |
| 0 | **env `LIVE_SEGREDO`** nos DOIS projetos, mesma string, + Redeploy |
| 1 | **regras v24** no Console |
| 2 | `moviki-robo/lib/livesessao.js` (NOVO) |
| 3 | `moviki-robo/api/pontos.js` |
| 4 | `moviki/api/live.js` |
| 5 | `moviki/live.html` |
| 6 | `moviki-app/live.html` |
| 7 | `moviki-app/eikoadm01.html` |

**Marcas:** `2026-09-15-sessao1` nos quatro arquivos de tela e API;
`2026-09-15-livesessao` no `pontos.js`.

⚠️ `moviki-app/live.html` e `eikoadm01.html` foram montados sobre
`2026-09-15-crachafila` e `2026-09-15-conferir`, que era o que estava no GitHub
na hora. Outra conversa subindo esses dois antes = **remontar**, nunca subir por
cima. O sintoma da colisao e **silencio**.

## 6. O teste que prova — FEITO, e passou

Resultado em 15/09/2026, na conta de teste (Enterprise), logada:

| Teste | Esperado | Resultado |
| --- | --- | --- |
| Escrita em `live_sessoes/{uid}` pelo navegador do lojista | negada | **NEGADA** (`permission-denied`) |
| Leitura em `live_sessoes/{uid}` | permitida | **PERMITIDA** (documento existia — a conta ja fez live) |

**A2 esta fechado de verdade**, nao so no papel: o lojista nao consegue se
declarar no ar nem apontar a propria pagina para o video de outro, e a pagina
de quem assiste continua lendo a sessao.

### Como o teste foi feito — e por que nao foi pelo Console

⚠️ **O Console do Firebase TIROU o simulador de regras.** O botao
**"Desenvolver e testar"**, na aba Regras, hoje so oferece o pacote de
emuladores (Cloud Shell ou maquina local) — que e outra coisa. Nao existe mais
o playground de "simular get/update neste caminho".

Duas tentativas que **nao servem** e custaram tempo:
1. **Console do navegador com `setDoc(...)`.** O codigo das telas roda em
   MODULO: `db`, `doc` e `setDoc` existem so la dentro. O comando devolve
   "db is not defined" e nao testa nada.
2. **Procurar o simulador.** Nao existe mais.

**O que funcionou:** uma pagina temporaria, `moviki-app/testeregras.html`,
subida na raiz, aberta logada em `app.moviki.com.br/testeregras.html`. Ela
tenta a escrita e a leitura contra as regras REAIS e mostra o veredito.

⚠️ A pagina **inicializa o App Check** igual as outras telas. Sem isso, TUDO
seria negado e o teste daria um falso "esta protegido" — a escrita apareceria
negada pelo motivo errado.

**A pagina foi apagada do repositorio depois do teste.** Se precisar de novo,
esta guardada no historico do chat. **Este e o metodo para testar regra do
Firestore daqui em diante**, enquanto o Console nao tiver simulador.

## 7. Correcao de um exagero da propria auditoria

O achado **A3** estava mais duro do que os fatos. O painel do dono **ja gravava**
`live_bloqueios` quando o castigo e diferente de zero (`eikoadm01.html:3837`). O
buraco real era menor: so com a opcao **"so encerrar, sem bloquear"** o lojista
voltava ao ar na hora. Registrado aqui para o mapa nao carregar a versao
inflada.

## 7-A. Bateria completa — TUDO PASSOU (15/09/2026)

| # | Teste | Resultado |
| --- | --- | --- |
| 1 | Estudio abre, entra ao vivo, sacolinha, gravar corte | **ok** |
| 2 | Escrita em `live_sessoes` pelo lojista | **negada** |
| 3 | Leitura em `live_sessoes` | **permitida** |
| 4 | **Chat da live** com a transmissao no ar | **ok** — o painel do dono contou a mensagem |
| 5 | **Encerrar pelo painel do dono** | **ok** — o estudio dela mostrou "Sua live foi encerrada pela equipe do Moviki por descumprir as Regras da Live (Outro: teste)" |

O teste 5 e o que prova o **A3 fechado**: o aviso agora nasce de
`live_sessoes.encerradaPor`, escrito pelo servidor — nao mais de um campo que o
proprio lojista apagava no console.

### Ajuste fino visto no teste 5

Depois de encerrada pela moderacao, o botao do estudio ficou em
**"Conectando..."** (vermelho) em vez de voltar para "Entrar ao vivo de novo"
ou dizer "Transmissao encerrada". A camera parou e o motivo apareceu — entao
nao e defeito de seguranca, e de tela. `encerradaPeloMoviki()` para a
transmissao mas nao redefine o rotulo do botao.

## 7-B. Limpeza pendente do teste

- [ ] **Apagar `moviki-app/testeregras.html`** do repositorio.
- [ ] A conta de teste ficou **Enterprise por edicao manual no Console**
      (`periodo: mensal`, vence em 2027). Reverter, ou marcar `origem: teste`.
- [ ] ⚠️ **O painel do dono ja mostra numero de teste como se fosse venda:**
      "Vendido pelo Pix R$ 25,41", "Pedidos pagos 1", "Conversao 50%". Sao os
      pedidos das provas de checkout. Antes de olhar relatorio para decidir
      qualquer coisa, esses registros precisam ser marcados como teste ou
      apagados — senao a primeira leitura de faturamento ja nasce errada.

## 8. Fica para a fase 2

- [ ] A lista **"Lives no ar"** do painel do dono ainda le a colecao `lives`,
      escrita pelo proprio lojista. **B2 so fecha de verdade** quando ela passar
      a usar a acao `live_adm_noar`, que ja existe no robo.
- [ ] B4 (WHEP sem URL assinada), B5 (sem throttle no `api/live.js`), B7 a B13.

## Ligacoes

[[P35 - Auditoria de seguranca do Modo Live]] ·
[[P34 - Travas contra abuso do teste gratis]] · [[A13 - Modo Live]] ·
[[R - Live - Arquitetura e arquivos]] ·
[[ARQ - Token de webhook por subconta e valor reconferido]]
