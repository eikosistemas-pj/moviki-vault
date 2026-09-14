---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, checkout, pix, asaas, subconta, financeiro]
atualizado: 2026-09-14
---

# R - Live - Checkout Pix e subcontas Asaas

Decisões do Paulo em 11/09/2026: **taxa do Moviki 0% no lançamento · checkout só
no Enterprise · só Pix · retirada no local ou entrega combinada pelo próprio
lojista (sem frete)**.

## Como o dinheiro anda

1. O lojista Enterprise abre, no estúdio da live, a aba **Receber no Pix**: uma
   **subconta Asaas em nome dele** (CPF ou CNPJ), criada pela conta principal do
   Moviki.
2. O Asaas pede os documentos (links de envio aparecem na própria aba) e aprova.
3. Aprovada e ligada, a live mostra **Comprar com Pix** no produto.
4. O cliente escolhe a quantidade, põe nome, WhatsApp, CPF e retirada ou entrega.
   O robô emite o Pix **pela subconta do lojista** e devolve QR + copia e cola.
5. O Pix cai **na conta do lojista**. O Asaas avisa o robô (webhook); o pedido
   vira **pago**, o estoque da oferta baixa, e — se o comprador deixou —
   "Ana comprou" aparece no chat.
6. O lojista vê o pedido na hora (Pedidos de hoje), fala com o cliente no
   WhatsApp e marca **entregue**. O saque é feito no app/site do Asaas.

**O dinheiro nunca passa pela conta da Eiko.** O Moviki não guarda nem repassa
valor de venda — não vira intermediador de pagamento. Quando houver taxa, ela
entra por split (`MOVIKI_TAXA_PCT` + `MOVIKI_WALLET_ID`); hoje o split não é
montado.

## Custo e pedido mínimo (confirmado em 12/09)

- **Asaas: R$ 1,99 fixos por Pix recebido**, pagos pelo lojista. Sem mensalidade.
- Por isso o **pedido mínimo subiu de R$ 5,00 para R$ 20,00**: a tarifa cai de
  40% para 10% da venda.
- **Moviki: 0% no lançamento.**

## Teto do período de avaliação

O Asaas mantém o Moviki em avaliação regulatória: **10 subcontas**, **R$ 2.000 em
cobranças por subconta**, **60 dias**. Pedir homologação antes de chegar no teto —
é o que segura o lançamento aberto ([[P29 - Teto de 10 subcontas no Asaas]]).
O painel do dono tem o botão **Conferir no Asaas**: faz `GET /accounts` (só
leitura) e responde em português se a conta já pode criar subconta por API e
quantas existem, do teto de 10. A ação `adm_asaas` é conferida em `admins/{uid}`
no servidor.

## Onde está o código

| Repo | Arquivo | Papel |
| --- | --- | --- |
| moviki-robo | `lib/checkout.js` | toda a lógica. Módulo, não conta no teto de 12 funções |
| moviki-robo | `api/pontos.js` | recebe as ações `loja_*` e `compra_*` antes da exigência de login |
| moviki-robo | `api/webhook.js` | desvia `pedido:<id>` ANTES de tudo e aceita o token `ASAAS_WEBHOOK_TOKEN_PEDIDOS` |
| moviki-app | `live.html` | aba Receber no Pix + Pedidos de hoje |
| moviki | `live.html` | Comprar com Pix, QR, confirmação |
| Firestore | regras v23 | `pedidos` e `checkout_publico` |

## Ações

| Ação | Quem | Faz |
| --- | --- | --- |
| `loja_estado` | lojista Enterprise logado | situação da subconta, etapas, links de documento, liga/desliga |
| `loja_criar` | idem | abre a subconta, cifra a chave, cadastra o webhook da subconta |
| `loja_ligar` | idem | liga/desliga o Pix na live |
| `loja_pedido` | idem | `entregue`, `cancelado` (só aguardando) ou `conferir` (pergunta ao Asaas) |
| `compra_criar` | cliente, sem login | cria cliente + cobrança Pix na subconta e devolve QR |
| `compra_status` | cliente, com a chave do pedido | status; se aguardando, pergunta ao Asaas (plano B do webhook) |
| `adm_asaas` | dono, conferido em `admins/{uid}` | `GET /accounts`: liberação e quantas subcontas existem |

## Dados

- `checkout_contas/{uid}` — chave de API da subconta **cifrada (AES-256-GCM)**
  com a env `CHECKOUT_CHAVE`, walletId, id da conta, status. **Sem regra = ninguém
  lê pelo app.**
- `checkout_publico/{uid}` — `{ ativo }`, o que a live consulta.
- `pedidos/{id}` — itens, total, comprador (nome, WhatsApp, **só os 2 últimos
  dígitos do CPF**), entrega, status (`aguardando`, `pago`, `entregue`,
  `expirado`, `cancelado`, `estornado`), id da cobrança.
- `checkout_freio/{hash do IP}` — 30 pedidos por IP a cada 10 min.

## Travas

- **Preço sai do servidor**, do estado da live: oferta ativa > preço da live >
  preço do cardápio. O que o navegador manda como preço é ignorado.
- Só vende com a **live no ar** (pulso de até 3 min), plano **Enterprise**
  vigente, conta **aprovada** e **ligada**.
- Estoque da oferta conferido antes de gerar o Pix.
- Pedido mínimo R$ 20,00 (`CHECKOUT_MIN`), até 10 unidades por pedido.
- Webhook repetido não conta duas vezes (transação).
- Vencimento ou exclusão depois de pago não desfaz o pago.
- `CHECKOUT_CHAVE` ausente: falha fechada. **Nunca trocar essa env depois de
  criar subconta** — as chaves guardadas ficam ilegíveis.
- Freio por IP largo de propósito: 4G usa IP compartilhado (CGNAT).

## Testado aqui (Firebase e Asaas de mentira)

35 casos do `lib/checkout.js` na primeira rodada e 48 casos no robô na rodada de
12/09: plano Premium barrado, token ruim, CPF/CNPJ inválidos, erro do Asaas
repassado, subconta criada e chave cifrada, webhook cadastrado com a chave da
subconta, público só ativo quando aprovado **e** ligado, preço do servidor
(tentativa de mandar R$ 0,01 ignorada), cobrança na subconta sem split, CPF
inteiro não guardado, estoque, mínimo, produto fora da sacola, chave do pedido,
webhook marca pago e baixa estoque, "Ana comprou", webhook repetido, conferir
manual, sem live não vende, freio, falha fechada. Mais o `api/webhook.js` real:
token errado 401, pedido pago, **nenhuma assinatura falsa criada**.

**Só o teste real prova:** a aprovação dos documentos da subconta e o Pix caindo
de verdade.

## Antes de abrir para cliente

- [ ] Confirmar com o gerente do Asaas: homologação para sair do teto de 10 subcontas e custo por subconta
- [ ] Teste real com R$ 20,00: subconta com o CPF do Paulo, live de teste, pagar de outro banco, conferir pedido pago e saque pelo app do Asaas
- [ ] Termos de uso e privacidade conferidos no ar ([[R - Live - Regras legais e conformidade]])

## Ligações

[[A13 - Modo Live]] · [[P24 - Modo Live - lancamento]] · [[A4 - Financeiro]] ·
[[R - Live - Arquitetura e arquivos]] · [[P29 - Teto de 10 subcontas no Asaas]] ·
[[R - Variaveis de ambiente]] · [[ARQ - Incidente - webhook do Asaas 401 em producao]]
