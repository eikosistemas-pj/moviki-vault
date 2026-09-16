---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [deploy, versao, armadilha]
atualizado: 2026-09-16
---

# R - Marcas de versao no ar

**Conferido clonando os repositórios em 16/09/2026.** Esta tabela envelhece
sozinha: a fonte de verdade é o repositório, nunca este arquivo. No navegador,
`F12` > Console > `MOVIKI_VERSAO`; valor antigo é cache, `Ctrl+Shift+R`.

Substitui a leitura de 14/09.

## Repo `moviki` (www.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (landing) | `2026-09-09-video` |
| `comerciantes.html` | `2026-09-11-criarconta` |
| `404.html` (página pública) | `2026-09-15-compra4` |
| `v.html` (verificação) | `2026-09-10-foto-parceiro` |
| `aovivo.html` (página de venda da live) | `2026-09-14-ocultar` |
| `live.html` (página de quem assiste) | `2026-09-15-filtro` |
| `regras-da-live.html` | `2026-09-11-regras1` |
| `api/live.js` | `2026-09-15-b5a` |
| `termos.html` · `privacidade.html` | `2026-09-12-live1` |
| `descadastro.html` | `2026-09-03-appcheck` |
| `enterprise.html` | `2026-08-27-ga4l2` |
| `parceiros.html` | `2026-08-28-vikparceiros` |
| `parceiros-ganhos.html` | `2026-08-27-conformidade` |
| `lib/gauth.js` | `2026-09-04-gauth1` |
| `api/og.js` | `2026-09-04-og-sa` — **marca mentirosa, ver alertas** |
| `api/vitrine.js` | `2026-09-04-vitrine1` |
| `vercel.json` | sem marca — contém `/v/:slug` e a rota `/aovivo` **antes** do curinga |
| `livehero.webp` (103 KB) · `livehero.jpg` (140 KB) | sem marca |
| `premium.html` · `regulamento.html` · `excluir-conta.html` · `p.html` · `pp.html` | **sem marca** |

## Repo `moviki-app` (app.moviki.com.br)

| Arquivo | Marca |
| --- | --- |
| `index.html` (painel do lojista) | `2026-09-15-liveaulas2` |
| `parceiro.html` | `2026-09-15-aulatrava` |
| `live.html` (estúdio) | `2026-09-15-liveaulas` |
| `liveaulas.js` | `2026-09-15-liveaulas2` |
| `eikoadm01.html` (painel do dono) | `2026-09-15-conferir` |
| `seja-parceiro.html` | `2026-09-04-conta-existente` |
| `mvqr.js` | `2026-09-04-mvqr1` |
| `material/catalogo.json` | `versao: 2026-09-12-1` |
| `icones/live.png` · `icones/material.png` | sem marca |
| `404.html` | `2026-08-28-404vik` |
| `quiz/quiz-segmentos.js` | com Suplementos, Sushi e Ótica (10 abas / 31 opções) |
| `regulamento.html` · `vercel.json` | **sem marca** (regulamento em conteúdo 1.1) |

## Repo `moviki-robo`

| Arquivo | Marca |
| --- | --- |
| `lib/livesessao.js` | `2026-09-15-b5b` |
| `lib/checkout.js` | `2026-09-15-whtoken` |
| `api/pontos.js` | `2026-09-15-livesessao` |
| `api/webhook.js` | `2026-09-15-escopo` |
| `lib/meta.js` · `api/novo-cliente.js` | revisão de 05/09 — timeout de 6 s no `Lead`, 2,5 s no `Purchase`, linha do resultado da medição no aviso do Telegram |

**12 funções em `api/` — no teto do plano Hobby.** O 13º arquivo derruba o deploy
inteiro.

## Repo `moviki-assistente-social`

`src/config.py` e `src/firestore.py` em 2026-09-04 — o robô não fala mais com o
Firestore, consome `moviki.com.br/api/vitrine`.

## Firestore

**Regras v24 publicadas**, sobre a v23 de 12/09. Cobre Modo Live, checkout Pix e
a coleção de autoridade `live_sessoes`, na raiz. O Console é a verdade; a cópia
no Project não prova o que está publicado.

## Vercel

`LIVE_SEGREDO` existe nos projetos `moviki` e `moviki-robo` — **só em
`Production`, não em `All Environments`**. Produção funciona. Um deploy de
**Preview não tem o segredo**, e sem ele a live não começa, por desenho (falha
fechada). Quem testar a live numa URL de preview vai ver "não consigo abrir a
live", sem erro visível.

## Alertas desta leitura

- **`parceiro.html` é o arquivo mais disputado do projeto.** Em 11/09 a entrega da
  aula P11 apagou a aba de material de apoio por ter sido montada sobre marca
  velha. Antes de subir qualquer versão dele, abrir o arquivo no GitHub e ler a
  marca **na hora** — ver [[ARQ - Incidente - aba de material apagada pela aula P11]]
- **O pacote de imagens otimizadas (favicon de 949 KB → 10 KB) não tem marca de
  versão** porque nenhum HTML mudou. Conferir pelo peso da página, não pela marca —
  ver [[ARQ - O favicon de 949 KB]]
- **`api/og.js` está no ar com conteúdo de 15/09 e marca de 04/09.** A prévia do
  link da live funciona; a marca não subiu junto. É a armadilha desta própria
  nota acontecendo — ver [[ARQ - Previa do link da live no WhatsApp 15092026]]
- **As catorze aulas do Modo Live estão com `id`.** O módulo tem trava de três
  aulas e está escondido pelo interruptor do beta — ver
  [[ARQ - Videoaulas do Modo Live concluidas 15092026]]
- **O briefing de 16/09 montado por outra sessão lista `moviki-app/live.html`
  como `2026-09-15-sessao5` e `index.html` como `2026-09-15-aulatrava`.** As duas
  marcas envelheceram: o módulo de aulas da live subiu por cima. Montar qualquer
  entrega desses dois arquivos sobre a base do briefing **apaga o módulo de
  aulas**, e o sintoma é silêncio
- **O domínio principal na Vercel é o `www`.** O apex redireciona, e
  redirecionamento entre origens quebra CORS — ver [[P30 - Decisao de dominio apex ou www]]

## Regra de ouro que sustenta esta nota

> **Marca de versão só vale se sobe junto com o conteúdo.** Arquivo que ganha
> funcionalidade e mantém a marca antiga é pior que arquivo sem marca: afirma um
> estado falso e o diagnóstico começa no lugar errado.
>
> **"Entregue" e "no ar" são estados diferentes, e só o repositório sabe qual é qual.**

## Ligações

[[A2 - Infraestrutura e Deploy]] · [[R - Regras de ouro]] ·
[[R - Regras de ouro novas de 11 a 14092026]] ·
[[ARQ - Modo Live no ar em beta fechado 12092026]] ·
[[ARQ - Live escondida durante o beta 14092026]] ·
[[ARQ - Previa do link da live no WhatsApp 15092026]] ·
[[ARQ - Modulo de aulas da live com trava 15092026]] ·
[[ARQ - Fase 2 da seguranca da live 15092026]]
