---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-16
---

# R - Marcas de versao no ar

**Conferido clonando os cinco repositorios em 16/09/2026, 05h.** Esta tabela
envelhece sozinha: a fonte de verdade e o repositorio, nunca este arquivo. No
navegador, `F12` > Console > `MOVIKI_VERSAO`; valor antigo e cache,
`Ctrl+Shift+R`.

Substitui a leitura da madrugada de 16/09, que ja nasceu velha: os paineis
andaram cinco vezes depois dela.

## Repo `moviki` (www.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (home) | `2026-09-16-ctavideo` |
| `comerciantes.html` | `2026-09-16-filmelive` |
| `aovivo.html` (venda da live) | `2026-09-16-aovivo8-publica` |
| `live.html` (quem assiste) | `2026-09-16-csp1` |
| `api/live.js` | `2026-09-16-teto3` |
| `api/og.js` | `2026-09-15-og` |
| `404.html` | `2026-09-15-compra4` |
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
| `eikoadm01.html` (painel do dono) | `2026-09-16-consumo3` |
| `parceiro.html` | `2026-09-16-wafoto` |
| `index.html` (painel do lojista) | `2026-09-15-liveaulas2` |
| `live.html` (estudio) | `2026-09-15-liveaulas` |
| `liveaulas.js` | `2026-09-15-liveaulas2` |
| `material/catalogo.json` | `versao: 2026-09-16-qr` |
| `mvqr.js` | `2026-09-14-mvqr2` |
| `seja-parceiro.html` | `2026-09-04-conta-existente` |
| `404.html` | `2026-08-28-404vik` |
| `regulamento.html` · `quiz/quiz-segmentos.js` · `mvmetrica.js` · `vercel.json` | **sem marca** |

## Repo `moviki-ai`

| Arquivo | Marca |
| --- | --- |
| `lib/catalogoPainel.js` | `2026-09-16-1` |

`MARCAS_CONFERIDAS` dentro desse arquivo: lojista `2026-09-15-liveaulas2`,
parceiro `2026-09-15-aulatrava`. **O parceiro no ar esta em `wafoto`** — ou
seja, o Vik esta em modo cauteloso agora. Ver
[[ARQ - Incidente - modo cauteloso do Vik ligado sem aviso]].

Os outros arquivos do repo (`api/chat.js`, `lib/prompt*.js`, `lib/memoria.js`,
`lib/segurancaVik.js`) nao tem marca nenhuma.

## Repo `moviki-robo`

| Arquivo | Marca |
| --- | --- |
| `api/pagar-saque.js` | `2026-09-16-saque1` |
| `api/pontos.js` | `2026-09-15-livesessao` |
| `api/webhook.js` | `2026-09-15-escopo` |
| `lib/livesessao.js` | `2026-09-15-b5b` |
| `lib/asaas.js` | `2026-09-14-falhafechada` |
| `lib/checkout.js` | `2026-09-14` |
| `lib/pix.js` | `2026-09-14-pixdireto` |
| `api/financeiro.js` · `api/pedido.js` | `2026-09-14-porta1` |
| `api/webhook-reprocessa.js` | `2026-09-14-repro1` |

**12 funcoes em `api/` — no teto do plano Hobby da Vercel.** Funcao nova entra
como etapa de uma existente, nunca como arquivo novo.

## Repo `moviki-assistente-social`

`src/config.py` e `src/firestore.py` em 2026-09-04 — o robo consome
`moviki.com.br/api/vitrine`.

## Firestore

**Regras v25 publicadas em 16/09/2026**, sobre a v24 de 15/09. O Console e a
verdade.

## Entregue e AINDA NAO no ar em 16/09/2026, 05h

| Repo | Arquivo | Marca entregue |
| --- | --- | --- |
| `moviki` | `icones-premium/live.png` (NOVO) | — |
| `moviki` | `comerciantes.html` | `2026-09-16-iconelive` |
| `moviki-app` | `icones/cat-*.png` (12 NOVOS) | — |
| `moviki-app` | `material/catalogo.json` | `2026-09-16-caticones` |
| `moviki-app` | `parceiro.html` | `2026-09-16-caticones` |
| `moviki-ai` | `lib/catalogoPainel.js` | `2026-09-16-2` |

## Alertas desta leitura

- **O modo cauteloso do Vik ligou duas vezes em dois dias sem ninguem ver.**
- **`premium.html` e `enterprise.html` continuam sem marca e sem uma linha
  sobre o Modo Live** — e `premium.html` e a landing que recebe trafego pago.
- **`p.html` e `pp.html` ganharam metatag de previa em 16/09 e continuam sem
  marca de versao.** Sao os links mais compartilhados do projeto.
- `regulamento.html` dos dois repos esta em conteudo 1.1 **sem marca** —
  diagnosticar por marca ali da a resposta errada.

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
[[ARQ - Incidente - modo cauteloso do Vik ligado sem aviso]] ·
[[ARQ - Icones 3D das categorias e da live 16092026]]
