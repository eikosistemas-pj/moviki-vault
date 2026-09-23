---
type: decisao
status: concluido
area: A5 - Programa de Parceiros
tags: [criadores, oferta, bonus, caixa, decisao]
atualizado: 2026-09-22
---

# Oferta do criador depende da porta de entrada — decisão de 22/09/2026

## Decisão (aprovada pelo Paulo)
| Como o criador chegou | O que recebe |
| --- | --- |
| **Convite direto do Moviki** (sem `indicadoPor`, ou pelo link do próprio dono) | comissão normal + **bônus de ativação** + **Premium liberado** |
| **Pelo link de um parceiro** (`parceiros/{uid}.indicadoPor` = apelido de outro parceiro) | **só a comissão normal** |

## Por quê
- Quem entra pelo link de um parceiro vira indicado direto dele, e o parceiro recebe o bônus de indicação. Somar a oferta do criador a esse bônus pode deixar a conta negativa: o bônus B já fica negativo contra lojista Premium com live.
- O dono escolhe a quem dá o bônus. Parceiro nenhum promete oferta em nome do Moviki.

## Onde isso aparece
- Menu **Criadores → Quem é criador** (`eikoadm01.html` `2026-09-22-criadores5`): cada criador mostra a oferta dele, em verde (convite) ou laranja (link de parceiro), e a confirmação de "Marcar como criador" repete a oferta.
- O painel só **mostra**. Na fase 0, o bônus de ativação é pago à mão.

## Consequências
- O vídeo convite v1.2 (Moviki → 3 criadores) **não vai** para o Material de apoio.
- A "versão parceiro" do vídeo não cita bônus, Premium nem vagas; cita só comissão, com "pode ser zero". Vai na categoria `recrutar`.
- **Conferir o termo v3.1:** se ele promete bônus de ativação a todo criador que assina, o criador que chega pelo link de parceiro não pode assinar essa versão. Ou o termo condiciona o bônus a "convite direto do Moviki", ou existe uma versão sem bônus.

## Ligações
- [[R - Regras de ouro novas de 22092026]]
- [[ARQ - Porta dos criadores - decisao 22092026]]
- handoff no Project: `claude/LEIA-PRIMEIRO - Area do criador pronta - aviso ao chat do video 22092026.md`
