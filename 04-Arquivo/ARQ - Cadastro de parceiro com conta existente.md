---
type: arquivo
status: concluido
area: A5 - Programa de Parceiros
tags: [cadastro, parceiros, onboarding]
atualizado: 2026-09-10
---

# ARQ - Cadastro de parceiro com conta existente

No ar em 04/09/2026: `moviki-app/seja-parceiro.html`, marca
`2026-09-04-conta-existente`.

## O problema

A pagina so sabia **criar conta nova**. Quem ja tinha conta batia em "use outro
e-mail" — **inclusive o dono**, que foi como o defeito apareceu.

O sistema **sempre** permitiu ser lojista e parceiro na mesma conta: a caixa de
mensagens e compartilhada exatamente por isso (`conversas/{uid}` e por uid da
conta, nao por papel).

## O conserto

Se a conta existe, a pagina **entra nela** com a senha digitada e **adiciona** o
cadastro de parceiro. Se a pessoa ja for parceiro, avisa e nao sobrescreve.

## A licao

> **Tela de cadastro que so sabe criar conta exclui o usuario mais valioso: o que
> ja esta dentro.** Quando o mesmo uid pode ter dois papeis, o fluxo de entrada
> precisa saber acrescentar papel, nao so nascer.

## Ligacoes

[[A5 - Programa de Parceiros]] · [[A1 - Produto e Paineis]] ·
[[R - Marcas de versao no ar]]
