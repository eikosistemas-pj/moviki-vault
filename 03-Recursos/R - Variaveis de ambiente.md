---
type: recurso
status: referencia
area: A2 — Infraestrutura e Deploy
tags: [infra, deploy]
atualizado: 2026-09-03
---

# R — Variáveis de ambiente

⚠️ **Chaves secretas nunca no chat, no código ou no GitHub. Cada projeto tem as suas.**
⚠️ **Mexeu em env → Redeploy.** Env criada depois do deploy não vale para o deploy existente.
⚠️ **A Vercel não deixa mais RELER o valor de uma env salva.** Só editar ou rotacionar.

*Lista conferida em 03/09/2026 varrendo `process.env` nos três projetos. A fonte de verdade é o código, não esta nota.*

## `moviki` — o site (Vercel)

`FIREBASE_API_KEY` — usada pelo `api/og.js`, a única função do projeto.

O projeto do site tem **1 função das 12**. É onde vai caber a conta de serviço quando o `og.js` virar Admin SDK. Ver [[P15 - Enforcement do App Check]].

## `moviki-robo` (Vercel)

**Base:** `FIREBASE_SERVICE_ACCOUNT` · `FIREBASE_STORAGE_BUCKET`

**Dinheiro:** `ASAAS_API_KEY` · `ASAAS_BASE_URL` · `ASAAS_WEBHOOK_TOKEN` · **`ASAAS_WEBHOOK_TOKEN_TRANSFER`**

**Avisos e apoio:** `TELEGRAM_TOKEN` · `TELEGRAM_CHAT_ID` · `RESEND_API_KEY` · `CRON_SECRET` · `GOOGLE_MAPS_KEY`

**Medição:** `GA_MEASUREMENT_ID` (G-GG5CSQZVGH) · `GA_API_SECRET` · `META_PIXEL_ID` · `META_CAPI_TOKEN` · *(opcionais: `META_TEST_CODE`, `META_API_VERSION`)*

**Instagram** — busca do @ no cadastro do parceiro, `lib/instagram.js`: `IG_TOKEN` · `IG_USER_ID` · *(opcional: `IG_API_VERSION`)*

⚠️ **`META_TEST_CODE` existindo = o evento NÃO conta como conversão de verdade.** Apagar depois do teste.
⚠️ **Sem `IG_TOKEN`/`IG_USER_ID` a busca do @ não quebra a tela** — devolve `achou:false` e o cartão do perfil some. Falha calada, de propósito. Para diagnosticar de fora: `api/novo-parceiro?instagram=natgeo&secret=<CRON_SECRET>` devolve a mensagem crua da Meta.

## `moviki-ai` (Vercel — projeto próprio, NÃO herda nada)

`FIREBASE_SERVICE_ACCOUNT` (**só Production** desde 03/09 — em Preview toda deployment de branch carregaria a chave de administrador) · **`ANTHROPIC_API_KEY`** (sem ela o Vik responde `null` e fica **mudo sem erro na tela**) · `ANTHROPIC_MODEL` (opcional, mas **preferir fixar** — troca de modelo sem deploy) · `ANTHROPIC_TIMEOUT` · `CHAT_ORIGENS` · `CHAT_LIMITE_DIA` · Telegram (opcional).

**WhatsApp — a tranca do stand-by:** `WHATSAPP_APP_SECRET` (cadastrada em 03/09) · `WHATSAPP_TOKEN` · `WHATSAPP_PHONE_ID` · `WHATSAPP_VERIFY_TOKEN`.

⚠️ **A falta da chave É a tranca.** O `api/atendimento.js` exige `WHATSAPP_APP_SECRET` **e** `WHATSAPP_TOKEN` para acordar; faltando qualquer uma, recusa tudo na entrada com **503 `{standby:true}`** e não gasta chamada de IA. Não existe estado "meio ligado". Para religar: cadastrar as três do WhatsApp → Redeploy → apontar o webhook no Meta Business. Para desligar de novo: apagar `WHATSAPP_TOKEN` → Redeploy.

## `moviki-assistente-social` (GitHub Secrets)

`PAGE_ACCESS_TOKEN` (System User, não expira) · `FACEBOOK_PAGE_ID` 1312620718595159 · `IG_ACCOUNT_ID` 17841440001427879 · `FIREBASE_PROJECT_ID` moviki-app · `SO_FACEBOOK` (**usar `sim`/`nao`, nunca `1`** — o Actions mascara todo dígito 1 nos logs) · `ANTHROPIC_API_KEY` (opcional) · `CRON_SECRET` (no repositório `moviki-robo`, para o workflow de aprovação de parceiros).

## Ligações

[[A2 - Infraestrutura e Deploy]] · [[R - Stack e repositorios]] · [[R - Checklist de deploy]] · [[P15 - Enforcement do App Check]]
