---
type: arquivo
status: concluido
area: "[[A13 - Modo Live]]"
tags: [seguranca, checkout, api, vercel]
atualizado: 2026-09-14
---

# Portas separadas do checkout — 14/09/2026

Fecha o achado **A7** de [[ARQ - Auditoria de seguranca do dinheiro 14092026]].
Continuacao de [[ARQ - Checkout em dois modos 14092026]].

## O problema

Desde 11/09 o `api/pontos.js` atendia dois publicos no mesmo arquivo: lojista
logado e visitante anonimo. Nao foi descuido — o plano Hobby limitava o projeto
a 12 funcoes e empilhar era a unica saida. Arquivo com dois publicos e onde
erro de autorizacao nasce.

Com o Vercel Pro assinado em 14/09, o teto acabou.

## O que mudou

| Repositorio | Arquivo | Marca | Tipo |
|---|---|---|---|
| moviki-robo | `api/pedido.js` | 2026-09-14-porta1 | NOVO |
| moviki-robo | `api/financeiro.js` | 2026-09-14-porta1 | NOVO |

- **`api/pedido.js`** — porta publica. So aceita acoes `compra_*`. Sem login,
  porque quem compra e visitante; as barreiras sao as do `lib/checkout.js`.
  CORS aceita o app e o site (com e sem www).
- **`api/financeiro.js`** — porta do lojista e do dono. So aceita `loja_*` e
  `adm_*`, todas com idToken. CORS so do painel.

O `api/pontos.js` **nao muda** e continua aceitando as mesmas acoes: a pagina da
live no ar ainda aponta para la. As portas novas sao para as telas novas.

## Armadilha achada no teste

O `lib/checkout.js` reescreve o cabecalho `Access-Control-Allow-Origin` com a
lista dele, que inclui o site. Se o `api/financeiro.js` apenas delegasse, uma
chamada vinda de `moviki.com.br` sairia com o CORS **afrouxado** — justamente o
que a porta queria fechar.

Conserto: a porta do lojista recusa com 403 qualquer Origin diferente de
`app.moviki.com.br` ANTES de delegar. Requisicao sem Origin (fora do navegador)
passa, porque ali quem protege e o idToken, nao o CORS.

## Testado fora do ar

13 verificacoes: acao trocada de porta, GET, preflight, ausencia de idToken,
origem estranha nao ecoada no CORS, CORS nao afrouxado pela delegacao, e a
resposta do painel sem chave crua.

## Firestore

Nenhuma regra nova. As duas portas escrevem pelo Admin SDK, e as colecoes do
Financeiro (`recebimento`, `financeiro_trilha`, `webhook_eventos`) nao tem match
nas regras de proposito.
