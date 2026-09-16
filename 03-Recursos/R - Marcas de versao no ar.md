---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-16
---

# R - Marcas de versao no ar

**Conferido clonando os repositorios em 16/09/2026, 05h**, com as entregas da
tarde somadas por cima. Esta tabela envelhece sozinha: a fonte de verdade e o
repositorio, nunca este arquivo. No navegador, `F12` > Console >
`MOVIKI_VERSAO`; valor antigo e cache, `Ctrl+Shift+R`.

## Repo `moviki` (www.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (home) | `2026-09-16-ctavideo` |
| `comerciantes.html` | `2026-09-16-filmelive` |
| `aovivo.html` (venda da live) | `2026-09-16-aovivo8-publica` |
| `live.html` (quem assiste) | `2026-09-16-csp1` |
| `404.html` (pagina publica) | `2026-09-16-capavideo` |
| `api/live.js` | `2026-09-16-teto3` |
| `api/og.js` | `2026-09-15-og` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `termos.html` · `privacidade.html` | `2026-09-12-live1` |
| `regras-da-live.html` | `2026-09-11-regras1` |
| `v.html` | `2026-09-10-foto-parceiro` |
| `api/vitrine.js` | `2026-09-04-vitrine1` |
| `lib/gauth.js` | `2026-09-04-gauth1` |
| `descadastro.html` | `2026-09-03-appcheck` |
| `enterprise.html` | `2026-08-27-ga4l2` |
| `parceiros.html` | `2026-08-28-vikparceiros` |
| `parceiros-ganhos.html` | `2026-08-27-conformidade` |
| `p.html` · `pp.html` · `premium.html` · `regulamento.html` · `excluir-conta.html` · `mvmetrica.js` · `js/moviki-3d.js` · `vercel.json` | **sem marca** |

`vercel.json` sem marca contem `/v/:slug`, `/p/:slug`, `/pp/:slug` e a rota
`/aovivo` **antes** do curinga. Mexer ali sem conferir a ordem quebra os links
do parceiro.

## Repo `moviki-app` (app.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (painel do lojista) | `2026-09-16-cena` |
| `parceiro.html` | `2026-09-16-trilha` |
| `eikoadm01.html` (painel do dono) | `2026-09-16-consumo3` |
| `liveaulas.js` | `2026-09-16-pixnovo` |
| `live.html` (estudio) | `2026-09-16-pixfinanceiro` |
| `material/catalogo.json` | `versao: 2026-09-16-caticones` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `seja-parceiro.html` | `2026-09-04-conta-existente` |
| `404.html` | `2026-08-28-404vik` |
| `regulamento.html` · `quiz/quiz-segmentos.js` · `mvmetrica.js` · `vercel.json` | **sem marca** |

## Repo `moviki-ai`

| Arquivo | Marca |
| --- | --- |
| `lib/catalogoPainel.js` | `2026-09-16-8` |

`MARCAS_CONFERIDAS` dentro desse arquivo: lojista `2026-09-16-cena`, parceiro
`2026-09-16-trilha` — **iguais as marcas dos paineis acima**. Enquanto as duas
baterem, o Vik responde em modo normal.

Os outros arquivos do repo (`api/chat.js`, `lib/prompt*.js`, `lib/memoria.js`,
`lib/segurancaVik.js`) nao tem marca nenhuma.

## Repo `moviki-robo`

| Arquivo | Marca |
| --- | --- |
| `api/upload-imagem.js` | `2026-09-16-capatiktok` |
| `lib/checkout.js` | `2026-09-16-subfechada` |
| `api/pagar-saque.js` | `2026-09-16-saque1` |
| `api/pontos.js` | `2026-09-15-livesessao` |
| `api/webhook.js` | `2026-09-15-escopo` |
| `lib/livesessao.js` | `2026-09-15-b5b` |
| `lib/asaas.js` | `2026-09-14-falhafechada` |
| `lib/pix.js` | `2026-09-14-pixdireto` |
| `api/financeiro.js` · `api/pedido.js` | `2026-09-14-porta1` |
| `api/webhook-reprocessa.js` | `2026-09-14-repro1` |

**15 funcoes em `api/`** (conferido clonando em 16/09): `ativar-trial`,
`criar-assinatura`, `excluir-conta`, `exclusoes`, `financeiro`,
`lembrete-trial`, `novo-cliente`, `novo-parceiro`, `pagar-saque`,
`parceiro-aprovado`, `pedido`, `pontos`, `upload-imagem`,
`webhook-reprocessa`, `webhook`.

> **Funcao nova entra como etapa de uma existente, nunca como arquivo novo.**
> Em 16/09 a capa do TikTok quase virou `api/video-capa.js`; foi dobrada dentro
> do `upload-imagem.js` como `tipo:'tiktok'`. Ver
> [[ARQ - Capa do TikTok automatica 16092026]].

## Repo `moviki-assistente-social`

`src/config.py` e `src/firestore.py` em 2026-09-04 — o robo consome
`moviki.com.br/api/vitrine`.

## Firestore

**Regras v25 publicadas em 16/09/2026**, sobre a v24 de 15/09. O Console e a
verdade.

## Alertas desta leitura

- **`premium.html` e `enterprise.html` continuam sem marca e sem uma linha
  sobre o Modo Live** — e `premium.html` e a landing que recebe trafego pago.
- **`p.html` e `pp.html` ganharam metatag de previa em 16/09 e continuam sem
  marca de versao.** Sao os links mais compartilhados do projeto.
- `regulamento.html` dos dois repos esta em conteudo 1.1 **sem marca** —
  diagnosticar por marca ali da a resposta errada.
- A capa automatica do TikTok **so pode ser testada no ar**: o dominio do
  TikTok e bloqueado no ambiente onde o codigo e escrito.

## Regra de ouro que sustenta esta nota

> **Marca de versao so vale se sobe junto com o conteudo.** Arquivo que ganha
> funcionalidade e mantem a marca antiga e pior que arquivo sem marca: afirma
> um estado falso e o diagnostico comeca no lugar errado.
>
> **"Entregue" e "no ar" sao estados diferentes, e so o repositorio sabe qual
> e qual.**
>
> **Tabela de marca do Vik sobe na MESMA rodada do painel.** Marca velha ali
> nao quebra nada — degrada tudo, devagar e sem ruido.

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[R - Regras de ouro]] ·
[[R - Checklist de deploy]] ·
[[ARQ - Capa do TikTok automatica 16092026]] ·
[[ARQ - Tela escura na escolha da cena 16092026]]
