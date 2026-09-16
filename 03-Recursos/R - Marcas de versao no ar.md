---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-16
---

# R - Marcas de versao no ar

**Conferido clonando os cinco repositorios em 16/09/2026, de madrugada.** Esta
tabela envelhece sozinha: a fonte de verdade e o repositorio, nunca este
arquivo. No navegador, `F12` > Console > `MOVIKI_VERSAO`; valor antigo e cache,
`Ctrl+Shift+R`.

A leitura de 10/09 que estava aqui antes ficou seis dias parada enquanto os
paineis andaram todo dia. Foi substituida inteira.

## Repo `moviki` (moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (home) | `2026-09-16-ctavideo` |
| `comerciantes.html` | `2026-09-16-iconelive` |
| `aovivo.html` | `2026-09-16-aovivo8-publica` |
| `live.html` | `2026-09-16-csp1` |
| `api/live.js` | `2026-09-16-teto3` |
| `api/og.js` | `2026-09-15-og-live` |
| `404.html` | `2026-09-15-compra4` |
| `v.html` | `2026-09-10-foto-parceiro` |
| `descadastro.html` | `2026-09-03-appcheck` |
| `enterprise.html` | `2026-08-27-ga4l2` |
| `parceiros.html` | `2026-08-28-vikparceiros` |
| `parceiros-ganhos.html` | `2026-08-27-conformidade` |
| `p.html` · `pp.html` · `premium.html` · `regulamento.html` · `termos.html` · `privacidade.html` · `excluir-conta.html` | **sem marca** |

## Repo `moviki-app` (app.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `eikoadm01.html` (painel do dono) | `2026-09-16-consumo3` |
| `parceiro.html` | `2026-09-16-caticones` |
| `index.html` (painel do lojista) | `2026-09-15-liveaulas2` |
| `live.html` (estudio) | `2026-09-15-liveaulas` |
| `material/catalogo.json` | `2026-09-16-caticones` |
| `seja-parceiro.html` | `2026-09-04-conta-existente` |
| `404.html` | `2026-08-28-404vik` |

## Repo `moviki-ai`

| Arquivo | Marca |
| --- | --- |
| `lib/catalogoPainel.js` | `2026-09-16-2` |

`MARCAS_CONFERIDAS` neste arquivo: lojista `2026-09-15-liveaulas2`, parceiro
`2026-09-16-caticones`. Divergiu de `MOVIKI_VERSAO` do painel, o Vik entra em
modo cauteloso sozinho — e **nao avisa ninguem**.

## Repo `moviki-robo`

`lib/checkout.js` com a revisao de 14/09. `api/pagar-saque.js` com o corte de
comissoes fechado, o id deterministico do saque e a quitacao em lotes de 400
(`2026-09-16-saque1`).

## Repo `moviki-assistente-social`

`src/config.py` e `src/firestore.py` em 2026-09-04 — o robo consome
`moviki.com.br/api/vitrine`.

## Alertas desta leitura

- **O modo cauteloso do Vik ligou duas vezes em dois dias sem ninguem ver.**
  Em 15/09 por `2026-09-13-vikpainel` contra `liveaulas2`/`aulatrava`; em 16/09
  por `aulatrava` contra `wafoto`. O mecanismo funciona; o problema e que ele e
  silencioso por desenho.
- **`premium.html` e `enterprise.html` continuam sem marca e sem uma linha
  sobre o Modo Live** — e `premium.html` e a landing que recebe trafego pago.
- **`p.html` e `pp.html` ganharam metatag de previa em 16/09 mas nao ganharam
  marca de versao.** Sao os links mais compartilhados do projeto.

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
[[R - Design system e icones]] ·
[[ARQ - Icones 3D das categorias e da live 16092026]]
