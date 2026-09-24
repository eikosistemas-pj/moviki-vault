---
type: arquivo
status: concluido
area: A5 - Programa de Parceiros
tags: [criador, painel-dono, ga4, medicao, aprovacao]
atualizado: 2026-09-23
---

# ARQ - Menu Criadores no painel do dono 22092026

No ar em `moviki-app/eikoadm01.html` `2026-09-22-criadores5` (depois
`2026-09-23-vikalarme`, sobre a `rodada2`), com o endpoint
`moviki/api/criadores.js` `2026-09-22-criadores2`.

## As quatro partes

| Parte | O que faz |
| --- | --- |
| **Fila de aprovação** | prévia, pré-triagem, **Aprovar / Recusar (motivo obrigatório) / Suspender**. É a segunda chave da peça |
| **Desempenho por criador** | visitas pelos links `/c/` e `/p/` (GA4), cadastros (`indicacoes`), pagantes e mensalidades (`comissoes` N1), receita líquida estimada (mensalidade − 6% − R$ 2), custo (comissões + bônus + `criadorCustoMes` opcional), resultado, veredito e posts do Moviki com peça dele. 4 gráficos e ranking |
| **Quem é criador** | marca `parceiros/{uid}.criador = true`; mostra a oferta de cada um (verde/laranja) — ver [[ARQ - Oferta do criador por porta de entrada - decisao 22092026]] |
| **Link de acesso** | Copiar / Abrir / WhatsApp para `app.moviki.com.br/criador`, também em Atalhos do dono |

## O endpoint

`moviki/api/criadores.js`: **GET** para o robô social (peças liberadas) e
**POST** para as visitas do GA4 (só admin, e `acao: meu_trafego` para o próprio
criador).

## O que precisou ser ligado fora do código — feito em 23/09

- Regras do Firestore **v27** e do Storage (`criadores/{uid}/`) publicadas
- `moviki-site-leitura@moviki-app.iam.gserviceaccount.com` como **Leitor** na propriedade GA4
- **Google Analytics Data API** ativada no projeto `moviki-app`
- Secret `CRIADORES_URL` = `https://www.moviki.com.br/api/criadores` no `moviki-assistente-social`

Sem os dois do GA4, as visitas não aparecem.

## Ligações

[[ARQ - Area do criador no painel do parceiro]] · [[A5 - Programa de Parceiros]] ·
[[A6 - Medicao e Analytics]]

*Reconstruída em 23/09/2026 a partir do MAPA-MESTRE e do LEIA-PRIMEIRO da Área do criador, ambos de 23/09.*
