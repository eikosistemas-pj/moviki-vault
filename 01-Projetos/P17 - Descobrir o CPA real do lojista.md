---
type: projeto
status: ativo
prioridade: 1
prazo: 2026-09-30
area: A7 - Aquisicao e Midia Paga
tags: [meta-ads, capi, medicao, aquisicao, cpa]
atualizado: 2026-09-10
---

# P17 - Descobrir o CPA real do lojista

> Era `P14` na fila represada de 05/09. Renumerado: `P14` ja existe no vault desde
> 03/09 ([[P14 - Verificacao de parceiro]]).

Descobrir quanto custa, de verdade, trazer um lojista cadastrado — e depois um
lojista pagante. Sem esse numero nao existe decisao de verba: qualquer conta hoje
usa referencia de mercado, nao dado do Moviki.

## Por que ainda nao ha numero

**Zero lojistas de verdade.** Todos os cadastros no sistema sao testes do proprio
Paulo; o unico cadastro verdadeiro e o do parceiro Alexandre. Logo **nao existe
taxa de teste gratis para pago medida**.

## O que ja esta pronto para medir

- `mvmetrica.js` captura o `fbclid` nos dois repos
- `lib/meta.js` manda fbc, fbp e IP, e `api/novo-cliente.js` repassa o fbc —
  **conferido no repositorio em 10/09: a revisao de 05/09 esta no ar**, com
  timeout de 6 s no cadastro (o Purchase fica em 2,5 s, contrato do webhook do
  Asaas intacto) e a linha do resultado da medicao no aviso do Telegram
  (`enviada`, `sem env`, `recusada HTTP xxx`, `tempo esgotado`)
- **CAPI confirmada funcionando** em 05/09: 2 eventos Lead no conjunto
  `2114417739495816`, qualidade de correspondencia 7,7/10
- Cadeia do fbc provada ponta a ponta com cadastro de teste: a landing, o salto de
  dominio, o wrapper de fetch e o `novo-cliente.js`

## Estado da campanha no Meta

`Moviki | Cadastro de lojista | Joao Pessoa | set-2026` · **R$ 10/dia**,
otimizando por LANDING_PAGE_VIEWS · **so o anuncio B ativo** (o A promete
descoberta — "aparece no mapa e o cliente te acha" — e o produto ainda nao entrega
isso em cidade com pouca gente no mapa) · teto **R$ 250 a partir de 05/09** ·
gatilho de parada: **R$ 120 sem nenhum cadastro**. Os R$ 43,20 gastos antes nao
entram no teto: foram com anuncio quebrado e sem medicao confirmada.

> **NAO MEXER em verba, publico nem criativo.** Cada mudanca reinicia o
> aprendizado do conjunto e queima dias de dado ja pagos.

## Pendencias

- [ ] **Ler o gasto acumulado desde 05/09** e conferir contra o gatilho de R$ 120
- [ ] **Tirar o `META_TEST_CODE` da Vercel.** Enquanto a variavel existir, o
      evento nao conta como conversao de verdade — e ha verba rodando
- [ ] Apagar a conta de teste `eikovida2021@gmail.com` pelo `eikoadm01.html`
- [ ] `Purchase` sem `fbc`: o `lib/meta.js` ja aceita o campo; falta o
      `criar-assinatura.js` gravar em `faturamento/{uid}` e o `webhook.js`
      repassar
- [ ] Copy dos anuncios do Meta alinhada ao posicionamento de 07/09 —
      ver [[ARQ - Posicionamento e home reescrita 07092026]]

## Licoes que ficaram

- **A Visao geral do Gerenciador de Eventos demora horas**, apesar de prometer 30
  minutos. Para conferir envio na hora, usar a aba **Eventos de teste**.
- **Log sem erro e ambiguo:** o `lib/meta.js` so grava `console.error` em falha —
  silencio significa sucesso **ou** envio nao tentado.
- **Lead de teste com `fbclid` inventado nao aparece em `actions_lead` da
  campanha**, so no Gerenciador de Eventos do conjunto. Confundir os dois faz
  parecer que falhou.

## Ligacoes

[[A7 - Aquisicao e Midia Paga]] · [[A6 - Medicao e Analytics]] ·
[[P01 - Aquisicao - campanha de trafego pago]] · [[P21 - Google Ads campanha de pesquisa]]
