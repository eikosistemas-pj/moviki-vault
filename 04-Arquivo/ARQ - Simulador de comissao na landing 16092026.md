---
type: decisao
status: concluido
area: A3 - Marketing e Aquisicao
tags: [conformidade, parceiros, simulador, landing, meta, conar]
atualizado: 2026-09-16
---

# ARQ - Simulador de comissao na landing 16092026

Decisao de 16/09/2026 sobre **como mostrar a escala do programa sem projetar
ganho**. Fecha a discussao aberta em
[[ARQ - Incidente PDF de parceiros com projecao de ganho 16092026]].

---

## O pedido e o problema

O grafico do `parceiros.pdf` (R$ 57 / R$ 171 / R$ 284 por 10, 30 e 50 lojistas)
existia **de proposito**: mostrar ao parceiro a escala do que o programa pode
virar. O objetivo e legitimo e o instrumento estava errado.

A diferenca nao e de redacao:

| | |
| --- | --- |
| **O anunciante afirma** "com 30 lojistas voce recebe R$ 171 por mes" | promessa de ganho |
| **O visitante escolhe 30** e a pagina aplica o percentual publicado | ferramenta de calculo |

No primeiro caso o numero e da Moviki. No segundo, e da pessoa. Meta, CONAR e o
CDC (art. 37) tratam os dois de forma diferente, e o segundo e o que sobrevive a
uma conferencia.

> **"Esta escondido" nao e protecao.** O PDF publico no proprio dominio e
> material da marca com ou sem link, e quem cobra a conta primeiro nao e a Meta:
> e o parceiro que entrou por causa do numero, nao chegou nele e guardou o
> arquivo. O grafico e exatamente a prova que ele levaria.

## O que foi feito

O grafico **nao voltou** ao PDF. Em vez disso, a landing publica
`parceiros-ganhos.html` ganhou o simulador — que **ja existia no painel do
parceiro** (`parceiro.html`, funcao `barras`) e estava atras do login, ou seja,
so era visto por quem ja tinha entrado.

**O instrumento certo estava no lugar errado.**

### Como funciona

- Abas Pro / Premium / Enterprise, com o preco de cada um
- Tres barras: indicados diretos, nivel 2 e nivel 3
- A escada de niveis REAL do Regulamento: 15% ate Prata, **16% Ouro, 17%
  Diamante, 18% Esmeralda**. Ao passar de 25 indicados, a legenda muda sozinha e
  anuncia o nivel novo — e este e o gatilho de progressao que o grafico estatico
  nunca teve
- Duas caixas **separadas**: recorrente (nivel 1) e bonus unico (niveis 2 e 3).
  Nunca somadas num numero so, porque nivel 2 e 3 sao pagos uma vez
- **Tudo comeca em zero.** Se a tela abrisse com um numero ja posto, seria a
  Moviki afirmando aquele resultado — e voltaria a ser projecao
- Fecha com: "E a regra acima aplicada aos numeros que voce escolheu. Quantas
  pessoas vao assinar pelo seu link e continuar pagando nao depende desta tela —
  pode ser zero."
- O aviso legal completo da pagina fica **imediatamente abaixo**, de proposito

### Por que converte mais que o grafico

O grafico do PDF era estatico e estava num arquivo que quase ninguem abre. O
simulador esta na pagina que os anuncios levam, **exige um gesto** (arrastar) e
o numero que aparece e o da propria pessoa — que e mais persuasivo que qualquer
numero que a marca escreva, e nao pertence a marca.

## A regra que fica

> **Numero que projeta ganho, quem escolhe e o visitante.** A marca publica o
> percentual e a regra; a conta e feita na tela, com o valor que a pessoa moveu,
> e sempre acompanhada de "pode ser zero". Nenhum material da Moviki — pagina,
> PDF, imagem, video ou criativo — afirma quanto alguem vai receber.

## Manutencao

⚠️ **A conta esta escrita em dois lugares:** `moviki-app/parceiro.html` (painel)
e `moviki/parceiros-ganhos.html` (landing). Percentual que mudar no Regulamento
tem que mudar nos dois, senao a landing promete uma conta que o robo nao paga.

## Pendencias

- [ ] Medir o uso do simulador: o evento `simulador_plano` ja dispara no
      `mvEv` quando a pessoa troca de aba
- [ ] Avaliar levar o mesmo simulador para a `parceiros.html` (hoje ela tem
      canonical para a `parceiros-ganhos.html` e so a tabela estatica)
- [ ] Conferir o PDF do prompt de atendimento na base da Meta com o mesmo
      criterio
