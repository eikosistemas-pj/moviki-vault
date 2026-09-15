---
type: recurso
status: ativo
area: A1 - Produto e Paineis
tags: [versao, upload, apendice, conferido]
atualizado: 2026-09-15
---

# Marcas de versao no ar — 15/09/2026

⚠️ **Apendice de [[R - Marcas de versao no ar]].** Separado porque o arquivo
principal nunca chegou integral aqui — substituir sem ele apagaria o historico.
**Fundir na proxima vez que o arquivo principal for entregue.**

Tudo abaixo foi **conferido byte a byte contra o GitHub** em 15/09, 20h40 — nao
e o que foi entregue, e o que esta la.

---

## moviki-robo

| Arquivo | Marca | O que trouxe |
| --- | --- | --- |
| `lib/livesessao.js` | **`2026-09-15-b5b`** | sessao da live no servidor, cota, freio duravel, saneamento dos bytes |
| `lib/checkout.js` | `2026-09-15-whtoken` | token de webhook proprio por subconta, `chaveDoPedido` por modo |
| `api/webhook.js` | `2026-09-15-escopo` | escopo por token, valor reconferido no Asaas, auto-indicacao barrada |
| `api/pontos.js` | `2026-09-15-livesessao` | liga a etapa `livesessao` |
| `api/ativar-trial.js` | (sem marca propria) | e-mail verificado, `trials_usados`, normalizacao de Gmail |

## moviki (site publico)

| Arquivo | Marca |
| --- | --- |
| `api/live.js` | **`2026-09-15-b5a`** |
| `live.html` | `2026-09-15-sessao1` |

## moviki-app (paineis)

| Arquivo | Marca |
| --- | --- |
| `live.html` (estudio) | **`2026-09-15-sessao5`** |
| `index.html` (lojista) | **`2026-09-15-aulatrava`** |
| `parceiro.html` | **`2026-09-15-aulatrava`** |
| `eikoadm01.html` | `2026-09-15-conferir` |

## Firestore

**Regras v24 publicadas no Console** — `live_sessoes/{uid}` (leitura publica,
escrita negada a todos), `live_cota/{uid}` (leitura so admin), e `liveNoAr(uid)`
lendo `live_sessoes` com `exists()` antes do `get()`.

## Vercel — envs (conferido nos prints de 15/09, 20h40)

`LIVE_SEGREDO` existe **nos dois projetos**, `moviki` e `moviki-robo`, com a
mesma string, adicionada no mesmo dia.

⚠️ **Nos dois ela esta so em `Production`**, nao em `All Environments`. Producao
funciona. **Um deploy de Preview nao tem o segredo** — e, sem ele, a live nao
comeca (falha fechada, de proposito). Se um dia um Preview for usado para testar
a live, o sintoma vai ser "nao consigo abrir a live" sem erro visivel.

## Limpezas que ficaram abertas

- [ ] A conta de teste (Karina) segue **Enterprise por edicao manual no Console**.
      Reverter ou marcar `origem: teste` quando os testes acabarem.
- [ ] O painel do dono conta **pedido de teste como venda** ("Vendido pelo Pix
      R$ 25,41", "Pedidos pagos 1", "Conversao 50%"). Marcar como teste ou apagar
      antes de olhar qualquer relatorio de faturamento.

## Ligacoes

[[R - Marcas de versao no ar]] · [[P35 - Auditoria de seguranca do Modo Live]] ·
[[ARQ - Sessao da live no servidor]] · [[ARQ - Bytes de controle no livesessao]]
