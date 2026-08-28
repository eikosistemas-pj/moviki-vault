---
type: decisao
status: concluido
data: 2026-08-27
area: A9 — IA e Atendimento (Vik)
tags: [decisao, ia]
atualizado: 2026-08-28
---

# Decisão: atendimento por WhatsApp resolvido por fora (PABX)

## Contexto
O `moviki-ai` tinha sido criado para ser o atendente de WhatsApp. A pendência "migrar o número oficial" arrastava há dias.

## O que aconteceu
O Paulo contratou um **PABX** no número oficial **(41) 2018-6848**, e a **IA do próprio WhatsApp Business** já está treinada na empresa e respondendo dúvida de cliente. Testado e rodando.

## Decisão
- O webhook de atendimento do `moviki-ai` **não vai mais para o WhatsApp**.
- A pendência "migrar o número oficial" está **encerrada**. O número de teste +1 555-201-4276 deixa de ser necessário.
- **O `moviki-ai` é reaproveitado** para o atendente de dentro do sistema — ele já existe, tem teto próprio de 12 funções e já tinha `lib/anthropic.js`.

## Por que os dois atendentes ainda fazem sentido
O atendente do painel **sabe quem está falando**. Lê `parceiros/{uid}`, `comissoes`, `saques` e `assinaturas` daquela pessoa e responde *"sua comissão de agosto é R$ 34,15 e libera dia 12"*.
**A IA do WhatsApp não tem esse dado e nunca vai ter.**

→ [[A9 - IA e Atendimento (Vik)]] · [[ARQ - Vik no ar (rodadas 7 e 8)]]
