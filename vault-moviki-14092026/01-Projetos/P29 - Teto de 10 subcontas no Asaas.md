---
type: projeto
status: bloqueado
area: A4 - Financeiro
tags: [asaas, subcontas, pix, checkout, lancamento]
atualizado: 2026-09-14
prioridade: 1
prazo: 2026-09-30
---

# P29 - Teto de 10 subcontas no Asaas

**É esta pendência que segura o lançamento aberto do Modo Live.** Nada de
técnico falta: o módulo está no ar, o interruptor do beta esvazia numa tela. O
que não existe é espaço para mais de dez lojistas recebendo por Pix.

## O que já está resolvido

Conferido no painel do dono, botão "Conferir no Asaas": resposta **Liberado,
0 de 10 subcontas**. A conta da Eiko pode criar subconta por API. Não precisou
de atendente.

## O teto

| Item | Valor |
| --- | --- |
| Subcontas permitidas | 10 |
| Volume por subconta | R$ 2.000 |
| Janela | 60 dias |

É limite regulatório, não comercial. Com dez lojistas usando o Pix na live, o
próximo que assinar Enterprise não consegue receber — e isso não é uma tela de
erro aceitável.

## A tarifa e o efeito no produto

O Asaas desconta **R$ 1,99 fixos por recebimento Pix**, pagos pelo lojista. Não
é percentual: pesa igual num pedido de R$ 5 e num de R$ 200.

Consequência já aplicada: **o pedido mínimo do checkout subiu de R$ 5 para
R$ 20.** Em R$ 5 a tarifa comeria 40% do pedido. A taxa do Moviki continua 0%.

Esse número é falado na aula 7 do módulo de videoaulas — se a tarifa mudar, a
aula precisa ser refeita.

## Etapas

- [ ] Perguntar ao Asaas o caminho formal para elevar o teto de subcontas e o de
      volume, e o que a Eiko precisa apresentar.
- [ ] Descobrir se há plano ou contrato do Asaas sem o teto de 10, e a que custo.
- [ ] Avaliar alternativa de provedor de split/subconta, com a mesma pergunta de
      tarifa fixa por Pix.
- [ ] Definir a regra de fila: o que a tela mostra ao 11º lojista que pedir Pix
      na live enquanto o teto não subir.
- [ ] Só depois: esvaziar a lista `liveBeta` e abrir o produto.

## Ligações

[[A4 - Financeiro]] · [[A13 - Modo Live]] ·
[[R - Live - Checkout Pix e subcontas Asaas]] · [[R - Planos e precos]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[P24 - Modo Live - lancamento]] · [[P28 - Videoaulas do Modo Live]] ·
[[ARQ - Incidente - webhook do Asaas 401 em producao]] ·
[[ARQ - Live escondida durante o beta 14092026]]
