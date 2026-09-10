---
type: projeto
status: ativo
prioridade: 2
prazo: 2026-09-30
area: A5 - Programa de Parceiros
tags: [parceiros, comissao, painel, regulamento, conformidade]
atualizado: 2026-09-10
---

# P19 - Plano de niveis do parceiro

> Era `P14` na entrega de 10/09. Renumerado: `P14` ja existe no vault desde
> 03/09 ([[P14 - Verificacao de parceiro]]).

**No ar em 10/09** — conferido nos repositorios: `webhook.js` com
`NIVEIS_PARCEIRO`, `contarAtivosDoMes`, `creditarMarco` e `guardarNivel`;
`parceiro.html` com o card "Seu nivel"; regulamento 1.1 nas duas copias.

## A escada

| Nivel | Diretos pagando no mes | Comissao nivel 1 | Bonus de marco |
| --- | --- | --- | --- |
| Bronze | 1 a 10 | 15% | - |
| Prata | 11 a 25 | 15% | R$ 25 |
| Ouro | 26 a 50 | 16% | R$ 50 |
| Diamante | 51 a 100 | 17% | R$ 150 |
| Esmeralda | 101 ou mais | 18% | R$ 300 |

## A regra que segura tudo

Sobe de nivel quem tem **cliente direto pagando a mensalidade no mes corrente**,
recalculado todo mes. O nivel sobe e desce. **Indicado indireto (nivel 2 e 3) nao
conta** para titulo nem beneficio — contar rede seria classificar por tamanho de
downline, e nao e isso que o programa e. Os bonus unicos de 7,5% e 5% seguem
iguais em qualquer nivel.

O percentual aplicado e o do nivel **no momento em que a mensalidade e
confirmada**; comissao ja creditada nao e recalculada. Falha na consulta cai nos
15% base — nunca trava o pagamento.

`creditarMarco` usa id `marco_{uid}_{nivel}` e `.create()`, entao o bonus e
barrado para sempre mesmo se o parceiro cair de nivel e voltar. Grava
`nivel: 0` e `tipo: 'marco'` para nao entrar na contagem nem no grafico.

## As tres barras voltaram

Saíram em 03/09 por conformidade; voltaram dentro de "Como a sua comissao e
calculada". Quatro diferencas de proposito em relacao ao simulador antigo:

1. **Nenhuma caixa somando tudo** num numero de "previsao do seu 1o saque".
   Recorrente e bonus unico ficam separados.
2. Cada barra conta **assinatura paga**, nao pessoa cadastrada.
3. Zero hierarquia visual entre os niveis.
4. O aviso de "pode ser zero" e o link do Regulamento continuam na tela.

Teto de 200 diretos e 100 indiretos. A barra anda de 1 em 1 ate 20 e de 5 em 5
daqui pra cima — 200 posicoes num trilho de celular dao menos de 2 px por pessoa.
A comissao de UMA assinatura e arredondada antes de multiplicar
(3 x R$ 5,69 = R$ 17,07); somar sem arredondar daria R$ 17,06 e o parceiro leria
como erro.

## Custo

Com todos no Pro (R$ 37,90): Ouro no teto (24 ativos) custa R$ 9,10/mes a mais;
Diamante no teto (49), R$ 37,14; Esmeralda com 50, R$ 56,85. Percentual de
dinheiro que ja entrou, nunca despesa fixa. Os marcos somam R$ 525 se um mesmo
parceiro percorrer a escada inteira.

## Decisoes

- Faixas ampliadas em relacao ao rascunho que comecava Prata em 5: nivel facil
  demais desvaloriza o titulo e antecipa custo.
- Topo encurtado em relacao a proposta 26-100 / 101-200: a 3 clientes por mes,
  ir de 26 a 100 seriam mais de 2 anos no mesmo degrau.
- Beneficio combinado: sem dinheiro nos primeiros, marco no meio, percentual
  maior so no topo.
- Nomes de metal mantidos.

## Em aberto

- [ ] **Revisao juridica do Regulamento** — o texto agora fixa percentual e bonus
      em dinheiro, ou seja, gera obrigacao financeira, e nunca passou por
      advogado. Ver [[P04 - Decisao fiscal do Programa de Parceiros]]
- [ ] Selo do nivel no cracha e na `v.html`
- [ ] Coluna de nivel na tabela de comissoes do painel do dono (`eikoadm01.html`)
- [ ] Saque minimo menor por nivel e prioridade no Vik — hoje o minimo e R$ 20
      para todos
- [ ] Ver o primeiro parceiro real batendo Prata, para o bonus de marco nascer

## Regras de linguagem destas telas

"Comissao maior", nunca "ganhe mais" ou "renda maior". O nivel e reconhecimento
por clientes ativos, nunca "sua equipe cresceu". A barra mostra quantos clientes
faltam, nunca quanto a pessoa vai receber.

## Ligacoes

[[A5 - Programa de Parceiros]] · [[A4 - Financeiro]] ·
[[A10 - Conformidade e LGPD]] · [[ARQ - Regulamento 1.1 nas duas copias]] ·
[[P20 - Conserto do player e liberacao do link]]
