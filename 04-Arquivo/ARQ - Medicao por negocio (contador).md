---
type: arquivo
status: concluido
data: 2026-08-26
area: A6 — Medicao e Analytics
tags: [medicao, custo]
atualizado: 2026-08-28
---

# ARQ — Medição por negócio (Fase 6) — NO AR 26/08/2026

O GA4 mede o site inteiro e **não devolve dado por lojista**. Este é o contador próprio que alimenta o card "Seu desempenho".

**Onde:** `metricas/{uid}/dias/{AAAA-MM-DD}`. **Coleção de topo de propósito** — dentro de `negocios/{uid}` o `match /{documento=**}` deixaria qualquer um ler o desempenho do concorrente.

Quem escreve é a própria página pública com `increment(1)` — **nenhuma função nova no Vercel**.

## Travas contra inflar
Nas regras: só os nomes previstos · no máximo 3 campos na criação e 2 alterados no update · cada contador sobe no máximo 1.
No cliente: trava de sessão (F5 não conta de novo) e debounce de 1,5 s.

**Limitação honesta:** por ser contador no cliente, alguém determinado consegue inflar os **próprios** números. A correção definitiva é um endpoint no robô → [[P12 - Metricas por ponto no Enterprise]].

## O conserto que valia mais que a métrica
A página pública lia **todas** as avaliações a cada visita. Negócio com 200 avaliações custava **204 leituras por visita** — **quanto mais sucesso, mais caro.** Agora a nota média e a quantidade vêm de `negocios/{uid}/resumo/avaliacoes` `{n, soma}`; a lista só carrega quando o visitante abre a aba, no máximo 20.

**Medido: de 204 para 4 leituras por visita — e agora é constante.**

Esse mesmo `{n, soma}` virou o `aggregateRating` do JSON-LD em [[ARQ - Preview e SEO (api og.js)]].

## TTL
Ligado em 26/08 no **Console do Google Cloud** (não existe no Console do Firebase): grupo `dias`, campo `expiraEm`, adiamento 0, retenção de 13 meses.

⚠️ **`expiraEm` é derivado da data do PRÓPRIO DOCUMENTO, em UTC.** Do relógio do visitante, dois fusos mandariam valores diferentes, o campo contaria como alterado, a escrita passaria do teto e seria **recusada**.

→ [[R - Custos e cotas]]
