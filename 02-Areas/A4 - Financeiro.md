---
type: area
status: ativo
tags: [dinheiro]
atualizado: 2026-08-28
---

# A4 — Financeiro (Asaas, cobrança, comissões, Pix)

## Padrão a manter
**Dinheiro e status = server-side.** Gate que afeta dinheiro precisa existir NO SERVIDOR, não só na UI.
**Repo de dinheiro isolado do conversacional.** Nada de IA entra no `moviki-robo`; ele muda o mínimo.

## O que está no ar
- Cobrança Asaas em produção + trial de 30 dias de Pró (1x por conta) + gating por plano.
- Motor de comissão no `webhook.js`: **N1 15% recorrente · N2 7,5% e N3 5% só no 1º pagamento**. Ledger idempotente, clawback no estorno, retenção de 7 dias, trava anti "cadastro fantasma".
- **Pagamento de comissão por Pix automático** — testado ao vivo com dois Pix reais. Ver [[ARQ - Pix automatico de comissao]].
- Webhook de transferência (`TRANSFER_*`) quitando e reabrindo comissões sozinho.

## Travas
| Trava | Valor |
| --- | --- |
| Teto por pagamento automático | **R$ 500** (`TETO_SAQUE_AUTOMATICO`) |
| Mínimo para o parceiro **pedir** saque | R$ 20 (pagamento iniciado pelo dono não tem mínimo) |
| Cota Asaas | **100 transferências Pix grátis/mês**, zera dia 1º, não acumula |
| Prazo prometido | Até 1 dia útil (24h) |

## Pendência
[[P04 - Decisao fiscal do Programa de Parceiros]] — CNPJ obrigatório ou RPA.

## Recursos
[[R - Planos e precos]] · [[R - Custos e cotas]] · [[R - Colecoes do Firestore]]
