---
type: arquivo
status: concluido
area: A5 - Programa de Parceiros
tags: [painel-parceiro, privacidade, entrega]
atualizado: 2026-09-10
---

# ARQ - Tres olhinhos no painel do parceiro

**No ar em 10/09/2026**, marca `2026-09-10-niveis-olhinhos` no
`moviki-app/parceiro.html`.

## O pedido

O painel tinha **um** olhinho so, no card "Saldo disponivel", que borrava tudo de
uma vez. Nao servia: o parceiro precisa poder mostrar a equipe dele a um
candidato **sem** mostrar o saldo, e as vezes o contrario.

## Os tres interruptores

| Olhinho | Onde fica | O que esconde |
| --- | --- | --- |
| Saldo / dinheiro | "Saldo disponivel" e "Resumo dos seus ganhos" | disponivel, aguardando liberacao, ganhos do mes/totais/recorrentes, variacao, extrato, ganhos por nivel, mes a mes, saques, avisos do proximo saque, coluna "Sua comissao", chave Pix em Meus dados e **os numeros do grafico** |
| Equipe / pessoas | "Seu nivel", "Suas indicacoes recentes", "Todas as suas indicacoes" | indicacoes ativas, as duas listas, o numero de clientes pagando e o "faltam X clientes" |
| Grafico | "Evolucao dos seus ganhos" | o desenho e a nota abaixo dele |

## Decisoes

- **O olhinho do saldo tambem apaga os numeros do grafico.** Sem isso, esconder o
  saldo e deixar o grafico entregaria os valores pelo eixo lateral e pelo balao. A
  linha continua desenhada, so os numeros somem.
- **O selo do nivel continua aparecendo.** E status, nao valor.
- O quadro "Indicacoes ativas" saiu da fileira de ganhos e foi para dentro de
  "Suas indicacoes recentes" — o numero de pessoas junto das pessoas.
- **Cada aparelho lembra a propria escolha** (guardada no navegador, nao na
  conta). Celular emprestado nao herda o do computador.
- Quem usava o olhinho antigo com tudo escondido continua com tudo escondido.
- Os botoes nascem **fora** do modulo do Firebase: se o Firebase falhar, ninguem
  fica preso com a tela borrada e sem botao para desborrar.

## A colisao de versoes

A primeira entrega foi montada sobre `2026-09-10-foto-parceiro`. No mesmo dia
**outra conversa** entregou o card "Seu nivel" (`2026-09-10-niveis`) — e foi essa
que subiu, apagando os olhinhos. Refeito como juncao das duas, sobre o arquivo
que estava no ar. Ver [[ARQ - Incidente - colisao de entregas no painel do parceiro]].

## Validacao

34 verificacoes: nascem 6 botoes, os tres escopos sao independentes, botoes do
mesmo escopo mudam o icone juntos, a escolha volta ao recarregar e a migracao do
olhinho antigo funciona nos dois sentidos. Renderizado em 360, 390, 768 e 1440 px
sem rolagem lateral.

## Ligacoes

[[A5 - Programa de Parceiros]] · [[P19 - Plano de niveis do parceiro]] ·
[[ARQ - Foto do parceiro e o CORS da pagina de verificacao]]
