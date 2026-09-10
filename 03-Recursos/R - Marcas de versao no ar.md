---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-10
---

# R - Marcas de versao no ar

**Conferido clonando os repositorios em 10/09/2026.** Esta tabela envelhece
sozinha: a fonte de verdade e o repositorio, nunca este arquivo. No navegador,
`F12` > Console > `MOVIKI_VERSAO`; valor antigo e cache, `Ctrl+Shift+R`.

## Repo `moviki` (moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (landing) | `2026-09-09-video` |
| `404.html` (pagina publica) | `2026-09-10-videos` |
| `v.html` (verificacao) | `2026-09-10-foto-parceiro` |
| `comerciantes.html` | `2026-09-09-video` |
| `descadastro.html` | `2026-09-03-appcheck` |
| `enterprise.html` | `2026-08-27-ga4l2` |
| `parceiros.html` | `2026-08-28-vikparceiros` |
| `parceiros-ganhos.html` | `2026-08-27-conformidade` |
| `lib/gauth.js` | `2026-09-04-gauth1` |
| `api/og.js` | `2026-09-04-og-sa` |
| `api/vitrine.js` | `2026-09-04-vitrine1` |
| `premium.html` · `regulamento.html` · `termos.html` · `privacidade.html` · `excluir-conta.html` · `p.html` · `pp.html` | **sem marca** |

## Repo `moviki-app` (app.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (painel do lojista) | `2026-09-10-videos` |
| `parceiro.html` | `2026-09-10-niveis-olhinhos` |
| `eikoadm01.html` (painel do dono) | `2026-09-04-cracha-busca` |
| `seja-parceiro.html` | `2026-09-04-conta-existente` |
| `mvqr.js` | `2026-09-04-mvqr1` |
| `404.html` | `2026-08-28-404vik` |
| `quiz/quiz-segmentos.js` | com Suplementos, Sushi e Otica (10 abas / 31 opcoes) |
| `regulamento.html` | **sem marca** (conteudo na versao 1.1) |

## Repo `moviki-robo`

`lib/meta.js` e `api/novo-cliente.js` com a revisao de 05/09: timeout de 6 s no
`Lead`, 2,5 s no `Purchase`, e a linha do resultado da medicao no aviso do
Telegram. `api/webhook.js` com `NIVEIS_PARCEIRO`, `contarAtivosDoMes`,
`creditarMarco` e `guardarNivel`. `api/upload-imagem.js`, `api/novo-parceiro.js` e
`lib/espelhoParceiro.js` com o campo `foto` do parceiro. **12 funcoes em `api/` —
no teto do plano Hobby.**

## Repo `moviki-assistente-social`

`src/config.py` e `src/firestore.py` em 2026-09-04 — o robo nao fala mais com o
Firestore, consome `moviki.com.br/api/vitrine`.

## Alertas desta leitura

- **`parceiro.html` no ar NAO tem o conserto do player nem os avisos de link
  fechado.** A entrega `2026-09-10-linkfechado` foi atropelada. Ver
  [[P20 - Conserto do player e liberacao do link]] e
  [[ARQ - Incidente - colisao de entregas no painel do parceiro]]
- **`novo-parceiro.js` no ar esta com `DELAY_MIN_MINUTOS = 10`** e sem
  `aprovarParceiro()` — a versao publicada e a da foto do parceiro
- **`premium.html` continua sem marca nenhuma**, e e a landing que recebe trafego
  pago
- `regulamento.html` dos dois repos esta em conteudo 1.1 mas **sem marca de
  versao** — diagnosticar por marca ali da a resposta errada
- `eikoadm01.html` esta em `2026-09-04-cracha-busca`: nao recebeu os cinco
  atendentes nem nada de 10/09

## Regra de ouro que sustenta esta nota

> **Marca de versao so vale se sobe junto com o conteudo.** Arquivo que ganha
> funcionalidade e mantem a marca antiga e pior que arquivo sem marca: afirma um
> estado falso e o diagnostico comeca no lugar errado.
>
> **"Entregue" e "no ar" sao estados diferentes, e so o repositorio sabe qual e
> qual.**

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[R - Regras de ouro]] ·
[[ARQ - Incidente - colisao de entregas no painel do parceiro]] ·
[[ARQ - App Check enforcement ligado]]
