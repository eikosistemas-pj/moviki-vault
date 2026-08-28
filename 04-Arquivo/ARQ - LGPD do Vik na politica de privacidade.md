---
type: decisao
status: concluido
data: 2026-08-28
area: A10 - Conformidade e LGPD
tags: [lgpd, ia, conformidade]
atualizado: 2026-08-28
---

# ARQ - LGPD do Vik na politica de privacidade

Fechamento do projeto **P02 — LGPD do Vik**, concluído em **28/08/2026** (rodada 11). Era o segundo bloqueio crítico do projeto e o único que travava ligar o Vik em escala.

## O que entrou no ar
`privacidade.html` (repo `moviki`) ganhou a **seção 5 — "Assistente de atendimento por inteligência artificial (Vik)"**, posicionada logo depois de "Com quem compartilhamos" e **não** enterrada no fim do documento.

A seção declara:

- a existência do assistente e a identificação dele na tela;
- o envio do texto à Anthropic como **operador que não treina modelo**;
- o resumo de atendimento (`vik_memoria`) — para que serve e o que é descartado antes de gravar;
- que **nenhuma decisão sobre o titular é automatizada** (Art. 20 da LGPD) — e isso é verdade no código: cobrança, saque e comissão contestada vão obrigatoriamente para humano;
- os quatro direitos do titular sobre o resumo;
- o prazo de retenção.

## O que mudou junto
Tabela de bases legais (item 3) · lista de operadores (item 4) · retenção (item 7) · direitos (item 8). As seções 5–12 viraram **6–13**.

## A única afirmação que não é verificável no código
**"não usa esse conteúdo para treinar modelos"** depende de contrato, não de implementação. Conferir nos termos da conta Anthropic → [[P11 - Pendencias operacionais do dono]].

## Por que a redação ficou boa
Ela descreve o **mecanismo**, não a intenção. Dizer que CPF, CNPJ, chave Pix e sequências de 8+ dígitos são filtrados por regex no `memoria.js` — e não só proibidos no prompt — é a diferença entre uma política que promete e uma que documenta uma trava. Prompt não é trava de segurança; regex é.

## O que isto destrava
Ligar o Vik para clientes reais em volume deixou de estar bloqueado por conformidade. **Mas continua bloqueado por calibragem:** o padrão global segue DESLIGADO de propósito, porque o botão multiplica qualquer erro de extração de memória por todas as conversas de uma vez. → [[P05 - Calibrar o Vik]]

## Ligações
[[A10 - Conformidade e LGPD]] · [[A9 - IA e Atendimento Vik]] · [[R - Vik - travas, prompt, memoria e ofertas]] · [[ARQ - Incidente - deploy no repositorio errado]]
