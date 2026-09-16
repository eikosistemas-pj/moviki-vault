---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, videoaulas, producao, entrega]
atualizado: 2026-09-15
---

# ARQ - Videoaulas do Modo Live concluidas 15092026

Fecha o [[P28 - Videoaulas do Modo Live]]. **Catorze de catorze no ar**, todas
com `id` preenchido em `moviki-app/liveaulas.js`.

O projeto previa treze. A catorze (`mod-live-cardapio`) nasceu no meio da
produção, quando o cardápio comprável virou uma porta de venda que funciona
**sem live** — e que precisava de aula própria.

## As catorze

| # | Chave | Título | Dur | id |
| --- | --- | --- | ---: | --- |
| 01 | `mod-live-abertura` | Live no Moviki: o que é e como funciona | 1:20 | `1TqgHffAyYU` |
| 02 | `mod-live-regras` | O que pode e o que não pode na live | 1:04 | `3WceM12RkWE` |
| 03 | `mod-live-primeira` | Sua primeira live: título, câmera e entrar ao vivo | 1:16 | `sngj1eUC7kU` |
| 04 | `mod-live-sacolinha` | Sacolinha e produto em destaque | 0:55 | `3Fsofzdj0u4` |
| 05 | `mod-live-chat` | Chat da live: responder e apagar | 0:33 | `V6WZqQ0s-bY` |
| 06 | `mod-live-agendar` | Agendar a próxima live e divulgar o link | 0:31 | `cWG2cWGMrII` |
| 07 | `mod-live-pix` | Como você recebe o dinheiro | 1:30 | `hhTBM163vK0` |
| 08 | `mod-live-pedidos` | Pedidos: conferir, confirmar e entregar | 1:00 | `qx4dFUC9ORs` |
| 09 | `mod-live-oferta` | Oferta relâmpago e estoque ao vivo | 0:55 | `pbWfLHoKGag` |
| 10 | `mod-live-cupom` | Cupom, brinde e "Estou aqui agora" | 0:50 | `BQPflIBLNG0` |
| 11 | `mod-live-fila` | Fila de pedidos | 0:21 | `hhooJvRXx2Q` |
| 12 | `mod-live-dados` | Dados ao vivo e o resumo da live | 0:31 | `07rQewrYNaI` |
| 13 | `mod-live-cortes` | Cortes para Reels e Status | 0:24 | `vzZOyzzfYHM` |
| 14 | `mod-live-cardapio` | Seu cardápio vendendo sozinho | 1:18 | `2_ty4YrgZ0I` |

Todas **não listadas** no YouTube até a abertura das portas.

## O que a produção exigiu que não estava previsto

**Um motor novo: `partes.py`.** As aulas 01 e 10 percorrem telas que não cabem
numa bancada só — painel, página pública, estúdio em Premium, estúdio em
Enterprise, tela de aceite. O motor antigo gravava uma bancada por vídeo. O novo
corta o roteiro no **meio da pausa entre blocos**, grava cada trecho na bancada
certa e costura, conferindo que nenhum quadro ficou de fora.

**Conferência de folga com sub-seletor.** `conferir_folga(..., dentro=...)`
mede se o alvo cabe na tela antes de gravar. Achou um painel de três cartões
faltando 70 px e uma página de estúdio que rolava 7 px — os dois teriam saído
com corte no quadro. `folego_rolagem` e o CSS `FOLEGO_CSS` resolvem acrescentando
respiro no fim do corpo.

**Leva mista, bloco a bloco.** A escolha entre a narração `r*` e a `b*` deixou de
ser por leva inteira e passou a ser por bloco: a aula 01 tinha só o `r2` regravado.

## Refações

- **Aula 09** saiu com imagem estática do personagem (`vendedor.y4m`) em vez do
  elenco. Regravada no motor comum, com o personagem `chapa`.
- **Aula 01 e aula 08** regravadas depois do conserto do relógio da bancada —
  ver [[ARQ - Incidente - camera e animacoes aceleradas na bancada]].

## Pendências que este arquivo deixa

- **As doze aulas restantes foram gravadas com a câmera acelerada.** Elas estão
  no ar e são legíveis; a decisão de regravar em lote continua aberta.
- **`WmpIQr36b2o` — a aula 08 antiga, com a fala errada — segue publicada** como
  não listada. Só pode ser apagada porque o painel já aponta para `qx4dFUC9ORs`.
- **Apagar `01-Projetos/P28 - Videoaulas do Modo Live.md` à mão**: projeto
  concluído vira registro de Arquivo, e o `.bat` de sincronização não apaga.

## Ligações

[[A13 - Modo Live]] · [[R - Live - Videoaulas do modulo]] ·
[[ARQ - Modulo de aulas da live com trava 15092026]] ·
[[ARQ - Incidente - camera e animacoes aceleradas na bancada]] ·
[[R - Regras de ouro de producao de video]] · [[R - Marcas de versao no ar]]
