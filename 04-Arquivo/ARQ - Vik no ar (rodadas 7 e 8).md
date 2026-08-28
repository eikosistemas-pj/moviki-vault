---
type: arquivo
status: concluido
data: 2026-08-27
area: A9 — IA e Atendimento (Vik)
tags: [ia]
atualizado: 2026-08-28
---

# ARQ — O Vik entrou no ar (rodadas 7 e 8) — 27/08/2026

Fecha a última peça da caixa de mensagens. O Vik responde dúvida de produto, painel, plano e comissão **com os dados reais da conta de quem está perguntando** — exatamente o que a IA do WhatsApp Business nunca vai saber fazer.

## As duas correções ao plano original
**1. O painel manda SÓ o `idToken`, nunca o texto.** O plano antigo mandava a mensagem junto — isso criaria duas versões da mesma frase, uma gravada pelo painel e outra enviada ao endpoint, sem nada garantindo que fossem iguais. Um cliente mal-intencionado gravaria um texto e mandaria outro. **Agora o endpoint lê do banco. O banco é a única fonte de verdade.**

**2. O que exigia regra nova não era o `'bot'` na leitura.** Regra de leitura no Firestore **não valida campo** — quem lê a subcoleção lê o documento inteiro. O motivo real da v14 está em [[R - Historico de regras v7 a v15]], e era mais grave.

## Por que `de: 'bot'` e não `'admin'`
Se entrasse como `'admin'`, o lojista acharia que era o Paulo falando e depois **não haveria como separar o que foi robô do que foi gente**. Nos três painéis a bolha do Vik é **roxa**.

## Entregue
`moviki-ai` publicado na Vercel (2 de 12 funções) · `api/chat.js` com **cinco travas** · contexto com os dados reais, incluindo desempenho com **a trava de plano copiada do painel** · assistente batizado de **Vik** · interruptor por conversa no painel do dono · **memória por cliente (`vik_memoria`)** com dois filtros de privacidade · **oferta proativa por gatilho objetivo** · cartão de auditoria com botão de apagar memória · regras **v14 e v15** · CSP dos painéis liberando o domínio do robô · o `catch` mudo passou a falar.

## Auditar a memória não é enfeite
**IA erra ao extrair fato, e memória errada envenena todas as conversas seguintes daquela conta, em silêncio.** → [[P05 - Calibrar o Vik]]

→ [[R - Vik - travas, prompt, memoria e ofertas]] · [[ARQ - Incidentes e cacadas de bug]]
