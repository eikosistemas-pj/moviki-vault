---
type: decisao
status: concluido
area: A1 - Produto e Paineis
tags: [vik, moviki-ai, modo-cauteloso, alarme, regra-de-ouro]
atualizado: 2026-09-23
---

# Trava contra o Vik desatualizado — 23/09/2026

## Problema
O Vik conhece as telas pela tabela `MARCAS_CONFERIDAS` (`moviki-ai/lib/catalogoPainel.js`). Painel que sobe sem ela deixa o Vik em **modo cauteloso para todos**, sem nenhum sintoma na tela. Aconteceu em 16/09 (três vezes), 22/09 e 23/09 — quase sempre com a entrega vinda de outro chat.

## As três camadas
1. **Alarme no painel do dono** (`eikoadm01.html` `2026-09-23-vikalarme`): ao abrir, o painel lê a marca no ar do `index.html` e do `parceiro.html` e a marca que o Vik conhece. Divergiu → item em "Precisa de você": "Vik em modo cauteloso (...) — subir moviki-ai/lib/catalogoPainel.js". Falhou a leitura → não acende nada (sem alarme falso).
2. **Endpoint** (`moviki-ai/api/chat.js`): `GET` público devolve só `catalogo` e `marcas`. Nenhum dado de usuário.
3. **Regra de ouro nº 13 no `CLAUDE.md`** dos 6 repositórios: subiu `index.html` ou `parceiro.html`, sobe junto a marca, o texto do catálogo e o `CATALOGO_VERSAO` — na mesma entrega. Todo chat e toda sessão do Claude Code lê isso ao começar.

## Por que as três
A regra escrita já existia e falhou cinco vezes: regra depende de quem lembra. O alarme não depende — ele vê a divergência mesmo quando ninguém lembrou.

## Ligações
- [[ARQ - Vik alinhado a rodada2 23092026]]
- [[ARQ - Vik em modo criador 22092026]]
- [[R - Regras de ouro novas de 22092026]]
