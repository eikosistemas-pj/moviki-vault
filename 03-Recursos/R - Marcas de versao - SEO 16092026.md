---
type: recurso
status: referencia
area: "[[A1 - Produto e Paineis]]"
tags: [marcas-de-versao, upload, seo]
atualizado: 2026-09-16
---

# R - Marcas de versao - SEO 16092026

Pacote `moviki-seo-16092026.zip`. Repositorio **moviki**, 15 arquivos.

| Pasta | Arquivo | Acao | Marca |
|---|---|---|---|
| `api/` | `sitemap.js` | **NOVO** | `2026-09-16-sitemap1` |
| `api/` | `og.js` | SUBSTITUI | `2026-09-15-og-live` (inalterada; mudou so a constante BASE) |
| raiz | `sitemap.xml` | SUBSTITUI | — (virou indice) |
| raiz | `sitemap-paginas.xml` | **NOVO** | — |
| raiz | `vercel.json` | SUBSTITUI | — |
| raiz | `index.html` | SUBSTITUI | `2026-09-16-livecommerce1` (inalterada) |
| raiz | `premium.html` | SUBSTITUI | `2026-09-16-livecommerce1` (inalterada) |
| raiz | `enterprise.html` | SUBSTITUI | `2026-09-16-livecommerce1` (inalterada) |
| raiz | `comerciantes.html` | SUBSTITUI | `2026-09-16-filmelive` (inalterada) |
| raiz | `parceiros.html` · `parceiros-ganhos.html` | SUBSTITUI | sem marca |
| raiz | `regras-da-live.html` | SUBSTITUI | `2026-09-16-publica` (inalterada) |
| raiz | `404.html` · `live.html` · `excluir-conta.html` | SUBSTITUI | inalteradas |

As marcas de versao **nao mudaram de proposito**: nenhuma tela mudou nesta
rodada. O que mudou foi `<head>`, canonical, JSON-LD e URL de link. Marca de
versao serve para o Vik e para a conferencia de tela — subir uma marca nova sem
tela nova ligaria o modo cauteloso do Vik por nada.

## Encoding, arquivo por arquivo

`comerciantes.html` e `regras-da-live.html` sao **CRLF + BOM**. Todos os outros,
LF sem BOM. Conferido byte a byte depois da edicao.

## Ordem de subida

Nao ha dependencia entre eles, com uma excecao: **`vercel.json` e
`api/sitemap.js` sobem juntos**. O `vercel.json` sozinho cria a rota
`/sitemap-negocios.xml` apontando para uma funcao que nao existe, e o indice
`sitemap.xml` passaria a apontar para um 404.

## Depois de subir — na ordem

1. Abrir `https://www.moviki.com.br/sitemap-negocios.xml` e conferir o
   cabecalho `X-Moviki-Negocios` (quantos negocios entraram) e o
   `X-Moviki-Firestore` (`sa` = conta de servico).
2. Search Console: reenviar `https://www.moviki.com.br/sitemap.xml` na
   propriedade do **www**.
3. Testar a home e a `/premium.html` no Teste de Resultados Aprimorados do
   Google e conferir se `Organization` e `SoftwareApplication` aparecem.
