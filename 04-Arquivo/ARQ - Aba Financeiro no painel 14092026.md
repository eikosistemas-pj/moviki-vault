---
type: arquivo
status: concluido
area: "[[A13 - Modo Live]]"
tags: [financeiro, painel, pix, termo, seguranca]
atualizado: 2026-09-14
---

# Aba Financeiro no painel do lojista — 14/09/2026

Terceira entrega da [[P31 - Financeiro e cardapio compravel]]. Agora o lojista
tem tela. Continua [[ARQ - Checkout em dois modos 14092026]] e
[[ARQ - Portas separadas do checkout 14092026]].

## Arquivos

| Repositorio | Arquivo | Marca | Tipo |
|---|---|---|---|
| moviki-robo | `lib/checkout.js` | 2026-09-14-aceite | SUBSTITUI |
| moviki-app | `index.html` | 2026-09-14-financeiro | SUBSTITUI |

Montado sobre a marca `2026-09-13-vikpainel`, que era a que estava no GitHub.

## A regra que a propria regra do Firestore ditou

A aba **nao grava nada em `negocios/{uid}`**. O `hasOnly` de `negocioValido()`
nao conhece campo do Financeiro, e o comentario da propria regra avisa: campo
fora do `hasOnly` faz **todo** save do painel ser negado — cardapio, fotos,
promocoes, eventos, tudo. Um campo `vendaAtiva` ali teria quebrado o painel
inteiro, com o sintoma aparecendo longe da causa.

Tudo passa pelo `/api/financeiro`, que escreve em `recebimento/` com Admin SDK.

## O que tem na aba

1. **Como voce recebe** — os dois modos lado a lado, com o custo escrito em cada
   um: Pix direto grátis com confirmacao sua, ou Pix automatico do Asaas a
   R$ 1,99 por Pix. Formulario da chave Pix (chave, titular, cidade, documento)
   ou campo da chave de API do Asaas.
2. **Ligar a venda** — forma de entrega, Termo de Venda e o interruptor.
3. **Vendas** — os pedidos em tempo real, com Confirmar, Recusar, Marcar
   entregue, Ver comprovante e WhatsApp do cliente.

Entra pelo menu lateral **e** por um cartao em Ferramentas, com icone SVG
proprio (nao depende de PNG que ainda nao existe).

## Termo de Venda versionado — e no servidor

O `lojaModo` passou a **exigir o aceite** antes de ligar a venda, com versao
(`2026-09-14`) gravada em `recebimento/{uid}.termo` e registrada na trilha.
Aceite que vive so no checkbox nao prova nada; por isso a barreira esta no
servidor, nao no botao. Quando o termo mudar de versao, quem aceitou a anterior
reaceita antes de voltar a vender.

O aceite e a **ultima** porta da validacao, depois de chave e conta: assim, o
lojista que ainda nao cadastrou a chave recebe a mensagem sobre a chave, e nao
uma sobre termo.

O texto cobre o que a decisao de 14/09 fixou: a venda e do lojista, o dinheiro
vai direto para a conta dele, ele responde por entrega, atendimento, CDC art. 49
e impostos, produto proibido bloqueia a venda, e no Pix direto quem confirma o
pagamento e ele — o Moviki nao ve o extrato de ninguem.

## Duas correcoes que sairam do teste visual

- **O botao "Salvar tudo" some na aba Financeiro.** Ele salva o CADASTRO do
  negocio e nao tem nada a ver com o Financeiro, que grava pelo endpoint em cada
  botao proprio. A vista, faria o lojista achar que precisa clicar nele para a
  chave Pix valer — e sair da tela sem clicar em "Salvar chave Pix".
- **O termo ganhou altura e uma dica de rolagem.** Cortado no meio da quarta
  linha, parecia texto truncado em vez de caixa rolavel.

## Lista de vendas sem indice composto

A consulta e so por igualdade (`lojistaUid`), com `limit(200)`, e a ordenacao
por data acontece no navegador. `where` + `orderBy` em campos diferentes exigiria
indice composto — que nao existe e **falharia calado na primeira venda**.

Divida registrada: acima de 200 pedidos por negocio, criar o indice no console e
trocar a consulta.

## Conferido

- Sintaxe do modulo inteiro valida.
- Balanceamento de `<div>` identico ao do arquivo original.
- Renderizado em 390x900 e 1100x1000 com Chromium: sem rolagem lateral.
- `index.html` entregue com **BOM + CRLF** — sem isso o navegador do Paulo
  bloqueia HTML com script dentro.

## Falta para a Fase 1 fechar

- Cardapio compravel nas paginas publicas (`moviki/404.html` e o app), com o QR
  desenhado pelo `mvqr.js` a partir do copia-e-cola que o servidor manda.
- Icones PNG 3D de Financeiro, Vender e Vendas (hoje caem no emoji por
  `onerror`, que e degradacao limpa).
- Aulas 07R, 08R e 14, que so podem ser gravadas com as telas no ar.
