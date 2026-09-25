---
data: 2026-09-24
projeto: Moviki
repos: [moviki-app, moviki-ai, moviki-assistente-social]
pr: upload manual pelo GitHub web
tags: [moviki, alteracao, live, material, redes]
---

# Live aberta a todos e material de apoio conferido (pendência 10)

## O que mudou
- O robô das redes volta a publicar as peças que vendem live na página oficial (secret LIVE_NA_PAGINA = 1).
- Duas legendas do material corrigidas: "oferta com contagem regressiva" e "estoque ao vivo" são do plano Enterprise e agora dizem isso.
- O Vik conhece o menu novo do material: cartão "Panfletos com o seu QR" e o ramo "Lojas de shopping".
- Teto de minutos de vídeo da live definido no painel do dono (a Cloudflare não tem teto próprio).

## Por quê
- O mapa dizia que a live estava em beta fechado; estava aberta havia tempo. Por isso o robô social só tinha 1 reel e 11 feeds para escolher.
- Legenda que promete recurso do Enterprise para quem assina outro plano vira reclamação e fere a regra de anúncio da Meta e do Google.

## Decisões tomadas
- Toda legenda que cita Pix na live, oferta relâmpago, estoque ao vivo, cupom, brinde ou cortes precisa dizer "plano Enterprise".
- Se a live for fechada de novo, apagar o secret LIVE_NA_PAGINA.

## O que conferir
- Painel do parceiro > Material de apoio > Lojas de shopping: os dois vídeos aparecem com a legenda nova.
- Nos próximos dias, a página oficial publica peças de live.

## Pendências
- Link do vídeo e cupom da live ainda públicos (pacote de código, junto com a validação de saque do Asaas).

Ver também: [[Moviki - Mapa Mestre]]
