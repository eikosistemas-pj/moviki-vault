---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, og, previa, armadilha, deploy]
atualizado: 2026-09-16
---

# ARQ - Previa do link da live no WhatsApp 15092026

`moviki.com.br/live/{apelido}` chegava **sem cartão** no WhatsApp. Consertado em
15/09/2026, no `api/og.js` do repo `moviki`.

## Por que não tinha cartão

A rota `/live/:slug` ia direto para o `live.html`, que **não tem uma única linha
de Open Graph**. Só a página do negócio passava pelo `og.js`.

## O conserto

`vercel.json`:

- rewrite `/live/:slug` → `/api/og?slug=:slug&live=1`
- `includeFiles: "{404,live}.html"` — antes levava só o `404.html`, e a função
  não conseguia ler a casca da live

`api/og.js` reconhece `live=1`, serve a casca `live.html` em vez da `404.html` e
injeta o bloco com o título da transmissão. A prévia é sempre **`noindex`** — a
live some do ar e o resultado morreria — e tem **cache curto**, senão o cartão
mostraria o título da live anterior.

## Dois defeitos achados no caminho

**1. Duas `description` no `<head>`.** O `live.html` já traz `description` e
`robots` próprios, escritos pelo lojista. Injetar por cima gerava duplicata e o
WhatsApp escolhia a errada. Nasceu a função `limpar()`, que remove `meta`/`link`
de `description`, `robots`, `canonical`, `og:*` e `twitter:*` **só até o primeiro
`<script>` ou `<style>`** — o corte evita mexer em texto dentro de código.

**2. `$&`, ``$` `` e `$'` expandindo dentro do `replace`.** Título de live com
cifrão virava lixo no cartão. Trocado por `replace` com **função**, que não
interpreta os padrões de substituição.

> **Este bug já existia na prévia da página do negócio.** Foi encontrado por
> acaso ao portar a função para a live.

## A armadilha da própria regra de ouro

A primeira subida do `og.js` foi feita **com a marca de versão antiga**.
Corrigida numa segunda subida — e, na conferência de 16/09, o arquivo no
repositório ainda trazia `2026-09-04-og-sa` com o conteúdo novo dentro. A
correção não tinha subido. Marca errada com conteúdo certo é pior que arquivo
sem marca: manda o diagnóstico começar no lugar errado.

## Ligações

[[R - Marcas de versao no ar]] · [[R - Live - Arquitetura e arquivos]] ·
[[A13 - Modo Live]] · [[R - Links e identificadores]] ·
[[R - Regras de ouro novas de 15 e 16092026]]
