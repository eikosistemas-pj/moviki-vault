---
type: recurso
status: referencia
area: A2 — Infraestrutura e Deploy
tags: [deploy, infra, armadilha]
atualizado: 2026-09-04
---

# R — Marcas de versão no ar

⚠️ **Esta tabela envelhece sozinha. A fonte de verdade é o repositório no GitHub.**

*Reconferida arquivo por arquivo em 04/09/2026, clonando os repositórios. O `parceiro.html` foi atualizado duas vezes depois disso: a abertura do parceiro e o crachá com QR.
A coluna "no ar" é o que o código publicado diz. A coluna "entregue" é o que o Mapa
Mestre afirma — quando as duas divergem, é arquivo que foi produzido e não subiu.*

**Para conferir ao vivo:** abrir a página → F12 → Console → `MOVIKI_VERSAO` → Enter.
Valor antigo ou `undefined` é cache: **Ctrl+Shift+R**. Não existe service worker.

## Repositório `moviki` — o site

| Arquivo | No ar | Entregue |
| --- | --- | --- |
| `index.html` (landing) | `2026-09-03-appcheck` | — |
| `404.html` (página pública) | `2026-09-03-appcheck` | **`2026-09-03-frescor`** ⚠️ |
| `descadastro.html` | `2026-09-03-appcheck` | — |
| `v.html` (verificação) | `2026-09-03-verificacao-appcheck` | ✅ igual |
| `enterprise.html` | `2026-08-27-ga4l2` | — |
| `comerciantes.html` | `2026-08-27-ga4l2` | — |
| `parceiros.html` | `2026-08-28-vikparceiros` | — |
| `parceiros-ganhos.html` | `2026-08-27-conformidade` | — |
| `premium.html` | **sem marca** | — |
| `excluir-conta.html` | **sem marca** | — |
| `termos.html` · `privacidade.html` · `regulamento.html` | **sem marca** | — |
| `p.html` / `pp.html` | sem marca (redirecionadores de 20 linhas) | — |

## Repositório `moviki-app` — os painéis

*Último commit: 03/09 às **15h35**, antes da rodada da noite.*

| Arquivo | No ar | Entregue |
| --- | --- | --- |
| `index.html` (painel do lojista) | **`2026-09-03-atendentes`** | ✅ em dia |
| `parceiro.html` | **`2026-09-03-cracha-aulas`** | ✅ em dia |
| `eikoadm01.html` | `2026-09-03-appcheck` | **`2026-09-03-atendentes`** ⚠️ |
| `seja-parceiro.html` | `2026-09-03-appcheck` | — |
| `404.html` | `2026-08-28-404vik` | — |
| `regulamento.html` | **sem marca** | — |

⚠️ **Os quatro arquivos marcados estão em [[ARQ - Entregue e nao subiu 03092026]].**
Três deles já têm conteúdo novo no ar carregando a marca ANTIGA — diagnosticar por
marca, neles, dá a resposta errada.

## O que "sem marca" custa

Página sem `window.MOVIKI_VERSAO` não dá para diagnosticar: não há como distinguir
"o arquivo certo está no ar" de "o navegador guardou o antigo". O `premium.html` é o
caso que mais dói — é a landing do tráfego pago, a página que vai receber a campanha.

**Regra:** todo arquivo grande carrega marca de versão, e **a marca sobe junto com o
conteúdo**. Marca antiga em arquivo novo é pior que marca nenhuma.

## Ligações

[[A2 - Infraestrutura e Deploy]] · [[R - Checklist de deploy]] · [[R - Regras de ouro]] · [[ARQ - Entregue e nao subiu 03092026]] · [[P09 - Faxina do repositorio moviki]]
