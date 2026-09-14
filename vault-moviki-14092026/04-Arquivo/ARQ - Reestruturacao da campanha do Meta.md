---
type: decisao
status: concluido
area: A7 - Aquisicao e Midia Paga
tags: [moviki, meta-ads, aquisicao, conversao, capi]
atualizado: 2026-09-11
---

# ARQ - Reestruturação da campanha do Meta

> A campanha antiga comprava **visita de página**, não cadastro: `OUTCOME_TRAFFIC`
> otimizando por `LANDING_PAGE_VIEWS`. Em 14 dias até 11/09 foram **R$ 118,02, 425
> cliques e ZERO lead**. Objetivo de campanha não é editável na Meta — exigiu campanha
> nova. Reestruturada em 11/09/2026 inteiramente pela ponte do Windsor.

---

## 1. O que estava errado

| Campanha antiga | Objetivo | Otimizando por | Gasto 14d | Cliques | Leads |
| --- | --- | --- | --- | --- | --- |
| Moviki \| Cadastro de lojista \| João Pessoa \| set-2026 | `OUTCOME_TRAFFIC` | **LANDING_PAGE_VIEWS** | R$ 103,24 | 348 | 0 |
| Post do Instagram (impulsionado) | `LINK_CLICKS` | LINK_CLICKS | R$ 14,78 | 77 | 0 |
| **Total** | | | **R$ 118,02** | **425** | **0** |

O algoritmo da Meta otimiza **literalmente** para o que se pede. Pedindo visualização
de página, ele aprende a achar quem clica e carrega — o público mais barato e menos
comprometido que existe, a R$ 0,44 a visita. Ele fez o trabalho certo para a pergunta
errada.

CPC de **R$ 0,28 no Meta** contra **R$ 1,85 no Google** no mesmo período: clique 6,6x
mais barato. Mas o número que decide é o último, e ele estava zerado dos dois lados.

## 2. A estrutura nova — 11/09/2026

Criada pela ponte do Windsor, conta Meta `920636768619509`.

| Nível | Nome / ID | Configuração |
| --- | --- | --- |
| Campanha | Moviki \| Cadastro de lojista \| Conversao \| set-2026 · `120251233014530770` | `OUTCOME_LEADS` · CBO R$ 10/dia · `LOWEST_COST_WITHOUT_CAP` |
| Conjunto | `120251233107600770` | `OFFSITE_CONVERSIONS` no pixel `2114417739495816`, evento **LEAD** · João Pessoa 25 km · 25-60 anos · Advantage+ **desligado** |
| Anúncio A | `120251233115630770` | CTA `SIGN_UP` |
| Anúncio B | `120251233121490770` | CTA `SIGN_UP` |

Página do Moviki.app: `1312620718595159`.

**Pausadas no mesmo dia:**

- campanha antiga `120251100284890770`
- impulsionamento `120251082810370770`

## 3. Por que Advantage+ desligado e CBO ligado

- **Advantage+ desligado:** com zero conversão histórica não há sinal para o
  público automático expandir em cima. Segmentação explícita mantém a leitura limpa.
- **CBO em R$ 10/dia:** o orçamento na campanha deixa a Meta escolher entre A e B
  sozinha. Já aconteceu: em 12/09 o anúncio A caiu de 243 para 26 impressões porque o
  CBO concentrou a verba no B.

## 4. A ressalva que veio junto

A campanha nova otimiza pelo evento **Lead**, que **nunca aconteceu de verdade** — os
2 `sign_up` do período são testes do próprio Paulo de 05/09. Sem sinal de conversão, a
Meta tende a entregar pouco e ficar em aprendizado.

Trocar o objetivo antes de consertar o gargalo foi ordem invertida. O gargalo medido é
a `comerciantes.html` (215 pessoas → 5 cliques no CTA), não a campanha. Ver
[[ARQ - O funil real do trafego pago]].

## 5. Regras de ouro que nascem daqui

> **Objetivo de campanha é o que você está comprando.** Otimizar por visita compra
> visita. Quem quer cadastro pede cadastro, mesmo que o volume caia.

> **Objetivo não é editável na Meta.** Errar o objetivo custa a campanha inteira:
> a correção é sempre campanha nova, com o aprendizado zerado.

## 6. O que fica

- [x] Recriar a campanha do Meta com objetivo de conversão/Lead — feito em 11/09
- [x] Desligar o impulsionamento "Post do Instagram" — pausado em 11/09
- [ ] Só julgar a campanha nova depois de a `comerciantes.html` converter
- [ ] Conferir se o evento Lead do pixel `2114417739495816` volta a registrar quando houver cadastro real

## Ligações

[[A7 - Aquisicao e Midia Paga]] · [[A6 - Medicao e Analytics]] ·
[[ARQ - O funil real do trafego pago]] ·
[[ARQ - Pulso das campanhas 12 e 13092026]] ·
[[R - Rotina de checagem das campanhas]] ·
[[R - Meta Business - ativos e contas]] ·
[[R - Checklist conformidade Meta e Google]] · [[R - Links e identificadores]] ·
[[R - Regras de ouro]]
