---
type: recurso
status: referencia
area: "[[A14 - Material de apoio do parceiro]]"
tags: [marcas-de-versao, upload, robo-social]
atualizado: 2026-09-22
---

# R - Marcas de versao - feed padronizado 22092026

Apendice de [[R - Marcas de versao no ar]]. Entregue em 22/09/2026 — **conferir se subiu**.

## moviki-assistente-social — marca `2026-09-22-formatos`

A marca mora em `src/config.py` (`VERSAO`) e sai na primeira linha do log do Feed.

| Arquivo | Acao |
|---|---|
| `run_feed.py` | SUBSTITUI |
| `run_verificar.py` · `run_reel.py` | SUBSTITUI |
| `run_story.py` | NOVO |
| `src/material.py` · `src/pecas.py` · `src/criadores.py` | NOVO |
| `src/arte.py` · `src/config.py` · `src/compliance.py` · `src/firestore.py` · `src/segmentos.py` | SUBSTITUI |
| `src/social/facebook.py` · `src/social/instagram.py` | SUBSTITUI |
| `tests/test_material.py` · `tests/test_criadores.py` · `tests/test_formatos.py` | NOVO |
| `tests/test_pipeline.py` · `tests/test_compliance.py` | SUBSTITUI |
| `conteudo/CRIADORES-CONTRATO.md` | NOVO |
| `assets/fundos/LEIA-ME.md` | SUBSTITUI |
| `.github/workflows/story.yml` | NOVO |
| `.github/workflows/feed.yml` · `reel.yml` · `manutencao.yml` | SUBSTITUI |
| `.claude/skills/praca/SKILL.md` | SUBSTITUI |

## moviki-app

| Arquivo | Acao |
|---|---|
| `material/LEIA-ME.md` | SUBSTITUI |
| `.claude/skills/canal/SKILL.md` | SUBSTITUI |

## Os seis repositorios

`CLAUDE.md` na raiz — SUBSTITUI nos seis (`moviki`, `moviki-app`, `moviki-robo`, `moviki-ai`, `moviki-assistente-social`, `moviki-vault`). Copia identica.

## Ligacoes

[[ARQ - Feed padronizado sobre o material de apoio]] · [[R - Marcas de versao no ar]]
