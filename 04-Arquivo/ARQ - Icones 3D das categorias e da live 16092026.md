---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [entrega, icones, material-de-apoio, live, design]
atualizado: 2026-09-16
---

# ARQ - Icones 3D das categorias e da live 16092026

Treze icones 3D novos, no mesmo estilo dos `icones-premium` do site: doze para
a faixa de categoria da aba "Material de apoio" do painel do parceiro, e um
para o cartao "Venda por video" do site.

## Por que

**A faixa de categoria era emoji.** Emoji nao e imagem: e um caractere que
cada sistema desenha do seu jeito. O mesmo painel aparecia diferente em cada
celular, e em Windows antigo alguns nem apareciam. A faixa e o primeiro nivel
de navegacao de 81 pecas — ela precisa ser igual para todo mundo.

**O icone da live nao existia.** `icones-premium/live.png` era chamado em tres
lugares (`index.html` x2 e `comerciantes.html` x1) e o arquivo nunca tinha sido
feito: os tres caiam no emoji pelo `onerror`. O cartao "Venda por video" e o
bloco central do novo posicionamento e era o unico da fileira sem desenho.

## O que foi feito

- 12 PNG 256x256 com alfa em `moviki-app/icones/cat-<id>.png`, um por
  categoria: `geral`, `alimentacao`, `moda`, `beleza`, `naturais`, `pet`,
  `artesanato`, `eletronicos`, `papelaria`, `automotivo`, `servicos`, `feira`
- 1 PNG 256x256 com alfa em `moviki/icones-premium/live.png`
- `material/catalogo.json`: campo `ico` em cada categoria. Versao
  `2026-09-16-caticones`
- `parceiro.html`: `catsUsadas()` passou a carregar `ico`, e a faixa desenha
  `<img class="matCatIco">` com o emoji escondido logo atras.
  Marca `2026-09-16-caticones`
- `comerciantes.html`: o comentario que dizia que o icone da live nao existia
  virou mentira no momento em que o arquivo subiu. Corrigido na mesma rodada.
  Marca `2026-09-16-iconelive`
- `moviki-ai/lib/catalogoPainel.js`: `MARCAS_CONFERIDAS.parceiro` atualizado.
  Versao `2026-09-16-2`

## A decisao que fica

**O emoji nao foi removido — foi rebaixado a reserva.** O `<span>` do emoji
continua no botao, escondido, e o `onerror` do `<img>` troca um pelo outro.
Arquivo que falta degrada a faixa, nunca quebra. E o mesmo desenho do
`mvIco()` do site, agora tambem no painel.

## Achado de brinde

O Vik estava em **modo cauteloso pela segunda vez em dois dias** e ninguem
tinha visto: `MARCAS_CONFERIDAS.parceiro` apontava `2026-09-15-aulatrava`
enquanto o painel no ar ja estava em `2026-09-16-wafoto`. O painel do parceiro
subiu tres vezes em 16/09 (`matfaixa`, `wafoto`, `caticones`) e a tabela ficou
parada. Ver [[R - Marcas de versao no ar]].

## Pendencia que sobra

`cat-feira.png` subiu mas **nao aparece na faixa**: "Feira, rua e delivery"
tem zero pecas no acervo, e categoria sem peca nao entra. E o caso de uso
central do produto e e a unica categoria sem material. Quando a primeira peca
entrar, a categoria aparece sozinha, ja com o icone.

## Conferencia

Chromium, 1280px e 390px: 11 botoes na faixa, 11 imagens carregadas, zero
emoji visivel por cima, zero erro de JavaScript. As tres chamadas de
`live.png` no site carregando a 256px. `catalogo.json` com as 81 pecas
intactas, incluindo as coordenadas do QR do panfleto.

## Ligacoes

[[R - Marcas de versao no ar]] · [[R - Design system e icones]] ·
[[A1 - Produto e Paineis]] · [[R - Regras de ouro]]
