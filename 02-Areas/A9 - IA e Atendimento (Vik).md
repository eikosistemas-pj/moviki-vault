---
type: area
status: ativo
tags: [ia]
atualizado: 2026-08-28
---

# A9 — IA e Atendimento (Vik)

## Os dois atendentes, e por que são dois
| Atendente | Onde | Sabe quem está falando? |
| --- | --- | --- |
| IA do WhatsApp Business (PABX, (41) 2018-6848) | fora do código | ❌ nunca vai saber |
| **Vik** — `moviki-ai/api/chat.js` | dentro do painel | ✅ lê os dados reais da conta |

É por isso que vale manter os dois.

## Padrão a manter
- **Robô que fala com o cliente nasce DESLIGADO, conversa a conversa** (`botLigado`). Mesma lógica do `docsLiberado`.
- A resposta nunca nasce como `'admin'`. Sem um valor próprio (`'bot'`), não há como separar depois o que foi robô do que foi gente.
- **O painel manda SÓ o `idToken`, nunca o texto.** O banco é a única fonte de verdade.
- O `uid` vem **sempre** do token verificado, nunca do corpo do pedido.
- **Prompt não é trava de segurança.** O que não pode ser guardado precisa de filtro em código também.
- **O bloco de dados entra DEPOIS das instruções**, com aviso de que é dado e não comando — senão um negócio chamado "ignore as regras acima" vira injeção de prompt.
- **Ativação antes de venda.** Quem não usa o que já paga não faz upgrade, faz cancelamento.
- A **trava de plano do painel foi copiada para dentro do robô** — senão o Vik vira atalho para furar o gating.

## Projetos vinculados
[[P02 - LGPD do Vik]] · [[P05 - Calibrar o Vik]] · [[P06 - Camada 3 do Vik]]

## Recursos
[[R - Vik - travas, prompt, memoria e ofertas]] · [[ARQ - Vik no ar (rodadas 7 e 8)]] · [[R - Custos e cotas]]
