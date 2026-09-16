---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, seguranca, firestore, regras, saque, cloudflare]
atualizado: 2026-09-16
---

# ARQ - Fase 2 da seguranca da live concluida 16092026

Fecha a **fase 2** de [[P35 - Auditoria de seguranca do Modo Live]]: lotes
**1B**, **1C** e **1D**, mais as **regras v25** e o bloco do dinheiro do
parceiro (**B11**, **B12**, **B13**). Tudo no ar em 16/09/2026.

## O que subiu

| Achado | Onde | O que passou a valer |
| --- | --- | --- |
| **B2** | `moviki-app/eikoadm01.html` | a lista de lives no ar do painel do dono vem de `live_adm_noar` -> `live_sessoes`. `lvAtivaDeVerdade()` foi **apagada**: ela lia `ativa` do documento do proprio lojista |
| **B4** | `moviki/api/live.js` | a entrada do Cloudflare vive **uma live**. Toda live nova comeca apagando a anterior |
| **B7** | regras v25 | `livepresenca` separa `create` (exige `liveNoAr(uid)`) de `update`; presenca expira em 10 min |
| **B10** | `moviki-app/eikoadm01.html` | fila de denuncias com teto de 300, agrupada por lojista, com selo de "possivel enxurrada" |
| **B11** | `moviki-robo/api/pagar-saque.js` | `selecionarComissoes` devolve `corteOk:false` quando a data de corte nao converte. **Falha fechada** — antes o saque passava com corte nulo |
| **B12** | idem | saque avulso com id deterministico `av_<parceiroUid>_<diaSaque>`, criado dentro de transacao. Duplo clique deixa de gerar dois saques |
| **B13** | idem | `quitarComissoes()` em lotes de 400. O saque **fecha antes** da baixa, com `quitacaoPendente` e retomada |
| **denuncias** | regras v25 | `create` exige `liveNoAr(lojistaUid)` — nao da mais para denunciar quem nao esta transmitindo |
| **saques** | regras v25 | `pedidoEm == request.time` — data do servidor, nao do cliente |

## A critica ao B4 como estava escrito

O briefing pedia `requireSignedURLs` mais token por espectador. **Isso nao fecha
o que promete:** o endpoint que emite o token seria publico, e o atacante
pediria N tokens. Foi entregue a metade que vale — a entrada vive uma live — e
registrado que **o que contem prejuizo de verdade e teto de gasto**, que e
configuracao, nao criptografia. Virou
[[ARQ - Teto de gasto de video no ar 16092026]].

## Regra de ouro reforcada

> **Regra do Firestore nao tem "deny".** Varios `match` que casam com o mesmo
> caminho **somam** permissoes. Colecao de autoridade vai para a **raiz**, onde
> o curinga `match /{documento=**}` de `negocios/{uid}` nao alcanca. E a razao
> de `live_sessoes/{uid}` existir onde existe.

## Fica em aberto

- Bloco C (C1-C4, C7-C9, C12-C15) — nao trava o lancamento.
- TTL no Google Cloud para `livechat`, `livepresenca`, `checkout_freio` e
  `pedidos`. Enquanto nao existir, "guardado por ate 30 dias" **nao e verdade**
  e o custo do B7 e permanente.

## Ligacoes

[[P35 - Auditoria de seguranca do Modo Live]] · [[P24 - Modo Live - lancamento]] ·
[[A13 - Modo Live]] · [[A3 - Dados e Regras]] ·
[[ARQ - Teto de gasto de video no ar 16092026]] ·
[[R - Marcas de versao no ar]] · [[R - Regras de ouro]]
