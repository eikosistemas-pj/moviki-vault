---
type: projeto
status: bloqueado
prioridade: 1
area: A2 — Infraestrutura e Deploy
prazo: 2026-09-10
tags: [infra, seguranca, armadilha]
atualizado: 2026-09-03
---

# P15 — Ligar o enforcement do App Check

Instalar foi metade. A proteção **só passa a valer** quando a chave é virada no Console do Firebase, e ela ainda não foi — de propósito.

## Onde o App Check já está

Oito páginas, todas as que falam com o Firebase:

`moviki/index.html` · `moviki/404.html` · `moviki/descadastro.html` · **`moviki/v.html`** (entrou em 03/09, tinha ficado de fora) · `moviki-app/index.html` · `moviki-app/eikoadm01.html` · `moviki-app/parceiro.html` · `moviki-app/seja-parceiro.html`

Conferido no GitHub em 03/09: **8 de 8**. As demais páginas dos dois repositórios não tocam no Firebase e não precisam do bloco.

## O que bloqueia

**`moviki/api/og.js`** — o cartão de compartilhamento de cada negócio no WhatsApp e no Facebook. Ele lê o Firestore pela **API REST, do servidor**, sem passar por navegador nenhum. Requisição de servidor não carrega token de App Check.

Enforçando o Firestore hoje, é provável que essa leitura passe a ser recusada e **todo link de lojista compartilhado vire cartão cinza** — que, no modelo single-vendor, é o canal de distribuição inteiro. Seria pior que o problema que o App Check resolve.

## O caminho, nesta ordem

1. Deixar as 8 páginas rodando alguns dias, com gente usando de verdade.
2. Firebase Console → **App Check** → métricas do **Cloud Firestore**: ver a divisão entre **verificadas** e **não verificadas**.
3. Sobrando um resto teimoso de não verificadas, é o `og.js`. Converter para **Admin SDK com conta de serviço**, que passa por cima do App Check por definição. Env nova no projeto Vercel do site — que hoje tem só 1 função das 12 (`api/og.js`), então há espaço de sobra.
4. **Só com o tráfego limpo é que a chave vira.**

## O que fica exposto enquanto isso

A escrita anônima — avaliações, resumo de avaliações, métricas por negócio, newsletter — segue **sem limite de velocidade**. Está protegida só pelas regras v19/v20, que dizem **o que** pode ser gravado, não **quem** pode gravar. Um script determinado ainda infla contador de outro negócio.

## Regra de ouro que nasceu daqui

> **App Check não vê só o navegador.** Todo pedaço do sistema que fala com o Firebase **de servidor** não carrega token e vira "não verificado". Antes de enforçar, listar quem fala com o Firebase de fora do navegador e dar a esses o Admin SDK — senão o enforcement quebra o que ninguém estava olhando.

> **App Check só se enforça depois que TODA página que fala com o Firebase o inicializa.** Enforçar com uma página de fora derruba aquela página inteira, calada.

## Ligações

[[A2 - Infraestrutura e Deploy]] · [[A3 - Dados e Regras]] · [[P14 - Verificacao de parceiro]] · [[R - Regras de ouro]] · [[ARQ - Auditoria de seguranca 03092026]]
