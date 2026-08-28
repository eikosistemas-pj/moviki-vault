---
type: projeto
status: ativo
prioridade: 1
area: A10 — Conformidade e LGPD
prazo: 
tags: [lgpd, ia, conformidade]
atualizado: 2026-08-28
---

# P02 — LGPD do Vik (`vik_memoria` na política de privacidade)

## Resultado esperado
`privacidade.html` declara que o Moviki mantém, sobre cada lojista, um resumo de atendimento gerado por IA — com base legal e prazo de retenção.

> **Nota de status (28/08):** este projeto **não está bloqueado — ele bloqueia.** Nada externo impede executá-lo; o trabalho é redigir e publicar. O que ele trava é ligar o Vik em escala. `status: bloqueado` estava semanticamente invertido e foi corrigido para `ativo`.

## Por que agora
**Bloqueia escala.** Enquanto o Vik é ligado conversa a conversa, o risco é pequeno. Ligar para clientes reais em escala com a política omissa é sujar uma conformidade que foi fechada no mesmo dia com Meta e Google.

## O que precisa entrar no texto
- Existência do resumo de atendimento por IA (`vik_memoria`): fatos do negócio, temas perguntados, objeções, ofertas recusadas/aceitas.
- Base legal (legítimo interesse em melhorar o atendimento — validar redação).
- Prazo de retenção e como pedir exclusão (hoje o dono apaga pelo cartão no `eikoadm01`).
- O que **não** é guardado: CPF, CNPJ, chave Pix, dado bancário, telefone, endereço, conteúdo de anexo — filtrado por regex no `memoria.js`, não só por prompt.

## Definição de pronto
- [ ] Seção nova redigida no `privacidade.html`
- [ ] Arquivo publicado no repo `moviki` com marca de versão nova
- [ ] Conferido ao vivo
- [ ] Só então: ligar o Vik em escala

## Ligações
[[A9 - IA e Atendimento Vik]] · [[A10 - Conformidade e LGPD]] · [[R - Vik - travas, prompt, memoria e ofertas]]
