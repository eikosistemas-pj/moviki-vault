---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [lojista, cardapio, foto, editor, entrega]
atualizado: 2026-09-11
---

# ARQ — Foto do cardápio e editor de ajuste

Editor **`mvAjustarFoto`**: o lojista enquadra a foto **antes** de enviar e vê o
resultado exato que vai para a página pública.

## O editor

| Controle | O que faz |
| --- | --- |
| **Foto inteira** | Cabe a imagem toda no quadro, sem cortar |
| **Preencher** | Preenche o quadro inteiro, cortando as sobras |
| **Girar** | Corrige foto deitada / de lado |
| **Zoom** | Aproxima e reposiciona o recorte |

## Formatos de saída

| Peça | Saída |
| --- | --- |
| Foto de produto | **1080x1080** (quadrado) |
| Capa de categoria | **1200x900** (**4:3**) |

## Entrega

| Repo | Arquivo | Marca |
| --- | --- | --- |
| `moviki-app` | `index.html` | `2026-09-11-fotoajuste` |
| `moviki` | `404.html` | `2026-09-11-fotoajuste` |

**Estado: ENTREGUE.** As fontes consultadas **não confirmam** que os dois
arquivos subiram e estão no ar — a conferência fica como pendência aberta
abaixo.

## Por que enquadrar antes do envio

A página pública preenche a moldura (`object-fit: cover`). Foto enviada sem
enquadramento chega cortada em lugar errado ou com barra ao lado. Enquadrando no
painel, **o que o lojista confirma é, pixel por pixel, o que vai ao ar** — e
some a classe de reclamação "a foto chegou cortada".

## Em aberto

- [ ] Conferir, clonando os repositórios, se `moviki-app/index.html` e
      `moviki/404.html` estão em `2026-09-11-fotoajuste` no ar.
- [ ] Atualizar `R - Marcas de versao no ar` com o resultado da conferência.

## Ligações

[[A1 - Produto e Paineis]] · [[A11 - Marca e Design System]] ·
[[A2 - Infraestrutura e Deploy]] · [[R - Marcas de versao no ar]] ·
[[R - Checklist de deploy]]
