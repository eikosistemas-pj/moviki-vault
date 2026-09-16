---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-16
---

# R - Marcas de versao no ar

**Conferido clonando os quatro repositorios publicos em 16/09/2026, 20h30**,
depois das subidas do `exclusao2`, do `atrib1` e do `tetoplano`. Esta tabela
envelhece sozinha: a fonte de verdade e o repositorio, nunca este arquivo. No
navegador, `F12` > Console > `MOVIKI_VERSAO`; valor antigo e cache,
`Ctrl+Shift+R` — aconteceu duas vezes hoje.

## Repo `moviki` (www.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `api/live.js` | **`2026-09-16-tetoplano`** |
| `index.html` (home) | `2026-09-16-preco2` |
| `live.html` (quem assiste) | `2026-09-16-paguei` |
| `404.html` | `2026-09-16-selovivo` |
| `aovivo.html` | `2026-09-16-aovivo8` |
| `comerciantes.html` · `premium.html` · `enterprise.html` · `parceiros.html` · `termos.html` | `2026-09-16-preco1` |
| `p.html` · `pp.html` | `2026-09-16-previa` |
| `parceiros-ganhos.html` | `2026-09-16-simulador` |
| `api/sitemap.js` | `2026-09-16-sitemap1` |
| `lib/seo.js` | `2026-09-16-seo1` |
| `api/og.js` | `2026-09-15-og` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `privacidade.html` | `2026-09-12-live1` |
| `regras-da-live.html` | `2026-09-11-regras1` |
| `api/vitrine.js` | `2026-09-04-vitrine1` |
| `lib/gauth.js` | `2026-09-04-gauth1` |
| `v.html` | `2026-09-03-verificacao` |
| `descadastro.html` | `2026-09-03-appcheck` |
| `regulamento.html` · `excluir-conta.html` · `mvmetrica.js` · `vercel.json` | **sem marca** |

## Repo `moviki-app` (app.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `eikoadm01.html` (painel do dono) | **`2026-09-16-tetoplano`** |
| `live.html` (estudio) | **`2026-09-16-tetoplano`** |
| `index.html` (painel do lojista) | **`2026-09-16-atrib1`** |
| `seja-parceiro.html` | **`2026-09-16-atrib1`** |
| `parceiro.html` | `2026-09-16-preco1` |
| `liveaulas.js` | `2026-09-16-pixnovo` |
| `material/catalogo.json` | `versao: 2026-09-16-fotografia` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `404.html` | `2026-08-28-404vik` |
| `regulamento.html` · `quiz/quiz-segmentos.js` · `mvmetrica.js` · `vercel.json` | **sem marca** |

## Repo `moviki-robo`

| Arquivo | Marca |
| --- | --- |
| `lib/livesessao.js` | **`2026-09-16-tetoplano`** |
| `api/novo-parceiro.js` | **`2026-09-16-leadparceiro`** |
| `lib/meta.js` | **`2026-09-16-leadid`** |
| `api/exclusoes.js` | `2026-09-16-exclusao2` |
| `lib/checkout.js` | `2026-09-16-livesessao` |
| `api/pagar-saque.js` | `2026-09-16-saque1` |
| `api/pontos.js` | `2026-09-15-livesessao` |
| `api/webhook.js` | `2026-09-15-escopo` |
| `lib/asaas.js` | `2026-09-14-falhafechada` |
| `lib/pix.js` | `2026-09-14-pixdireto` |
| `api/financeiro.js` · `api/pedido.js` | `2026-09-14-porta1` |
| `api/webhook-reprocessa.js` | `2026-09-14-repro1` |
| `api/excluir-conta.js` · `api/ativar-trial.js` · `api/criar-assinatura.js` · `api/lembrete-trial.js` · `api/novo-cliente.js` · `api/parceiro-aprovado.js` · `api/upload-imagem.js` · `api/video-capa.js` · `lib/firebase.js` · `lib/ga.js` · `lib/instagram.js` · `lib/espelhoParceiro.js` · `lib/boasVindasParceiro.js` | **sem marca** |

`api/` segue com **12 arquivos, no teto do plano Hobby**. Nada novo cabe la.

## Repo `moviki-ai`

`lib/catalogoPainel.js` **`2026-09-16-9`**.

✅ **`MARCAS_CONFERIDAS` bate com o que esta no ar**: lojista `2026-09-16-atrib1`,
parceiro `2026-09-16-preco1`. O Vik saiu do modo cauteloso em 16/09 as 20h,
depois de um dia inteiro nele sem ninguem ver.

> A melhoria que falta e o painel do dono **acusar** a divergencia. Marca velha
> ali degrada o Vik sem sintoma nenhum na tela — foi assim duas vezes no mesmo
> dia. Ver [[ARQ - Incidente - modo cauteloso do Vik ligado sem aviso]].

## Regras do Firestore

**v25 publicada e conferida em 16/09/2026** — `denuncias` e `livepresenca` com
`liveNoAr()` no create, `saques` com `pedidoEm == request.time`.
O Console e a verdade; a copia no Project nao prova o que esta publicado.

## Como conferir

```
git clone --depth 1 https://github.com/eikosistemas-pj/<repo>.git
```

Funciona sem credencial em `moviki`, `moviki-app`, `moviki-robo` e `moviki-ai`.
O `moviki-vault` e privado. **WebFetch pega cache de CDN** — para saber o que
esta no ar, clonar.

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[P - Abertura da live para lojista pagante]] ·
[[ARQ - Teto de minutos de video por plano 16092026]]
