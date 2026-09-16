---
type: arquivo
status: concluido
area: A5 - Programa de Parceiros
tags: [whatsapp, compartilhamento, open-graph, previa, parceiro, armadilha]
atualizado: 2026-09-16
---

# ARQ - Previa de link e compartilhamento no WhatsApp 16092026

Dois defeitos de compartilhamento achados em 16/09/2026, os dois no caminho que
o parceiro usa para divulgar. Nenhum dos dois dava erro: os dois falhavam em
silencio.

## 1. O WhatsApp engolia a imagem do material de apoio

O botao **WhatsApp** do material de apoio mandava, pela Web Share API,
`files` **e** `text` juntos.

> **O WhatsApp no Android descarta o arquivo quando recebe `files` + `text`.**
> E pior: ele **aceita** o share — nao rejeita, nao avisa. O parceiro clicava,
> o WhatsApp abria, e chegava so a legenda. A imagem sumia sem erro.

**Conserto:** o pacote do share do WhatsApp passa a levar **so o arquivo**. A
legenda vai para a area de transferencia e o parceiro cola.

> **Regra de ouro:** Web Share API com arquivo **nao** leva texto junto. Um dos
> dois, nunca os dois.

## 2. Os links mais compartilhados do projeto nao tinham previa

`moviki/p.html` e `moviki/pp.html` — o link de indicacao do parceiro e o de
upline, **os links mais compartilhados do projeto inteiro** — tinham
`<title>Moviki</title>` e **zero metatag**. Nenhuma. Colados no WhatsApp,
saiam como cartao mudo: sem titulo util, sem descricao, sem imagem.

**Conserto:** `<title>`, `description`, `og:*` e `twitter:*` nas duas.

> **O crawler de previa le o HTML ANTES de rodar JavaScript.** Por isso a
> metatag funciona mesmo numa pagina que so existe para redirecionar. Foi o que
> permitiu consertar sem tocar no redirecionamento.

## O que sobra

As duas paginas continuam **sem marca de versao**. Ver
[[R - Marcas de versao no ar]].

## Ligacoes

[[A5 - Programa de Parceiros]] · [[A14 - Material de apoio do parceiro]] ·
[[A6 - Medicao e Analytics]] · [[R - Links e identificadores]] ·
[[R - Regras de ouro]] · [[R - Marcas de versao no ar]] ·
[[ARQ - Previa do link da live no WhatsApp 15092026]]
