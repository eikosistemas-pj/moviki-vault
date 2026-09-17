---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [checkout, pix, metrica, dado, painel]
atualizado: 2026-09-16
---

# ARQ - Origem do pago separada 16092026

No ar em 16/09/2026: `moviki-robo/lib/checkout.js` (`2026-09-16-origempago`) e
`moviki-app/eikoadm01.html` (`2026-09-16-origempago`).

## O defeito

Um pedido chega a `pago` por **dois caminhos que valem coisas diferentes**:

| Caminho | O que prova |
| --- | --- |
| **gateway** | o Asaas confirmou que o dinheiro **caiu na subconta**. E venda, conferida contra o extrato |
| **lojista** | o lojista clicou em **"Recebi"** olhando o proprio celular. E a **palavra dele** |

O documento do pedido **nao guardava a diferenca**. Só a trilha guardava, num
log que nenhum painel le. Entao o card **"Vendido pelo Pix"** somava os dois no
mesmo numero:

- lojista distraido que nunca clica em "Recebi" -> aparecia **vendendo zero**
- lojista que clica sem conferir o extrato -> aparecia **vendendo tudo**

Ou seja: **o numero media a diligencia do lojista, nao a venda.** E e por
numero assim que se decide preco, meta e em quem prestar atencao.

## O que NAO foi feito

Nao se conserta isso escondendo ou desencorajando o caminho manual. No modo
**chave Pix propria nao existe gateway**: confirmar na mao e o **unico** caminho
possivel, e ele e legitimo — foi entregue de proposito em 16/09. O conserto e
**separar os dois no banco** e deixar quem le decidir com a diferenca a vista.

## O que mudou

- `marcarPago(pedidoRef, origem)` passou a exigir a origem e grava
  `confirmadoPor: 'gateway' | 'lojista'` e `confirmadoEm` no pedido.
- As **tres** chamadas que vinham de `confirmarNoAsaas` (conferir do lojista,
  plano B da tela do comprador, webhook) passam `'gateway'`; a de
  `lojaPedidoPix` passa `'lojista'`. Nenhuma chamada ficou sem origem.
- O painel do dono ganhou o KPI **"Conferido no extrato"** ao lado de "Vendido
  pelo Pix hoje", e uma linha embaixo do card que abre as duas origens em
  dinheiro e em quantidade.

## Pedido antigo nao entra em nenhum dos dois

Quem foi pago antes de 16/09 nao tem `confirmadoPor` e cai em **"sem origem
registrada"**, contado a parte. Chutar a origem de dado velho seria inventar
exatamente o que este conserto existe para parar de inventar.

`pedidos` e `write: if false` — so o Admin SDK escreve. **Nenhuma regra nova.**

## Regras de ouro

1. **Numero que soma duas provas diferentes nao mede nenhuma das duas.**
2. **Se o produto tem um caminho que depende da palavra do usuario, esse
   caminho precisa ficar marcado no dado** — nao no log.
3. **Dado antigo sem o campo novo nao se adivinha:** conta separado, com nome.
4. O log de trilha nao substitui campo no documento: **so vale o que o painel
   consegue ler.**

## Ligacoes

[[A13 - Modo Live]] · [[ARQ - Confirmacao manual de pagamento na live 16092026]] ·
[[R - Marcas de versao no ar]]
