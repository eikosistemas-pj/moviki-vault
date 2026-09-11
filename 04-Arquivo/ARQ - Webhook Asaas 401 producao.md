---
type: incidente
status: aberto
area: Cobranca
tags: [asaas, webhook, moviki-robo, vercel, 401, producao]
atualizado: 2026-09-11
---

# ARQ - Webhook Asaas 401 producao

## Sintoma

11/09/2026, painel de PRODUCAO do Asaas (asaas.com). Webhook "Moviki Robo" ->
`https://moviki-robo.vercel.app/api/webhook` devolvendo **401 Unauthorized**
desde 10:48, com retentativas ate 13:48 e **Penalizacao aplicada**. Evento visto:
`PAYMENT_DELETED` do pagamento `pay_ilwt3fvueu98ydri`, assinatura
`sub_exw3bw1ega1kmkx7`, criada em 07/09. A fila pausa sozinha na 15a tentativa.

## Causa

Configuracao, nao codigo. Conferido no repositorio: o trecho do token no
`api/webhook.js` e o mesmo desde antes de 10/09 (o upload de 10/09 01:53 so
mexeu nos niveis do parceiro). O token do cadastro de producao no Asaas nao bate
com `ASAAS_WEBHOOK_TOKEN` da Vercel.

Provavel origem: a pendencia "Para ir a producao" do incidente de 04/09 — o
cadastro de producao nunca recebeu o token sincronizado, e este foi o primeiro
evento de cobranca de producao a chegar. O `PAYMENT_DELETED` das 10:48 bate com
exclusao de conta pelo painel do dono (o `exclusoes.js` cancela a assinatura no
Asaas, que dispara o evento).

## Gravidade

Critica. Com a fila pausada, `PAYMENT_RECEIVED` nao chega: lojista que pagar fica
em Basico e a comissao do parceiro nao e creditada. O webhook "Transferencias"
usa token proprio (`ASAAS_WEBHOOK_TOKEN_TRANSFER`) e nao e afetado.

## Conserto

1. Gerar token novo: 48 caracteres, so letras e numeros.
2. Vercel `moviki-robo` -> Settings -> Environment Variables ->
   `ASAAS_WEBHOOK_TOKEN` -> Edit -> colar, sem espaco nem Enter no fim -> Save.
3. Deployments -> ultimo -> Redeploy, sem cache de build. Esperar Ready.
4. Asaas producao -> Integracoes -> Webhooks -> "Moviki Robo" -> Editar ->
   mesmo valor em "Token de autenticacao" -> fila de sincronizacao ATIVA -> Salvar.
5. Logs de Webhooks, eventos em 401:
   - cliente `cus_000149223165` e a conta de teste excluida hoje -> **Remover da
     fila** (reenviar recriaria `assinaturas/{uid}` orfao de conta apagada);
   - cliente real -> **Reenviar**, esperar 200.
6. Prova: criar cobranca avulsa qualquer e exclui-la -> o log novo tem que
   mostrar **200**.

Nao mexer no webhook "Transferencias". O cadastro do Sandbox passa a dar 401 —
irrelevante com o robo em producao.

## Pendencias que ficam

- Alerta no Telegram antes do 401 (trava de 1 por hora), `trim()` no token e na
  env, e `PAYMENT_DELETED` ignorado quando `assinaturas/{uid}` nao existe.
  **Entram no `api/webhook.js` do pacote Modo Live**, que substitui este arquivo
  — entregar versao separada agora faria um upload apagar o outro.

## Regra de ouro

- Todo webhook do Asaas tem cadastro separado por ambiente. Virar para producao
  exige sincronizar o token no cadastro de producao no mesmo dia.

## Ligacoes

- [[ARQ - Webhook Asaas 401 token dessincronizado]]
- [[R - Regras de ouro]]
