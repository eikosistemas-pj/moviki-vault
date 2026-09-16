---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-16
---

# R - Marcas de versao no ar

**Conferido clonando os repositorios em 16/09/2026, 19h32** — depois de todas as
subidas do dia. Esta tabela envelhece sozinha: a fonte de verdade é o
repositório, nunca este arquivo. No navegador, `F12` > Console >
`MOVIKI_VERSAO`; valor antigo é cache, `Ctrl+Shift+R`.

Substitui a leitura das 05h de 16/09: dez arquivos andaram depois dela.

## Repo `moviki` (www.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `live.html` (quem assiste) | **`2026-09-16-paguei`** |
| `404.html` (pagina do negocio) | **`2026-09-16-selovivo`** |
| `api/live.js` | `2026-09-16-teto3` |
| `api/sitemap.js` | `2026-09-16-sitemap1` |
| `lib/seo.js` | `2026-09-16-seo1` |
| `aovivo.html` | `2026-09-16-aovivo8-publica` |
| `p.html` · `pp.html` | `2026-09-16-previa` |
| `parceiros-ganhos.html` | `2026-09-16-parceirolive` |
| `comerciantes.html` · `enterprise.html` · `premium.html` · `termos.html` | `2026-09-16-preco1` |
| `api/og.js` | `2026-09-15-og-live` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `privacidade.html` | `2026-09-12-live1` |
| `regras-da-live.html` | `2026-09-11-regras1` |
| `api/vitrine.js` | `2026-09-04-vitrine1` |
| `lib/gauth.js` | `2026-09-04-gauth1` |
| `v.html` | `2026-09-03-verificacao` |
| `descadastro.html` | `2026-09-03-appcheck` |
| `parceiros.html` | `2026-08-28-vikparceiros` |
| `index.html` (home) | `2026-08-28-vikfaq` |
| `excluir-conta.html` · `regulamento.html` · `mvmetrica.js` · `js/moviki-3d.js` · `vercel.json` | **sem marca** |

Binários na raiz (`parceiros.pdf` 120.953 B, `comerciantes.pdf` 82.412 B)
atualizados em 16/09 — commit `e7140e6`. **Arquivo binário público é material da
marca mesmo sem link, e não aparece em busca de texto.**

`vercel.json` sem marca contém `/v/:slug`, `/p/:slug`, `/pp/:slug`, `/live/:slug`
e `/aovivo` **antes** do curinga `/:slug`. Mexer ali sem conferir a ordem quebra
os links do parceiro.

## Repo `moviki-app` (app.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `live.html` (estudio) | **`2026-09-16-imersivo3`** |
| `liveaulas.js` | `2026-09-16-pixnovo` |
| `eikoadm01.html` (painel do dono) | `2026-09-16-preco1` |
| `seja-parceiro.html` | `2026-09-16-parceirolive` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `index.html` (painel do lojista) | `2026-08-28-vikpadrao` |
| `parceiro.html` | `2026-08-28-vikpadrao` |
| `404.html` | `2026-08-28-404vik` |
| `regulamento.html` · `quiz/quiz-segmentos.js` · `mvmetrica.js` · `vercel.json` | **sem marca** |

## Repo `moviki-robo`

| Arquivo | Marca |
| --- | --- |
| `lib/checkout.js` | **`2026-09-16-livesessao`** |
| `api/pagar-saque.js` | `2026-09-16-saque1` |
| `lib/livesessao.js` | `2026-09-15-b5b` |
| `api/pontos.js` | `2026-09-15-livesessao` |
| `api/webhook.js` | `2026-09-15-escopo` |
| `lib/asaas.js` | `2026-09-14-falhafechada` |
| `lib/pix.js` | `2026-09-14-pixdireto` |
| `api/financeiro.js` · `api/pedido.js` | `2026-09-14-porta1` |
| `api/webhook-reprocessa.js` | `2026-09-14-repro1` |
| `api/exclusoes.js` · `api/excluir-conta.js` · `api/ativar-trial.js` · `api/criar-assinatura.js` · `api/lembrete-trial.js` · `api/novo-cliente.js` · `api/novo-parceiro.js` · `api/parceiro-aprovado.js` · `api/upload-imagem.js` · `api/video-capa.js` · `lib/firebase.js` · `lib/ga.js` · `lib/meta.js` · `lib/instagram.js` · `lib/espelhoParceiro.js` · `lib/boasVindasParceiro.js` | **sem marca** |

## Repo `moviki-ai`

| Arquivo | Marca |
| --- | --- |
| `lib/catalogoPainel.js` | `2026-09-16-8` |

`MARCAS_CONFERIDAS` dentro desse arquivo precisa ser reconferida: o estúdio e a
página pública andaram várias vezes em 16/09.

Os outros arquivos do repo (`api/chat.js`, `lib/prompt*.js`, `lib/memoria.js`,
`lib/segurancaVik.js`) não têm marca nenhuma.

## Repo `moviki-assistente-social`

Só estado (`estado/*.json`), sem marca de versão.

## Armadilha

**WebFetch pega cache de CDN.** Para saber o que está no ar, clonar:
`git clone --depth 1 https://github.com/eikosistemas-pj/<repo>.git` funciona sem
credencial nos quatro repos de código (o `moviki-vault` é privado).

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[R - Regras de ouro]] ·
[[ARQ - Estudio imersivo da live 16092026]] ·
[[ARQ - Regressoes da migracao b5b 16092026]]
