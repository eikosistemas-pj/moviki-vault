---
type: recurso
status: referencia
area: A6 — Medicao e Analytics
tags: [medicao]
atualizado: 2026-08-28
---

# R — Eventos GA4 (dicionário)

**Propriedade:** "Moviki" · **Measurement ID:** `G-GG5CSQZVGH`
Método: script **oficial** do Google (gtag.js), carregado pelo `mvmetrica.js` servido do próprio domínio. Consent Mode: **analytics SIM, anúncio NÃO**.

## Leva 1 (25/08) — o funil do dinheiro
`page_view` · `cta_painel` · `quiz_etapa` · `sign_up` · `modal_plano_aberto` · `plano_selecionado` · `begin_checkout` · `checkout_redirecionado` · `checkout_falhou` · **`purchase`** (servidor, valor em BRL, `transaction_id`)

## Página pública (26/08)
`pagina_negocio` · `nav_publica` · `cardapio_aberto` · `unidades_aberto` · `unidade_trocada` · `mapa_cheio` · `compartilhar` · `favorito` · `avaliacao_enviada` · `clique_publico` (delegação por `data-ev`)

## Leva 2 (27/08) — topo do funil
`cta_click` `{cta, pagina}` — **23 CTAs nomeados** em `enterprise.html`, `comerciantes.html`, `parceiros.html`, `parceiros-ganhos.html`
`chegou_por_indicacao` `{ref, destino}`

## Leva 3 (27/08) — ramo de parceiro (`seja-parceiro.html`)
`pagina_seja_parceiro` `{tem_upline}` · `chegou_por_indicacao` `{ref, destino:'seja_parceiro'}` · `parceiro_cadastro_iniciado` · `parceiro_cadastro_erro` `{motivo}` · `sign_up` (via `mvSignup`) · `parceiro_cadastrado` `{tem_upline, metodo}` · `cta_click`

⚠️ **A CSP precisou dos 3 hosts do GA:** `googletagmanager` no `script-src`, `*.google-analytics.com` no `img-src`, os três no `connect-src`. Sem isso a página "tem GA" e não mede.

## Meta CAPI (servidor)
| Evento | Onde nasce | `action_source` |
| --- | --- | --- |
| `Lead` | `novo-cliente.js` (cadastro do comerciante) | `website` (com user agent real) |
| `Purchase` | `webhook.js` (webhook do Asaas) | **`system_generated`** |

Conjunto de dados: **2114417739495816**.
O segundo conjunto (`1003679066038534`) é o de **aplicativo**, criado sozinho pela Meta — nunca recebe evento e **não deve ser apagado**.

## Atribuição ponta a ponta
Linker cross-domain → o painel lê `client_id`/`session_id` (`window.mvIds()`, resolve em ≤0,8 s para nunca travar o checkout) → manda no `criar-assinatura` → gravado em `faturamento/{uid}` → o `webhook.js` dispara o `purchase`.
**Dedup:** `faturamento/{uid}/ga/{payId}.create()` — o Asaas manda 2 eventos por pagamento; a mesma trava protege GA e Meta.

## UTM dos redirecionadores
`/p/joao_silva` → `/comerciantes.html?utm_source=parceiro&utm_medium=indicacao&utm_campaign=programa_parceiros&utm_content=joao_silva&ref=joao_silva`
Em **Aquisição > Aquisição de tráfego** aparece `parceiro / indicacao`, e o `utm_content` diz **qual parceiro**. Sem apelido válido: `utm_content=sem_ref`.
