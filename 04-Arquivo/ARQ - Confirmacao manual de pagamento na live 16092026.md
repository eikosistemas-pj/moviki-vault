---
type: decisao
status: no ar
area: A13 - Modo Live
tags: [live, pix, checkout, confirmacao]
atualizado: 2026-09-16
---

# ARQ - Confirmacao manual de pagamento na live 16092026

## O problema

No modo **chave Pix do lojista** não existe gateway a quem perguntar se o Pix
caiu: `confirmarNoAsaas` devolve `erro` nesse modo, por desenho. Quem confirma é
o lojista, olhando o extrato pelos **centavos identificadores**.

A tela do comprador, porém, dizia: *"Esta tela confirma sozinha quando o
pagamento cair."* Nunca confirmava. O comprador pagava, ficava até 30 minutos
olhando "Esperando o pagamento…" e no fim lia *"O prazo deste Pix passou"* —
depois de já ter pago. E não havia botão nenhum que avisasse o lojista.

Sintoma no painel: **"Pedidos pagos hoje 0"** com o dinheiro na conta.

## A ideia descartada: comprovante pelo chat

O comprovante de Pix é o documento mais falsificado do Brasil; o chat é público
e exporia dado pessoal do comprador; imagem no chat abre um vetor que a
moderação de texto não cobre; e a mensagem some no rolar.

**Não é preciso comprovante:** os centavos são únicos por pedido. O lojista
procura o valor exato no extrato — prova de dinheiro recebido, não de papel.

## O que ficou

O backend **já tinha tudo**: `compra_paguei` (inclusive com comprovante
opcional, validado pelos bytes e guardado como anexo privado), `loja_pedido`
aceitando `pago`, e `pix.centavosUnicos`. Faltava só tela.

1. Comprador paga e toca em **"Já paguei"** → status `conferindo`, aviso ao
   lojista. Comprovante é **opcional** e vai como anexo privado, nunca no chat.
2. Estúdio: aviso **por cima da tela**, com o valor grande, nome, número do
   pedido e a frase *confira este valor exato no seu extrato*. Botões
   **Recebi**, **Ver comprovante** e **Depois**.
3. A tela do comprador vira "Pagamento confirmado" sozinha — o polling já existia.
4. O texto passa a dizer a verdade conforme o modo.

Corrigido junto: **"Conferir pagamento"** aparecia para pedido aguardando mesmo
no modo chave própria, onde sempre responderia "ainda não caiu".

## O que isso custa, e foi aceito

O "Recebi" **confia no lojista** — o Moviki não vê a conta dele. Logo,
"Vendido pelo Pix" depende de ele clicar: lojista relapso mostra venda menor do
que teve, e isso contamina a conversão do funil.

## Ligacoes

[[A13 - Modo Live]] · [[R - Checkout - tres modos]] · [[R - Regras de ouro]] ·
[[ARQ - Teste de fumaca da live executado 16092026]]
