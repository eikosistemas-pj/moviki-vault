---
type: incidente
status: resolvido
area: Painel do lojista
tags: [video, capa, webview, instagram, diagnostico]
atualizado: 2026-09-16
---

# Tela escura na escolha da cena — 16/09/2026

## O relato
"Mesmo tendo o vídeo no celular, quando arrasto pra escolher a parte do vídeo
que será a capa, a tela continua escura."

## A causa real
O print entregou a resposta: no topo da tela estava escrito
**"app.moviki.com.br / Instagram"**. O painel não estava no Chrome — estava no
**navegador embutido do Instagram**, aquele que abre quando você clica num link
de dentro do aplicativo.

Esse navegador não decodifica vídeo local. O elemento de vídeo carrega, a
duração até aparece, mas nenhum quadro é desenhado. Tela preta, para sempre.
Não é o formato do arquivo, não é o vídeo do lojista, não é o painel.

E o caminho até o erro é o caminho natural: o lojista posta o Reels, clica no
próprio link do perfil, cai no painel por dentro do Instagram e vai justamente
mexer na capa do vídeo que acabou de postar.

## O que foi feito
- **Detecção do navegador embutido** pela assinatura do aparelho (Instagram,
  Facebook, Messenger, TikTok, Line, OK). Vale para os três aplicativos, não só
  o Instagram.
- **Aviso antes**, em laranja, nas duas telas — na folha de capa e na tela de
  escolher a cena.
- **Botão nasce desligado.** Botão aceso sobre tela preta é o que faz a pessoa
  achar que o sistema está quebrado. Ele só acende quando o navegador provou
  que consegue desenhar o vídeo (largura real e duração real).
- **Liberação por três eventos** em vez de um. Em vários navegadores de celular
  a largura só aparece depois que o vídeo toca um instante.
- **Empurrão mudo**: se em 0,4 s nada veio, o painel toca o vídeo sem som por
  um quarto de segundo para forçar a decodificação do primeiro quadro.
- **Desistência em 4,5 s** com mensagem que depende do caso: no navegador
  embutido, manda abrir app.moviki.com.br no Chrome; fora dele, aponta o
  formato do arquivo e oferece a galeria.

## Lição
Quando alguém disser que a tela fica escura, a primeira pergunta não é sobre o
vídeo — é **por onde ele abriu o painel**. O Vik já está instruído assim.

## Testes
Chromium, quatro cenários: vídeo bom / vídeo quebrado, cada um com e sem
assinatura de Instagram. Botão, mensagem e aviso corretos nos quatro.

[[ARQ - Quadro do video como capa 16092026]]
[[ARQ - Capa do video escolhida pelo lojista 16092026]]
[[R - Regras de ouro]]
