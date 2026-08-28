---
type: recurso
status: referencia
area: A2 — Infraestrutura e Deploy
tags: [deploy]
atualizado: 2026-08-28
---

# R — Marcas de versão no ar

**Conferir:** abrir a página → F12 > Console > digitar `MOVIKI_VERSAO` > Enter.
Valor antigo ou `undefined` = **cache** → Ctrl+Shift+R.

⚠️ **Conferir também EM QUAL domínio.** Em 28/08 três arquivos do `moviki-app` foram subidos no `moviki` e `moviki.com.br` passou a servir o painel do lojista. A marca de versão foi o que provou o erro. → [[ARQ - Incidente - deploy no repositorio errado]]

| Arquivo | Repositório | Versão |
| --- | --- | --- |
| `404.html` | moviki | `2026-08-27-wppunidade` |
| `descadastro.html` | moviki | `2026-08-27-descadastro` |
| `enterprise.html` | moviki | `2026-08-27-ga4l2` |
| `comerciantes.html` | moviki | `2026-08-27-ga4l2` |
| `parceiros.html` | moviki | `2026-08-27-conformidade` |
| `parceiros-ganhos.html` | moviki | `2026-08-27-conformidade` |
| `privacidade.html` | moviki | **sem marca — atualizado em 28/08 (seção 5, Vik)** |
| `p.html` / `pp.html` | moviki | sem marca (redirecionadores de 20 linhas) |
| `api/og.js` | moviki | `2026-08-27-og3` |
| `index.html` | moviki-app | **`2026-08-28-vikpadrao`** |
| `eikoadm01.html` | moviki-app | **`2026-08-28-vikpadrao`** |
| `parceiro.html` | moviki-app | **`2026-08-28-vikpadrao`** |
| `seja-parceiro.html` | moviki-app | `2026-08-27-ga4parceiro` |
| `404.html` | moviki-app | `2026-08-27-404app` |
| `api/chat.js`, `lib/memoria.js`, `lib/oportunidade.js`, `lib/promptPainel.js`, `lib/contextoUsuario.js`, `lib/anthropic.js` | moviki-ai | sem marca — **a verdade é o commit no GitHub e o deploy na Vercel** |

> Atualizar esta tabela a cada upload. Ela é a primeira coisa a conferir antes de caçar bug.
> **`privacidade.html` não tem marca de versão e deveria ter** — é um documento legal, e "está no ar a versão certa?" é exatamente a pergunta que uma marca responde.
