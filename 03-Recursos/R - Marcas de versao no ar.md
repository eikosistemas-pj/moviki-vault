---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-16
---

# R - Marcas de versao no ar

**Reconferido clonando os repositorios em 16/09/2026, 15h.** Esta tabela
envelhece sozinha: a fonte de verdade e o repositorio, nunca este arquivo. No
navegador, `F12` > Console > `MOVIKI_VERSAO`; valor antigo e cache,
`Ctrl+Shift+R`.

A leitura das 05h ja estava velha em quase todas as linhas — os dois paineis e
a home andaram depois dela.

## Repo `moviki` (www.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (home) | `2026-09-16-livecommerce1` |
| `premium.html` · `enterprise.html` | `2026-09-16-livecommerce1` |
| `comerciantes.html` | `2026-09-16-iconelive` |
| `aovivo.html` (venda da live) | `2026-09-16-aovivo8-publica` |
| `live.html` (quem assiste) | `2026-09-16-csp1` |
| `404.html` (pagina publica do negocio) | `2026-09-16-capavideo` |
| `p.html` · `pp.html` | `2026-09-16-previa` |
| `api/live.js` | `2026-09-16-teto3` |
| `api/sitemap.js` | `2026-09-16-sitemap1` |
| `lib/seo.js` | `2026-09-16-seo1` |
| `api/og.js` | `2026-09-15-og-live` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `termos.html` · `privacidade.html` | `2026-09-12-live1` |
| `regras-da-live.html` | `2026-09-11-regras1` |
| `api/vitrine.js` | `2026-09-04-vitrine1` |
| `lib/gauth.js` | `2026-09-04-gauth1` |
| `v.html` | `2026-09-03-verificacao` |
| `descadastro.html` | `2026-09-03-appcheck` |
| `parceiros.html` | `2026-08-28-vikparceiros` |
| `parceiros-ganhos.html` | `2026-08-27-conformidade` |
| `regulamento.html` · `excluir-conta.html` · `mvmetrica.js` · `js/moviki-3d.js` · `vercel.json` | **sem marca** |

`vercel.json` sem marca contem `/v/:slug`, `/p/:slug`, `/pp/:slug` e a rota
`/aovivo` **antes** do curinga. Mexer ali sem conferir a ordem quebra os links
do parceiro.

## Repo `moviki-app` (app.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (painel do lojista) | `2026-09-16-asaasconta` ← esta rodada |
| `parceiro.html` | `2026-09-16-trilha` |
| `live.html` (estudio) | `2026-09-16-pixfinanceiro` |
| `liveaulas.js` | `2026-09-16-pixnovo` |
| `eikoadm01.html` (painel do dono) | `2026-09-16-consumo3` |
| `material/catalogo.json` | `versao: 2026-09-16-caticones` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `seja-parceiro.html` | `2026-09-04-conta-existente` |
| `404.html` | `2026-08-28-404vik` |
| `regulamento.html` · `quiz/quiz-segmentos.js` · `mvmetrica.js` · `vercel.json` | **sem marca** |

O `index.html` estava em `2026-09-16-quadro` quando esta rodada comecou.

## Repo `moviki-robo`

| Arquivo | Marca |
| --- | --- |
| `lib/checkout.js` | `2026-09-16-asaasconta` ← esta rodada (era `2026-09-16-subfechada`) |
| `api/pagar-saque.js` | `2026-09-16-saque1` |
| `api/webhook.js` | `2026-09-15-escopo` |
| `api/pontos.js` | `2026-09-15-livesessao` |
| `lib/livesessao.js` | `2026-09-15-b5b` |
| `api/pedido.js` · `api/financeiro.js` | `2026-09-14-porta1` |
| `api/webhook-reprocessa.js` | `2026-09-14-repro1` |
| `lib/asaas.js` | `2026-09-14-falhafechada` |
| `lib/pix.js` | `2026-09-14-pixdireto` |
| `api/ativar-trial.js` · `api/criar-assinatura.js` · `api/excluir-conta.js` · `api/exclusoes.js` · `api/lembrete-trial.js` · `api/novo-cliente.js` · `api/novo-parceiro.js` · `api/parceiro-aprovado.js` · `api/upload-imagem.js` | **sem marca** |
| `lib/boasVindasParceiro.js` · `lib/espelhoParceiro.js` · `lib/firebase.js` · `lib/ga.js` · `lib/instagram.js` · `lib/meta.js` | **sem marca** |

**15 arquivos em `api/`.** O teto de 12 do Hobby deixou de valer com o Vercel
Pro, assinado em 14/09 — mas a regra de nao inflar `api/` sem necessidade
continua: cada arquivo ali e uma funcao com cold start propria.

## Repo `moviki-ai`

| Arquivo | Marca |
| --- | --- |
| `lib/catalogoPainel.js` | `2026-09-16-8` ← esta rodada (era `2026-09-16-7`) |

`MARCAS_CONFERIDAS` dentro desse arquivo, depois desta rodada: lojista
`2026-09-16-asaasconta`, parceiro `2026-09-16-trilha`.

⚠️ **O parceiro no ar esta em `2026-09-16-trilha` e a tabela tambem** — mas
isso ja divergiu tres vezes so em 16/09, sempre em silencio. Painel que sobe,
`MARCAS_CONFERIDAS` que sobe junto, na mesma rodada. Ver
[[ARQ - Incidente - modo cauteloso do Vik ligado sem aviso]].

Os outros arquivos do repo (`api/chat.js`, `lib/prompt*.js`, `lib/memoria.js`,
`lib/segurancaVik.js`) nao tem marca nenhuma.

## Repo `moviki-assistente-social`

`src/config.py` e `src/firestore.py` sem marca — consome `api/vitrine`.

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[R - Stack e repositorios]] ·
[[ARQ - Conta Asaas na tela do lojista 16092026]]
