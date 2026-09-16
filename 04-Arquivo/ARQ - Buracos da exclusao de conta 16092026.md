---
type: incidente
status: aberto
area: A5 - Financeiro
tags: [exclusao, asaas, comissao, lgpd, armadilha]
atualizado: 2026-09-16
---

# ARQ - Buracos da exclusao de conta 16092026

Conferido lendo `moviki-robo/api/exclusoes.js` em 16/09, antes de apagar as
contas de teste.

## O que esta certo

A exclusão **cancela a assinatura no Asaas** e na ordem certa: `DELETE
/subscriptions/{id}` **antes** de apagar o faturamento, lendo o
`asaasSubscriptionId` enquanto o documento ainda existe. Cobrança órfã por
esquecimento não acontece.

## Buraco 1 - falha no cancelamento nao para a exclusao

O `DELETE` está num try/catch que grava `assinaturaErro` no resumo e **segue
apagando tudo**. Asaas fora do ar ou chave expirada: a conta some, o
`asaasSubscriptionId` some junto com o documento de faturamento, e a assinatura
continua viva **sem nenhum rastro no Firestore** para encontrá-la depois. O erro
aparece na tela quando já é irreversível.

## Buraco 2 - comissao orfa (grave)

A limpeza roda `where('parceiroUid','==',uid)` — só quando quem sai é o
**parceiro**. As comissões carregam também **`lojistaUid`**, e **não existe
nenhuma limpeza por esse campo**.

Excluir um lojista deixa na carteira do parceiro a comissão que aquele lojista
gerou. E `pagar-saque.js` monta o saque lendo `comissoes where parceiroUid`
direto — não há saldo agregado que pudesse divergir e denunciar. **A comissão
órfã é indistinguível de uma legítima e sai por Pix normalmente.**

## Conserto

Arquivo inteiro em `moviki-robo/api/exclusoes.js`: abortar se o cancelamento
falhar e limpar comissão por `lojistaUid`. Enquanto isso, a ordem manual está em
[[P - Abertura da live para lojista pagante]].

## Ligacoes

[[A5 - Financeiro]] · [[R - Regras de ouro]] · [[R - Programa de parceiros]]
