---
type: recurso
status: ativo
area: A2 - Infraestrutura e Deploy
tags: [versao, upload, apendice, marcas-de-versao]
atualizado: 2026-09-23
---

# R - Marcas de versao no ar em 19 a 23092026

⚠️ **Apêndice de [[R - Marcas de versao no ar]]** (conferido em 16/09). Separado
porque o arquivo principal nunca chegou integral aqui. **Fundir junto com**
[[R - Marcas de versao no ar em 15092026]].

⚠️ **Isto é o que foi ENTREGUE, não o que foi conferido no ar.** Conferir no
GitHub ou com `F12` > Console > `MOVIKI_VERSAO`.

## 23/09 — Motion e lazy loading

| Repo | Arquivo | Marca |
| --- | --- | --- |
| moviki e moviki-app | `mvmotion.js` (**NOVO**) | `2026-09-23-motion1` (`mvMotion.versao`) |
| moviki e moviki-app | `mvmetrica.js` | sem marca — bloco `MOTION (23/09/2026)` no fim |
| moviki e moviki-app | `movikiui.css` | sem marca — seção `16. MOTION` |
| moviki-app | `icones/` (18) · `quiz/icones/` (38) | `icones/financeiro.png` = 13 KB |
| moviki | `icones-premium/` (8) | `icones-premium/presente.png` = 10 KB |

## 22 e 23/09 — Criadores, Vik e painéis

| Repo | Arquivo | Marca |
| --- | --- | --- |
| moviki-app | `parceiro.html` | `2026-09-23-rodada2` (Área do criador, card e porta `/criador` preservados) |
| moviki-app | `eikoadm01.html` | `2026-09-23-vikalarme` (sobre a `rodada2`) |
| moviki-app | `vercel.json` | rewrite `/criador` → `parceiro.html` (sem marca) |
| moviki-app | `material/catalogo.json` | `2026-09-23-convitecriador` |
| moviki | `api/criadores.js` | `2026-09-22-criadores2` |
| moviki-ai | `lib/catalogoPainel.js` · `lib/promptPainel.js` · `lib/contextoUsuario.js` · `api/chat.js` | `CATALOGO_VERSAO 2026-09-23-3` · `MARCAS_CONFERIDAS` lojista e parceiro `2026-09-23-rodada2` |
| moviki-assistente-social | `src/config.py` | `2026-09-22-criador` (sucede `formatos` e `feedpadrao`) |
| Firebase | regras do Firestore e do Storage | **v27** publicada (`criador_pecas`, `criadores/{uid}/`) |

⚠️ O `moviki-ai` esperava o lojista em `2026-09-23-rodada3` enquanto o GitHub
estava em `rodada2` — havia entrega de outro chat em trânsito. Conferir antes de
subir qualquer `index.html`.

## 19/09 — Cota de live (P41)

| Repo | Arquivo | Marca antes | Marca entregue |
| --- | --- | --- | --- |
| moviki-robo | `lib/livesessao.js` | `2026-09-16-vitrinelive` | `2026-09-19-cotalive` |
| moviki | `api/live.js` | `2026-09-16-tetoplano` | `2026-09-19-cotalive` |
| moviki | `live.html` | `2026-09-16-paguei` | `2026-09-19-lotada` |
| moviki | `premium.html` · `enterprise.html` · `termos.html` | `2026-09-16-preco1` | `2026-09-19-cotalive` |
| moviki-app | `live.html` | `2026-09-16-chatfolha` | `2026-09-19-cotalive` |
| moviki-app | `eikoadm01.html` | `2026-09-16-origempago` | `2026-09-19-cotalive` |
| moviki-app | `index.html` | `2026-09-16-cadastro1` | `2026-09-19-cotalive` |

## 17/09 — Regras

| Onde | O que |
| --- | --- |
| Firebase | regras **v26** (curinga de `negocios/{uid}` removido) |
| moviki-app | `firebase/` com as regras e os testes do emulador |
| moviki-ai | teto `ATENDIMENTO_LIMITE_DIA` + `lib/tetoDia.test.js` |

## Ligações

[[R - Marcas de versao no ar]] · [[P41 - Cota de live por lojista]] ·
[[ARQ - Motion e lazy loading 23092026]] · [[ARQ - Area do criador no painel do parceiro]]

*Montada em 23/09/2026 a partir da seção 7 do MAPA-MESTRE de 23/09.*
