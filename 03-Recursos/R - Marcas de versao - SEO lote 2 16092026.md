---
type: recurso
status: referencia
area: "[[A1 - Produto e Paineis]]"
tags: [marcas-de-versao, upload, seo]
atualizado: 2026-09-16
---

# R - Marcas de versao - SEO lote 2 16092026

Pacote `moviki-seo-lote2-16092026.zip`. Repositorio **moviki**. Vai POR CIMA do
`moviki-seo-16092026.zip`, ja no ar — os outros nove arquivos daquele pacote nao
mudaram e nao entram aqui.

| Pasta | Arquivo | Acao | Marca |
|---|---|---|---|
| `lib/` | `seo.js` | **NOVO** | `2026-09-16-seo1` |
| `api/` | `og.js` | SUBSTITUI | `2026-09-15-og-live` (inalterada) |
| `api/` | `sitemap.js` | SUBSTITUI | `2026-09-16-sitemap1` (inalterada) |
| raiz | `index.html` | SUBSTITUI | `2026-09-16-livecommerce1` (inalterada) |
| raiz | `premium.html` | SUBSTITUI | `2026-09-16-livecommerce1` (inalterada) |
| raiz | `enterprise.html` | SUBSTITUI | `2026-09-16-livecommerce1` (inalterada) |

## Ordem

`lib/seo.js` **antes** de `api/og.js` e `api/sitemap.js` — os dois passam a
importa-lo, e sem o arquivo a funcao quebra no primeiro acesso.

## Variavel de ambiente — projeto Vercel do SITE

```
SEO_SLUGS_FORA = ricopj,karina
```

Production e Preview. Sem ela nada quebra: as duas contas continuam indexaveis
ate a env existir. Para tirar outra conta do indice depois, basta acrescentar na
lista, separada por virgula — nao precisa de deploy, so redeploy da funcao.

## Conferir depois de subir

1. `/sitemap-negocios.xml` com cache-buster (`?x=1`): `/email`,
   `/fabiofffggggmailcom`, `/ricopj` e `/karina` devem ter sumido, e o cabecalho
   `X-Moviki-Negocios` deve cair para 1.
2. Compartilhar a home no WhatsApp: a previa agora e a arte larga
   (`ogmoviki.jpg`), nao o quadradinho da logo.
