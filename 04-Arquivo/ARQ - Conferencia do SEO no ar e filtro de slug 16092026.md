---
type: incidente
status: concluido
area: "[[A7 - Aquisicao e Midia Paga]]"
tags: [seo, sitemap, indexacao, base-suja, entrega]
atualizado: 2026-09-16
---

# ARQ - Conferencia do SEO no ar e filtro de slug 16092026

Conferencia do pacote `moviki-seo-16092026.zip` logo depois da subida, e o
conserto do que ela achou. Continua
[[ARQ - SEO reposicionado e sitemap de negocios 16092026]].

## O que esta certo no ar

- `/sitemap.xml` responde como `<sitemapindex>` com as duas listas.
- `/sitemap-negocios.xml` **funciona**: XML valido, montado pela funcao nova.
- `/hamburguermaster` com `canonical` e `og:url` em **www**.
- Home com o title novo e canonical em www.

Detalhe do caminho: a primeira leitura do `/hamburguermaster` ainda trouxe o
canonical no apex. Nao era o arquivo — era o **cache da CDN**, que o proprio
`og.js` pede em `s-maxage=300`. Com uma query string diferente, para forcar
miss, veio o www. **Conferencia de deploy em rota cacheada se faz com
cache-buster**, senao se lê o passado e se conserta o que nao esta quebrado.

## O que a conferencia achou de errado

### 1. O sitemap listou cinco paginas, e quatro nao deviam estar la

```
/email                  <- slug lixo
/fabiofffggggmailcom    <- e-mail digitado no campo do apelido
/ricopj                 <- conta do dono
/karina                 <- conta de demonstracao
/hamburguermaster       <- o unico negocio de verdade
```

As duas primeiras passavam no portao de qualidade do `og.js` porque ele
pergunta *"a pagina esta preenchida?"* — tinham nome, ponto no mapa e segmento.
Ninguem tinha perguntado *"isto representa um negocio de verdade?"*.

O proprio comentario do `og.js` ja avisava do risco: *"pagina magra em
quantidade derruba a reputacao do dominio inteiro, e o dominio e um so pra todos
os lojistas"*. Com a base deste tamanho, **40% do que o Google veria do dominio
era lixo de cadastro**.

### 2. A arte de previa ja existia, e eu tinha posto o favicon no lugar dela

`ogmoviki.jpg`, **1200x630, 66 KB**, esta na raiz do repositorio desde sempre —
e o proprio `og.js` a usa como `OG_PADRAO`. Na rodada anterior a home, a
`premium.html` e a `enterprise.html` sairam apontando para o `favicon512.png`,
de 512x512. O item "criar arte 1200x630" da [[P37 - Alinhar campanhas e previa da home ao posicionamento novo]]
**nao precisava existir**: bastava usar o que ja estava la.
Corrigido nas tres, com `og:image:alt` e `twitter:card` em `summary_large_image`.

## O conserto: `lib/seo.js`

Uma regra, num lugar so, importada pelo `og.js` (que escreve o meta robots) e
pelo `api/sitemap.js` (que escreve a lista). Se a regra vivesse copiada nos
dois, um dia divergiriam e o Search Console encheria de "Enviada, mas marcada
como noindex".

**Duas camadas:**

1. **Heuristica**, automatica: slug que e palavra generica de formulario
   (`email`, `teste`, `admin`, `undefined`, so digitos...) ou que termina em
   provedor de e-mail achatado (`...gmailcom`, `...hotmailcombr`).
2. **Env `SEO_SLUGS_FORA`**, manual: contas internas e demonstracoes, que
   heuristica nenhuma adivinha. E env, e nao codigo, para tirar e por sem
   deploy.

**A ancora no fim da regex e o detalhe que evita o estrago.** Sem ela, um
negocio chamado "Bol Comidas" vira `bolcomidas`, casa com `bol` + `com` e sai
do indice sem ninguem entender por que. Falso positivo aqui e pior que falso
negativo: o lixo o Paulo tira na mao, mas o negocio legitimo barrado ninguem
descobre. Testado com 16 slugs que devem sair e 11 que devem ficar — entre eles
`emailmarketing`, `bolcomidas`, `yahoocomida`, `uolcomercio` e `terracafe`.

**Nada fica escondido de gente.** O link continua abrindo, o preview do WhatsApp
continua completo. O efeito e `noindex,follow` e ficar fora do sitemap.

## O numero que importa mais que o SEO

Depois do filtro, o `/sitemap-negocios.xml` vai listar **um** negocio.

> O gargalo do posicionamento hoje nao e tecnica de busca. E base.

Nenhum ajuste de palavra-chave muda um dominio com uma pagina de conteudo. A
alavanca real, por enquanto, continua sendo prospeccao — e a limpeza da base,
que e trabalho de cinco minutos no painel do dono.

## Ligacoes

[[R - Marcas de versao - SEO lote 2 16092026]] ·
[[ARQ - SEO reposicionado e sitemap de negocios 16092026]] ·
[[P38 - Search Console e conteudo de intencao]]
