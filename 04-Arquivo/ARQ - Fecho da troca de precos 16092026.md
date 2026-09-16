---
type: arquivo
status: concluido
area: A4 - Financeiro
tags: [preco, planos, documentacao, imagem, material, fecho]
atualizado: 2026-09-16
---

# ARQ - Fecho da troca de precos 16092026

Terceira e ultima rodada da troca de precos de 16/09/2026. Fecha a divida
que nao aparece em tela: **documentacao, teste e imagem.**

Relacionado: [[ARQ - Troca de precos executada 16092026]] ·
[[ARQ - Enterprise sem plano anual 16092026]] · [[R - Planos e precos]]

---

## Varredura final nos quatro repositorios

Rodada com grep nos clones, por todos os valores antigos
(37,90 / 49,90 / 99,90 / 379 / 499 / 134,90 / 5,69 / 7,49 / 14,99).
Alem dos 13 arquivos ja trocados, **sobraram tres**:

| Repo | Arquivo | O que tinha |
| --- | --- | --- |
| `moviki-robo` | `README.md` | tabela de planos com o trimestral, sem o Enterprise |
| `moviki-ai` | `lib/segurancaVik.test.js` | tres frases LEGITIMAS com preco velho |
| `moviki-ai` | `lib/segurancaVik.js` | comentario citando "R$ 37,90/mes" como frase que passa |

**Nenhum dos tres muda comportamento.** Sao o que uma pessoa le para saber o
preco — inclusive eu, numa proxima sessao. Preco velho em README e o tipo de
erro que volta meses depois como se fosse verdade.

O `segurancaVik.test.js` foi executado com os valores novos: **0 falhas**. O
filtro do Vik nao depende do valor, so do padrao de linguagem — mas as frases
de exemplo agora batem com a realidade.

### Falsos positivos confirmados (nao mexer)

`moviki-app/quiz/quiz-segmentos.js` — "Pre-treino (300g), preco 99,90" e produto
de exemplo do quiz. · `moviki-robo/api/webhook.js` — `value: 99.90` num payload
de exemplo em comentario. · `moviki-app/icones/comissoes.png` — icone 3D de
moeda, **sem valor escrito**. Conferido abrindo a imagem.

---

## As duas imagens de preco

Refeitas do zero, **1080 x 1350 em 2x** (4:5, feed do Instagram e Facebook sem
corte), na identidade do site: fundo `#0D1B2A`, ciano `#00D4FF`, verde
`#25e39b`, Poppins.

### `moviki-img-planos.png`
Os quatro planos com os valores novos, o anual de Pro e Premium, o Enterprise
marcado como **sempre mensal**, e a faixa `30 dias gratis · 0% sobre a sua
venda · 7 dias de garantia`.

### `moviki-img-parceiros-comissoes.png`
Tabela plano x comissao direta (0,00 / 5,99 / 10,49 / 19,49), os tres niveis
(15% recorrente, 7,5% e 5% como bonus unico), as cinco regras que valem e os
tres passos.

> **Conformidade:** a peca descreve a REGRA, nunca o resultado. Nenhum numero
> projeta ganho, nenhuma soma, nenhuma multiplicacao. Fecha com "Isto e a regra
> de calculo, nao uma previsao. Quantas pessoas vao assinar e continuar pagando
> nao depende desta tabela — pode ser zero. O Moviki nao promete rendimento."
> Meta e CONAR 2026.

**Onde trocar:** material de apoio do parceiro, WhatsApp, Drive e a base de
conhecimento do robo na Meta. As imagens nao vivem em nenhum dos repositorios —
por isso nao aparecem em busca de texto e por isso circulam com preco velho.

---

## Regra que fica

> **Documentacao e teste sao lugares onde o preco vive.** Nao dao erro, nao
> quebram nada e sao exatamente onde a proxima pessoa vai procurar a verdade.
> Uma troca de preco so termina quando o README bate com o `lib/asaas.js`.

## O que ainda falta desta troca

- [ ] Trocar o PDF do prompt de atendimento na base da Meta
- [ ] Conferir as 81 pecas do material de apoio do parceiro, uma a uma
- [ ] Atualizar a secao 2 do `MAPA-MESTRE.md`
