---
type: recurso
status: referencia
area: "[[A7 - Aquisicao e Midia Paga]]"
tags: [regras-de-ouro, seo, sitemap, canonical, sandbox]
atualizado: 2026-09-16
---

# R - Regras de ouro novas de 16092026 - SEO

Entram em `03-Recursos/R - Regras de ouro.md` na proxima recompilacao.

## 1. Sitemap e `noindex` sao a MESMA decisao

Quem decide se a pagina entra no sitemap e a mesma regra que decide o `robots`
do HTML. Hoje isso vive em dois arquivos — `api/og.js` e `api/sitemap.js` — e a
regra esta copiada linha a linha nos dois. **Mudou o portao de qualidade num,
muda no outro, na mesma rodada.** URL no sitemap com `noindex` no HTML enche o
Search Console de sinal contraditorio, e o dominio e um so para todos os
lojistas.

## 2. Sitemap quebrado responde erro, nunca lista vazia

Sitemap vazio nao e "nada aconteceu": e a afirmacao de que as paginas sumiram, e
o Google tira do indice o que ja tinha entrado. Falha de leitura devolve **503
com `no-store`**. Vale para qualquer gerador de sitemap que dependa de banco.

## 3. `lastmod` sai do banco, nao da vontade

Use o `updateTime` do proprio documento. Carimbar a data de hoje em tudo a cada
geracao ensina o Google a ignorar o campo.

## 4. Canonical aponta para o dominio que RESPONDE 200

O apex esta como "Redirects to www" na Vercel. Canonical, `og:url` e `@id` de
JSON-LD apontando para o apex indicam uma URL que responde 301. Toda constante
de URL base no codigo usa **www**. A unica excecao e allowlist de **Origin** de
CORS, que precisa aceitar as duas — `api/live.js` fica como esta.

## 5. Duas paginas com a mesma intencao: uma canonical, a outra fora do sitemap

Nunca apagar a segunda — link antigo continua chegando nela. Canonical cruzado e
remocao do sitemap resolvem sem quebrar nada, e sao reversiveis.

## 6. `aggregateRating` inventado nao entra em JSON-LD

Nota agregada so com avaliacao real e publica na propria pagina. Marcar
avaliacao que nao existe e caminho curto para acao manual do Google.

## 7. Comentario de codigo que descreve trava tem que morrer junto com a trava

O `regras-da-live.html` carregava `<!-- noindex enquanto o Modo Live estiver em
beta fechado -->` sem nenhuma meta robots no arquivo. Duas rodadas trataram a
pagina como fora do indice por causa de um comentario obsoleto. **Comentario que
descreve comportamento e documentacao: sai junto com o comportamento.**

## 8. Arquivo de teste NUNCA nasce dentro da pasta do repositorio

Nesta rodada, para renderizar as paginas fora do ar, um `mvmetrica.js` de
mentira foi escrito por cima do arquivo real de 13.556 bytes. O que pegou foi o
**diff final contra o zip original, arquivo por arquivo, por hash**.

> Toda rodada termina comparando a pasta de trabalho com o zip que o Paulo
> mandou: `ALTERADO`, `NOVO` e `SUMIU`. Arquivo alterado que nao esta na lista da
> entrega e um acidente, nao uma surpresa boa.

Placeholder de teste vive em pasta separada, ou o repositorio e restaurado do zip
antes de empacotar.
