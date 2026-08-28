---
type: projeto
status: ativo
prioridade: 1
area: A7 — Aquisicao e Midia Paga
prazo: 
tags: [aquisicao, midia-paga, conformidade]
atualizado: 2026-08-28
---

# P01 — Aquisição: campanha de tráfego pago

## Resultado esperado
Campanha de Tráfego/Conversão rodando para `premium.html` com UTM, gerando `cta_painel` → `begin_checkout` → `purchase` mensuráveis no GA4 e na Meta CAPI.

## Por que agora
**É o maior risco em aberto do projeto inteiro.** O produto está pronto, o funil está medido de ponta a ponta (GA4 + CAPI) e as landings estão em conformidade. Não há mais nada de produto bloqueando: falta trazer gente.

## Estado da conta em 27/08
- "Nova campanha de Reconhecimento" — R$ 6,00/dia, ativa desde 24/08, **0 impressão e R$ 0,00 gasto**. Objetivo errado (Reconhecimento não gera evento de funil). → **desligar**.
- Impulsionamento de post no Instagram (26–27/08) — LINK_CLICKS, 338 impressões, 48 cliques, R$ 5,12, alcance 335. **Prova que a conta entrega.**

## Definição de pronto
- [ ] Campanha de Reconhecimento desligada
- [ ] Campanha nova: objetivo Tráfego ou Conversão, destino `premium.html`
- [ ] UTM completo no destino
- [ ] Criativo passou pelas [[R - Checklist conformidade Meta e Google|três perguntas de conformidade]] — a Meta julga o anúncio junto com a landing
- [ ] `META_TEST_CODE` conferido e removido da Vercel (com ele, evento não conta como conversão)
- [ ] Primeira semana com `Lead` chegando pela CAPI

## Restrição conhecida
Sem pixel de navegador, **não há remarketing nem público semelhante**. Ver [[ARQ - Decisao - sem pixel de navegador]]. Com volume, a conta muda.

## Próxima ação física
Desligar a campanha de Reconhecimento no Gerenciador.

## Ligações
[[A7 - Aquisicao e Midia Paga]] · [[R - Meta Business - ativos e contas]] · [[ARQ - Meta CAPI]]
