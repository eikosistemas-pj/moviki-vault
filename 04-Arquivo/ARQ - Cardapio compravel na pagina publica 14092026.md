---
type: arquivo
status: concluido
area: "[[A13 - Modo Live]]"
tags: [financeiro, cardapio, checkout, pix, pagina-publica, entrega]
atualizado: 2026-09-14
---

# ARQ - Cardapio compravel na pagina publica 14092026

Quarta entrega da [[P31 - Financeiro e cardapio compravel]] e o item 7 da ordem
de execucao. Fecha o lado do comprador: o dinheiro agora tem por onde entrar.
Continua [[P31 - Checkout em dois modos]], [[ARQ - Portas separadas do checkout 14092026]]
e [[P31 - Aba Financeiro no painel do lojista]].

## Arquivos

| Repositorio | Arquivo | Marca | Tipo |
|---|---|---|---|
| moviki | `404.html` | 2026-09-14-compra1 | SUBSTITUI |

Montado sobre a marca `2026-09-11-live1`, que era a que estava no GitHub.

## O que o lojista relatou, e por que nao era bug

Chave Pix cadastrada na aba Financeiro e nada aparecendo na pagina publica. Era
o esperado: a aba Financeiro e o item 6 da ordem; a pagina publica e o 7, e nao
existia. Nenhuma linha de compra existia no `404.html` ate esta entrega.

## Duas descobertas que mudaram o plano

- **`sku` nao era bloqueio.** O `acharNoCardapio` do `lib/checkout.js` casa por
  `sku` **ou**, quando ele nao existe, pelo nome normalizado sem acento. Cardapio
  antigo vende hoje, sem `sku`, sem regra v24 e sem mexer no painel. Divida
  registrada: dois produtos de mesmo nome em categorias diferentes casam com o
  primeiro — o `sku` continua sendo a correcao definitiva.
- **A colecao publica e `checkout_publico`, nao `recebimento_publico`.** O plano
  de 14/09 escreveu um nome e o codigo entregue usa outro. A pagina le
  `checkout_publico/{uid}` — `{ativo, modo, minimo, entrega}` —, que ja tem
  leitura publica desde as regras **v23**. Ler o nome do plano daria exatamente
  o sintoma de "nada aparece", sem erro nenhum no console.

**Nenhuma regra nova do Firestore.** A v24 continua pendente, mas nao bloqueia
mais nada desta fase.

## O interruptor

So existe tela de compra quando `checkout_publico/{uid}.ativo === true`, o
negocio esta no Premium ou Enterprise e `vendaAtiva` nao e `false`. Fora disso a
pagina e byte a byte a de ontem: sem botao, sem sacola, sem rodape novo.
Conferido no teste — cardapio inteiro, zero elemento novo.

## O que o comprador ve

1. **Adicionar** em cada item com preco numerico valido. "a partir de 30", "sob
   consulta" e campo vazio continuam no cardapio, sem botao, com uma linha
   dizendo para chamar no WhatsApp.
2. **Barra da sacola** presa no rodape da folha do cardapio — fora do corpo
   rolavel de proposito: dentro dele ela sumiria no meio da lista.
3. **Uma folha de pedido com tres telas** (revisao, dados, pagamento). Telas em
   folhas diferentes fariam o comprador perder o pedido ao voltar.
4. **Pagamento**: valor com os centavos identificadores, copia-e-cola com botao
   de copiar, e o quadro **Confira antes de pagar** com nome e documento
   mascarado do recebedor.
5. **Ja paguei**, com comprovante opcional reduzido no proprio navegador antes de
   subir — o servidor recusa acima de ~1,7 MB e foto de celular passa disso.
6. **Status em tempo real** a cada 8 s; quando o lojista confirma, a tela troca
   sozinha e a sacola esvazia.

## O que a pagina NAO faz, de proposito

- **Nao calcula preco.** Manda `sku`/nome e quantidade; quem soma e o servidor,
  lendo o cardapio do lojista. Conferido no teste: nenhum campo `preco` sai do
  navegador.
- **Nao monta o codigo Pix.** O copia-e-cola vem pronto do servidor.
- **Nao escreve nada no Firestore.** Tudo passa por `api/pedido.js`.

## O QR ficou de fora, e por que

O `mvqr.js` cobre as versoes **1 a 6**, nivel M — teto de 108 bytes. Um BR Code
Pix real fica entre **130 e 190 bytes**, mesmo com chave curta: **nao cabe em
nenhum caso**. Pendura-lo assim geraria `null` em toda venda.

Subir o QR exige estender o gerador para as versoes **7 a 10**, o que traz tres
coisas novas: tabela de blocos, **contador de 16 bits** a partir da v10 e o
**bloco de version info** (18 bits BCH nos cantos), obrigatorio da v7 em diante.
Nao ha biblioteca de referencia neste ambiente (PyPI e npm recusam), entao a
validacao teria de repetir o metodo do cracha: decodificador independente. E uma
rodada propria — [[P32 - QR do Pix no cardapio]].

Enquanto isso, **copia-e-cola e o caminho certo no celular**: ninguem aponta a
camera para a propria tela. No modo Asaas o QR ja aparece, porque ali a imagem
vem pronta do gateway.

## Rede

`connect-src` da CSP ganhou `https://moviki-robo.vercel.app`, que e a porta
publica. Sem isso o navegador bloquearia o POST sem erro visivel na tela.

## Conferido fora do ar

Chromium, 390x900 e 1100x1000, 37 verificacoes por tela, todas passando:
botao so no item com preco valido · indice do produto e o da lista ORIGINAL (o
filtro renumerava e o pedido apontaria para outro item) · totais da sacola ·
nome, WhatsApp, CPF, endereco e aceite cobrados antes do envio · total e
recebedor vindos do servidor · nenhum preco no corpo da requisicao · aviso de
pagamento · confirmacao chegando pelo polling · **negocio sem o interruptor: zero
elemento novo na tela** · nenhum erro de JavaScript · sem rolagem lateral.
Sintaxe do modulo inteiro valida e balanceamento de `<div>` conferido contra o
arquivo original.

## Falta para a Fase 1 fechar

- QR do Pix no cardapio ([[P32 - QR do Pix no cardapio]]).
- `sku` gerado pelo painel e regras v24 (`vendaAtiva` e `sku`).
- Icones PNG 3D de Financeiro, Vender e Vendas.
- Aulas 07R, 08R e 14.
