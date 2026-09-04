---
type: projeto
status: concluido
prioridade: 1
area: A10 — Conformidade e LGPD
prazo: 2026-09-03
tags: [moviki, conformidade, parceiros, armadilha]
atualizado: 2026-09-03
---

# P18 — Conformidade do simulador de ganhos

**Resolvido em 03/09/2026**, no mesmo dia em que foi encontrado.

## O que havia

Um bloco `mkSim` com três controles deslizantes e quatro caixas de valor:
**"Simule seus ganhos"** · "Seu ganho fixo mensal" · **"Bônus de equipe — nível
2"** e **"nível 3"** · **"Previsão do seu 1º saque total"**.

**Estava nos DOIS painéis** — no do parceiro e, mais grave, no do **lojista**,
que nem parceiro é.

Isso é exatamente o que saiu do ar da landing em 27/08 (o gráfico de R$ 57 /
171 / 284), só que pior: aqui o número era **calculado ao vivo pelo próprio
usuário** e rotulado como *previsão do seu saque*. E usava "equipe" e "nível
2/3", a linguagem que a regra de ouro proíbe por ser a estética do multinível —
a mesma que o roteiro da P00 evita de propósito.

## A pergunta do Paulo, e a resposta honesta

Ele perguntou se dava para manter o cálculo — que atiça — mas impedir o print,
lembrando que alguém pode até fotografar a tela com outro celular.

**Não existe defesa técnica contra print, e muito menos contra foto da tela.**
Bloquear a tecla não funciona, marca d'água não impede nada, e uma câmera apontada
para o monitor passa por cima de qualquer coisa. **A única defesa é o conteúdo:
uma tela que não promete nada não vira problema quando alguém fotografa.**

## O que ficou no lugar

**No painel do parceiro** — bloco novo **"Como a sua comissão é calculada"**:

- Quatro abas de plano. Escolhendo uma, mostra **a comissão de UMA assinatura
  daquele plano** — Básico R$ 0,00 · Pró R$ 5,69 · Premium R$ 7,49 ·
  Enterprise R$ 14,99. Isso é a **regra aplicada**, não uma previsão, e é a
  mesma conta que a landing pública já publica desde 27/08.
- Os três níveis em **cards iguais, sem hierarquia e sem cor de "melhor"** —
  hierarquia visual entre níveis é a estética do multinível.
- Escritos como regra: *quem você indica* (15%, todo mês, enquanto a pessoa
  continuar cliente pagante) · *quem essa pessoa indica* (7,5%, uma vez, no
  primeiro pagamento) · *e quem essa segunda pessoa indica* (5%, uma vez).
- Aviso fixo: **a comissão só existe sobre assinatura efetivamente paga, não há
  pagamento por cadastrar pessoas nem por montar equipe, e se ninguém assinar a
  comissão é zero.** Com link para o Regulamento.

**No painel do lojista** — o simulador foi **removido**, sem substituto. O bloco
"Como você ganha", que fica logo acima, já descrevia a regra inteira e
corretamente. Só faltava a frase do "pode ser zero", que entrou.

## O que continua atiçando, e é legítimo

A **recorrência**. "R$ 5,69 por mês, enquanto essa pessoa continuar cliente
pagante" é o argumento forte de verdade — e é regra, não promessa. O que se
perdeu foi só a multiplicação por indicações imaginárias.

## Conferido antes de entregar

Varredura do texto renderizado nos dois painéis: nenhuma ocorrência de "Simule
seus ganhos", "Previsão do", "Bônus de equipe", "Nível 2/3" ou "ganho fixo". As
quatro abas devolvem os valores certos. A frase "efetivamente paga" e a palavra
"zero" estão presentes. Zero erro de página.

## Ligações

[[A10 - Conformidade e LGPD]] · [[A5 - Programa de Parceiros]] · [[R - Checklist conformidade Meta e Google]] · [[R - Regras de ouro]] · [[P16 - Rodada da credibilidade]]
