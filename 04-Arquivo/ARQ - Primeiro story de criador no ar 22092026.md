---
type: arquivo
status: concluido
area: redes-sociais
tags: [criadores, robo-social, story, facebook, marco]
atualizado: 2026-09-22
---

# Primeiro story de criador no ar — 22/09/2026

## O que aconteceu
- 22/09 às 23h26, o robô social publicou o 1º story de criador na Página do Facebook.
- Peça: "Ligue a câmera. Receba o pedido." de @lucianopessoa, com o selo "Conteúdo de @lucianopessoa".
- media_id `1073800858578044` (`photo_stories`).

## O que ficou provado em produção
Caminho inteiro das duas chaves:
envio na Área do criador → autorização do criador → aprovação do dono (menu Criadores) → `GET /api/criadores` → robô → Página.

## Pontos em aberto
- Story em vídeo (`video_stories`) ainda sem publicação real.
- Com `SO_FACEBOOK` ligado, nada vai ao Instagram.
- A peça tinha 941x1672 (abaixo de 1080 de largura): pedir o arquivo original em 1080x1920 aos criadores.
- O selo de crédito ficou sobre o campo de mensagem do celular desenhado na arte; avaliar subir o selo.

## Ligações
- [[ARQ - Area do criador no painel do parceiro]]
- [[ARQ - Porta dos criadores - decisao 22092026]]
