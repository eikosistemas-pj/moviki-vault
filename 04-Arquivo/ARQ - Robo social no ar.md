---
type: arquivo
status: concluido
data: 2026-08-24
area: A8 — Conteudo e Social
tags: [social]
atualizado: 2026-08-28
---

# ARQ — Robô social no ar — 24/08/2026

**Primeiro post automático publicado em 24/08/2026, 20h36**, na Página do Facebook Moviki.app. Pauta `endereco-que-muda`, arte composta com Pillow sobre fundo aprovado, hospedada em `raw.githubusercontent.com`, publicada via Graph API v25.0, estado commitado de volta.

## Os 3 bugs que só apareceram na 1ª publicação real
*(Passaram por 46 testes, 2 dry-runs e um verificador verde.)*

| Bug | Conserto |
| --- | --- |
| `hospedagem.py` usava POST onde o GitHub exige **PUT** | `util_net` ganhou `put()` |
| Publicar em Página exige **Page Access Token** | o robô troca o token sozinho via `GET /{page-id}?fields=access_token` |
| **"link na bio" não existe no Facebook** | `run_feed` ganhou `_texto_facebook()` |

## A regra que ficou
**Dry-run valida conteúdo; só a publicação real valida integração.**

→ [[A8 - Conteudo e Social]]
