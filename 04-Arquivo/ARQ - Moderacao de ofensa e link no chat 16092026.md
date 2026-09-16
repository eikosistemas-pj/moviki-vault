---
type: decisao
status: no ar
area: A13 - Modo Live
tags: [live, moderacao, chat, seguranca, conformidade]
atualizado: 2026-09-16
---

# ARQ - Moderacao de ofensa e link no chat 16092026

## Dois filtros, nao um

`mvProibido` roda também no **nome de produto**, oferta, cupom e sacolinha: é o
filtro do que não pode ser **vendido** (conformidade Meta e Google). Jogar
palavrão na mesma lista impediria o lojista de cadastrar **"galinha caipira"**.

Por isso a moderação de ofensa entrou como **`mvOfensa`, lista separada, só no
chat** — texto e nome, de qualquer autor, o dono da live inclusive.

## A curadoria da lista

Lista de 388 termos trazida pelo Paulo (gerada por outra IA, no modelo das
plataformas de live). **30 termos retirados** por colidirem com o público do
Moviki:

- Comida: **delicia**, **gostoso/gostosa** (os dois comentários mais comuns numa
  live de comida), **galinha**, **pinto**, **pau** (pau-de-arara), **grelo**,
  **molhadinho**, **meter** ("meter no forno"), **bater uma** ("bater uma massa")
- Comércio: **banca** (o feirante trabalha numa), **rodada**, **oferecida**,
  **sob** (preposição: "sob encomenda"), **lixo**, **vergonha**
- Região: **paraiba** — a lista tratava como xingamento; é onde o dono mora
- Ruído: **mf**, **sob**, **k9**, **spice** (tempero em inglês), **invalido**
  ("CPF inválido"), **autista**, **mongol**

Ficaram **358**. O caso real do teste — *"Oi delícia quero te comer"* — cai pela
frase "quero te comer", sem precisar bloquear "delícia".

## Ofuscacao

Além do texto normalizado (minúsculas, sem acento, leet), `mvOfensa` confere uma
cópia com as letras soltas juntadas e colapsa letra repetida. Pega `p.u.t.a`,
`p-u-t-a`, `v.a.i t.o.m.a.r n.o c.u`, `puuuuta`, `c4r4lh0`.

A compactação do texto inteiro só vale para termo de 6+ caracteres, e a busca do
termo sem espaços só em texto reconhecidamente ofuscado — senão **"disputa"**
viraria "puta" e **"cuscuz"** viraria "cu".

Conferido com 48 casos: 24 que devem barrar e 24 de frase legítima de comida.

## Link no chat

O chat não bloqueava endereço nenhum. Numa live de venda, todo mundo ali já veio
com intenção de pagar — link colado por espectador é o vetor de golpe mais
barato que existe, dentro de uma página com a marca do Moviki em volta.

**Agora: link só do dono da live** (`tipo:'dono'`, que só o estúdio autenticado
escreve; a regra do Firestore limita o visitante a `msg` e `quero`). Vale também
na **leitura**, então mensagem gravada antes também para de aparecer.

## Ligacoes

[[A13 - Modo Live]] · [[R - Regras de ouro]] · [[R - Filtro de conteudo da live]]
