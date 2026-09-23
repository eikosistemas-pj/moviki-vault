---
type: incidente
status: concluido
area: A1 - Produto e Paineis
tags: [vik, moviki-ai, modo-cauteloso, marcas, clausula-2-4]
atualizado: 2026-09-23
---

# Vik alinhado à rodada2 — 23/09/2026

## O que aconteceu
Outro chat subiu a `rodada2` em `index.html`, `parceiro.html`, `eikoadm01.html` e `live.html` (marca `2026-09-23-rodada2`) sem atualizar a tabela `MARCAS_CONFERIDAS` do Vik. Resultado: **modo cauteloso para todos os lojistas e parceiros**, pela terceira vez. A Área do criador e o menu Criadores sobreviveram intactos à rodada2 (conferido no código).

## O que o cliente passou a ver na rodada2 e o Vik não sabia
- **Lojista:** o teste grátis não renova sozinho — escolher o plano em Meu Plano durante o teste, primeira cobrança só no fim; confirmar o e-mail libera o teste na hora; botão "Conferir no Asaas" no pedido aguardando (o sistema também confere a cada 5 min).
- **Parceiro:** aviso amarelo da **cláusula 2.4** — quem também é lojista só gera comissão com o plano do próprio negócio pago e em dia; no teste ou no Básico, os pagamentos dos indicados não geram comissão, nem depois.

## Conserto (`moviki-ai` catálogo `2026-09-23-3`)
- `MARCAS_CONFERIDAS`: lojista e parceiro `2026-09-23-rodada2`.
- Catálogo com as três mudanças do lojista e a cláusula 2.4 do parceiro.
- Contexto da conta: para quem é parceiro **e** lojista, a linha "Cláusula 2.4 cumprida / NÃO cumprida", com a mesma conta do painel (ativo, não vencido, período diferente de teste, plano diferente de Básico).

## Regra (reforço)
Chat que sobe painel sobe junto a tabela do Vik. Quando a subida vem de outro chat, quem conferir depois fecha a ponta — antes de qualquer outra coisa.

## Ligações
- [[ARQ - Vik em modo criador 22092026]]
- [[R - Regras de ouro novas de 22092026]]
