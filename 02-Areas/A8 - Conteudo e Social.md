---
type: area
status: ativo
tags: [social, conteudo]
atualizado: 2026-08-28
---

# A8 — Conteúdo e Social (`moviki-assistente-social`)

## O que está no ar
Robô de publicação em Python 3.11, **100% GitHub Actions**, repositório público. Graph API oficial v25.0. Primeiro post automático em 24/08/2026, 20h36.

## Calendário
| Quando | O quê |
| --- | --- |
| Seg/Qua 10h · Ter/Qui 19h · Sex 12h | Feed (vitrine/institucional) |
| Ter e Sáb 17h | Reel (só com Instagram ativo) |
| Segunda 8h | Verificação de saúde |
| Domingo 4h | Limpeza (arte +60 dias) |

## Modo `SO_FACEBOOK`
Nasceu porque a conta antiga do Instagram estava restrita. **Plano B permanente.** Ligado → só Página do Facebook. Desligado → Instagram principal + Facebook espelho. **Reverter é apagar o secret.**
⚠️ Usar `sim`/`nao`, **nunca `1`** — o Actions mascara todo dígito 1 nos logs.

## Vitrine — o motor estratégico
Divulga negócio real que autorizou (`autorizaDivulgacao === true`). **2 de 3** (`MIN_NEGOCIOS_VITRINE=3`). Abaixo disso, tudo institucional. 11 fundos em `assets/fundos/` (1024×1024). Trava de conteúdo em `src/compliance.py` — `ganho_facil = pirâmide` é o risco nº 1. 46/46 testes passando.

## Regras de tom
- "Link na bio" é gramática de **Instagram**; no Facebook o endereço vai no texto.
- Não nomear fornecedores/stack em post.
- Não inventar depoimentos; não usar o Caldeirão como prova.

## Lição
**Dry-run valida conteúdo; só a publicação real valida integração.** Os 3 bugs que só apareceram no primeiro post real passaram por 46 testes, 2 dry-runs e um verificador verde.

## Projetos vinculados
[[P08 - Aquecimento do Instagram]] · [[P10 - Vitrine - terceiro negocio autorizado]]

## Recursos
[[R - Regras de conteudo e tom]] · [[R - Meta Business - ativos e contas]]
