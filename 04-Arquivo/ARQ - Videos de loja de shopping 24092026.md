---
type: arquivo
status: concluido
area: A14 - Material de apoio do parceiro
tags: [material-de-apoio, video, shopping, live, kairogen, simulador]
atualizado: 2026-09-24
---

# ARQ - Videos de loja de shopping 24092026

## O que foi feito

Dois vídeos de 38 s para o lojista de shopping, no posicionamento de **live
shop**: o corredor esvaziou, o cliente está no celular, a loja vai até ele ao
vivo, ele compra por Pix na live ou toca em "Como chegar" e vai até a loja.

- `video-shopping-moda.mp4`: loja fictícia Aurora Moda
- `video-shopping-esportes.mp4`: loja fictícia Ritmo Esportes

Cenas de ambiente geradas no Wan 3.0 (Kairogen). **As telas da live são a
`moviki/live.html` real**, rodando num navegador com Firebase de mentira e
gravada quadro a quadro. Nenhuma interface foi desenhada por IA. Voz Malu,
legenda queimada, trilha gerada.

## Decisões

- Para o lojista de shopping, o Moviki é **live shop**. O mapa não entra.
- Reprovado o ângulo "o shopping fecha às 22h" (lojista não quer vender de
  madrugada).
- Tela com loja fictícia leva o selo **"Cena ilustrativa · loja fictícia"**, e
  a cena do Pix leva **"Pix dentro da live: plano Enterprise"**.
- **Marca de terceiro que o gerador puser na cena não é retocada** (decisão do Paulo, 24/09): o borrão e o preenchimento ficaram piores que a marca. Só se pede "sem logo" no prompt.

## Estado final (24/09, noite)

- [x] Categoria própria `shopping` ("Lojas de shopping") no catálogo, ícone 3D — ver [[ARQ - Categoria Lojas de shopping no material de apoio 24092026]]
- [x] Vídeos e capas tocando no painel do parceiro (capas em `material/capas/`)
- [x] Skill `video-shopping` e kit reaproveitável (`kit-video-shopping.zip` no Release `material-bruto` do repo `moviki`)
- [ ] Próximo ramo: artigos para pet (precisa recarregar o Kairogen: ~165 créditos por vídeo)
- [ ] Secret `LIVE_NA_PAGINA=1` no robô social, já que a live está aberta
- [ ] Em tela de 360x640, o botão Sacolinha fica por cima da faixa OFERTA DA LIVE na `live.html`

Ligações: [[A14 - Material de apoio do parceiro]] · [[A13 - Modo Live]] ·
[[ARQ - Modo Live aberto para todos 23092026]]
