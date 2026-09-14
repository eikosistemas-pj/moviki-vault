---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-14
---

# R - Marcas de versao no ar

**Conferido clonando os quatro repositorios em 14/09/2026, ao fim do dia.** Esta
tabela envelhece sozinha: a fonte de verdade e o repositorio, nunca este
arquivo. No navegador, `F12` > Console > `MOVIKI_VERSAO`; valor antigo e cache,
`Ctrl+Shift+R`. Em pagina com `script-src 'none'` (regras-da-live), a marca vive
em `<meta name="moviki-versao">` e se le no F12 > Elements.

## Repo `moviki` (moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `comerciantes.html` | `2026-09-14-porta` |
| `aovivo.html` | `2026-09-14-ocultar` |
| `regras-da-live.html` | `2026-09-14-ocultar` |
| `live.html` | `2026-09-12-beta1` |
| `api/live.js` | `2026-09-12-beta1` |
| `404.html` (pagina publica do negocio) | `2026-09-11-live1` |
| `v.html` (verificacao do parceiro) | `2026-09-10-foto-parceiro` |
| `index.html` (landing) | `2026-09-09-video` |
| `lib/gauth.js` | `2026-09-04-gauth1` |
| `api/og.js` | `2026-09-04-og-sa` |
| `api/vitrine.js` | `2026-09-04-vitrine1` |
| `descadastro.html` | `2026-09-03-appcheck` |
| `enterprise.html` | `2026-08-27-ga4l2` |
| `parceiros.html` | `2026-08-28-vikparceiros` |
| `parceiros-ganhos.html` | `2026-08-27-conformidade` |
| `premium.html` · `regulamento.html` · `termos.html` · `privacidade.html` · `excluir-conta.html` · `p.html` · `pp.html` | **sem marca** |
| `vercel.json` | rotas `/aovivo` e `/regras-da-live` antes do curinga · **HSTS 1 ano** · **CSP `frame-ancestors 'self'`** (14/09) |

## Repo `moviki-app` (app.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (painel do lojista) | `2026-09-14-financeiro` |
| `parceiro.html` | `2026-09-13-vikpainel` |
| `live.html` (estudio) | `2026-09-12-www2` |
| `eikoadm01.html` (painel do dono) | `2026-09-12-www1` |
| `mvqr.js` | `2026-09-04-mvqr1` |
| `seja-parceiro.html` | `2026-09-04-conta-existente` |
| `material/catalogo.json` | `2026-09-12-1` |
| `404.html` | `2026-08-28-404vik` |
| `vercel.json` | **HSTS 1 ano** · **CSP `frame-ancestors 'self'`** (14/09) |
| `regulamento.html` | **sem marca** (conteudo na versao 1.1) |

## Repo `moviki-robo`

**15 funcoes em `api/`.** O teto de 12 do plano Hobby deixou de existir com a
assinatura do **Vercel Pro em 14/09/2026**.

| Arquivo | Marca |
| --- | --- |
| `lib/checkout.js` | `2026-09-14-aceite` |
| `lib/pix.js` | `2026-09-14-pixdireto` (NOVO) |
| `lib/asaas.js` | `2026-09-14-falhafechada` |
| `api/webhook.js` | `2026-09-14-fila1` |
| `api/webhook-reprocessa.js` | `2026-09-14-repro1` (NOVO) |
| `api/pedido.js` | `2026-09-14-porta1` (NOVO) |
| `api/financeiro.js` | `2026-09-14-porta1` (NOVO) |
| `api/pontos.js` | `2026-09-11-checkout1` |
| `vercel.json` | 2 crons: `lembrete-trial` 0 12 · `webhook-reprocessa` 20 * * * * |

Demais arquivos sem marca propria: `lib/meta.js`, `lib/ga.js`,
`lib/espelhoParceiro.js`, `lib/instagram.js`, `lib/firebase.js`,
`lib/boasVindasParceiro.js`, `api/novo-cliente.js`, `api/novo-parceiro.js`,
`api/criar-assinatura.js`, `api/ativar-trial.js`, `api/lembrete-trial.js`,
`api/pagar-saque.js`, `api/parceiro-aprovado.js`, `api/upload-imagem.js`,
`api/excluir-conta.js`, `api/exclusoes.js`.

## Repo `moviki-assistente-social`

`src/config.py` e `src/firestore.py` em 2026-09-04 — o robo nao fala mais com o
Firestore, consome `moviki.com.br/api/vitrine`.

## Regras do Firestore

**v23**, publicada em 12/09/2026. Conferida linha a linha em 14/09: a Fase 1 do
Financeiro **nao precisa de v24**.

## ⚠️ Alertas desta leitura (14/09/2026)

- **`moviki-app/liveaulas.js` NAO EXISTE no repositorio.** A entrega de 13/09
  (catalogo das 13 aulas do Modo Live) nunca subiu. O `live.html` no ar e o
  `2026-09-12-www2`, sem o motor de aulas — ou seja, **as duas entregas de 13/09
  do modulo de aulas estao perdidas**, nao so o catalogo.
- **O MAPA-MESTRE afirma que o `liveaulas.js` "esta no ar sem id de video".**
  Esta errado: ele nao esta no ar. Corrigir no proximo `/atualizarmapa`.
- **O editor de foto do cardapio (`mvAjustarFoto`, marca `2026-09-11-fotoajuste`)
  nao existe em nenhum dos dois arquivos** — nem no `index.html` do app nem no
  `404.html` do site. Entrega perdida, precisa ser refeita sobre
  `2026-09-14-financeiro`.
- **O `404.html` do site esta em `2026-09-11-live1`** — e o arquivo da pagina
  publica do negocio, onde o cardapio compravel vai entrar.
