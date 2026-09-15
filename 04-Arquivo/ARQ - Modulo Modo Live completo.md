---
type: arquivo
status: concluido
area: A3 - Conteudo e Videoaulas
tags: [moviki, modo-live, videoaulas, youtube]
atualizado: 2026-09-15
---

# ARQ - Modulo Modo Live completo

**As catorze aulas do Modo Live estao no ar**, nao listadas, em 15/09/2026.
Producao inteira na bancada Playwright, com o painel e as telas de verdade
contra um Firebase de mentira.

## O catalogo, com os ids

| # | Chave | Titulo | Dur | YouTube |
| --- | --- | --- | --- | --- |
| 01 | `mod-live-abertura` | Live no Moviki: o que e e como funciona | 1:20 | `1TqgHffAyYU` |
| 02 | `mod-live-regras` | O que pode e o que nao pode na live | 1:04 | `3WceM12RkWE` |
| 03 | `mod-live-primeira` | Sua primeira live: titulo, camera e entrar ao vivo | 1:16 | `sngj1eUC7kU` |
| 04 | `mod-live-sacolinha` | Sacolinha e produto em destaque | 0:55 | `3Fsofzdj0u4` |
| 05 | `mod-live-chat` | Chat da live: responder e apagar | 0:33 | `V6WZqQ0s-bY` |
| 06 | `mod-live-agendar` | Agendar a proxima live e divulgar o link | 0:31 | `cWG2cWGMrII` |
| 07 | `mod-live-pix` | Como voce recebe o dinheiro | 1:30 | `hhTBM163vK0` |
| 08 | `mod-live-pedidos` | Pedidos: conferir, confirmar e entregar | 1:00 | `qx4dFUC9ORs` |
| 09 | `mod-live-oferta` | Oferta relampago e estoque ao vivo | 0:55 | `pbWfLHoKGag` |
| 10 | `mod-live-cupom` | Cupom, brinde e "Estou aqui agora" | 0:50 | `BQPflIBLNG0` |
| 11 | `mod-live-fila` | Fila de pedidos | 0:21 | `hhooJvRXx2Q` |
| 12 | `mod-live-dados` | Dados ao vivo e o resumo da live | 0:31 | `07rQewrYNaI` |
| 13 | `mod-live-cortes` | Cortes para Reels e Status | 0:24 | `vzZOyzzfYHM` |
| 14 | `mod-live-cardapio` | Seu cardapio vendendo sozinho | 1:18 | `2_ty4YrgZ0I` |

Total: cerca de **12 minutos** de video.

Playlist: `youtube.com/playlist?list=PLS95RqpuM64M` ("Vide Aulas - Live",
canal Moviki App).

## Duas que foram regravadas, e por que

**Aula 09.** A primeira leva era o VIDEO PILOTO, feito antes do elenco existir:
usava `vendedor.y4m`, uma FOTO com deriva de zoom. Na tela, o personagem ficava
parado, destoando das outras treze. Portada para o motor comum, com a camera do
chapa e a vitrine vinda do `dados.py`.

**Aula 08.** O primeiro id (`WmpIQr36b2o`) subiu ANTES do aceite da regravacao
do bloco 6: a fala dizia que o prazo de pagamento e escolhido pelo lojista, e
ele e **fixo em 30 minutos**. O video certo e o `qx4dFUC9ORs`. O antigo continua
publicado e nao listado — **apagar ou deixar e decisao do Paulo**, mas ele nao
pode entrar em catalogo nenhum.

> **Regra que nasce daqui:** id de YouTube enviado ANTES de uma regravacao
> aprovada aponta para o video velho. Quando uma regravacao e aceita, o id da
> aula volta para o estado "sem id" ate a nova subida.

## O que ainda falta

1. **Montar o modulo no catalogo do painel** com as catorze chaves. Decisao
   pendente: onze das catorze pertencem a abas do ESTUDIO (`live.html`), nao do
   painel, e o `sel` do `MOVIKI_TUTORIAIS` aponta para `#tab-*` do painel. O
   documento de 13/09 previa um `liveaulas.js` separado, que nunca foi criado.
2. **Decidir sobre a aceleracao das doze anteriores** (a 01 e a 08 ja sairam
   consertadas) — ver [[ARQ - Bancada presa ao relogio do video]].

## Ligacoes

[[ARQ - Motor de partes da aula 01]] · [[ARQ - Bancada presa ao relogio do video]] ·
[[A3 - Conteudo e Videoaulas]] · [[R - Marcas de versao no ar]]
