---
type: arquivo
status: concluido
area: "[[A13 - Modo Live]]"
tags: [seguranca, auditoria, dinheiro, checkout, asaas]
atualizado: 2026-09-14
---

# Auditoria de seguranca do dinheiro — 14/09/2026

Feita clonando os tres repositorios no estado real do GitHub, antes de escrever
qualquer linha da Fase 1 do Financeiro. Base normativa:
[[R - Doutrina de seguranca financeira]].

---

## O que ja esta certo (nao mexer)

- **Webhook autenticado em tempo constante.** `api/webhook.js` compara o header
  `asaas-access-token` com `crypto.timingSafeEqual` e aceita dois tokens (o de
  cobranca e o de pedidos). Nao vaza o token por medicao de tempo.
- **Comissao idempotente de verdade.** O documento e
  `comissoes/{payId}_n{nivel}` gravado com `create()`, que falha se ja existe.
  Reenvio do mesmo pagamento nao credita duas vezes. Isso ja atende o modelo
  at-least-once do Asaas.
- **GA4 deduplicado** por `faturamento/{uid}/ga/{payId}`.
- **Cifra da chave da subconta** em `lib/checkout.js`: AES-256-GCM, chave
  derivada por SHA-256 da `CHECKOUT_CHAVE`, falha fechada se a variavel tiver
  menos de 24 caracteres, colecao `checkout_contas` sem match nas regras.
- **Entrada saneada**: validacao real de CPF e CNPJ com digito verificador,
  remocao de caracteres de controle, teto de caracteres, piso de valor.
- **Retencao de dados pensada**: pedido abandonado expira em 7 dias, pedido
  pago fica 5 anos (prazo do CDC), e o `expiraEm` do documento e separado da
  janela de 30 minutos do Pix — detalhe que evita TTL apagando pedido pago.
- **CORS com lista fechada** e `Vary: Origin` no checkout e em `pontos.js`.
- **Cabecalhos** `X-Content-Type-Options`, `Referrer-Policy`,
  `Permissions-Policy` com `payment=()` e `Cross-Origin-Opener-Policy` nos dois
  `vercel.json`.
- **Freio por IP** no caminho publico do checkout, com 429.

## Achados — o que falta

### A1. Sem HSTS em nenhum dos dois projetos
`Strict-Transport-Security` nao existe no `vercel.json` do site nem do app. Sem
ele, a primeira visita em http continua sujeita a interceptacao. Correcao de
uma linha, aplicada aos dois.

### A2. Tela de pagamento pode ser enquadrada (clickjacking)
Nao ha `X-Frame-Options` nem `frame-ancestors`. Uma pagina hostil pode carregar
o checkout num iframe invisivel. Em tela que exibe QR de Pix, isso e grave.
`frame-ancestors` so vale em CABECALHO — nao funciona em meta tag, que e como a
CSP vive hoje no projeto.

### A3. Webhook processa antes de responder 200
O robo executa a regra de negocio e so entao responde. O Asaas conta como falha
tudo que nao for 200 e PAUSA a fila apos 15 falhas consecutivas, guardando os
eventos por 14 dias antes de apagar. Uma fila pausada significa plano nao
ligado, comissao nao creditada e pedido preso em "aguardando" — tudo calado.
Ja houve o incidente de 401 em producao em 11/09. Correcao: persistir o evento
bruto, responder 200, processar depois, e monitorar a fila todo dia.

### A4. Nenhum evento bruto do Asaas e guardado
Sem copia crua do payload nao ha reprocessamento nem pericia depois de um
incidente. Colecao `webhook_eventos/{eventId}` resolve, e de quebra vira a
idempotencia de primeiro nivel.

### A5. Falha ABERTA na base do Asaas
`lib/checkout.js` faz `process.env.ASAAS_BASE_URL || sandbox`. Se a variavel
sumir da Vercel, o sistema passa a emitir cobranca no sandbox sem avisar: o
comprador ve um QR que nunca cai na conta de ninguem, e a tela continua normal.
Em producao, a ausencia da variavel tem que derrubar o modulo, nao rebaixa-lo.

### A6. Freio so por IP
IP e o piso. Falta limite por conta, por negocio e por telefone do comprador.
Ataque distribuido barato passa por cima de freio por IP.

### A7. O teto de 12 funcoes ja estourou
`moviki-robo/api` tem exatamente 12 arquivos. O plano Hobby recusa o 13o com a
mensagem "No more than 12 Serverless Functions can be added to a Deployment on
the Hobby plan". Consequencia de seguranca, nao so de espaco: o teto obriga a
empilhar responsabilidades em `pontos.js`, que hoje atende lojista logado e
comprador anonimo no mesmo arquivo. Um arquivo com dois publicos e duas
autenticacoes e onde erro de autorizacao nasce.

### A8. O lib/checkout.js atual e todo baseado em SUBCONTA
O arquivo no ar (`2026-09-12-beta1`) pressupoe subconta Asaas criada pela conta
da Eiko, com a chave cifrada por lojista. A decisao de 14/09 rebaixa a subconta
a opcao e promove o Pix direto do lojista a padrao. O modulo precisa de
reescrita com dois modos, nao de remendo.

### A9. App Check nao cobre o Authentication
Enforcement esta ligado so no Cloud Firestore desde 05/09. O Auth continua
descoberto — e o Storage tem que ficar em monitoramento para sempre, por causa
das URLs diretas de imagem.

### A10. Conta do dono sem segundo fator
O painel do dono aprova parceiro e paga saque. E a conta mais valiosa do
sistema e depende so de senha do Google.

### A11. Nenhum monitoramento do caminho do dinheiro
Nao existe alerta para: fila do webhook pausada, pedido preso em aguardando,
divergencia entre pedido pago e evento recebido, pico de pedidos num negocio so.

---

## Ordem de correcao

| # | Achado | Custo | Quando |
|---|--------|-------|--------|
| 1 | A5 falha aberta no sandbox | 1 linha | antes de qualquer coisa |
| 2 | A1 HSTS + A2 frame-ancestors | 2 arquivos | nesta rodada |
| 3 | A3 + A4 webhook responde 200 e guarda evento | 1 arquivo | nesta rodada |
| 4 | A7 Vercel Pro | US$ 20/mes | antes da Fase 1 |
| 5 | A8 reescrita do checkout em dois modos | rodada propria | Fase 1 |
| 6 | A6 freio por conta e negocio | junto da Fase 1 | Fase 1 |
| 7 | A11 monitoramento diario | rotina | com a Fase 1 no ar |
| 8 | A10 segundo fator do dono | Identity Platform | antes do 1o lojista real vender |
| 9 | A9 App Check no Auth | dia separado | depois |
