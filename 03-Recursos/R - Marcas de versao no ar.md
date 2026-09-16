---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-16
---

# R - Marcas de versao no ar

**Conferido clonando os cinco repositorios em 16/09/2026, depois da subida do
`exclusao2`.** Esta tabela envelhece sozinha: a fonte de verdade e o
repositorio, nunca este arquivo. No navegador, `F12` > Console >
`MOVIKI_VERSAO`; valor antigo e cache, `Ctrl+Shift+R`.

Substitui a leitura das 05h de 16/09, que ja nasceu velha — os paineis andaram
muitas vezes depois dela.

## Repo `moviki` (www.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (home) | `2026-09-16-preco2` |
| `comerciantes.html` | `2026-09-16-preco1` |
| `premium.html` · `enterprise.html` · `parceiros.html` · `termos.html` | `2026-09-16-preco1` |
| `aovivo.html` (venda da live) | `2026-09-16-aovivo8` |
| `live.html` (quem assiste) | **`2026-09-16-paguei`** |
| `404.html` | **`2026-09-16-selovivo`** |
| `api/live.js` | `2026-09-16-teto3` |
| `api/sitemap.js` | `2026-09-16-sitemap1` |
| `lib/seo.js` | `2026-09-16-seo1` |
| `p.html` · `pp.html` | `2026-09-16-previa` |
| `parceiros-ganhos.html` | `2026-09-16-simulador` |
| `api/og.js` | `2026-09-15-og` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `privacidade.html` | `2026-09-12-live1` |
| `regras-da-live.html` | `2026-09-11-regras1` |
| `api/vitrine.js` | `2026-09-04-vitrine1` |
| `lib/gauth.js` | `2026-09-04-gauth1` |
| `v.html` | `2026-09-03-verificacao` |
| `descadastro.html` | `2026-09-03-appcheck` |
| `regulamento.html` · `excluir-conta.html` · `mvmetrica.js` · `js/moviki-3d.js` · `vercel.json` | **sem marca** |

`vercel.json` sem marca contem `/v/:slug`, `/p/:slug`, `/pp/:slug`,
`/live/:slug` e `/aovivo` **antes** do curinga `/:slug`. Mexer ali sem conferir
a ordem quebra os links do parceiro.

## Repo `moviki-app` (app.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `eikoadm01.html` (painel do dono) | **`2026-09-16-exclusao2`** |
| `live.html` (estudio) | `2026-09-16-imersivo3` |
| `liveaulas.js` | `2026-09-16-pixnovo` |
| `index.html` (painel do lojista) | `2026-09-16-preco1` |
| `parceiro.html` | `2026-09-16-preco1` |
| `seja-parceiro.html` | `2026-09-16-parceirolive` |
| `material/catalogo.json` | `versao: 2026-09-16-fotografia` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `404.html` | `2026-08-28-404vik` |
| `regulamento.html` · `quiz/quiz-segmentos.js` · `mvmetrica.js` · `vercel.json` | **sem marca** |

## Repo `moviki-robo`

| Arquivo | Marca |
| --- | --- |
| `api/exclusoes.js` | **`2026-09-16-exclusao2`** |
| `lib/checkout.js` | `2026-09-16-livesessao` |
| `api/pagar-saque.js` | `2026-09-16-saque1` |
| `lib/livesessao.js` | `2026-09-15-b5b` |
| `api/pontos.js` | `2026-09-15-livesessao` |
| `api/webhook.js` | `2026-09-15-escopo` |
| `lib/asaas.js` | `2026-09-14-falhafechada` |
| `lib/pix.js` | `2026-09-14-pixdireto` |
| `api/financeiro.js` · `api/pedido.js` | `2026-09-14-porta1` |
| `api/webhook-reprocessa.js` | `2026-09-14-repro1` |
| `api/excluir-conta.js` · `api/ativar-trial.js` · `api/criar-assinatura.js` · `api/lembrete-trial.js` · `api/novo-cliente.js` · `api/novo-parceiro.js` · `api/parceiro-aprovado.js` · `api/upload-imagem.js` · `api/video-capa.js` · `lib/firebase.js` · `lib/ga.js` · `lib/meta.js` · `lib/instagram.js` · `lib/espelhoParceiro.js` · `lib/boasVindasParceiro.js` | **sem marca** |

`api/` segue com **12 arquivos, no teto do plano Hobby**. Nada novo cabe la.

## Repo `moviki-ai`

`lib/catalogoPainel.js` **`2026-09-16-8`**.

> ⚠️ **`MARCAS_CONFERIDAS` esta divergente do que esta no ar.** O arquivo espera
> lojista `2026-09-16-asaasconta` e parceiro `2026-09-16-trilha`; no ar estao
> **`2026-09-16-preco1`** nos dois. **O Vik esta em modo cauteloso agora, sem
> aviso na tela.** Ver [[ARQ - Incidente - modo cauteloso do Vik ligado sem aviso]].

Os outros arquivos do repo (`api/chat.js`, `lib/prompt*.js`, `lib/memoria.js`,
`lib/segurancaVik.js`) nao tem marca nenhuma.

## Repo `moviki-assistente-social`

So estado (`estado/*.json`), sem marca.

## Como conferir

```
git clone --depth 1 https://github.com/eikosistemas-pj/<repo>.git
```

Funciona sem credencial em `moviki`, `moviki-app`, `moviki-robo` e `moviki-ai`.
O `moviki-vault` e privado. **WebFetch pega cache de CDN** — para saber o que
esta no ar, clonar.

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[P - Abertura da live para lojista pagante]]
