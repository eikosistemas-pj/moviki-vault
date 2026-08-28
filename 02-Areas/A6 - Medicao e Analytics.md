---
type: area
status: ativo
tags: [medicao]
atualizado: 2026-08-28
---

# A6 — Medição e Analytics (GA4 + CAPI + contador próprio)

## Padrão a manter
**Medição nunca derruba cobrança — e tráfego pago nunca antes da medição.**

## As três camadas, que são coisas diferentes
| Camada | Onde | Mede o quê |
| --- | --- | --- |
| **GA4 no navegador** | `mvmetrica.js`, idêntico nos repos `moviki` e `moviki-app` | funil do site inteiro |
| **Measurement Protocol** | `lib/ga.js` no `moviki-robo` | `purchase` confirmado pelo servidor |
| **Meta CAPI** | `lib/meta.js` no `moviki-robo` | `Lead` (cadastro) e `Purchase` |
| **Contador por negócio** | escrito pela própria página pública | `metricas/{uid}/dias/{AAAA-MM-DD}` |

⚠️ **O `mvmetrica.js` é SÓ Google Analytics — não escreve nada no Firestore.** Confundir os dois já custou meia sessão.

## Regras de ouro desta área
- **Não mexer no `mvmetrica.js` sem necessidade** — idêntico nos dois repos e no caminho do dinheiro. Medição de página nova entra **inline**.
- **Página que redireciona na hora não carrega GA.** Carimbe UTM no destino.
- **Carimbar UTM só vale se o DESTINO medir.** O par `pp.html → seja-parceiro.html` ficou aberto por dias porque os dois "estavam feitos".
- **Evento de venda sozinho não tira campanha do aprendizado.** Com pouco volume, o `Lead` é o que dá material.
- **`action_source` descreve de onde o evento NASCEU.** `website` exige `client_user_agent`; webhook de pagamento não tem navegador → `system_generated`.
- **Campo de correspondência vazio não se manda para a Meta.** String vazia derruba a qualidade do conjunto de dados inteiro.
- **Antes de instalar rastreador, ler a própria política de privacidade.**
- Dedup do `purchase`: `faturamento/{uid}/ga/{payId}.create()` — o Asaas manda 2 eventos por pagamento, e a mesma trava protege GA e Meta.

## Recursos
[[R - Eventos GA4 dicionario]] · [[ARQ - GA4 levas 1, 2 e 3]] · [[ARQ - Meta CAPI]] · [[ARQ - Medicao por negocio contador]]
