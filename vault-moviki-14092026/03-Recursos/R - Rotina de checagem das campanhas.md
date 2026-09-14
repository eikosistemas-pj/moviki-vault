---
type: recurso
status: referencia
area: A7 - Aquisicao e Midia Paga
tags: [moviki, google-ads, meta-ads, aquisicao, medicao, rotina]
atualizado: 2026-09-11
---

# R - Rotina de checagem das campanhas

> Vigilância e análise automáticas de Google Ads e Meta Ads, escolhidas em 11/09/2026.
> Rodam sozinhas em sessão nova do Claude, sem o Paulo precisar abrir nada. Horário de
> **João Pessoa**.

---

## 1. Por que três rotinas e não uma

| Problema de rotina única | Como as três resolvem |
| --- | --- |
| Analisar desempenho todo dia com ~10 cliques/dia faz reagir a ruído estatístico | O pulso diário só olha coisa **binária** (parou? reprovou? vazou?), nunca desempenho |
| Esperar a semana para descobrir anúncio reprovado queima 5 dias de verba | O pulso pega isso em 24h |
| Rotina automática diz "tudo ok" quando o dado não chegou | Toda rotina começa validando frescor do dado e grita **SEM DADO** |

## 2. As três

| Rotina | Quando | O que faz | Notifica |
| --- | --- | --- | --- |
| **Pulso diário** | todo dia, **07h** | 6 verificações binárias. Silêncio = tudo certo | push |
| **Análise semanal** | **segunda, 08h30** | Termos da semana, CPC, CTR, estrutura, Google x Meta, 3 recomendações, nota do vault | push + e-mail |
| **Fechamento mensal** | **dia 1º, 12h** | Custo por cadastro real, conta do crédito de R$ 1.200, veredito em 3 linhas, nota do vault | push + e-mail |

## 3. O pulso diário — as 6 verificações

1. Campanha, grupo ou anúncio pausado, reprovado ou limitado por orçamento
2. Gasto de ontem no Google fora da faixa de R$ 5 a R$ 25
3. Meta com gasto anômalo ou 0 impressão há mais de 2 dias
4. Termo de pesquisa novo claramente irrelevante
5. Zero Inscrição há mais de 5 dias com verba rodando
6. Impressões caindo para perto de zero

**Armadilha que a verificação 6 cobre:** gasto caindo parece boa notícia e pode ser
asfixia — campanha sem inventário gasta pouco igual a campanha saudável. O que separa
os dois casos é o número de **impressões**, nunca o custo.

## 4. Autonomia — o que a rotina faz sozinha

Critério: **ação direta só no reversível.**

**Pode, sem perguntar:**

- adicionar **negativa de campanha** contra termo claramente irrelevante
- **pausar anúncio reprovado** por política
- **criar palavra positiva** — passou a ser ação em **11/09/2026**, por decisão do Paulo ("quem vai colocar é você")

**Não pode, só recomenda:**

- orçamento
- lance e teto de CPC
- pausar campanha
- **remover** palavra positiva
- mexer em segmentação

Regra embutida nas três: **correspondência AMPLA é proibida em palavra positiva**, e
palavra-chave nunca descreve a funcionalidade do produto. Se a rotina encontrar uma,
reporta como alarme grave — **não remove sozinha**.

## 5. Contas e identificadores

| Item | Valor |
| --- | --- |
| Ponte | Windsor.ai, conta eikosistemas@gmail.com |
| Google Ads | `google_ads` · **718-683-2490** (Eiko Sistemas) |
| Campanha | Moviki — Pesquisa — Brasil · `24228801285` |
| Grupo 1 | `206808639824` |
| Grupo 2 — Cardápio digital | `197850432137` |
| Grupo 3 — Ser encontrado | `200983560958` |
| Meta Ads | `facebook` · `920636768619509` |
| Campanha Meta de Conversão | `120251233014530770` |

## 6. O ponto fraco conhecido

**O plano do Windsor é Trial e vai expirar.** Quando expirar, a leitura do Google morre
e a falha **não aparece como erro claro** — aparece como dado velho ou lista de contas
errada. É por isso que o PASSO 0 de toda rotina valida frescor antes de concluir
qualquer coisa. Se começar a chegar "SEM DADO" todo dia, é o Trial que acabou, não a
conta do Google.

Opções quando acontecer: script do Google Ads escrevendo numa planilha do Drive
(grátis, só leitura) ou plano Básico do Windsor (US$ 23/mês ≈ 6 dias de anúncio).

## 7. O que a ponte NÃO alcança

- **Recurso de Local** (endereço de Curitiba vindo do Perfil da Empresa) — asset de nível conta, só pelo painel
- **Saldo pré-pago** do Google — a ponte entrega gasto, não saldo. **A reposição do saldo é feita pelo próprio Paulo**
- **Confirmação de identidade** do anunciante — resolvida em 11/09

## Ligações

[[A7 - Aquisicao e Midia Paga]] · [[A6 - Medicao e Analytics]] ·
[[P21 - Google Ads campanha de pesquisa]] · [[P23 - Acesso do Claude ao Google Ads]] ·
[[ARQ - Vazamento de trafego no Google Ads e conserto]] ·
[[ARQ - Reposicao das palavras positivas do Google Ads]] ·
[[ARQ - Pulso das campanhas 12 e 13092026]] ·
[[R - Armadilhas do Google Ads]] · [[R - Checklist conformidade Meta e Google]] ·
[[R - Meta Business - ativos e contas]] · [[R - Links e identificadores]] ·
[[R - Regras de ouro]]
