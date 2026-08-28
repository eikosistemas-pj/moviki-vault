---
type: arquivo
status: concluido
data: 2026-08-27
area: A6 — Medicao e Analytics
tags: [medicao]
atualizado: 2026-08-28
---

# ARQ — GA4: levas 1, 2 e 3 — FUNIL INTEIRO MEDIDO

**Resolveu a pendência nº 1 histórica do projeto: medição zero.**

- **Leva 1 (25/08)** — funil do dinheiro, do `page_view` ao `purchase` pelo servidor.
- **Leva 2 (27/08)** — topo do funil: `enterprise`, `comerciantes`, `parceiros`, `parceiros-ganhos` ganharam `mvmetrica.js` e delegação de `data-ev`. 23 CTAs nomeados. *(A home já estava medida desde a Fase 1 — o mapa listava como pendente e não era.)*
- **Leva 3 (27/08)** — o ramo de parceiro. A auditoria dos 5 repos achou o buraco: o `pp.html` carimbava UTM para o `seja-parceiro.html`, **e essa página não tinha GA4 nenhum**. Todo o funil de recrutamento rodava cego. A captura do `ref` para o upline sempre funcionou — o que não existia era a medição.

## A lição que virou regra
**Carimbar UTM só vale se o DESTINO medir.** O par `p.html → comerciantes.html` estava fechado e o par `pp.html → seja-parceiro.html` ficou aberto por dias porque os dois "estavam feitos".

## A CSP mordeu de novo
`seja-parceiro.html` precisou dos **3 hosts do GA**. Sem isso o `mvmetrica.js` carregaria e o `gtag.js` seria bloqueado em silêncio — a página "tem GA" e não mede.

## Decisão de arquitetura mantida
**O `mvmetrica.js` NÃO foi alterado nas levas 2 e 3.** Ele é idêntico nos dois repos e está no caminho do dinheiro. A medição das landings é **inline** — sem arquivo novo e sem requisição a mais.

→ [[R - Eventos GA4 dicionario]] · [[A6 - Medicao e Analytics]]
