---
type: projeto
status: ativo
prioridade: 2
area: A1 — Produto e Paineis
tags: [produto, deploy]
atualizado: 2026-08-28
---

# P07 — Aviso de mensagem nova para o LOJISTA

## O buraco
O **dono** já é avisado dentro do painel (título da aba, sino, aviso flutuante, bipe). O **lojista** só descobre a resposta entrando no painel.

O Vik respondendo na hora reduz a urgência, **mas não resolve**: resposta do dono continua chegando sem aviso.

## Restrição de arquitetura
Sairia pelo **Resend**, mas o `moviki-robo` está em **12/12 funções**. Precisa entrar como **etapa dentro de um endpoint que já existe** — nunca arquivo novo em `moviki-robo/api`.

## Alternativa a avaliar
O teto de 12 é **por projeto** da Vercel. O projeto do site (`moviki`) usa 1 de 12 e o `moviki-ai` usa 2 de 12 — perguntar em qual projeto a função deveria morar antes de espremer etapa.

## Definição de pronto
- [ ] Projeto Vercel escolhido
- [ ] Disparo por Resend no evento de mensagem do admin
- [ ] Sem duplicar aviso quando o Vik responde

## Ligações
[[A1 - Produto e Paineis]] · [[A2 - Infraestrutura e Deploy]] · [[R - Regras de ouro]]
