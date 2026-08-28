---
type: recurso
status: referencia
area: A2 — Infraestrutura e Deploy
tags: [infra, deploy]
atualizado: 2026-08-28
---

# R — Variáveis de ambiente

⚠️ **Chaves secretas nunca no chat, no código ou no GitHub. Cada projeto tem as suas.**
⚠️ **Mexeu em env → Redeploy.** Env criada depois do deploy não vale para o deploy existente.
⚠️ **A Vercel não deixa mais RELER o valor de uma env salva.** Só editar ou rotacionar.

## `moviki-robo` (Vercel)
`FIREBASE_SERVICE_ACCOUNT` · `ASAAS_API_KEY` · `ASAAS_BASE_URL` · `ASAAS_WEBHOOK_TOKEN` · **`ASAAS_WEBHOOK_TOKEN_TRANSFER`** · `TELEGRAM_TOKEN` · `TELEGRAM_CHAT_ID` · `RESEND_API_KEY` · `CRON_SECRET` · `GOOGLE_MAPS_KEY` · `GA_MEASUREMENT_ID` (G-GG5CSQZVGH) · `GA_API_SECRET` · `META_PIXEL_ID` · `META_CAPI_TOKEN` · *(opcionais: `META_TEST_CODE` só durante o teste, `META_API_VERSION`)*

⚠️ **`META_TEST_CODE` existindo = o evento NÃO conta como conversão de verdade.** Apagar depois do teste.

## `moviki-ai` (Vercel — projeto próprio, NÃO herda nada)
`FIREBASE_SERVICE_ACCOUNT` · **`ANTHROPIC_API_KEY`** (sem ela o Vik responde `null` e fica **mudo sem erro na tela**) · `ANTHROPIC_MODEL` (opcional, mas **preferir fixar** — troca de modelo sem deploy) · `ANTHROPIC_TIMEOUT` · `CHAT_ORIGENS` · `CHAT_LIMITE_DIA` · e para o WhatsApp: `WHATSAPP_TOKEN`, `WHATSAPP_PHONE_ID`, `WHATSAPP_VERIFY_TOKEN`, `WHATSAPP_APP_SECRET`, Telegram (opcional).

## `moviki-assistente-social` (GitHub Secrets)
`PAGE_ACCESS_TOKEN` (System User, não expira) · `FACEBOOK_PAGE_ID` 1312620718595159 · `IG_ACCOUNT_ID` 17841440001427879 · `FIREBASE_PROJECT_ID` moviki-app · `SO_FACEBOOK` (**usar `sim`/`nao`, nunca `1`**) · `ANTHROPIC_API_KEY` (opcional) · `CRON_SECRET` (no `moviki-robo`, para o workflow de aprovação de parceiros)
