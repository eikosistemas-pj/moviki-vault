---
type: decisao
status: concluido
area: A4 - Financeiro
tags: [preco, planos, enterprise, anual, decisao]
atualizado: 2026-09-16
---

# ARQ - Enterprise sem plano anual 16092026

**Decisao: o Enterprise nao tera plano anual.** Continua so mensal,
R$ 129,90. Tomada em 16/09/2026, logo apos a troca de precos.

Relacionado: [[ARQ - Troca de precos executada 16092026]] ·
[[R - Planos e precos]] · [[ARQ - Decisao de preco antes do lancamento 16092026]]

---

## O que levantou a questao

Com o toggle da home em **Anual**, os quatro cards liam:
`Gratis` · `R$ 399/ano` · `R$ 699/ano` · `R$ 129,90/mes`.

O card do Enterprise nao tinha `data-anual`, entao o toggle nao o tocava.
Ninguem conclui "este plano nao tem anual" — conclui que **o Enterprise e
absurdamente mais caro que os outros tres**. O plano de maior ticket era o
que mais perdia na comparacao visual.

## Por que NAO criar o anual

1. **Comissao adiantada.** O `webhook.js` paga o parceiro sobre o valor
   efetivamente pago. Enterprise anual a R$ 1.299 pagaria **R$ 194,85 de
   comissao de uma vez**, antes de o cliente completar um mes de uso. Com
   direito de arrependimento de 7 dias e reembolso proporcional, um
   cancelamento no mes 2 deixa a comissao ja paga no negativo. Pro e
   Premium anuais ja carregam esse risco (R$ 59,85 e R$ 104,85); o
   Enterprise o triplicaria, justamente no plano de maior valor.
2. **Ciclo misto na mesma conta.** O ponto extra (R$ 19,90) e uma
   assinatura recorrente **mensal separada**. Base anual + pontos mensais
   na mesma conta e a mesma classe de complexidade que aposentou o
   trimestral horas antes.
3. **Zero cliente pagante.** Criar uma quarta combinacao de checkout para
   um produto que ainda nao vendeu contradiz a decisao que acabou de ser
   tomada.

## O que foi feito em vez disso

`moviki/index.html`, marca **2026-09-16-preco2**: o card do Enterprise
ganhou os spans `data-ciclo-mensal` / `data-ciclo-anual` que Pro e Premium
ja tinham, e uma linha que so aparece no modo anual:

> "O Enterprise e sempre mensal: voce paga mes a mes e cancela quando
> quiser, sem 12 meses de fidelidade."

**A ausencia passa a ser dita, e dita como vantagem.** Nenhum preco mudou,
nenhuma outra tela mudou, o `lib/asaas.js` nao foi tocado.

## Regra que fica

> **Card de plano dentro de um toggle de ciclo precisa responder aos dois
> estados do toggle.** Um card mudo nao le como "nao se aplica" — le como
> preco fora da curva.

## Se um dia o Enterprise anual for criado

- Segurar a comissao do anual em parcelas, ou so liberar apos o prazo de
  arrependimento
- Decidir o que acontece com o ponto extra: entra no anual ou continua
  mensal a parte
- Valor coerente com os outros dois: R$ 1.299,00 (2 meses gratis,
  R$ 108,25/mes)
