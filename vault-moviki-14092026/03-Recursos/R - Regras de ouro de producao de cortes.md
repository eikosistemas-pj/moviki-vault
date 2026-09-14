---
type: recurso
status: referencia
area: A7 - Aquisicao e Midia Paga
tags: [cortes, midia-paga, video, legenda, conformidade]
atualizado: 2026-09-13
---

# R — Regras de ouro de produção de cortes

Tiradas da montagem dos cortes do filme hero em 13/09/2026 — ver
[[ARQ - Cortes do filme hero vertical e pago 13092026]]. Complementam
[[R - Regras de ouro de producao de video]].

## O corte se monta das fontes, não do master

Recortar o master 16:9 para 9:16 fecha o quadro, come o produto na lateral e
degrada duas vezes. Remontar das fontes custa zero crédito novo e entrega quadro
limpo.

## Formatos de entrega

| Uso | Formato | Duração |
| --- | --- | ---: |
| Orgânico / Short | 1080x1920 30 fps | 45–60 s |
| Pago 9:16 | 1080x1920 30 fps | 15–30 s |
| Pago 4:5 | 1080x1350 30 fps | 15–30 s |

Loudness de entrega: **I = −14 LUFS, TP = −1,5**.

## Legenda

- **Legenda queimada em toda peça de corte** — o feed toca sem som.
- Tempos medidos por `silencedetect`, não estimados no olho.
- **Legenda não se escreve por adivinhação.** Se o texto literal da locução de
  uma cena não estiver registrado em nota, a cena **não entra no corte** — foi o
  que tirou a D3 e colocou a C06 no lugar.

## Conformidade dentro do corte

- Cena que mostra o botão Comprar com Pix leva rodapé
  `Pix dentro da live: recurso Enterprise`.
- Selo `ENTERPRISE` da barra do estúdio sai do quadro quando o corte não é sobre
  o plano Enterprise.
- Nenhuma promessa de faturamento, de volume de vendas ou de audiência.

## Assinatura

- Logo: `logo.png` da **raiz** dos repos `moviki` e `moviki-app` — 560x192, fundo
  transparente, área pintada 556x189.
- Usar a **620 px de largura** em 1080p: ampliação de 1,11x é o teto seguro.
  Acima disso a arte quebra.
- **Nada de texto ao lado da logo** — a arte já contém a palavra "moviki".
- Composição fixa: logo, régua ciano, `DO MAPA PARA O AO VIVO`, `moviki.com.br` e
  a pílula `30 DIAS GRÁTIS, SEM CARTÃO`.
- **Nunca substituir a logo por wordmark tipográfico.** Se o proxy negar o
  download (`moviki.com.br` e `i.ytimg.com` dão 403 no CONNECT), pedir o PNG
  anexado ao Paulo em vez de improvisar.
- Trocar só a assinatura: reprocessar a cena de assinatura, não a peça inteira.

## Seleção de cenas

- Vertical de 60 s: C04 · C05 · C06 · C08 · C07 · C11 · C13 com CTA.
- Pago de 27 s: C02 (2,5 s sem locução) · C04 · C08 · C11 · C13 com CTA.
- A abertura do pago entra **sem locução** — o gancho é imagem.
- O par C03/C08 ("a foto não responde" → "agora a vitrine responde") é o núcleo
  emocional; C11 é o fecho.

## Ligações

- [[A7 - Aquisicao e Midia Paga]]
- [[A8 - Conteudo e Social]]
- [[A11 - Marca e Design System]]
- [[R - Regras de ouro de producao de video]]
- [[R - Live - Folha de producao do filme hero]]
- [[R - Regras de conteudo e tom]]
- [[R - Checklist conformidade Meta e Google]]
- [[P26 - Cortes do filme hero - vertical e pago]]
- [[ARQ - Cortes do filme hero vertical e pago 13092026]]
