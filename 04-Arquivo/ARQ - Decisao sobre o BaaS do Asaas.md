---
type: decisao
status: concluido
area: A4 - Financeiro
tags: [asaas, baas, subcontas, dinheiro, conformidade, decisao]
atualizado: 2026-09-15
---

# Decisao sobre o BaaS do Asaas — 15/09/2026

Pergunta do Paulo: achou a documentacao de **criacao de subcontas BaaS** e
perguntou se colocamos em pratica.

**Decisao: NAO adotar o BaaS agora.** Aproveitar tres coisas concretas da
documentacao, uma delas ja aplicavel a um defeito critico aberto.

Liga [[P29 - Teto de 10 subcontas no Asaas]] ·
[[P31 - Financeiro e cardapio compravel]] ·
[[P35 - Auditoria de seguranca do Modo Live]] ·
[[R - Live - Checkout Pix e subcontas Asaas]].

---

## 1. A premissa que a documentacao derruba

**O BaaS nao remove o teto.** Os mesmos limites do periodo de avaliacao
regulatoria valem para ele, palavra por palavra:

- **10 subcontas** por conta-pai;
- **R$ 2.000,00 em cobrancas por subconta**;
- **60 dias corridos** a partir da primeira subconta criada em Producao;
- atingido qualquer um: *"a criacao de novas subcontas e emissao adicional de
  cobrancas, assinaturas, links de pagamento sera automaticamente bloqueada"* —
  e as **assinaturas existentes sao canceladas automaticamente**.

Ou seja: **o BaaS nao e a saida do que segurou o lancamento.** Quem tira o teto
e a homologacao regulatoria, que vale para os dois modelos.

## 2. O que o BaaS realmente muda — e por que isso pesa contra

No BaaS *"seu cliente nao precisara ter acesso ao nosso sistema e nao recebera
nenhuma comunicacao por parte do Asaas"*. Bonito de marca. Caro de operacao:

| No BaaS, quem faz | Hoje, quem faz |
| --- | --- |
| Tela de abertura de conta, no Moviki | Asaas |
| Envio de documento e selfie, pelo `onboardingUrl` ou API | Asaas |
| Tela de saldo | app do Asaas |
| **Tela de saque (Pix/TED)** | app do Asaas |
| Comunicacao com o titular | Asaas |

⚠️ **Isto contradiz o produto que ja esta escrito.** A aula `mod-live-pix` diz,
com estas palavras: *"O saque do dinheiro e feito por voce, no aplicativo ou no
site do Asaas."* No BaaS **esse aplicativo deixa de existir para o lojista** — o
Moviki teria que construir e manter um modulo bancario inteiro: saldo,
extrato, saque, onboarding, documentos, status.

E mais: o modelo *"esta sujeito as regras de exposicao e identificacao do Asaas
como instituicao prestadora, conforme a Resolucao Conjunta n. 16/17"*, exige
**conta-pai PJ**, **alinhamento previo com o gerente de contas** e homologacao
com *"Playbook de adequacao"*, documentacao e checklists.

**Mais responsabilidade regulatoria e mais codigo para o Paulo manter sozinho —
em troca de zero alivio no teto.**

## 3. O ponto decisivo: a subconta ja tinha sido adiada em 14/09

[[P31 - Financeiro e cardapio compravel]] fechou isto ha um dia, depois de o
suporte do Asaas nao responder sobre o teto:

- **Modo A — Pix direto do lojista: o PADRAO.** Sem Asaas, sem tarifa, **sem teto**.
- **Modo B — Asaas conectado:** o lojista cola a chave da **propria conta**.
  Nao usa subconta, **nao consome o teto de 10** e **nao poe a EIKO na cadeia**.
- **Modo C — Subconta: ADIADO.** So se o Asaas liberar o teto e se aparecer
  lojista que nao consegue abrir conta propria.

**Adotar BaaS agora seria voltar atras nessa decisao e reintroduzir a Eiko na
cadeia do dinheiro — que e exatamente o que os modos A e B evitam.**

BaaS so volta a fazer sentido no dia em que o Modo C voltar **e** o volume
justificar operar um banco dentro do Moviki. Nao e hoje.

---

## 4. O que APROVEITAR da documentacao, agora

### 4.1 `authToken` por subconta na criacao — conserta o defeito critico A1

O `POST /v3/accounts` aceita o campo **`webhooks`**, com `url`, `events` e
**`authToken`**, na propria criacao da subconta.

Isso resolve, sem mudar de modelo, o achado mais grave de
[[P35 - Auditoria de seguranca do Modo Live]]:

> hoje `mr/lib/checkout.js:316-325` grava o webhook na subconta com o
> **`ASAAS_WEBHOOK_TOKEN_PEDIDOS`, o mesmo para todos**, e
> `mr/api/webhook.js:585-591` aceita os tres tokens **para qualquer evento** —
> um lojista que leia esse token liga assinatura de graca e fabrica comissao.

**Correcao com o que a documentacao mostra:**
1. gerar um token **aleatorio por subconta** no `lojaCriar`;
2. passa-lo no campo `webhooks` **do proprio `POST /accounts`** (uma chamada a
   menos que hoje, que faz `POST /webhooks` depois);
3. guardar cifrado em `checkout_contas/{uid}`;
4. no `api/webhook.js`, token de subconta **so vale para o ramo `pedido:`**.

Vale igual no modelo de subconta padrao. **Nao depende de BaaS.**

### 4.2 Homologacao regulatoria pode ser pedida JA

*"A solicitacao pode ser iniciada a qualquer momento durante o periodo de
avaliacao, sem necessidade de aguardar o prazo de 60 dias."*

**Nao e preciso bater no teto para pedir.** E a acao concreta de
[[P29 - Teto de 10 subcontas no Asaas]], que estava parada esperando resposta do
suporte: abrir a solicitacao de homologacao pelo gerente de contas, pedindo o
**Playbook de adequacao** e a lista de documentos.

⚠️ E a mesma porta que nao respondeu em 14/09. Entao: **pedir, e nao parar o
lancamento esperando.** Os modos A e B ja tiram a subconta do caminho critico.

### 4.3 Acompanhar aprovacao por webhook, nao por botao

- evento **`ACCOUNT_STATUS_GENERAL_APPROVAL_APPROVED`** avisa a aprovacao;
- **`GET /v3/myAccount/status`** confirma: aprovado quando `general === 'APPROVED'`;
- **esperar no minimo 15 segundos** depois de criar a conta antes de consultar
  os documentos pendentes em `GET /v3/myAccount/documents`.

Hoje o estudio depende do lojista tocar em **Conferir de novo**. Com o evento, a
aba acende sozinha quando o Asaas aprova.

---

## 5. O que fica decidido

| Item | Decisao |
| --- | --- |
| Adotar BaaS agora | **Nao** |
| Modelo de recebimento | Modo A (padrao) e Modo B (upgrade), como em [[P31 - Financeiro e cardapio compravel]] |
| Subconta (Modo C) | continua adiada |
| Token de webhook por subconta | **Fazer** — conserta A1 de [[P35 - Auditoria de seguranca do Modo Live]] |
| Homologacao regulatoria | **Pedir agora**, sem esperar o teto |
| Webhook de status da conta | **Fazer** quando o Modo C voltar |
| Reavaliar BaaS | so com Modo C ativo e volume que justifique |

## Fontes

- [Criacao de subcontas com o BaaS do Asaas](https://docs.asaas.com/docs/cria%C3%A7%C3%A3o-de-subcontas-baas)
- [FAQ Periodo de Avaliacao](https://docs.asaas.com/docs/faq-periodo-de-avaliacao)
- [BaaS com o Asaas](https://docs.asaas.com/docs/sobre-baas)
- [Detalhamento do fluxo de aprovacao de subcontas](https://docs.asaas.com/docs/detalhamento-do-fluxo-de-aprova%C3%A7%C3%A3o-de-subcontas)
