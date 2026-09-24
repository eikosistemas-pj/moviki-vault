---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [material-de-apoio, catalogo, shopping, video, icone]
atualizado: 2026-09-24
---

# ARQ - Categoria Lojas de shopping no material de apoio

## O que entrou

- Categoria nova `shopping` — "Lojas de shopping", emoji 🛍️, grupo `ramo`,
  ícone 3D `cat-shopping.png` (256) + `cat-shopping-48.png`.
- Posição na lista: entre "Fotografia e eventos" e "Moda e acessórios" (ordem alfabética do grupo ramo).
- 2 peças `video`, ambas `novo: true`:
  - `video-shopping-moda` — 0:39, 17,8 MB
  - `video-shopping-esportes` — 0:38, 17,3 MB
- `catalogo.json` versão **`2026-09-24-shopping3`** (capas em `material/capas/<id>.webp`, padrão das outras 79 peças): 92 entradas. Os 2 vídeos aparecem também em "Para qualquer negócio" > Vídeos por entrada duplicada no catálogo (`<id>-geral`, `categoria: geral`, mesmo arquivo e mesma capa) — o HTML aceita uma categoria só por peça, e assim o `parceiro.html` não foi tocado.

## Regras aplicadas

- Legendas começam com `#publi`, sem promessa quantificada.
- Pix dentro da live declarado como recurso do plano Enterprise.
- Cenas geradas não são retocadas por marca de terceiro (decisão do Paulo, 24/09).

## Ordem de subida (moviki-app)

1. `material/` — 2 vídeos; `material/capas/` — 2 capas (NOVO)
2. `icones/` — 2 ícones (NOVO)
3. `material/catalogo.json` (SUBSTITUI) — por último

## Ligações

[[ARQ - Videos de loja de shopping 24092026]] · [[R - Marcas de versao no ar]] ·
[[R - Marcas de versao no ar em 24092026]] · [[A1 - Produto e Paineis]]
