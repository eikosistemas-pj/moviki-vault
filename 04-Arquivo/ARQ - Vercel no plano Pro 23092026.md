---
type: decisao
status: concluido
area: A2 - Infraestrutura e Deploy
tags: [vercel, infra, funcoes, regra-de-ouro, armadilha]
atualizado: 2026-09-23
---

# ARQ - Vercel no plano Pro 23092026

## O fato

Print da conta Vercel (Eiko Sistemas) mandado pelo Paulo em 23/09/2026: **uma
única equipe, "moviki-robo", plano Pró**, com o Paulo como Proprietário.

## O que muda

- **O teto de 12 funções por projeto é do plano Hobby e não vale mais.** O `moviki-robo` com 16 funções em `/api` é suportado.
- A regra de ouro "**NUNCA criar arquivo novo em `moviki-robo/api`**" e o "12/12 — NO TETO" do [[R - Stack e repositorios]] e do [[R - Regras de ouro]] **ficam desatualizados**. Atualizar os dois na próxima rodada em que forem lidos inteiros.

## O que NÃO muda

- **`moviki-robo` continua sendo o repositório de DINHEIRO e muda o mínimo.** O motivo nunca foi só o teto: é isolar o caminho do dinheiro do resto.
- O `moviki-ai` continua separado do robô — isolamento do conversacional, não só do teto.
- Função serverless com tempo curto: toda chamada externa segue com idempotência e confirmação assíncrona.

## Pendência

- [ ] Conferir no painel da Vercel se os projetos `moviki` e `moviki-ai` estão na mesma equipe Pro.

## Ligações

[[A2 - Infraestrutura e Deploy]] · [[R - Regras de ouro novas de 17 a 23092026]]

*Registrada em 23/09/2026 a partir do print da conta mandado pelo Paulo.*
