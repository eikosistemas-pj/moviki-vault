---
type: decisao
status: concluido
area: "[[A7 - Aquisicao e Midia Paga]]"
tags: [seo, sitemap, json-ld, canonical, apex-www, entrega]
atualizado: 2026-09-16
---

# ARQ - SEO reposicionado e sitemap de negocios 16092026

Terceira volta do reposicionamento de 16/09. Continua
[[ARQ - Reposicionamento da home para live commerce 16092026]].

## A descoberta que mudou a estrategia

O pedido era "consertar o SEO, porque na busca a gente aparece como mapa". A
conferencia mostrou que o problema nao era a palavra-chave da home.

**As paginas que valem estavam invisiveis.** Desde 15/09 cada pagina de negocio
(`moviki.com.br/apelido`) e servida pelo `api/og.js` com HTTP 200, title,
description, Open Graph, canonical e **JSON-LD LocalBusiness** — e com portao de
qualidade, marcando `noindex,follow` em cadastro pela metade. Tecnicamente
prontas. So que o `sitemap.xml` listava nove paginas institucionais e mais nada.
O proprio arquivo assumia: *"as paginas de negocio sao descobertas pelos links
que os proprios lojistas compartilham"*.

Nao sao. Link em status de WhatsApp e em grupo fechado nao e link rastreavel.

> O unico conteudo LOCAL do dominio — nome do negocio, segmento, cidade,
> cardapio, ponto no mapa — estava fora do indice. E conteudo local e a unica
> coisa que um SaaS pequeno consegue ranquear.

## Por que nao atacar "live commerce" de frente

A primeira pagina de *live commerce*, *como fazer live para vender* e *cardapio
digital* e de Nuvemshop, Stone, Cielo, Sebrae, Cardapio Web, OlaClick e Saipos —
dominios com anos de autoridade e equipe de conteudo. Landing de produto nao
tira o lugar deles. Alem disso **"live commerce" e termo de agencia**: o lojista
digita "vender ao vivo pelo celular", nao a categoria.

Estrategia registrada: **volume por pagina local** (o ativo que so o Moviki tem)
+ cauda longa de intencao com o diferencial (Pix direto, sem comissao, sem loja
fisica). Cabeca de cauda fica para quando houver autoridade.

## O que entrou

### 1. Sitemap das paginas de negocio — `api/sitemap.js` (NOVO)

Monta o XML na hora, a partir do Firestore, com o **mesmo portao de qualidade do
`og.js`**, copiado linha a linha: nome + ponto no mapa + algum conteudo real.
Listar URL que o HTML marca como `noindex` encheria o Search Console de "Enviada,
mas marcada como noindex" — sinal contraditorio, e o dominio e um so para todos
os lojistas.

- **Nao usa o filtro `autorizaDivulgacao`** do `api/vitrine.js`. Aquilo e
  permissao para o Moviki POSTAR o negocio nas redes da marca. Indexacao e outra
  coisa; confundir as duas esconderia quase todo mundo.
- Saneia o slug pelo mesmo formato da rota (`[A-Za-z0-9_-]{3,40}`) e tira
  duplicados: slug fora do formato nao tem pagina, e listar seria emitir 404.
- `lastmod` sai do `updateTime` do proprio documento, nao de um campo que o
  painel teria que gravar. Lastmod mentiroso e pior que lastmod ausente.
- `select` no `runQuery` — a base tem negocio com cardapio inteiro dentro.
- **Falha fechada:** Firestore fora do ar devolve **503**, nunca um `urlset`
  vazio. Sitemap vazio faz o Google **tirar do indice** o que ja entrou.
- Cache de CDN: 6 h, servindo velho por 24 h.

Teto de funcoes: a regra dos 12 e do `moviki-robo`. O projeto do site usava tres
(og, vitrine, live); com esta, quatro.

### 2. O sitemap virou indice

- `sitemap.xml` (SUBSTITUI) = `<sitemapindex>` com as duas listas
- `sitemap-paginas.xml` (NOVO) = as institucionais
- `/sitemap-negocios.xml` -> `api/sitemap` por rewrite no `vercel.json`

### 3. O canonical de TODA pagina de negocio apontava para o apex

`api/og.js` tinha `const BASE = 'https://moviki.com.br'` — sem `www`. Na Vercel o
apex esta como *"Redirects to www"*. Ou seja: o canonical, o `og:url` e o `@id`
do JSON-LD de cada pagina de lojista indicavam uma URL que responde **301**.
Corrigido. Com os 16 links internos, fecha a parte de codigo da
[[P30 - Decisao de dominio apex ou www]].

### 4. Canibalizacao entre as duas paginas de parceiro

`parceiros.html` e `parceiros-ganhos.html` tem o mesmo H1 em essencia, a mesma
description e a mesma intencao. As duas no sitemap, nenhuma com canonical: o
Google escolhe sozinho e dilui a outra.

`parceiros-ganhos.html` e a principal (maior, mais completa, e a que a home e o
regulamento linkam). A outra recebeu canonical apontando para ela e saiu do
sitemap. **Nada foi apagado** — quem chega por link antigo continua lendo.

### 5. Dados estruturados, que nao existiam fora da /aovivo

- Home: `Organization` + `WebSite` + `SoftwareApplication` com os quatro planos
  e os precos reais
- `premium.html` e `enterprise.html`: `SoftwareApplication` com as ofertas do
  plano + `BreadcrumbList`
- `comerciantes.html`: `BreadcrumbList`

Nenhum `aggregateRating`: nao existe nota agregada real do produto, e inventar
uma e o caminho mais curto para acao manual do Google.

### 6. Dois defeitos achados de passagem

- **`comerciantes.html` tinha o `>>` na meta description** — o mesmo erro da
  home, corrigido em outra rodada, que tinha gemeo aqui.
- **`comerciantes.html` usava o title antigo da home** (*"Moviki · Seu negocio no
  mapa. E em video."*). Duas paginas com o mesmo titulo. Agora e
  *"Pagina do seu negocio: cardapio, mapa e venda ao vivo | Moviki"*.
- **`regras-da-live.html`**: o comentario no `<head>` dizia "noindex enquanto o
  Modo Live estiver em beta fechado" e **nao existe meta robots nenhuma na
  pagina**. A trava saiu em algum momento e o comentario ficou, fazendo duas
  rodadas acharem que a pagina estava fora do indice. Comentario corrigido,
  canonical e Open Graph adicionados, pagina incluida no sitemap.

## Conferido

XML dos tres sitemaps validado no parser. `vercel.json` validado como JSON, com
o rewrite novo **antes** do generico `/:slug`. `node --check` nas duas funcoes.
`api/sitemap.js` testado com Firestore falso em cinco cenarios: nove documentos
entrando, tres saindo (os outros seis barrados por falta de conteudo, de mapa,
de slug ou por duplicidade), falha fechada em 503, base vazia, escape de XML.
As dez paginas HTML renderizadas em 390x844: zero erro de JavaScript, zero
rolagem lateral, HTML balanceado, canonical certo em todas, **zero link para o
apex** fora da allowlist de CORS do `api/live.js`, que e onde ele tem que ficar.

## O quase-acidente desta rodada

Para renderizar as paginas fora do ar eu escrevi um `mvmetrica.js` de mentira na
pasta do repositorio — **por cima do arquivo real, de 13.556 bytes**. O diff
final contra o zip original pegou. Vira regra: ver [[R - Regras de ouro novas de 16092026 - SEO]].

## Ligacoes

[[R - Marcas de versao - SEO 16092026]] ·
[[P38 - Search Console e conteudo de intencao]] ·
[[P30 - Decisao de dominio apex ou www]] ·
[[P37 - Alinhar campanhas e previa da home ao posicionamento novo]]
