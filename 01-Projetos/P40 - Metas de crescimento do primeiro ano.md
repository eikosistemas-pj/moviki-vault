---
type: projeto
status: ativo
prioridade: 1
prazo: 2027-09-16
area: A4 - Financeiro
tags: [metas, projecao, crescimento, faturamento, churn, cac]
atualizado: 2026-09-16
---

# P40 - Metas de crescimento do primeiro ano

> Projecao de 12 meses entrando **50 lojistas pagantes por mes**, com os custos
> reais do painel e o preco novo. Grafico: `projecao12meses.png`.

Relacionado: [[ARQ - Decisao de preco antes do lancamento 16092026]] ·
[[R - Sustentabilidade e custo de escala]] ·
[[P37 - Prospeccao de parceiros e influenciadores]] ·
[[P39 - Remuneracao do influenciador e midia dos parceiros]]

---

## Correcao importante: o Vik NAO e de graca

O Vik de producao **nao roda dentro da assinatura do Claude**. Ele chama a
**API da Anthropic** com uma chave propria — `ANTHROPIC_API_KEY`, do
`console.anthropic.com`, guardada nas envs do projeto `moviki-ai`. Esta escrito
no proprio `lib/anthropic.js` e no `CLAUDE.md` do repo.

Assinatura do claude.ai e API sao **contas e faturas diferentes**. Uma paga o
trabalho de construir; a outra paga cada resposta que o Vik da para um lojista.

**Quanto custa:** modelo `claude-haiku-4-5`, ~US$ 0,004 por resposta, com teto de
**40 respostas por conta por dia** (`CHAT_LIMITE_DIA`). A 10 respostas por lojista
por mes, sao **R$ 0,22 por lojista** — com 460 lojistas, cerca de **R$ 100/mes**.
Pequeno, mas **cresce com a base** e ja esta somado na projecao abaixo.

> **O que e de graca e o Vik ter sido construido aqui. Cada resposta que ele da
> em producao e cobrada.** A boa noticia: o teto por conta ja existe, entao uma
> conta sozinha nao consegue torrar a chave.

## Premissas da projecao

| | |
| --- | --- |
| Entrada | 50 lojistas pagantes novos por mes |
| Saida (churn) | 5% da base por mes |
| Mix | 60% Pro · 30% Premium · 10% Enterprise |
| Preco | Pro 39,90 · Premium 69,90 · Enterprise 129,90 |
| Ticket medio | R$ 57,90 |
| Margem media por cliente | **R$ 44,43** |
| Imposto | 6% sobre a receita bruta |
| Comissao de parceiro, nivel 1 | **15,3% medio**, em metade dos clientes (ver a escada abaixo) |
| Comissao de nivel 2 | 7,5% do 1o pagamento, em 40% dos clientes de parceiro |
| Comissao de nivel 3 | 5% do 1o pagamento, em 15% dos clientes de parceiro |
| Bonus de marco | R$ 25 a cada parceiro que cruza o degrau Prata |
| Tarifa Asaas | R$ 2,00 por cobranca |
| Video | Premium 1.200 min/mes · Enterprise 3.000 min/mes |
| Custo fixo | R$ 1.755, mais R$ 300 a cada 200 lojistas |

## Os 12 meses

| Mes | Ativos | Receita | Custo | Lucro | Acumulado |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 1 | 50 | R$ 2.895 | R$ 2.513 | R$ 382 | R$ 382 |
| 2 | 98 | R$ 5.645 | R$ 3.174 | R$ 2.471 | R$ 2.853 |
| 3 | 143 | R$ 8.258 | R$ 3.796 | R$ 4.462 | R$ 7.314 |
| 4 | 185 | R$ 10.740 | R$ 4.388 | R$ 6.352 | R$ 13.667 |
| 5 | 226 | R$ 13.098 | R$ 5.249 | R$ 7.849 | R$ 21.515 |
| 6 | 265 | R$ 15.338 | R$ 5.783 | R$ 9.555 | R$ 31.070 |
| 7 | 302 | R$ 17.466 | R$ 6.290 | R$ 11.176 | R$ 42.247 |
| 8 | 337 | R$ 19.488 | R$ 6.772 | R$ 12.716 | R$ 54.963 |
| 9 | 370 | R$ 21.409 | R$ 7.229 | R$ 14.179 | R$ 69.142 |
| 10 | 401 | R$ 23.233 | R$ 7.964 | R$ 15.269 | R$ 84.411 |
| 11 | 431 | R$ 24.966 | R$ 8.377 | R$ 16.590 | R$ 101.001 |
| **12** | **460** | **R$ 26.613** | **R$ 8.769** | **R$ 17.844** | **R$ 118.845** |

**Faturamento do ano: R$ 189.150. Lucro acumulado: R$ 118.845.**

⚠️ **12 x 50 nao da 600.** Com 5% de saida por mes, a base fecha em **460**. O
churn nao aparece no discurso de ninguem e e ele que decide o tamanho do ano.

## O Programa de Parceiros inteiro, dentro da conta

A primeira versao deste documento tinha **so o nivel 1**. Refeito com a escada
completa:

| O que | Como entra | Custo no ano |
| --- | --- | ---: |
| **Nivel 1** | recorrente, todo mes, sobre a base vinda de parceiro | R$ 13.200 |
| **Escada de niveis** | 15% no Bronze e Prata, 16% do Ouro para cima — media de **15,3%** | +R$ 473 |
| **Nivel 2** | 7,5%, **uma vez**, no 1o pagamento | +R$ 521 |
| **Nivel 3** | 5%, **uma vez**, no 1o pagamento | +R$ 130 |
| **Bonus de marco** | R$ 25 / 50 / 150 / 300, uma vez por degrau, por parceiro | +R$ 239 |
| **TOTAL** | | **R$ 15.360** |

**O programa inteiro custa R$ 1.174 a mais no ano do que a conta anterior — 0,98%
do lucro.** A razao e estrutural, e vale ficar registrada:

> **O nivel 1 e recorrente; os niveis 2 e 3 sao pagos UMA vez, sobre o primeiro
> pagamento.** Um bonus unico de 7,5% sobre uma mensalidade nao se compara a uma
> comissao de 15% que volta todo mes. O que parece "comissao de tres niveis"
> custa, na pratica, quase o mesmo que a de um nivel so.

### O pior caso, para nao restar duvida

100% dos clientes vindos de parceiro, **todos** com nivel 2 e nivel 3 na cadeia,
e a comissao de nivel 1 no teto de **18%** (Esmeralda):

| | Lucro no mes 12 | Acumulado no ano |
| --- | ---: | ---: |
| Cenario da tabela | R$ 17.844 | R$ 118.845 |
| **Pior caso possivel** | **R$ 14.802** | **R$ 95.815** |

**Cabe na margem com folga.** E esse pior caso so acontece se o programa der
muito certo — 100% de aquisicao por parceiro e parceiros no topo da escada. O
custo maior chega junto com o volume que o gerou.

### O mesmo ano com o preco de hoje

| | Preco novo | Preco de hoje |
| --- | ---: | ---: |
| Faturamento do ano | R$ 189.150 | R$ 155.828 |
| Lucro acumulado | R$ 118.845 | R$ 90.186 |

**A mudanca de preco vale R$ 28.659 no primeiro ano** — e o trabalho de venda e
exatamente o mesmo.

## A conta que falta na projecao: o custo de trazer os 50

A tabela acima assume que os 50 clientes aparecem com os R$ 200/mes de midia que
estao no painel hoje. **Nao vao.** Com o teto de aquisicao de R$ 92 por cliente
(payback em 3 meses), 50 clientes custam R$ 4.600 por mes.

| Custo por cliente | Aquisicao/mes | Lucro no mes 12 | Acumulado no ano | Meses no vermelho |
| ---: | ---: | ---: | ---: | --- |
| R$ 0 (so a pe e parceiro) | R$ 0 | R$ 17.844 | R$ 118.845 | nenhum |
| R$ 40 | R$ 2.000 | R$ 15.844 | R$ 94.845 | mes 1 |
| R$ 60 | R$ 3.000 | R$ 14.844 | R$ 82.845 | meses 1 e 2 |
| R$ 92 (o teto) | R$ 4.600 | R$ 13.244 | R$ 63.645 | meses 1 a 3 |

**O negocio se paga em qualquer um dos quatro.** O que muda e o tamanho do
buraco inicial: no pior caso sao tres meses no vermelho antes de virar.

## O funil que 50 pagantes por mes exige

| Conversao teste -> pago | Cadastros/mes | Por dia |
| ---: | ---: | ---: |
| 15% | 333 | 11 |
| 20% | 250 | 8 |
| 30% | 167 | 6 |

> **E aqui que a projecao encosta na realidade.** Hoje sao **zero** cadastros em
> nove dias de anuncio. A barreira nao e a margem, nao e o custo e nao e o
> imposto: e o topo do funil. Todo o resto deste documento ja esta resolvido no
> papel.

## As metas, por trimestre

| Marco | Quando | O que significa |
| --- | --- | --- |
| **Primeiro lojista pagante real** | mes 1 | o dado que nao existe hoje e destrava todo o resto |
| **50 ativos** | fim do mes 1 | a operacao passa a se pagar |
| **143 ativos · lucro de R$ 4.500/mes** | fim do trimestre 1 | da para reinvestir em midia sem tirar do bolso |
| **265 ativos · lucro de R$ 9.650/mes** | fim do semestre | o programa de parceiros comeca a girar sozinho |
| **370 ativos · lucro de R$ 14.300/mes** | fim do trimestre 3 | cabe pro-labore de verdade na conta |
| **460 ativos · R$ 26.600/mes de receita** | fim do ano | R$ 119 mil acumulados |

### O indicador que vale mais que todos

**Churn.** A 5% ao mes, a base fecha o ano em 460. A **8%**, fecha em ~390 — 70
lojistas a menos sem nenhuma venda a menos. Medir a saida mes a mes desde o
primeiro cliente e mais importante que comemorar entrada.

## Pendencias

- [ ] Ler no `console.anthropic.com` o gasto real da API do Vik e por a linha no
      painel, separada da assinatura
- [ ] Decidir o preco (o ano inteiro depende disso, e a janela fecha no
      lancamento)
- [ ] Definir o orcamento mensal de aquisicao — a projecao assume R$ 0 a R$ 4.600
- [ ] Medir a conversao teste -> pago a partir do primeiro cliente real
- [ ] Medir quantos clientes vem com nivel 2 e 3 na cadeia — hoje sao 40% e 15% de estimativa
- [ ] Refazer esta projecao com **dado medido** depois de 60 dias de venda
