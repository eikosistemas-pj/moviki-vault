---
type: incidente
status: concluido
area: A13 - Modo Live
tags: [video, estudio, armadilha, playwright]
atualizado: 2026-09-15
---

# ARQ - Incidente - camera e animacoes aceleradas na bancada

O maior achado da rodada de 15/09/2026, e o que valia para as catorze aulas de
uma vez.

## O sintoma

Paulo, sobre a aula 01: *"a tarja vermelha ficou piscando bem rápido... o pino
também balançando bem rápido, como se aquela imagem estivesse correndo... quando
passou para o próximo take que mostrou a moça do bolo na tela do celular, ela
estava totalmente acelerada"*.

Medido depois: **6x a 18x** mais rápido que o real.

## A causa

A bancada grava quadro a quadro e **falsifica o relógio** (`Date.now`) para que
cada quadro caia num instante escolhido. Isso governa tudo que é escrito em
JavaScript — e **nada mais**.

> **O relógio falso não governa o `<video>` nem o compositor de animações CSS.**
> Esses dois correm no tempo real da máquina. Numa bancada que leva meio segundo
> de máquina para produzir um quadro de 1/30 de segundo de vídeo, a diferença
> entre os dois relógios é exatamente o fator de aceleração.

## O conserto

Três peças, nesta ordem:

1. **`window.__camIr(t)`** — a câmera deixou de ser um fluxo correndo sozinho.
   `getUserMedia` foi substituído pelo `captureStream()` de um `<video>`
   **pausado**, e cada quadro manda o vídeo para o segundo exato.
2. **`window.__animarEm(ms)`** — as animações passaram a ser posicionadas no
   mesmo carimbo de tempo do quadro, em vez de correrem livres.
3. **Esperar dois `requestAnimationFrame` depois do `seeked`.** O evento
   `seeked` sozinho não basta: sem os dois quadros de folga, **um seek em cada
   dois saía com a imagem anterior**.

## A armadilha que quase passou batido

**Sem cabeçalho `Range`, um `<video>` servido por rota própria não é seekable** —
`video.seekable.end(0)` devolve `0` e todo seek é ignorado em silêncio. As rotas
`/__camera.webm` do `estudio.py` e do `publica.py` ganharam resposta **206**.

## O efeito colateral bom, e o mau

As câmeras `.y4m` tinham sido geradas a **3 fps**. Isso *compensava por acidente*
a bancada acelerada — e por isso o defeito demorou a aparecer. Com o relógio
consertado, elas ficaram lentas demais. Foram regeradas a **12 fps** a partir do
bruto (`hero/cams/*.mp4`).

## Regras de ouro que nascem daqui

> **Relógio falsificado governa o JavaScript, não a mídia.** Vídeo, áudio e
> animação CSS correm no tempo real da máquina, por mais lento que o quadro seja.
>
> **`seeked` não quer dizer "pintado".** Depois de todo seek, esperar dois
> `requestAnimationFrame` antes de capturar.
>
> **Vídeo sem `Range` não é seekable.** Rota própria que serve mídia responde
> 206, ou o `<video>` finge obedecer e não obedece.
>
> **Ativo gerado com fps errado que "fica bom" esconde defeito de motor.**
> Quando o motor for consertado, o ativo quebra — e o culpado parece ser o
> conserto.

## Ligações

[[R - Regras de ouro de producao de video]] ·
[[R - Regras de ouro novas de 15 e 16092026]] ·
[[ARQ - Videoaulas do Modo Live concluidas 15092026]] ·
[[R - Live - Videoaulas do modulo]] · [[A13 - Modo Live]]
