---
type: incidente
status: resolvido
area: Cobranca
tags: [asaas, webhook, moviki-robo, vercel, 401, sandbox]
atualizado: 2026-09-04
---

# ARQ - Webhook Asaas 401 token dessincronizado

## O que aconteceu

04/09/2026, entre 04:00 e 04:10 (Sandbox). O Asaas disparou
`PAYMENT_OVERDUE` para `https://moviki-robo.vercel.app/api/webhook` e recebeu
**401 Unauthorized** nas 5 tentativas (04:00, 04:01, 04:02, 04:05, 04:10).
O painel marcou o webhook "Moviki Robo" com **Penalizacao aplicada** e pausou
a fila de eventos.

## Causa

Nao foi bug de codigo. O `api/webhook.js` compara o header
`asaas-access-token` com a env `ASAAS_WEBHOOK_TOKEN` (e a opcional
`ASAAS_WEBHOOK_TOKEN_TRANSFER`) em comparacao de tempo constante. O valor
enviado pelo Asaas nao batia com o valor da Vercel.

Origens possiveis, todas de configuracao:

- Campo "Token de autenticacao" vazio no cadastro do webhook no Asaas.
- Espaco ou quebra de linha invisivel colado no valor da env na Vercel — o
  comprimento diferente reprova antes mesmo da comparacao.
- Env criada ou alterada sem **Redeploy** na Vercel.

## Gravidade

Alta enquanto durou. Com a fila penalizada, `PAYMENT_RECEIVED` tambem para de
chegar: assinatura paga nao liga `ativo: true` em `assinaturas/{uid}` e o
lojista continua em Basico depois de pagar.

## Conserto aplicado

1. Vercel, projeto `moviki-robo` -> Settings -> Environment Variables ->
   `ASAAS_WEBHOOK_TOKEN` substituido por token novo de 48 caracteres
   alfanumericos, sem espaco e sem quebra de linha, nos 3 ambientes.
2. Redeploy sem cache de build.
3. Asaas Sandbox -> Integracoes -> Webhooks -> "Moviki Robo" -> mesmo valor
   colado em "Token de autenticacao".
4. Fila do webhook penalizado reativada.
5. Os 5 eventos em 401 reenviados pelos Logs de Webhooks. Todos em 200.

Confirmado OK em 04/09/2026.

## Pendencia aberta que este incidente revelou

O 401 e silencioso. Token dessincronizado derruba a cobranca inteira e o
descobrimento so acontece pela penalizacao da fila, horas depois. O
`moviki-robo` ja tem `TELEGRAM_TOKEN` e `TELEGRAM_CHAT_ID` configurados: o
`api/webhook.js` deve avisar no Telegram antes de devolver 401, com trava de
1 aviso por hora para o retry do Asaas nao virar spam. Vale tambem para
chamada que chega com token de tamanho zero.

Depende de subir aqui o `api/webhook.js` atual — arquivo de dinheiro nao se
remonta por pedaco vindo de busca.

## Regras confirmadas

- Segredo nunca vai no codigo nem no GitHub. Token de webhook vive so nas
  Environment Variables da Vercel e no campo do painel do Asaas.
- Alterar env na Vercel exige Redeploy para valer.
- Trocar token e operacao de dois lados na mesma janela: Vercel e Asaas. Um
  lado sozinho penaliza a fila.

## Para ir a producao

O webhook de producao e outro cadastro, no painel real do Asaas, com token
proprio. Repetir os mesmos 5 passos la, e nao reaproveitar o token do
Sandbox.

## Ligacoes

- [[R - Regras de ouro]]
- [[R - Marcas de versao no ar]]
