---
type: recurso
status: referencia
area: A11 — Marca e Design System
tags: [design]
atualizado: 2026-08-28
---

# R — Design system e ícones

## `movikiui.css`
**SEM hífen** — o nome com hífen já fez a landing subir crua. Tokens `--mv-*`.
**Toda página repete um bloco `:root{}` com todos os tokens** como rede de segurança.

## Variável de respiro
`--gut` na página pública: 14 → 22 → 36 → 56 → 80px.

## Ícones 3D — prompt canônico
> 3D glossy plastic, formas arredondadas, luz de estúdio, brilho especular, sem contorno, objeto único centralizado, paleta ciano/azul com acentos amarelo e verde.

Kairogen · modelo **nano-banana-pro** · **6 créditos/imagem** · 1:1 · **sempre com `reference_image_urls`**.

## Cobertura
128 ícones nos HTML dos dois repos · 48 em `moviki-app/icones/` · 39 em `moviki/icones-premium/`.
**Falta `mensagens.png`** nos dois pacotes.

## Editor de logo do pino (24/08)
3 estados: vazio (drag-and-drop) → editor (canvas quadrado, máscara circular, arraste, pinça, zoom 1x–4x, fundo claro/escuro) → salvo (moldura 250px, selo "assim no mapa"). Saída **384px JPEG q0.88**. Prefixo `.lc*`.

Servidor: `upload-imagem.js` no modo `tipo:'logo'` escreve `negocios/{uid}.markerLogo` via Admin SDK. Sempre `.jpg`; teto `MAX_B64 = 2.800.000`. Grava em `logos/{uid}/` e `produtos/{uid}/` com `public:true`.

## Regras
- `logo.png` já contém a palavra "moviki" — **nunca** texto ao lado.
- **Emoji não é ícone.**
- **Onde a arte pede um dado que não existe, troca-se o rótulo — não se inventa o dado.**
