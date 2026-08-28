---
type: recurso
status: referencia
area: A2 — Infraestrutura e Deploy
tags: [infra]
atualizado: 2026-08-28
---

# R — Stack e repositórios

**5 repositórios no GitHub, conta `eikosistemas-pj`.** Os 4 primeiros na Vercel com deploy automático a cada push; o 5º roda 100% em GitHub Actions. **Todos clonáveis anonimamente.**

| Repo | Domínio | Funções `/api` | Papel |
| --- | --- | --- | --- |
| `moviki` | moviki.com.br | **1 de 12** | site público + `api/og.js` |
| `moviki-app` | app.moviki.com.br | — | painéis |
| `moviki-robo` | moviki-robo.vercel.app | **12 de 12 — NO TETO** | backend de **dinheiro** |
| `moviki-ai` | moviki-ai.vercel.app | **2 de 12** | os dois atendentes de IA |
| `moviki-assistente-social` | GitHub Actions | — | robô de publicação (Python 3.11) |

## Arquivos por repo
**moviki:** `index.html`, `404.html` (página pública `/apelido`), `comerciantes.html`, `parceiros.html`, `parceiros-ganhos.html`, `regulamento.html`, `p.html`, `pp.html`, `termos.html`, `privacidade.html`, `descadastro.html`, `enterprise.html`, `premium.html`, `mvmetrica.js`, `movikiui.css`, `icones-premium/`, `vercel.json`, `robots.txt`, `sitemap.xml`, `ogmoviki.jpg`, `api/og.js`, `.nojekyll`.

**moviki-app:** `index.html` (painel do lojista + Quiz + caixa de mensagens), `eikoadm01.html` (painel do dono), `parceiro.html`, `seja-parceiro.html`, `regulamento.html`, `mvmetrica.js`, `movikiui.css`, `icones/`, `quiz/`.

**moviki-robo:** `lib/firebase.js` (`{admin, db}`), `lib/asaas.js`, `lib/boasVindasParceiro.js`, `lib/ga.js`, `lib/meta.js`.
**Regra do repo: é o robô de DINHEIRO, muda o mínimo. Nada conversacional/IA entra aqui.**

**moviki-ai:** `api/atendimento.js` (webhook WhatsApp), `api/chat.js` (o Vik), `lib/firebase.js`, `lib/anthropic.js`, `lib/whatsapp.js`, `lib/promptAtendimento.js`, `lib/promptPainel.js`, `lib/contextoUsuario.js`, `lib/memoria.js`, `lib/oportunidade.js`.

## Serviços
Firebase (Auth, Firestore, Storage `moviki-app.firebasestorage.app`, App Check) — **plano Blaze** · Asaas em produção · Resend (`suporte@moviki.com.br`) · HostGator (domínio/DNS/Titan) · Anthropic (Claude API) · WhatsApp Cloud API · GA4 · Kairogen (PRO).

**Firestore:** banco `(default)`, modo nativo, **southamerica-east1 (São Paulo)**. Projeto no Firebase = `moviki`; código no Google Cloud = `moviki-app`. **São o mesmo projeto.**

## Armadilha de repositório
`moviki` e `moviki-app` são domínios diferentes. **Arquivo no repo errado não dá 404 claro** — o `404.html` do `moviki` é o roteador de slug e responde "Negócio não encontrado". Sempre dizer o repositório de destino junto do nome do arquivo.

## Acesso do Claude
Os 5 repos são fontes GitHub na Base de Conhecimento. **Claude lê por clone anônimo, mas não tem push** — entrega arquivos, upload é manual.
