---
type: projeto
status: pausado
prioridade: 2
area: A9 — IA e Atendimento (Vik)
tags: [ia, produto]
atualizado: 2026-08-28
---

# P06 — Camada 3 do Vik: os Viks alimentando o painel do dono

## Resultado esperado
Cron diário no `moviki-ai` (ficaria em 3 de 12 funções) lendo todas as `vik_memoria` e agregando num documento único que o `eikoadm01` exibe:
- o que os clientes mais perguntam;
- quem está maduro para upgrade;
- **por que os que não assinam não assinam**.

Pesquisa de produto contínua e de graça.

## Por que está pausado
**Só faz sentido depois de algumas semanas de memória acumulada.** Hoje agregaria o vazio.

## Gatilho para retomar
Memória acumulada em pelo menos algumas dezenas de contas ativas.

## Ligações
[[A9 - IA e Atendimento Vik]] · [[P05 - Calibrar o Vik]]
