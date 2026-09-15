---
type: arquivo
status: concluido
area: A4 - Financeiro
tags: [dinheiro, asaas, webhook, seguranca, comissao, regra-de-ouro, armadilha]
atualizado: 2026-09-15
---

# Token de webhook por subconta e valor reconferido — 15/09/2026

Fecha os achados **A1** e **A5** de [[P35 - Auditoria de seguranca do Modo Live]].
Os dois eram exploraveis **hoje**, fora do Modo Live, por um lojista Enterprise.

Entrega: `lib/checkout.js` e `api/webhook.js` (repo `moviki-robo`), **testados**.

---

## 1. O que estava aberto

### A1 — o token do webhook era entregue a cada lojista

`lib/checkout.js` registrava o webhook **dentro da subconta Asaas do lojista**
com `ASAAS_WEBHOOK_TOKEN_PEDIDOS` — **o mesmo token para todas as subcontas**.
A subconta e aberta com o nome, o CPF e **o e-mail dele**: ele entra no Asaas e
le esse token em Integracoes.

E `api/webhook.js` aceitava **qualquer um dos tres tokens para qualquer evento**.

Com o token na mao, de qualquer lugar do mundo:

```
POST /api/webhook
{ "event":"PAYMENT_RECEIVED",
  "payment":{ "id":"x", "externalReference":"<uid>", "value":99.90 } }
```

→ **o plano daquele uid ligava por 34 dias, de graca.** O dele, ou o de
terceiros. Com `TRANSFER_DONE` fechava saque; com `PAYMENT_REFUNDED` derrubava
pedido pago alheio.

E `acumularComissoes` usava `Number(pay.value)` **do proprio payload**: um evento
com `value: 20000` gerava **R$ 3.000 de comissao sacavel por Pix**.

O caminho de PEDIDO ja fazia o certo — `confirmarNoAsaas` pergunta ao Asaas
antes de marcar pago. O caminho da MENSALIDADE nao fazia.

### A5 — auto-indicacao

`acumularComissoes` **nunca comparava `p1.uid` com `lojistaUid`**. A trava
equivalente **existe** na cadeia de parceiros (a regra do Firestore recusa
`indicadoPor == slug` proprio) e faltava aqui.

O parceiro aprovado abria a propria conta de lojista com `?ref=<slug dele>`,
assinava Enterprise e recebia **15-18% da propria mensalidade, todo mes, para
sempre** — e o upline dele ainda levava N2 e N3 no primeiro pagamento.

---

## 2. O que foi feito

### 2.1 Token proprio por subconta

- gerado no `lojaCriar` (`crypto.randomBytes(24)`), **passado ao Asaas dentro do
  proprio `POST /accounts`**, no campo `webhooks` documentado em docs.asaas.com
  — **uma chamada a menos** que o desenho anterior;
- guardado **cifrado** em `checkout_contas/{uid}.whToken` (mesma cifra
  AES-256-GCM da chave da subconta);
- indexado em **`checkout_tokens/{sha256(token)}` → `{ uid }`**: o webhook
  descobre o dono em **uma leitura direta**, sem varrer coleção. Guardar o hash,
  e nao o token, significa que quem ler a colecao **nao consegue assinar
  chamada nenhuma**.

⚠️ **O indice e gravado ANTES de conferir o webhook.** O Asaas ja cria o webhook
junto com a conta; se o indice nao existisse ainda, o primeiro evento chegaria
com token sem dono e seria recusado.

### 2.2 O token passa a definir ESCOPO, nao so entrada

| Token | Pode |
| --- | --- |
| `ASAAS_WEBHOOK_TOKEN` (mae) | tudo |
| `ASAAS_WEBHOOK_TOKEN_TRANSFER` | so `TRANSFER_*` |
| token proprio da subconta | so `pedido:` **daquela subconta** (o dono e conferido em `pedidos/{id}.lojistaUid`) |
| `ASAAS_WEBHOOK_TOKEN_PEDIDOS` (legado) | so `pedido:` — e **some quando a env for apagada** |

Recusa por escopo responde **200** e marca o evento como **`ok`**, de proposito:
nao e falha nossa a reprocessar, e 200 impede a fila do Asaas de pausar
(doutrina de 14/09, artigo 6).

### 2.3 O valor passa a vir do Asaas, nunca do payload

No ramo que LIGA assinatura, o pagamento e **reconferido com a chave MAE**
(`GET /payments/{id}`). Valem o `value`, o `status` e o `externalReference` que
**o Asaas devolver**. Sem confirmacao, **nao liga nada** (falha fechada).
`acumularComissoes` e `registrarPurchase` passaram a receber esse objeto
confirmado, nao o do corpo da requisicao.

### 2.4 Auto-indicacao barrada

`if (p1.uid === lojistaUid) return;` — **barra o pagamento inteiro**, nao so o
nivel 1: N2 e N3 so existem por causa de uma indicacao que nao vale. Mais
`p2.uid !== lojistaUid` e `p3.uid !== lojistaUid`.

### 2.5 De quebra: o pedido do modo B que nunca confirmava (C15 da auditoria)

`confirmarNoAsaas` lia **sempre** `checkout_contas/{uid}`, que so existe no modo
subconta. No **modo B (Asaas conectado)** a chave mora em
`recebimento/{uid}.asaasChave` — a funcao devolvia `'erro'` para sempre: **o
comprador pagava, o webhook nao confirmava, o botao Conferir pagamento nao
confirmava, e o pedido ficava `aguardando` eternamente.** Agora a chave e
escolhida pelo `modo` do pedido (`chaveDoPedido`), e o cancelamento no Asaas
tambem.

### 2.6 Rotacao, para nao precisar recriar subconta

Acao nova do dono: **`adm_wh_rotacionar`** (conferida em `admins/{uid}` no
servidor). Apaga os webhooks que apontam para a nossa URL, cria um com token
novo e reindexa. O hash antigo **continua no indice de proposito** — apagar
abriria uma janela em que um evento ja em transito chegaria sem dono.

---

## 3. Testes

`16/16` no escopo do webhook, mais dois de comissao:

| # | Caso | Resultado |
| --- | --- | --- |
| 1 | token desconhecido | 401 |
| 2 | token de subconta tentando ligar assinatura | recusado, **assinatura nao criada** |
| 3 | token de subconta em `TRANSFER_DONE` | recusado |
| 4 | token legado tentando ligar assinatura de R$ 5.000 | recusado |
| 5 | token mae, Asaas fora do ar | **nao liga** (falha fechada) |
| 6 | token mae, Asaas diz `PENDING` | recusado por status |
| 7 | payload com `value: 20000`, Asaas diz 99,90 | liga, **e o payload e ignorado** |
| 8 | `externalReference` divergente do Asaas | recusado |
| 9 | pedido de OUTRO lojista com token de subconta | recusado por dono |
| 10 | pedido do proprio lojista | passa |
| 11 | toda recusa responde 200 | sim |
| 12 | auto-indicacao (parceiro = lojista) | **zero comissao**, nem N2/N3 |
| 13 | fluxo legitimo (parceiro ≠ lojista) | comissao de 15% = **R$ 14,99** de R$ 99,90 |

---

## 4. Ordem de upload — importa

1. **`moviki-robo/lib/checkout.js` — SOZINHO E PRIMEIRO.**
2. **`moviki-robo/api/webhook.js`.**

⚠️ **Nao criar subconta entre os dois uploads.** Com o `checkout.js` novo e o
`webhook.js` velho, uma subconta nasceria com token proprio que o webhook antigo
nao reconhece → 401 nos pedidos dela. O caminho inverso (webhook novo, checkout
velho) nao quebra: `uidPorTokenWebhook` esta dentro de try/catch.

**Envs: nenhuma nova.** `ASAAS_WEBHOOK_TOKEN_PEDIDOS` vira **legado opcional**.

⚠️ **So apague essa env depois de rotacionar as subcontas que ja existem** —
enquanto existirem subcontas com o token antigo, apagar a env faz o webhook
delas responder 401. Quantas existem: botao **Conferir no Asaas** no painel do
dono (`adm_asaas`). **Se for 0, apague a env junto com este upload.**

---

## 5. Regras de ouro que nascem aqui

> **1. Token que e entregue a um terceiro nao e credencial de autorizacao.**
> Ele diz *quem* chamou, nunca *o que pode ser feito*. Segredo que sai da nossa
> mao define ESCOPO — e o escopo mais estreito que servir.

> **2. Valor de dinheiro nunca vem do corpo do webhook.**
> O corpo e um aviso de "va conferir". A fonte e a consulta ao gateway, com a
> nossa chave. Sem confirmacao, nao liga (falha fechada).

> **3. Trava que existe numa ponta tem que existir na outra.**
> A auto-indicacao estava barrada na regra do Firestore e aberta no servidor que
> paga. Regra de negocio escrita em dois lugares diverge — e diverge calada.

⚠️ Estas tres entram em `03-Recursos/R - Regras de ouro.md`. **A nota nao foi
substituida aqui**, pela mesma razao de 14/09: sem o arquivo integral em maos,
substituir apagaria regra antiga. A fusao e uma rodada propria.

## 6. Marcas de versao

| Arquivo | Marca |
| --- | --- |
| `moviki-robo/lib/checkout.js` | `2026-09-15-whtoken` |
| `moviki-robo/api/webhook.js` | `2026-09-15-escopo` |

Entram em `03-Recursos/R - Marcas de versao no ar.md` na proxima fusao.

## 7. Fica aberto

- [ ] Botao de **rotacionar webhook** no painel do dono (a acao existe no
      servidor; hoje so da para chamar por fetch autenticado)
- [ ] Apagar `ASAAS_WEBHOOK_TOKEN_PEDIDOS` depois de conferir/rotacionar
- [ ] Achado **B11** (`saques.pedidoEm` escrito pelo cliente) e **B12** (saque
      pago em dobro) — continuam abertos em [[P35 - Auditoria de seguranca do Modo Live]]

## Ligacoes

[[P35 - Auditoria de seguranca do Modo Live]] · [[A4 - Financeiro]] ·
[[R - Doutrina de seguranca financeira]] ·
[[R - Live - Checkout Pix e subcontas Asaas]] ·
[[ARQ - Decisao sobre o BaaS do Asaas]]
