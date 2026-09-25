---
data: 2026-09-24
projeto: Moviki
repos: [moviki, moviki-app]
pr: upload manual pelo GitHub web
tags: [moviki, alteracao, anuncios, lgpd, privacidade]
---

# Google Ads medido sem cookie de anúncio + aviso de medição (pendência 11)

## O que mudou
- O Google Ads passa a saber quais campanhas trouxeram cadastro e assinatura, importando essas conversões do Google Analytics.
- Aviso discreto no rodapé do site e do painel na primeira visita: "Ok" ou "Não medir".
- Política de privacidade atualizada (itens 4 e 10) com essa medição e o link de preferências.

## Por quê
- Anunciar no Google sem medir conversão é gastar verba no escuro — o Google não aprende quem vira cliente.
- A política dizia que o Google Analytics não servia a anúncio; com a importação, isso deixou de ser verdade e precisava ser dito.

## Decisões tomadas
- Nada de tag do Google Ads nem pixel da Meta no navegador: continua "nenhum cookie de publicidade".
- Se um dia instalar tag de anúncio, antes reescrever a política e trocar o aviso por consentimento "Aceitar/Recusar".

## O que conferir
- Site em janela anônima: o aviso aparece no rodapé; "Não medir" some com ele e ele não volta.
- moviki.com.br/?medicao=escolher reabre o aviso.
- Google Ads > Metas > Conversões: "sign_up" e "purchase" importados do GA4.

## Pendências
- Pendência 12: limpeza das contas de teste.

Ver também: [[Moviki - Mapa Mestre]]
