---
type: arquivo
status: concluido
area: "[[A1 - Produto e Paineis]]"
tags: [painel-lojista, sku, cardapio, pedido, aviso, icones, entrega]
atualizado: 2026-09-15
---

# ARQ - Sku e aviso de pedido no painel 15092026

Fecha as tres pontas que dependiam do `index.html`. Continua
[[ARQ - Aviso de pedido ao lojista 15092026]],
[[ARQ - Icones 3D do painel do lojista 15092026]] e
[[ARQ - Cardapio compravel na pagina publica 14092026]].

## Arquivos

| Repositorio | Arquivo | Marca | Tipo |
|---|---|---|---|
| moviki-app | `index.html` | 2026-09-15-sku-aviso | SUBSTITUI |

Montado sobre a marca `2026-09-14-financeiro2`, que era a que estava no GitHub.
**Os cinco PNG de `icones/` precisam subir ANTES** — sem eles os tres cartoes
ficam vazios (o `onerror` esconde a imagem que nao existe).

## 1. Os icones entraram

Financeiro (cartao **e** menu), Mensagens e Tutoriais deixaram de ser SVG de
linha e passaram a `<img src="icones/*.png">` com o mesmo `onerror` que o resto
do painel usa. Nenhum SVG de linha sobrou na grade nem no menu — conferido por
teste, que conta os elementos.

## 2. O `sku` do produto

O pedido vindo do cardapio publico precisa dizer **ao servidor** qual item o
cliente escolheu. Sem id estavel, o `acharNoCardapio` do robo cai no nome
normalizado: funciona, mas dois produtos de mesmo nome em categorias diferentes
casam com o primeiro, e renomear um item aponta o pedido para o vazio.

O sku nasce no save do painel e **nao muda nunca mais**. Por isso ele viaja no
DOM (`r._sku`) do carregamento ate o proximo save: se o `lerCardapio` gerasse um
novo a cada vez, o id deixaria de ser estavel e nao serviria para nada. Seis
caracteres de um alfabeto **sem l, o, 0 e 1** — o sku vai parar em log e em
relatorio, e esses quatro sao os que se confundem lendo.

Duplicata dentro do mesmo negocio e pior que sku nenhum (o servidor casaria com
o primeiro que achasse). So acontece se o lojista duplicar uma linha na tela, e
e resolvida no proprio save, por um conjunto de usados.

**Nenhuma regra nova do Firestore.** `negocioValido()` valida o TAMANHO da lista
`cardapio`, nunca o conteudo de cada item — regra do Firestore nao le mapa
dentro de lista. Campo novo dentro do produto passa livre, do mesmo jeito que
`descricao` passou em 20/08. A v24 continua sem existir, e agora sem motivo para
existir: `vendaAtiva` tambem nao e necessario, porque o interruptor de verdade e
o `checkout_publico/{uid}.ativo`, escrito pelo Admin SDK.

## 3. Aviso de pedido dentro do painel

O e-mail cobre o lojista de porta fechada. Isto cobre o contrario: painel aberto
numa aba enquanto ele trabalha em outra.

- **Som curto, sintetizado na hora** (WebAudio, dois bipes). Arquivo de audio
  significaria mais um arquivo no repositorio, mais um host na CSP e mais um
  jeito de falhar. Tudo em `try/catch`: aviso que nao toca nao pode derrubar a
  lista de vendas.
- **Contador no titulo da aba** — `(2) Moviki — Painel...` —, que e o unico
  lugar que ele enxerga sem estar olhando para a tela.
- **A primeira carga nunca avisa.** O `onSnapshot` entrega todos os pedidos de
  uma vez ao abrir; sem esse cuidado, o painel gritaria a cada login com o
  historico inteiro. A primeira leva vira so o ponto de partida.
- **So conta o que exige acao dele**: pedido que nasceu, e comprador que avisou
  que pagou. Mudanca de status feita pelo proprio lojista nao vira aviso.
- **Zera sozinho** quando ele abre a aba Financeiro, ou quando volta para a aba
  do navegador ja estando nela. Em qualquer outra secao o contador fica — e ali
  que ele serve.

## Conferido fora do ar

26 verificacoes no Chromium, com Firebase de mentira e o save interceptado,
todas passando: os quatro pontos de icone · o cardapio salvando com sku em todo
produto · **sku vindo do banco preservado** · dois saves seguidos devolvendo os
MESMOS sku · produto novo ganhando o seu sem mexer nos outros · duplicata
desfeita no save · primeira carga em silencio · `(1)` e `(2)` no titulo · o
lojista confirmando nao contando como novidade · o contador zerando ao abrir o
Financeiro e voltando a contar depois · o som disparando uma vez · nenhum erro
de JavaScript.

Sintaxe do modulo principal valida, balanceamento de `<div>` identico ao do
arquivo original, e o arquivo entregue com **BOM + CRLF** — sem isso o navegador
do Paulo bloqueia HTML com script dentro.

## O que ficou de fora, e por que

A **tela de escolha de canal** (e-mail / Telegram / SMS) nao entrou. Escolher
canal so faz sentido quando existe mais de um, e hoje existe um. O e-mail fica
sempre ligado — alem de avisar, e o registro de que o Moviki avisou.

- **SMS: recusado.** R$ 0,08 a R$ 0,15 por mensagem. Tres avisos por pedido com
  20 pedidos por dia dao R$ 144 a R$ 270 por mes, por lojista, contra uma
  mensalidade Premium de R$ 49,90. Mesmo no cenario fraco — 1 aviso, 5 pedidos
  por dia — sao R$ 12 a R$ 22 por mes, entre 24% e 45% da mensalidade so em
  notificacao.
- **Web Push** e o substituto certo: custo zero, chega na tela de bloqueio com o
  painel fechado, que e o que o SMS entregaria. Android e computador direto; no
  iPhone o lojista precisa adicionar o painel a tela de inicio uma vez.
- **Telegram** entra depois, com vinculo de um clique
  (`t.me/<bot>?start=CODIGO`), e exige um endpoint novo no `moviki-robo` para o
  webhook do bot.
