---
type: decisao
status: parcial
area: A14 - Material de apoio do parceiro
tags: [material-de-apoio, catalogo, navegacao, decisao]
atualizado: 2026-09-24
---

# ARQ - Categorias secas no material de apoio

## Decisão do Paulo (24/09/2026)

- **Cada peça fica só na sua categoria.** Sem cópia de vídeo em "Para qualquer negócio" ou em outro ramo. O catálogo não incha.
- **Panfletos ganham categoria própria:** "Panfletos com o seu QR" (`panfletos`, grupo `principal`, ícone 3D `cat-panfletos.png`).
- **Sai o filtro "Tudo".** Dentro da categoria ficam só os tipos que existem nela (Feed, Stories, Vídeos, Textos).

## Entregue

- `catalogo.json` **`2026-09-24-secas`**: 90 peças; os 2 panfletos em `panfletos`; saíram as cópias `video-shopping-*-geral`.
- `icones/cat-panfletos.png` e `cat-panfletos-48.png`.

## Falta (mexe no `parceiro.html`)

- Tirar "Tudo" e "Panfletos" da faixa de tipo; abrir no primeiro tipo que existe na categoria; esconder a faixa quando só há um tipo (ex.: Lojas de shopping, só vídeos).
- `.mcTopo` com 3 colunas no computador: com Panfletos são três cartões grandes, e hoje o terceiro fica sozinho na segunda linha.
- Montar sobre o arquivo que está no GitHub no dia; um chat por vez nesse arquivo.

## Ligações

[[A14 - Material de apoio do parceiro]] · [[ARQ - Categoria Lojas de shopping no material de apoio 24092026]] · [[R - Marcas de versao no ar em 24092026]]
