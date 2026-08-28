---
type: recurso
status: referencia
tags: [custo]
atualizado: 2026-08-28
---

# R — Custos e cotas

## Firestore (plano Blaze — cota grátis diária: 50 mil leituras / 20 mil escritas)
**Depois do conserto de custo da página pública** (de 204 para **4 leituras por visita**, e agora constante):

| Visitas/dia | Leituras/dia | Escritas/dia | Custo/dia |
| --- | --- | --- | --- |
| 5.000 | 20.000 | 5.000 | grátis |
| 10.000 | 40.000 | 10.000 | grátis |
| 50.000 | 200.000 | 50.000 | ~US$ 0,05 |
| 100.000 | 400.000 | 100.000 | ~US$ 0,14 |

## Anthropic — Vik
Modelo **`claude-haiku-4-5-20251001`** · US$ 1/MTok entrada · US$ 5/MTok saída.
Prompt ~2.700 tokens + contexto, resposta curta → **~US$ 0,004 por resposta**, ou US$ 5 a cada ~1.200 respostas. Mais ~20 leituras e 1 escrita de Firestore por resposta.

## Asaas
**100 transferências Pix grátis por mês.** Cota zera dia 1º e **não acumula**. Sai do saldo da conta Asaas.
Consulta de titular de chave: **5 por minuto**.

## Vercel (Hobby)
**12 funções serverless por projeto** · **~10 s** por execução.

## Kairogen
PRO · 930 créditos/mês · R$ 0,16/crédito · renova dia 20. Ícone 3D = 6 créditos.

## `api/og.js`
4 leituras por **miss** de cache. `s-maxage=300` + `stale-while-revalidate=86400` na CDN → o caso comum não lê nada.
