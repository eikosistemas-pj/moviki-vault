---
type: projeto
status: em-andamento
area: "[[A13 - Modo Live]]"
tags: [financeiro, checkout, pix, cardapio, asaas, seguranca]
prioridade: alta
prazo: 2026-09-30
atualizado: 2026-09-14
---

# P31 — Financeiro e cardapio compravel (Fase 1)

Destrava a venda sem depender do Asaas. Decidido por Paulo em 14/09/2026 depois
de o suporte do Asaas nao responder sobre o teto de 10 subcontas.

Normativa: [[R - Doutrina de seguranca financeira]].
Auditoria de partida: [[ARQ - Auditoria de seguranca do dinheiro 14092026]].

## Decisoes fechadas em 14/09

- Cardapio compravel no **Premium e Enterprise**. Live continua so no Enterprise.
- **Pix direto do lojista e o modo PADRAO** — sem Asaas, sem tarifa, sem teto.
  Asaas conectado e upgrade opcional.
- **Responsabilidade do pedido e do lojista**, com termo explicito, canal de
  denuncia e bloqueio do reincidente.
- Um unico modulo de checkout serve live e cardapio.

---

## 1. Os dois modos de recebimento

### Modo A — Pix direto (padrao)
O lojista cadastra a propria chave Pix. O servidor monta o payload EMV e o QR.
O dinheiro cai na conta dele, sem intermediario e sem tarifa.

Confirmacao: o comprador anexa o comprovante, o pedido entra em conferencia e o
lojista confirma num toque. Para facilitar a conferencia, **cada pedido recebe
centavos unicos** (R$ 20,07, R$ 20,13) — o lojista bate o valor no extrato sem
procurar nome.

Limite honesto: o Moviki nao sabe, por conta propria, que o pagamento caiu.
Isso vai escrito na tela do lojista, nao escondido.

### Modo B — Asaas conectado (upgrade)
O lojista cola a chave de API da propria conta Asaas. Cobranca emitida pela
conta dele, confirmacao automatica por webhook, tarifa de R$ 1,99 por Pix paga
por ele. Nao usa subconta, nao consome o teto de 10 e nao poe a EIKO na cadeia.

### Modo C — Subconta (adiado)
So se o Asaas liberar o teto e se aparecer lojista que nao consegue abrir conta
propria. Fora do escopo da Fase 1.

Um modo ativo por vez, por negocio.

---

## 2. Menu Financeiro no painel do lojista

Aba nova, visivel no Premium e Enterprise.

**2.1 Como eu recebo**
- Escolha do modo, com comparacao honesta (tarifa, confirmacao, o que exige).
- Modo A: chave Pix (tipo + valor), nome do recebedor, CPF/CNPJ do titular.
  Validacao de formato no cliente e de digito verificador no servidor.
- Modo B: campo da chave de API, botao "testar conexao", estado
  conectada/nao conectada com data. A chave nunca volta para a tela.
- Troca de chave exige reautenticacao e dispara e-mail e aviso no painel.

**2.2 Regras de venda**
- Pedido minimo (piso de R$ 20 no modo B por causa da tarifa; R$ 5 no modo A).
- Retirada no local, entrega combinada, ou os dois.
- Prazo para confirmar o pedido (padrao 30 min) e horario de atendimento.
- Aceite versionado dos Termos de Venda do lojista. Sem aceite, sem botao de
  comprar.

**2.3 Vendas**
- Lista unica, com origem marcada (live ou cardapio), status e valor.
- Cartao do pedido: itens, comprovante anexado, botoes Confirmar / Recusar,
  contato do comprador, forma de entrega.
- Aviso sonoro e no titulo da aba quando entra pedido novo.

**2.4 Extrato**
- Entradas do periodo, taxa (zero no modo A), ticket medio, itens mais vendidos.
- Exportar CSV.

Nao se mistura com o saldo de comissao do parceiro: outro painel, outro dinheiro.

---

## 3. Cardapio compravel

O cardapio hoje e um array dentro de `negocios/{uid}` —
`cardapio: [{categoria, capa, produtos: [{nome, preco, acabando, fotos, descricao}]}]`.
Produto **nao tem id estavel**, e o preco e texto livre. Duas consequencias:

1. **Cada produto ganha um `sku`** curto e estavel, gerado ao salvar o cardapio.
   Sem isso, renomear ou reordenar um item aponta o pedido para o vazio.
2. **So e vendavel o produto com preco numerico valido.** "a partir de 10",
   "sob consulta" e campo vazio continuam aparecendo no cardapio, sem botao de
   comprar. O servidor usa o mesmo `precoNum` que o checkout ja tem.

Na pagina publica (`moviki/404.html` e a pagina do app):
- botao "Adicionar" por produto vendavel, sacola flutuante, tela de pedido;
- produto marcado como "acabando" aceita pedido; produto sem preco, nao;
- se o negocio nao tem recebimento configurado, o cardapio segue igual ao de
  hoje — nenhuma tela nova aparece.

---

## 4. Maquina de estados do pedido

```
       (comprador envia)
aguardando_pagamento ──30 min──> expirado
        │
        ├─ modo A: comprador anexa comprovante ─> em_conferencia
        │            lojista confirma ─> pago
        │            lojista recusa  ─> recusado
        │
        └─ modo B: webhook do Asaas ─> pago
                                        │
                             lojista marca ─> entregue
                                        │
                              estorno ─> estornado
```

Regras duras:
- Quem escreve status e o Admin SDK (modo B) ou o lojista dono (modo A). O
  comprador nunca escreve status.
- `pago` e terminal para valor: o total congela na criacao e nao muda mais.
- Transicao invalida e rejeitada no servidor, nao escondida na tela.
- Todo salto de estado grava trilha com quem, quando, IP e valores.

---

## 5. Dados no Firestore

| Colecao | Quem escreve | Quem le |
|---|---|---|
| `recebimento/{uid}` | so Admin SDK | ninguem pelo app (segredo cifrado) |
| `recebimento_publico/{uid}` | so Admin SDK | publico: `{ativo, modo, minimo, entrega}` |
| `pedidos/{id}` | Admin SDK cria; lojista dono atualiza status | lojista dono; comprador so pelo token do pedido |
| `pedidos_trilha/{id}/eventos` | so Admin SDK | so painel do dono |
| `webhook_eventos/{eventId}` | so Admin SDK | ninguem |
| `checkout_freio/{id}` | so Admin SDK | ninguem |

- `negocios/{uid}` ganha `sku` dentro do cardapio e o campo `vendaAtiva`.
- O comprador acompanha o pedido por link com token aleatorio de 32 caracteres,
  nao por sessao logada. O token nao da direito de escrever nada alem de
  cancelar o proprio pedido enquanto estiver aguardando.
- `hasOnly` fechado em toda escrita nova; campo novo entra opcional e a regra so
  e publicada DEPOIS que o codigo que grava o campo esta no ar.

---

## 6. Endpoints

Com o **Vercel Pro** (item obrigatorio, secao 8), o teto de 12 deixa de existir
e o caminho do dinheiro ganha arquivo proprio — o que e melhor de auditar do que
empilhar mais um publico dentro de `pontos.js`:

- `api/pedido.js` — publico, sem login: criar pedido, consultar por token,
  anexar comprovante, cancelar. Freio por IP, por negocio e por telefone.
- `api/recebimento.js` — lojista logado: configurar modo, testar conexao,
  confirmar/recusar pedido. idToken verificado no servidor.
- `api/webhook.js` — ganha o desvio de `pedido:{id}` e passa a responder 200
  logo apos persistir o evento.

Se o Pro nao entrar, o plano B e empilhar as duas primeiras como acoes de
`pontos.js` — funciona, mas com a divida de seguranca registrada no achado A7.

**Toda chamada de API do site aponta para `www.moviki.com.br`.** O apex
redireciona, e redirecionamento entre origens troca a origem por `null`, o que
o navegador bloqueia por CORS. Foi o que derrubou o estudio da live em 12/09.

---

## 7. Modelo de ameaca por fluxo

| Ataque | Barreira |
|---|---|
| Alterar o preco no navegador | servidor recalcula pelo `sku` no cardapio do lojista |
| Comprovante falso | conferencia do lojista + centavos unicos + aviso na tela |
| Trocar o QR por injecao de script | QR so do servidor, CSP fechada, zero terceiro na tela, nome do recebedor visivel para conferir no banco |
| Trocar a chave Pix do lojista invadido | reautenticacao + e-mail + aviso no painel + trilha |
| Enxurrada de pedidos falsos | freio por IP, conta, negocio e telefone; 429 |
| Reenvio do webhook | id deterministico com `create()` |
| Webhook forjado | token em tempo constante, dois tokens aceitos |
| Ler pedido de outro negocio | regra por `negocioUid`; token do pedido so abre o proprio |
| Lojista adultera a propria venda | trilha imutavel + painel do dono ve tudo |
| Clickjacking na tela de pagamento | `frame-ancestors 'self'` em cabecalho |
| Vazamento da chave de API do lojista | AES-256-GCM, falha fechada, colecao sem match, nunca volta para a tela |
| Golpe de "paguei, libera" | status so muda por Admin SDK ou lojista |

---

## 8. O que exige orcamento

| Item | Preco | Veredito |
|---|---|---|
| **Vercel Pro** | US$ 20/mes por membro | **Necessario.** O robo esta em 12/12 funcoes; sem Pro nao entra endpoint novo. Tambem libera limite de taxa no WAF e mais duracao de funcao. |
| Vercel WAF — regras e bloqueio de IP | **gratis em todos os planos** | Ligar agora. Trafego bloqueado nem e cobrado. |
| Vercel WAF — limite de taxa e regras gerenciadas OWASP | cobranca por uso, so no Pro | Ligar depois do Pro, no caminho do pedido. |
| Firebase Identity Platform (2FA do dono) | cobranca por usuario ativo, com faixa gratuita | Necessario antes do primeiro lojista real vender. TOTP evita o custo de SMS. |
| Cloudflare Stream | ja contratado, pague-pelo-uso | Sem mudanca. |
| Cloudflare na frente da Vercel | — | **Nao.** Mantida a recomendacao de 12/09: a Vercel ja entrega WAF, DDoS e TLS, e nao ha IP de origem para proteger. |
| Monitoramento externo de endpoint | gratis ate um limite | Opcional; a rotina diaria ja cobre o essencial. |

---

## 9. Ordem de execucao

1. Correcoes de seguranca que nao dependem de nada (A5, A1, A2, A3, A4).
2. Assinar o Vercel Pro.
3. Reescrever `lib/checkout.js` em dois modos.
4. `api/pedido.js` e `api/recebimento.js`.
5. Regras do Firestore v24 — publicadas so depois que o codigo que grava os
   campos novos estiver no ar.
6. Aba Financeiro no painel do lojista.
7. Cardapio compravel nas paginas publicas.
8. Live passa a consumir o mesmo checkout.
9. Videoaulas do Financeiro.

## 10. Pendencias que continuam abertas

- Teto de 10 subcontas no Asaas — agora sem bloquear nada.
- Apex x www: os 16 links do site ainda batem no apex e pegam redirecionamento.
- Exigir CNPJ do parceiro para receber comissao.
- App Check no Authentication.
