---
type: decisao
status: concluido
data: 2026-08-27
area: A6 — Medicao e Analytics
tags: [decisao, lgpd, medicao]
atualizado: 2026-08-28
---

# Decisão: sem pixel de navegador, medição só pelo servidor

## Contexto
Para rodar campanha de conversão na Meta, o caminho padrão é o pixel de navegador. Mas o `privacidade.html`, seção 9, já dizia publicamente que o site **não usa cookie de publicidade**.

## Alternativas
1. Subir o pixel + banner de consentimento + reescrever a seção 9.
2. **Só Conversions API (servidor), sem cookie e sem banner.**

## Decisão
**Opção 2.** Evento do robô direto para a Meta, com e-mail e telefone em SHA-256.

## Consequência aceita
**Fica de fora: remarketing e público semelhante a partir de visitante** — os dois dependem do cookie.
Com tráfego perto de zero, não há visitante acumulado para perseguir.

## O que reabriria esta decisão
**Volume de visita.** Com público acumulado, o remarketing passa a valer o custo de banner de consentimento + reescrita da seção 9 + base legal de cookie de anúncio (diferente da analítica).

## A regra que nasceu daqui
**Antes de instalar rastreador, ler a própria política de privacidade.**

→ [[ARQ - Meta CAPI]] · [[P01 - Aquisicao - campanha de trafego pago]]
