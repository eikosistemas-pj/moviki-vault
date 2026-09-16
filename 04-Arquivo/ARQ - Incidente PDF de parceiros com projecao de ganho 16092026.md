---
type: incidente
status: concluido
area: A3 - Marketing e Aquisicao
tags: [conformidade, meta, conar, pdf, parceiros, incidente]
atualizado: 2026-09-16
---

# ARQ - Incidente PDF de parceiros com projecao de ganho 16092026

**Achado em 16/09/2026, por acaso**, enquanto eu rastreava onde as imagens de
preco vivem. O arquivo `parceiros.pdf`, publico na raiz do repo `moviki` e
acessivel em `moviki.com.br/parceiros.pdf`, **projetava ganho com numero**.

Relacionado: [[ARQ - Fecho da troca de precos 16092026]] ·
[[R - Regras de ouro]] · [[P37 - Prospeccao de parceiros e influenciadores]]

---

## O que estava escrito

Um grafico de barras, com titulo **"Quanto da pra ganhar"**:

| | |
| --- | --- |
| 10 lojistas / mes | **R$ 57** |
| 30 lojistas / mes | **R$ 171** |
| 50 lojistas / mes | **R$ 284** |

Legenda: *"So com indicacoes diretas (nivel 1), em lojistas no plano Pro —
**recorrente, todo mes**"* e *"Valores de exemplo (15% de R$37,90 por lojista
Pro). **Planos maiores rendem mais.**"*

E, no resto das tres paginas, mais dez ocorrencias do vocabulario proibido:

- "Indique o Moviki e **ganhe** todo mes"
- "**Renda recorrente de verdade**"
- "**Ganho recorrente**" (titulo de bloco)
- "Enquanto o lojista pagar, voce **ganha** todo mes"
- "Indicou 10, 30, 50 lojistas? **A renda vai somando** mes apos mes"
- "veja sua **renda crescer**"

## Por que e grave

> **A regra e descrever a REGRA, nunca o RESULTADO.** Um numero que diz quanto
> a pessoa vai receber por uma quantidade de indicacoes e projecao de ganho,
> mesmo rotulado como "valores de exemplo". A palavra "renda" e "recorrente,
> todo mes" ao lado de um numero fecham a violacao.

Politica da Meta sobre produtos financeiros e oportunidades de ganho, e Codigo
do CONAR (atualizado em 2026 para conteudo comissionado). Um PDF publico no
proprio dominio e material da marca: se a conta de anuncios for revisada, ele
conta. **Nao adianta a landing estar limpa se o PDF linkado dela nao esta.**

Agravante: o PDF **nao e linkado de nenhuma pagina**. Estava solto na raiz,
circulando por WhatsApp e impressao — invisivel para qualquer conferencia que
olhasse so o HTML. Foi por isso que passou em todas as auditorias anteriores.

## O que foi feito

`parceiros.pdf` **refeito do zero**, 3 paginas A4, sob a autorizacao permanente
de corrigir violacao de Meta ou Google sem pedir permissao.

| Antes | Depois |
| --- | --- |
| "Indique o Moviki e ganhe todo mes" | "Indique o Moviki. A comissao e recorrente." |
| "Renda recorrente de verdade" | "uma parte dela e a sua comissao, a cada mes em que ele continuar sendo cliente pagante" |
| Bloco "Ganho recorrente" | Bloco "Comissao recorrente" |
| Bloco "Cresce sozinho / a renda vai somando" | Bloco "Tres niveis" |
| Grafico R$57 / R$171 / R$284 | **Tabela de regra**: plano x comissao (0,00 / 5,99 / 10,49 / 19,49) |
| "Planos maiores rendem mais" | removido |
| "veja sua renda crescer" | "Acompanhe e saque por Pix" |

Acrescentado: as seis regras que valem, o bloco **"Divulgacao e publicidade"**
com a instrucao de `#publi` do CONAR, e o fecho:

> "Isto e a regra de calculo, nao uma previsao. Quantas pessoas vao assinar e
> continuar pagando nao depende desta tabela — pode ser zero. O Moviki nao
> promete rendimento, retorno ou resultado de nenhum tipo."

Conferido no texto extraido do PDF novo: **zero ocorrencias** de renda, ganhe,
ganha, ganho, rende ou rendem.

`comerciantes.pdf` tambem foi refeito — nao tinha violacao, mas estava com
preco velho (37,90 / 49,90 / 99,90) e sem o Modo Live.

## A regra que fica

> **Arquivo binario publico e material da marca, mesmo sem link.** PDF, imagem
> e video na raiz de um repositorio publico nao aparecem em busca de texto, nao
> quebram nada e nao entram em nenhuma conferencia de HTML — e e exatamente por
> isso que sao onde a violacao sobrevive por mais tempo. Toda auditoria de
> conformidade precisa listar os binarios do repositorio, nao so as paginas.

## Pendencia que isto abre

- [ ] Conferir o **PDF do prompt de atendimento** que esta na base de
      conhecimento do robo na Meta — mesma origem, mesma epoca, mesmo risco
- [ ] Conferir os **4 videos** de `moviki-app/material/` com o mesmo criterio:
      audio e legenda nao aparecem em grep
- [ ] Decidir se os dois PDFs devem ser linkados de alguma pagina ou sair da
      raiz publica
