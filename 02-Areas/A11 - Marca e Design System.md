---
type: area
status: ativo
tags: [design, marca]
atualizado: 2026-08-28
---

# A11 — Marca e Design System

## Design system: `movikiui.css`
**SEM hífen.** O nome com hífen já fez a landing subir crua. Tokens `--mv-*`.

**Toda página que usa a folha repete um bloco `:root{}` com todos os tokens como rede de segurança** — se a folha não carregar, a página degrada legível e na marca. Presente nos dois repositórios.

## Ícones 3D — estilo canônico
3D glossy plastic, formas arredondadas, luz de estúdio, brilho especular, sem contorno, objeto único centralizado, paleta ciano/azul com acentos amarelo e verde.

Produção: modelo **nano-banana-pro** no Kairogen, 6 créditos/imagem, 1:1, **sempre com `reference_image_urls`**.

**Emoji NÃO é ícone no Moviki.**

| Pacote | Onde | Quantidade |
| --- | --- | --- |
| `moviki-app/icones/` | painéis | 48 |
| `moviki/icones-premium/` | site | 39 |
| Cobertura total nos HTML | ambos | 128 |

Falta: **`mensagens.png`** — hoje o balão da caixa de mensagens é SVG inline.

## Regras
- `logo.png` já contém a palavra "moviki" — **nunca** pôr texto ao lado.
- A **ARTE manda no visual; os SPECS mandam na copy**, na estrutura e nas regras.
- Página de venda usa **comparação, não adjetivo**.

## Recursos
[[R - Design system e icones]] · [[R - Custos e cotas]]
