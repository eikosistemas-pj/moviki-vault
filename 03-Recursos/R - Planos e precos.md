---
type: recurso
status: referencia
area: A1 - Produto e Paineis
tags: [produto, comercial, preco]
atualizado: 2026-09-16
---

# R — Planos e preços

**Esta tabela é a fonte de verdade para landing, atendente de IA e material de venda.**

> **Preços trocados em 16/09/2026** (cenário B), antes do primeiro cliente
> pagante real. Histórico da decisão em
> [[ARQ - Decisao de preco antes do lancamento 16092026]]. Execução em
> [[ARQ - Troca de precos executada 16092026]].

| Plano | Preço/mês | Inclui |
| --- | --- | --- |
| Básico | Grátis | Pino no mapa, página pública, link próprio, GPS ao vivo, WhatsApp, avaliações, **visitas dos últimos 7 dias** |
| Pró | **R$ 39,90** | + cardápio, promoções, eventos, **painel de desempenho completo** (14 dias, 4 números, gráfico, melhor dia, horário de pico) |
| Premium | **R$ 69,90** | + logo no pino, cor da marca, fotos dos produtos, galeria (12 fotos), **Modo Live** |
| Enterprise | **R$ 129,90** | + multi-ponto (até 3; extra R$ 19,90/mês), **WhatsApp por unidade**, relatórios, Pix dentro da live |

**Anual (2 meses grátis):** Pró **R$ 399,00** · Premium **R$ 699,00**.
**Trimestral: APOSENTADO em 16/09/2026.** Não existe mais em nenhuma tela nem no
`lib/asaas.js`. Link antigo com `?periodo=trimestral` cai no mensal.
**Enterprise não tem anual** — só mensal.
**Trial:** 30 dias de Pró, 1x por conta; fotos e desempenho completo liberados
durante o trial.

## Preços anteriores (até 16/09/2026)

Pró 37,90 · Premium 49,90 · Enterprise 99,90 · anual 379/499 ·
trimestral 99,90/134,90. **Qualquer peça que ainda mostre estes números está
velha** — a lista de onde o valor vive está em
[[R - Troca de precos - onde o valor vive]].

## Conferido no código — os três enganos comuns

- **Avaliações são de TODOS os planos**, Básico incluído.
- **Fotos são do Premium**, não do Pró.
- **Métricas: isca no Básico, tudo no Pró.**

## Comissão do parceiro (15% da mensalidade paga)

| Plano | Comissão N1 |
| --- | --- |
| Básico | R$ 0,00 (**plano grátis não gera comissão**) |
| Pró | **R$ 5,99** |
| Premium | **R$ 10,49** |
| Enterprise | **R$ 19,49** |

N2 = 7,5% e N3 = 5%, **só no 1º pagamento**. Do nível Ouro para cima o N1 sobe
para 16%, 17% e 18% — a escada está no Regulamento, cláusulas 4.6 a 4.11.

⚠️ **O percentual não mudou; o valor em reais mudou porque a mensalidade mudou.**
O `api/webhook.js` calcula sobre o valor efetivamente pago, então ele não
precisou ser tocado.

## Deep-link

`app.moviki.com.br?plano=premium|pro|enterprise&periodo=mensal|anual` abre o
modal já com o botão certo selecionado. **`periodo=trimestral` não é mais
válido** — o painel força mensal em vez de abrir tela sem rótulo.
