---
type: arquivo
status: concluido
area: A10 - Conformidade e LGPD
tags: [seo, google, json-ld, faq, conformidade, aovivo]
atualizado: 2026-09-16
---

# ARQ - Violacao de FAQPage na pagina aovivo 16092026

## O defeito

`moviki/aovivo.html` trazia um bloco **JSON-LD do tipo `FAQPage`** com **cinco**
perguntas **reescritas**, enquanto a pagina mostrava **sete** perguntas com
outro texto. Uma das respostas marcadas — a do teste gratis — ainda carregava a
redacao antiga, ja corrigida na tela.

O Google exige que o conteudo marcado com dado estruturado seja **identico ao
visivel**. Marcacao que nao confere com a pagina e violacao das diretrizes de
spam de dado estruturado: rende acao manual e perda do rich result.

## O conserto

O JSON-LD foi **regerado a partir do texto visivel**: sete perguntas, **7 de 7
identicas**, palavra por palavra.

Feito **sem pedir autorizacao**, pela autorizacao permanente do Paulo para
corrigir violacao de regra da Meta e do Google direto.

## Regra de ouro

> **Dado estruturado se gera a partir do HTML visivel, nunca se escreve a
> mao.** Texto da tela muda e a marcacao fica para tras — e a partir dai a
> pagina esta afirmando ao Google uma coisa que nao mostra ao visitante.

## Cuidado registrado

A `/aovivo` foi mandada tres vezes para conferencia como se fosse a landing
principal — nao e: e a **pagina de venda da live**. E subir de novo um pacote
antigo dela **desfaria** duas coisas ja corrigidas: a remocao do `noindex` e o
conserto deste JSON-LD.

## Ligacoes

[[A10 - Conformidade e LGPD]] · [[P25 - Pagina de venda da live]] ·
[[A13 - Modo Live]] · [[R - Checklist conformidade Meta e Google]] ·
[[R - Regras de ouro]] · [[R - Marcas de versao no ar]]
