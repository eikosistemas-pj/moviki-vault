---
type: recurso
status: referencia
tags: [referencia]
atualizado: 2026-08-28
---

# R — Glossário

| Termo | O que é |
| --- | --- |
| **Apelido / slug** | o endereço público do lojista: `moviki.com.br/apelido`. Vive em `slugs/`. Na cabeça de quem usa, **o negócio "é" o apelido** |
| **Single-vendor** | cada lojista leva os próprios clientes ao próprio link. Vende desde o dia 1, sem depender de marketplace de dois lados |
| **Vitrine** | modo do robô social que divulga um negócio real que autorizou (`autorizaDivulgacao`) |
| **Vik** | o assistente de IA de dentro do painel (`moviki-ai/api/chat.js`) |
| **Upline** | o parceiro que indicou outro parceiro (níveis 2 e 3) |
| **Clawback** | reversão da comissão quando o pagamento é estornado |
| **`hasOnly`** | função das regras do Firestore que limita quais campos podem existir/mudar |
| **Handoff** | trava do Vik: admin falou nos últimos 30 min → o robô cala |
| **Marca de versão** | `window.MOVIKI_VERSAO` — primeira coisa a conferir antes de caçar bug |
| **CAPI** | Conversions API da Meta: evento mandado do servidor, sem cookie |
| **Measurement Protocol** | o equivalente no GA4 (`lib/ga.js`) |
| **Portão de qualidade** | regra do `api/og.js` que decide se a página entra no índice do Google (≠ trava de plano) |
| **Trava de plano** | o que cada plano vê. **Coleta nunca trava; só a exibição** |
| **Cloaking** | servir HTML diferente para robô e para gente. O Google pune |
| **PARA** | Projects, Areas, Resources, Archives — o método deste vault |
