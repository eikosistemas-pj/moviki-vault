---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, teste, fumaca, cloudflare]
atualizado: 2026-09-16
---

# ARQ - Teste de fumaca da live executado 16092026

Primeiro teste de fumaça completo do Modo Live, feito com **dois celulares e um
computador**, conta `karina` (CALDEIRÃO NORDESTINO) em Enterprise. Roteiro em
[[R - Teste de fumaca da live]].

## O que passou

- Nível e limite corretos ponta a ponta: servidor devolveu `limiteMin:180`,
  tela mostrou **3 h**.
- Transmissão, imagem e áudio em 5 telas simultâneas; contador bateu 5 de 5.
- Chat, oferta relâmpago com contador, cupom, sacolinha e fixar.
- **Pix pago de verdade, dinheiro na conta** — depois do conserto do checkout.
- QR Code na tela junto do copia-e-cola.
- Encerrar e reabrir sem esbarrar no freio.

## O que o teste revelou

Quatro regressões da migração b5b — [[ARQ - Regressoes da migracao b5b 16092026]].
Todas encontradas **por percorrer o fluxo até o fim**: o Pix só apareceu porque
se chegou à tela de gerar o QR.

Mais: no modo chave Pix própria **não existe confirmação automática**, e a tela
prometia que confirmava sozinha — ver
[[ARQ - Confirmacao manual de pagamento na live 16092026]].

## O que NAO foi testado

| Pendencia | Por que |
| --- | --- |
| Live em **4G** | sinal fraco dentro de casa daria falso negativo |
| **Carga real** (30 espectadores) | abas do mesmo IP não são concorrência |
| Limite de **3 h** | exige uma live de uma hora |
| Cota do teste grátis (2 lives) | exige 15 min de carência entre as tentativas |
| B4, B7 | só aparecem com requisição forjada |

## Parametro calibrado

Teto de vídeo do ciclo baixado de **50.000 para 12.000 minutos** entregues
(ciclo dia 12). 50.000 = US$ 50/mês, cerca de 60% da receita estimada de um mês
sem cliente pagante nenhum. 12.000 cobre o uso máximo teórico dos planos que
hoje têm live.

**O teto é global da conta, não por lojista** — um lojista pode consumi-lo
sozinho e travar a live dos outros, sem aviso. O teto por plano
(Premium 1.500 / Enterprise 5.000 / trial 300) **não existe**.

## Ligacoes

[[A13 - Modo Live]] · [[R - Teste de fumaca da live]] ·
[[P - Abertura da live para lojista pagante]]
