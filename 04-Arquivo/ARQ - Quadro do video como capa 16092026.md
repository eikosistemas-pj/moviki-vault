---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [videos, capa, instagram, canvas, painel, privacidade]
atualizado: 2026-09-16
---

# ARQ - Quadro do video como capa 16092026

Pedido do Paulo: *"no Instagram, quando você escolhe o vídeo, aparece a linha
do tempo e arrastando você escolhe a capa. Seria interessante ter isso."*

## O que NÃO dá, e por quê

**Não é possível arrastar a linha do tempo de um vídeo que já está publicado no
Instagram ou no TikTok.** Três paredes, cada uma bastando sozinha:

1. O endereço do arquivo de vídeo dessas redes é **assinado e temporário** —
   não existe endereço estável que a nossa página possa abrir.
2. O **oEmbed público do Instagram acabou**; o que restou exige token de app da
   Meta com revisão, e devolve no máximo uma miniatura — não o vídeo.
3. Mesmo que houvesse endereço, **canvas de outra origem não deixa ler o
   quadro** (o canvas fica "contaminado" e `toDataURL` é bloqueado).

O Instagram consegue porque, na hora de publicar, **o arquivo está no aparelho**
— é o vídeo local, não o publicado.

## O que foi feito, e entrega a mesma coisa

**"Pegar um quadro do vídeo"**, terceira opção na tela de capa: abre o vídeo que
está **no celular do lojista** — que é de onde ele postou —, ele arrasta a linha
do tempo e escolhe a cena. O quadro vira a capa.

**O vídeo nunca sobe.** Tudo acontece no aparelho: `URL.createObjectURL`,
`<video>` local, `canvas.drawImage` e JPEG. Sai dali só a imagem do quadro
escolhido, pelo mesmo `/api/upload-imagem` das fotos. O endereço temporário é
liberado (`revokeObjectURL`) ao fechar ou voltar — vídeo de celular é pesado, e
segurar isso na memória trava aparelho fraco.

Degradação: navegador que não sabe abrir aquele arquivo (`.mov` HEVC de iPhone
em alguns Android) recebe aviso na tela, com o botão desabilitado e o caminho
alternativo escrito — em vez de uma tela preta que a pessoa arrasta sem
entender.

## A regra que fica

> **Quando a rede de terceiro não deixa, o caminho é trazer a tarefa para o
> aparelho do lojista — não fingir que dá.** O arquivo que o Instagram não
> entrega está no celular dele desde o começo.

E a segunda:

> **Mídia pesada processada no navegador se resolve no navegador.** Nada de
> subir 40 MB de vídeo para o servidor recortar um quadro de 80 KB.

## Arquivos

| Repo | Arquivo | Ação | Marca nova | Montado sobre |
| --- | --- | --- | --- | --- |
| moviki-app | `index.html` | SUBSTITUI | `2026-09-16-quadro` | `2026-09-16-capavideo` |
| moviki-ai | `lib/catalogoPainel.js` | SUBSTITUI | `2026-09-16-7` | `2026-09-16-6` |

O `404.html` `2026-09-16-capavideo` da rodada anterior **não muda** — ele já
mostra qualquer capa, venha ela da galeria, de upload ou do quadro.

## Prova, com vídeo de verdade

Vídeo de 6 segundos gerado em três faixas de cor (vermelho 0–2s, verde 2–4s,
azul 4–6s), entregue ao painel em Chromium:

- a tela abriu e leu a duração (6 s);
- a linha do tempo arrastada até ~5 s;
- o quadro capturado saiu **azul** (RGB 1,14,253) — ou seja, **a imagem
  corresponde exatamente ao ponto escolhido**, que era o ponto da prova;
- resolução mantida (540x960, sem ampliar), imagem enviada, capa aplicada,
  folha fechada e aviso de salvar.

De quebra, a degradação foi exercitada sem querer: o Chromium de teste não tem
codec H.264, e o mesmo vídeo em `.mp4` caiu no aviso *"este vídeo não abre aqui
no navegador"* com o botão desabilitado — que é o comportamento desenhado para
o iPhone/Android teimoso.

## Ligações

[[ARQ - Capa do video escolhida pelo lojista 16092026]] · [[A1 - Produto e Paineis]] ·
[[R - Regras de ouro]]
