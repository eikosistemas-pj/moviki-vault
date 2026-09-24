---
type: arquivo
status: concluido
area: A11 - Marca e Design System
tags: [motion, lazy, performance, icones, interface, upload]
atualizado: 2026-09-23
---

# ARQ - Motion e lazy loading 23092026

Entrega de 23/09/2026. **Entregue, conferir se subiu.** Regras e API em
[[R - Motion principles]].

## O que entrou

| Repo | Arquivo | Marca / conferência |
| --- | --- | --- |
| moviki e moviki-app | `mvmotion.js` (**NOVO**) | `2026-09-23-motion1` |
| moviki e moviki-app | `mvmetrica.js` | sem marca — bloco `MOTION (23/09/2026)` no fim |
| moviki e moviki-app | `movikiui.css` | sem marca — seção `16. MOTION` |
| moviki-app | `icones/` (18) · `quiz/icones/` (38) | `icones/financeiro.png` = 13 KB |
| moviki | `icones-premium/` (8) | `icones-premium/presente.png` = 10 KB |

**Nenhuma marca de HTML mudou** — o Vik não precisa de atualização.

## Ganho de peso

Ícones recomprimidos para PNG de paleta, **mesmo nome e mesma dimensão**:
`moviki-app` **2.519 KB → 646 KB** · `moviki` 387 → 159 KB
(ex.: `financeiro.png` 73 → 13 KB).

O resto do site já estava certo: imagens `lazy`, herói `fetchpriority="high"`,
YouTube em fachada, vídeo `preload="none"`.

## Conferido

Playwright, 390×780, 14 páginas: motor no modo certo, zero erro novo, zero bloco
preso depois de rolar, tela final idêntica à sem motor, `reduce` sem nada
escondido.

## O que ficou de fora — e por quê

Regra **"um chat por arquivo"**: o `moviki-ai` já esperava o lojista em
`rodada3` com o GitHub em `rodada2`, ou seja, havia entrega de outro chat em
trânsito. Ficou para o chat dono desses arquivos:

- [ ] `moviki-app/parceiro.html` — linha do `mvmotion.js` depois do `movikiui.css`; `lazy` nas imagens do Material de apoio e nos ícones dos menus
- [ ] `moviki-app/eikoadm01.html` — linha do `mvmotion.js`; Leaflet com `defer`; ícones com `lazy`
- [ ] `moviki-app/index.html` — `lazy` nos 11 ícones da gaveta e nos 2 do quiz
- [ ] `moviki/404.html` — Leaflet com `defer`
- [ ] Capas de vídeo com `srcset` (herói da home e da `comerciantes.html`): a capa de 1280 px (195 KB) é servida a tela de 390 px e é o LCP

**Marca de versão:** em `index.html` e `parceiro.html`, se esses itens entrarem
sozinhos, a marca **não troca** (o Vik compara). Handoff completo:
`claude/LEIA-PRIMEIRO - Motion nos paineis 23092026.md` no Project.

## Como conferir depois de subir

- Console do painel: `mvMotion.modo` responde `painel`.
- Abrir e fechar um modal: o fundo acende e a caixa sobe. Com "reduzir movimento" ligado no aparelho, nada se mexe.

## Ligações

[[R - Motion principles]] · [[A11 - Marca e Design System]] ·
[[R - Marcas de versao no ar em 19 a 23092026]]

*Reconstruída em 23/09/2026 a partir do MAPA-MESTRE de 23/09.*
