---
type: arquivo
status: concluido
area: "[[A1 - Produto e Paineis]]"
tags: [vik, catalogo, conformidade, planos, financeiro, live, entrega]
atualizado: 2026-09-16
---

# ARQ - Vik atualizado para venda ao vivo e Pix 16092026

Fecha a rodada aberta em [[ARQ - Porta de entrada do app no eixo da live 16092026]].
O painel subiu para `2026-09-16-quizlive1`; o Vik sobe junto, como manda a
regra de ouro. Ao abrir o catalogo para trocar a marca, apareceu bem mais que
uma linha desatualizada.

## O buraco que estava aberto ha dois dias

A aba **Financeiro** esta no ar desde 14/09 — menu lateral, grade Ferramentas,
chave Pix, termo de venda, lista de pedidos. **O catalogo do Vik nao tinha uma
unica linha sobre ela.** O Vik nao sabia que o cardapio passou a vender, nem o
que responder sobre um pedido, um centavo identificador ou uma chave Pix.

O modo cauteloso estava ligado (marca divergente) e fez o que devia: impediu o
Vik de NEGAR a aba. So isso.

> **O modo cauteloso protege contra a resposta errada, nao contra a resposta
> ignorante.** Ele compra tempo; nao substitui a atualizacao do catalogo.

## Tres erros de plano corrigidos — dois deles em canal de venda

1. **`catalogoPainel.js`** dizia que no teste gratis a live entra *"em nivel
   Pro"*. O `api/live.js` entrega **Premium** (60 min, sacolinha de 5), e quem
   assina o **Pro** depois do teste **perde a live**. O catalogo agora diz isso
   com todas as letras.
2. **`promptAtendimento.js`** (o robo que fala no WhatsApp e no Meta) dizia
   *"Galeria de fotos (a partir do Pro)"* e *"Avaliacoes de clientes (a partir
   do Premium)"*. As duas ao contrario: **fotos sao Premium, avaliacoes sao de
   TODOS os planos**. Estava vendendo o que o plano nao tem e escondendo o que
   ele ja tem.
3. **`oportunidade.js`** oferecia o upgrade Pro -> Premium vendendo
   *"avaliacoes de clientes na pagina"*. Avaliacoes ja estao no Basico: a
   proposta vendia o que a pessoa ja tinha. Trocada pelo que o Premium abre de
   verdade hoje — Modo Live e venda pelo cardapio com Pix.

## O que entrou de conhecimento novo

**PRODUTO** (vale para os dois paineis)
- Premium ganhou a venda pelo cardapio; Enterprise, o Pix dentro da live.
- Bloco novo **"COMO O DINHEIRO DA VENDA ANDA"**: os dois modos de
  recebimento (Pix direto sem taxa, minimo R$ 5 · Asaas a R$ 1,99 por Pix,
  minimo R$ 20), so Pix, sem frete calculado pelo Moviki, e o dinheiro nunca
  passando pela conta da Eiko.
- **As duas caras do teste gratis**, que ja confundiram gente: na live ele e
  Premium; na venda pelo cardapio ele nao entra.
- A aba Financeiro **nao tem cadeado** — abre em qualquer plano. O que pede
  Premium ou Enterprise pago e o botao "Ligar a venda".

**LOJISTA**
- Financeiro no menu e na grade.
- Secao nova descrevendo os tres blocos da aba, campo por campo, lida do HTML
  publicado — inclusive por que a chave Pix volta so como mascara, por que o
  nome e o documento do titular aparecem para o cliente, e por que pedido
  expirado ainda pode ser confirmado.
- As mensagens de erro reais da tela e o que cada uma quer dizer.
- Seis erros comuns novos, do tipo que chega no Vik: "cadastrei a chave e nao
  aparece nada", "o cliente pagou e o pedido nao mudou sozinho", "cobraram
  centavos a mais", "meu produto nao tem botao de comprar".

**PARCEIRO**
- O que ele pode prometer ao lojista no eixo novo, com as tres travas de plano
  escritas como frase pronta — e a proibicao de prometer faturamento ou
  audiencia na live.

**O QUE NAO EXISTE** (lista fechada) ganhou sete itens: venda pelo cardapio no
Basico, no Pro e no teste gratis; Pix na live fora do Enterprise; cartao e
boleto no checkout do cliente; frete pelo Moviki; o Moviki receber ou guardar
dinheiro de venda; e comissao do Moviki sobre a venda.

## Conferido

`node --check` nos tres arquivos, os quatro modulos carregando,
`lib/segurancaVik.test.js` com **0 falhas**, e `avisoVersao` testado nos dois
sentidos: marca nova devolve vazio, marca velha liga o modo cauteloso.
Nenhum simbolo exportado perdido. LF sem BOM, zero byte de controle.

## Ligacoes

[[R - Marcas de versao - Vik e painel 16092026]] ·
[[ARQ - Porta de entrada do app no eixo da live 16092026]] ·
[[ARQ - Reposicionamento da home para live commerce 16092026]]
