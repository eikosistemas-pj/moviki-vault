---
type: recurso
status: referencia
area: A2 — Infraestrutura e Deploy
tags: [deploy, infra]
atualizado: 2026-09-03
---

# R — Marcas de versão no ar

⚠️ **Esta tabela envelhece sozinha. A fonte de verdade é o repositório no GitHub, nunca esta nota.**

*Reconferida arquivo por arquivo em 03/09/2026, nos dois repositórios.*

**Para conferir ao vivo:** abrir a página → F12 → Console → digitar `MOVIKI_VERSAO` → Enter.
Veio o valor antigo ou `undefined`? É cache: **Ctrl+Shift+R**. Não existe service worker nos repos.

## Repositório `moviki` — o site

| Arquivo | Versão |
| --- | --- |
| `index.html` (landing) | `2026-09-03-appcheck` |
| `404.html` (página pública `/apelido`) | `2026-09-03-appcheck` |
| `descadastro.html` | `2026-09-03-appcheck` |
| **`v.html`** (verificação de parceiro) | **`2026-09-03-verificacao-appcheck`** |
| `enterprise.html` | `2026-08-27-ga4l2` |
| `comerciantes.html` | `2026-08-27-ga4l2` |
| `parceiros.html` | `2026-08-28-vikparceiros` |
| `parceiros-ganhos.html` | `2026-08-27-conformidade` |
| `premium.html` | **sem marca** |
| `termos.html` · `privacidade.html` · `regulamento.html` | **sem marca** |
| `excluir-conta.html` | **sem marca** |
| `p.html` / `pp.html` | sem marca (redirecionadores de 20 linhas) |

## Repositório `moviki-app` — os painéis

| Arquivo | Versão |
| --- | --- |
| `index.html` (painel do lojista) | `2026-09-03-authdominio` |
| `parceiro.html` | `2026-09-03-appcheck` |
| `eikoadm01.html` | `2026-09-03-appcheck` |
| `seja-parceiro.html` | `2026-09-03-appcheck` |
| `404.html` | `2026-08-28-404vik` |
| `regulamento.html` | **sem marca** |

## O que "sem marca" custa

Página sem `window.MOVIKI_VERSAO` não dá para diagnosticar: não há como distinguir "o arquivo certo está no ar" de "o navegador guardou o antigo". O `premium.html` é o caso que mais dói — é a landing do tráfego pago, a página que vai receber a campanha.

**Regra:** todo arquivo grande carrega marca de versão. Entrou na tabela, tem marca.

## Ligações

[[A2 - Infraestrutura e Deploy]] · [[R - Checklist de deploy]] · [[R - Regras de ouro]] · [[P09 - Faxina do repositorio moviki]]
