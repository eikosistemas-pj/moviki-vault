---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [cloudflare, custo, teto, live, analytics]
atualizado: 2026-09-16
---

# R - Teto de gasto de video no Cloudflare

Como o Moviki impede que a conta do Cloudflare Stream vire uma fatura sem fim.
O registro datado esta em [[ARQ - Teto de gasto de video no ar 16092026]].

## O que o Cloudflare NAO tem

- **Nao tem hard cap de gasto.** "Budget alerts" mandam e-mail e nada mais.
- Nao tem botao de "parar de entregar quando passar de X".

## Como o preco funciona

| Item | Valor |
| --- | --- |
| Minutos **entregues** | US$ 1 por 1.000 |
| Como se conta | **por espectador** |

Uma live de 60 min com 50 pessoas assistindo = **3.000 minutos**, nao 60.
Cobranca de WebRTC comeca em **15/10/2026**.

## O ciclo de faturamento nao e o mes-calendario

Vira no dia da assinatura da conta. A conta do Paulo vira **dia 12** — o
Billing mostra "Sep 12 - Oct 11". Medir do dia 1 da numero errado todo mes.

## A parede do Moviki

Em `moviki/api/live.js`:

| Funcao | O que faz |
| --- | --- |
| `medirConsumo(cicloDia)` | GraphQL do Cloudflare, dataset `streamMinutesViewedAdaptiveGroups`, soma o ciclo corrente |
| `inicioDoCiclo()` | calcula a virada a partir de `cicloDia` |
| `vereditoTeto(termos)` | decide e devolve o motivo |

Motivos possiveis: `sem_teto` · `medicao_falhou` · `teto_atingido` ·
`medicao_zerada` · `abaixo_do_teto`.

O token do Cloudflare precisa da permissao **Account Analytics**. Sem ela a
consulta responde erro e o veredito vira `medicao_falhou`.

## A trava falha ABERTA — e de proposito

> Medicao que nao responde **nao** impede a live. E a **unica** trava do
> projeto assim. Aceite, plano, beta, corte de comissao e abertura de sessao
> falham fechadas.
>
> Motivo: a analytics do Cloudflare e um terceiro fora do caminho critico.
> Falhar fechada ali pararia o Modo Live inteiro porque um endpoint de
> relatorio ficou lento. O risco de uma live a mais e dinheiro; o risco de
> falhar fechada e o produto.

## Onde se configura

Painel do dono > Lives, sem deploy. Documento `configuracoes/liveTermos`:

| Chave | Hoje |
| --- | --- |
| `tetoMinutosMes` | **50000** |
| `cicloDia` | **12** |

⚠️ Escrita nesse documento e **sempre `merge`**. Ele carrega tambem `liveBeta`,
`liveDesligada`, `extras` e `demoYoutube`; sobrescrever inteiro desliga o teto e
abre o beta sem querer.

## Onde se le

Painel do dono, card **Consumo de video**: minutos do ciclo, teto, e a linha
**"Proxima live: LIBERADA / BARRADA"** com o motivo. Essa linha existe porque
trava sem tela e indistinguivel de trava quebrada.

## Ligacoes

[[A13 - Modo Live]] · [[A4 - Financeiro]] ·
[[R - Live - Ferramentas de transmissao]] · [[R - Custos e cotas]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[ARQ - Teto de gasto de video no ar 16092026]]
