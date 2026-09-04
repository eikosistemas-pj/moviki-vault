---
type: projeto
status: em andamento
area: A7 — Midia paga
tags: [meta-ads, cpa, caixa, medicao]
prioridade: alta
prazo: 2026-09-25
atualizado: 2026-09-04
---

# P14 — Descobrir o CPA real do lojista com teto de R$ 250

## O objetivo desta rodada nao e vender. E descobrir um numero.

Quanto custa um cadastro de lojista vindo de anuncio. Sem esse numero nao da pra
decidir nada: nem escalar, nem parar, nem mexer na oferta.

## Base de calculo (campanha de Joao Pessoa, 02–04/09)

- R$ 33,06 → 75 visitas na pagina de destino = **R$ 0,44 por visita**
- Com R$ 20/dia: ~45 visitas/dia
- Cadastros: 0 em 75 — com o anuncio quebrado. Estatisticamente so diz que a
  taxa esta entre 0% e ~4%.

## Custo de cada nivel de certeza

| Quero saber | Cadastros | Custo | Prazo a R$ 20/dia |
| --- | --- | --- | --- |
| A medicao funciona | 1 | R$ 0 (cadastro de teste) | hoje |
| Ordem de grandeza do CPA | 5 | R$ 110 – 220 | 6–11 dias |
| CPA utilizavel (±32%) | 10 | **R$ 220 – 440** | 11–22 dias |
| CPA confiavel (±20%) | 25 | R$ 550 – 1.100 | 28–55 dias |

## Decisao: teto de R$ 250 e gatilho de parada em R$ 120

**Se em R$ 120 (~270 visitas) nao vier NENHUM cadastro, a midia para.**
Esse resultado ja e o dado: taxa abaixo de 1%, e o problema nao e o anuncio —
e a landing ou a oferta. Continuar comprando trafego nao conserta isso.

## O teto de CPA que o caixa aguenta

Plano Pro R$ 37,90/mes, trial de 30 dias sem cartao.

Com trial→pago de 15% (referencia de mercado para SaaS SMB com trial sem cartao,
NAO e dado do Moviki), cada cliente pagante custa 6,7 cadastros:

| CPA do cadastro | Custo por pagante | Payback |
| --- | --- | --- |
| R$ 22 | R$ 147 | 3,9 meses |
| R$ 44 | R$ 293 | 7,7 meses |

**Teto pratico: CPA de cadastro ate ~R$ 25.** Acima disso a midia paga nao fecha
no caixa de hoje, e o gargalo passa a ser oferta, nao trafego.

**Numero que falta:** quantos lojistas entraram no trial ate hoje e quantos
viraram pagantes. Esse dado do Moviki vale mais que a referencia de mercado.

## Fase 3 original foi RETIRADA

A proposta era campanha OUTCOME_LEADS otimizando por `Lead`, com R$ 60–80/dia.
**Errada para este caixa.** Otimizar por `Lead` exige 50 conversoes/semana pra
Meta sair do aprendizado — com CPA de R$ 22 isso e **R$ 1.100 por semana**.
Conjunto preso em aprendizado entrega caro e instavel: seria pior que hoje.

## O que foi feito no lugar, custo zero — 04/09/2026

- Objetivo de otimizacao do conjunto `Joao Pessoa + 25km | 25-60 | Site`
  (`120251100289180770`) trocado de cliques para **LANDING_PAGE_VIEWS**.
  A Meta passa a comprar quem carrega a pagina, nao quem toca sem querer.
  45 visitas/dia e volume de sobra: o aprendizado fecha em 2–3 dias.
- Verba mantida em R$ 20/dia.
- Os dois criativos ficam no MESMO conjunto. Com 10 conversoes no horizonte
  inteiro nao existe A/B por conversao — A e B se comparam por CPC e por taxa
  visita/clique, que tem volume. A/B formal so quando houver verba.
- O `Lead` continua **medido** pela CAPI, so nao e o alvo da otimizacao.
  E assim que se descobre o CPA gastando pouco.

## Regra que nasce daqui

**Otimizar por um evento que voce nao consegue gerar 50 vezes por semana e pior
do que nao otimizar por ele.** O conjunto nunca sai do aprendizado, o CPM sobe e
a entrega fica instavel. Com caixa curto, otimiza-se pelo evento mais frequente
do funil e mede-se o evento raro.

## Proximo passo

Cadastro de teste real (custo zero) para fechar o ultimo elo: confirmar que o
`Lead` chega na Meta **com fbc**. So depois disso o relogio dos R$ 250 comeca.

→ [[ARQ - Atribuicao do Lead ao anuncio - fbc e fbp]] · [[ARQ - Anuncios com marcacao vazada no ar]] · [[A7 - Midia paga]]
