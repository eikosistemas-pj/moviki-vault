---
type: arquivo
status: no ar
area: A13 - Modo Live
tags: [live, estudio, interface, celular]
atualizado: 2026-09-16
---

# ARQ - Estudio imersivo da live 16092026

## Por que

No celular, ao vivo, a câmera ocupava **44vh** para o chat e as nove abas
caberem embaixo. O lojista ficava com menos da metade da tela para **mostrar o
produto**, que é a única coisa que a live precisa fazer bem. Referência trazida
pelo Paulo: a tela de LIVE do TikTok.

## Como ficou

- **Vídeo em tela cheia** (100dvh), sem moldura.
- **Dock lateral direita**, balões translúcidos com ícone e legenda: Produtos,
  Oferta, Cupom, Fila (com contador), Chat, Avisar, Mais.
- **Chat sobre o vídeo**, canto inferior esquerdo, sete últimas mensagens
  subindo, topo esmaecido. "Quero" em âmbar, compra em verde, dono em azul.
- **Encerrar virou botão redondo vermelho** no topo, só o quadrado de parar.
- **Toque no vídeo abaixa tudo** e deixa só o risquinho no rodapé; tocar ou
  arrastar o risquinho para cima traz de volta.
- **Folha que sobe** em dois terços da tela para cada ferramenta; a barra das
  nove abas virou o índice no topo dela, que o botão "Mais" abre.

## A regra que tornou isso seguro

Vale **só em tela pequena e só no ar** (`body.imersivo`). Antes de transmitir o
lojista precisa do título e do botão; no desktop as duas colunas aproveitam bem
o espaço.

E **nenhum handler foi tocado**: os painéis existentes foram envolvidos num
contêiner que, fora do imersivo, usa `display:contents` — some do layout e os
painéis ficam exatamente onde sempre estiveram. Os botões novos (parar, avisar)
**acionam os botões originais**, que continuam no DOM com toda a lógica.

## O que sobra

Com a folha aberta, o chat flutuante fica atrás dela. Aceito por ora: a folha
ocupa dois terços e empilhar chat por cima devolveria a poluição que se estava
tirando.

## Ligacoes

[[A13 - Modo Live]] · [[R - Marcas de versao no ar]] · [[R - Regras de ouro]]
