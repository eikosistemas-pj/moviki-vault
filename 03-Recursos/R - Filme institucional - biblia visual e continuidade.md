---
type: recurso
status: referencia
area: A8 - Conteudo e Social
tags: [video, marca, armadilha]
atualizado: 2026-08-31
---

# R — Filme institucional: biblia visual e continuidade

O que precisa se manter igual entre uma cena e outra. Ler antes de gerar
qualquer take novo ou refazer qualquer cena.
Projeto: [[P13 - Video institucional da landing]].

## Regra que originou este documento

**Nenhuma geracao antes da biblia escrita e aprovada.**
As tres primeiras variacoes de C01 foram rejeitadas em bloco porque a direcao de
arte foi escrita e mandada gerar sem validacao humana previa. O custo dessa
rodada foi de mais de 200 creditos.

## Personagens canonicos

| ID | Quem | Aparece em | Trava |
| --- | --- | --- | --- |
| `MV-Rita` | Mulher, 38, brasileira parda, cabelo preso, avental de trabalho gasto sobre camiseta simples | C01, C05, C08, C11 | rosto, cabelo, avental, maos |
| `MV-Nando` | Homem, 27, brasileiro negro, roupa casual de fim de expediente, mochila | C03, C04, C09, C10, C11 | rosto, cabelo, roupa, mochila |
| `MV-Caio` | Figuracao de fila e rua | C11 | so silhueta |

**Regra dura:** o cliente que procura em C03/C04 e **o mesmo** que encontra em
C09 e que e atendido em C11. Se o rosto mudar, o filme perde o unico arco
narrativo que tem.

## Carrinho / trailer

Trailer branco compacto, luzes de corda tungstenio quente, janela de
atendimento, balcao. **Mesmo veiculo em C01, C05, C08 e C11.**

**Autenticidade nao significa precariedade.** Regra criada na correcao de C12:
o negocio precisa parecer cuidado, limpo e bem montado — nao improvisado nem
pobre. Vender para quem se move nao e vender para quem esta mal.

## Biblia de luz — 3 estados

| Estado | Quando | Descricao |
| --- | --- | --- |
| **L1 — Dourada residual** | C01 | contraluz quente ao fundo, praticas do trailer acendendo durante a tomada |
| **L2 — Hora azul** | C04, C05, C06, C07 | ceu azul profundo, praticas quentes isoladas, asfalto frio |
| **L3 — Noite fechada** | C11, C13 | so praticas quentes e luz urbana; ceu quase preto |

**O ciano nunca vem da fotografia.** Nenhuma luz pratica ciano em cena gerada —
o ciano so existe na camada grafica. E o que faz o espectador ler o ciano como
"a Moviki agindo sobre o mundo".

## Lei da continuidade em image-to-video

**O `first_frame` governa a POSICAO. O prompt so governa o MOVIMENTO a partir
dela.**

Consequencia pratica: nao adianta descrever no prompt onde as coisas estao. Se o
enquadramento esta errado, o conserto e o keyframe, nunca o prompt. Foi assim
que o metodo estabilizou em **keyframe still -> aprovacao humana ->
image-to-video -> inspecao humana -> proxima cena**.

## Armadilhas de geracao ja pagas

- **Nao existe simulacao de corpo rigido.** Objeto que atravessa objeto nao se
  conserta por prompt. Em C01, a bandeja atravessou o poste em tres takes; a
  unica solucao foi **remover a bandeja da cena**. Regra derivada: **objeto
  manipulado fica abaixo da linha do balcao, ou nao entra.**
- **`nano-banana-pro` rejeita `negative_prompt`** (400 VALIDATION_ERROR).
  As negativas entram no corpo do prompt como `STRICTLY AVOID: ...`.
- **Veo aceita 4, 6 ou 8 segundos. 5 s nao existe.** Toda duracao fracionada do
  roteiro vira 4, 6 ou 8 e se ajusta na montagem.
- **Nunca gerar variacao automaticamente.** Uma cena por vez, parada para
  inspecao humana.
- **Nao usar o primeiro nem o ultimo 0,3 s** de nenhum take gerado.

## Prioridade que governa toda decisao

> **QUALIDADE CINEMATOGRAFICA > CONSISTENCIA > EFICIENCIA DE CREDITOS > VELOCIDADE**

E o corolario operacional:

> **Buscar antes de pedir. Usar o oficial antes de recriar. Produto real antes
> de mockup. Precisao antes de velocidade.**

## Ligacoes

[[R - Roteiro do video institucional]] · [[ARQ - Armadilhas de geracao por IA]] ·
[[P13 - Video institucional da landing]] · [[A11 - Marca e Design System]]
