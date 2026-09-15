---
type: decisao
status: concluido
area: A4 - Financeiro
tags: [dinheiro, checkout, pix, cartao, decisao]
atualizado: 2026-09-15
---

# Decisao sobre cartao de credito na venda — 15/09/2026

**Decidido por Paulo em 15/09/2026: o Moviki lanca com Pix. Cartao de credito
fica para depois.** Nada muda no que ja esta construido.

Liga [[P31 - Financeiro e cardapio compravel]] ·
[[ARQ - Decisao sobre o BaaS do Asaas]] · [[A13 - Modo Live]].

---

## 1. A separacao que a decisao deixa registrada

**Cartao e BaaS sao decisoes diferentes.** O cartao **nunca dependeu** de BaaS
nem de subconta: no **Modo B** (Asaas conectado, chave de API da conta do
proprio lojista) a cobranca pode sair como cartao **sem consumir o teto de 10
subcontas e sem por a EIKO na cadeia do dinheiro**.

O que falta e so tecnico: `mr/lib/checkout.js:553` fixa
`billingType: 'PIX'`. A conta ja emite cartao — `mr/api/criar-assinatura.js:89`
usa `billingType: 'UNDEFINED'`, deixando o lojista escolher Pix, cartao ou
boleto na **mensalidade do proprio Moviki**.

⚠️ **A receita recorrente do Moviki nao perde nada com esta decisao.** Ela ja
aceita cartao. O adiamento vale so para a venda do lojista dentro da live e do
cardapio.

## 2. Por que adiar nao custa o que parece

Numeros de **junho a agosto de 2026** (dados de transacao da Nuvemshop e pesquisa
NuvemCommerce 2026, 1.500+ varejistas):

| Fato | Numero |
| --- | --- |
| Pix no e-commerce brasileiro | quase **metade das transacoes**, +50% no ano |
| Cartao | lidera em **faturamento**, nao em volume |
| Ticket medio Pix | **R$ 233,80** |
| Ticket medio cartao | **R$ 339,97** (45% maior) |
| Ticket medio em 12x | **R$ 1.003** |
| Lojistas que dao desconto no Pix | 52% |

**O cartao ganha no parcelado longo, e o Moviki nao esta nessa faixa.** Pedido
minimo de R$ 20 no Modo B e R$ 5 no Modo A. Feira, pastel, semijoia de bairro,
roupa em live: e o terreno onde o Pix ja domina.

## 3. O que o cartao cobraria pela venda a mais

- Taxa de **3% a 4%** por venda, contra **R$ 1,99 fixos** do Pix.
- **Chargeback**, que no Pix nao existe. Na live o produto sai na hora: cartao
  clonado com entrega imediata e o cenario classico de prejuizo — e **o prejuizo
  cai no lojista**, que e quem vende.
- Captura de dado de cartao: PCI, tokenizacao, mais uma superficie para a
  auditoria de [[P35 - Auditoria de seguranca do Modo Live]] cobrir.

**Irreversibilidade do Pix, para feirante, e vantagem — nao limitacao.**

## 4. O gatilho de reavaliacao

Nao reabrir por intuicao. Reabrir quando **o beta fechado mostrar**:

- pedido travado por falta de parcelamento, relatado por lojista do beta; **ou**
- ticket medio dos pedidos pagos passando de ~R$ 300 de forma consistente; **ou**
- entrada de categoria de ticket alto (semijoia em lote, eletronico, movel).

Nenhum dos tres aconteceu ate 15/09/2026 — **nao ha pedido pago em producao
ainda.**

## 5. O que NAO fazer por causa disto

- Nao adotar BaaS para "ter cartao" — ver [[ARQ - Decisao sobre o BaaS do Asaas]].
- Nao prometer cartao em peca de divulgacao, aula ou pagina de venda.
- Nao mexer no `lib/checkout.js` por antecipacao: o arquivo esta com defeitos
  abertos em [[P35 - Auditoria de seguranca do Modo Live]] e toda entrega dele
  sobe **sozinha e primeiro**, pela regra de ouro que nasceu do webhook de 11/09.

## Fontes

- [Pix ou cartao? Dados mostram como o brasileiro paga no comercio eletronico](https://www.ecommercebrasil.com.br/noticias/pix-ou-cartao-dados-mostram-como-o-brasileiro-paga-no-comercio-eletronico)
- [Pix chega a 42% dos pagamentos on-line no Brasil](https://www.poder360.com.br/poder-economia/pix-chega-a-42-dos-pagamentos-on-line-no-brasil/)
