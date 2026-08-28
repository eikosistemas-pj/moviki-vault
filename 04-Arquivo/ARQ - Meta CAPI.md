---
type: arquivo
status: concluido
data: 2026-08-27
area: A6 — Medicao e Analytics
tags: [medicao, lgpd]
atualizado: 2026-08-28
---

# ARQ — Conversão para a Meta pela CAPI — NO AR 27/08/2026

**O problema não era técnico, era o que já estava publicado.** O `privacidade.html`, seção 9, dizia com todas as letras que o site **não usa cookie de publicidade**. Pixel de navegador grava cookie de publicidade — subir o pixel contradiz a própria política e vira **problema de LGPD, não de gosto**.

**Decisão: só servidor, sem banner.** A Conversions API manda o evento do robô direto para a Meta, com e-mail e telefone em **SHA-256**. Nenhum cookie, nenhum banner.

## Arquitetura — irmã gêmea do `lib/ga.js`
- **`lib/meta.js`** (NOVO) — `try/catch`, timeout de 2,5 s, devolve booleano, **nunca lança**. Sem env, vira no-op silencioso. **Zero função nova: continua 12/12.**
- **`webhook.js`** — `registrarPurchaseGA` virou **`registrarPurchase`** e mede nos dois. **A trava de duplicidade é a mesma** (`faturamento/{uid}/ga/{payId}.create()`).
- **`novo-cliente.js`** — dispara **`Lead`** no cadastro. **Enquanto o volume de venda for baixo, é ESTE o evento que dá material para a campanha otimizar** — `Purchase` sozinho não sai do aprendizado. Vem **antes** do aviso no Telegram de propósito.

## Dados de correspondência
E-mail do **Firebase Auth** (`negocios/{uid}` não tem campo de e-mail) · telefone do `whatsapp` (o banco guarda sem o 55; o `lib/meta.js` acrescenta) · `uid` vira `external_id`.
**Campo vazio não é enviado** — a Meta trata string vazia como valor inválido e derruba a qualidade do conjunto de dados inteiro.

## `action_source` é por evento
A Meta exige `client_user_agent` quando o evento é `website` — e a venda nasce no **webhook do Asaas**, onde não existe navegador. Então `Purchase` vai como **`system_generated`** e `Lead` como **`website`** com o agente real.
**Marcar tudo como `website` faria a Meta recusar ou rebaixar justamente o evento de venda.**

## Testado ao vivo em 27/08, 13h09
`Lead` na aba **Eventos de teste**, marcado **Processado**, recebido de **Servidor**, `action_source: website`, `event_id: lead_<uid>`, `content_name: cadastro_comerciante`, e as **quatro** chaves de correspondência reconhecidas: País, Email, Identificação externa, Agente do usuário. Conjunto **2114417739495816**.

**O `Purchase` não foi testado** — exige pagamento real.

⚠️ **`META_TEST_CODE`: usar para testar e TIRAR depois.** Enquanto existir, o evento **não conta como conversão de verdade**.

→ [[ARQ - Decisao - sem pixel de navegador]] · [[A6 - Medicao e Analytics]]
