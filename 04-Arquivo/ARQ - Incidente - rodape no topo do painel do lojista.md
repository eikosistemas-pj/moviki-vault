---
type: incidente
status: concluido
area: A1 - Produto e Paineis
tags: [armadilha, painel-lojista, layout]
atualizado: 2026-09-10
---

# ARQ - Incidente - rodape no topo do painel do lojista

Introduzido em 03/09/2026 na rodada da credibilidade, achado e corrigido em
05/09 (`moviki-app/index.html`, marca `2026-09-05-resposta`).

## O sintoma

O lojista abria o painel e **a primeira coisa que lia era o CNPJ da EIKO**.

## A causa

O rodape institucional foi colocado no espaco que sobrou do cabecalho antigo —
ou seja, **antes de todo o conteudo**. No `parceiro.html` sempre esteve certo: o
defeito era so no painel do lojista.

## O conserto

Movido para depois do `mvShell`.

## A licao

> **Espaco vago no HTML nao e o lugar certo, e o navegador nao reclama.** Bloco
> novo entra pela posicao que ele deve ocupar na leitura da pagina, nao pelo
> buraco que sobrou de um componente removido.

Corolario: rodape institucional existe para dar autoridade — no topo ele faz o
oposto, comeca a conversa falando de quem cobra em vez de para que serve.

## Ligacoes

[[A1 - Produto e Paineis]] · [[A11 - Marca e Design System]] ·
[[R - Marcas de versao no ar]]
