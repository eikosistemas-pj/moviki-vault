---
type: arquivo
status: concluido
area: "[[A4 - Financeiro]]"
tags: [financeiro, pedido, aviso, email, lgpd, meta, entrega]
atualizado: 2026-09-15
---

# ARQ - Aviso de pedido ao lojista 15092026

Fecha o buraco que o cardapio compravel deixou a mostra: a venda existe, mas
ninguem avisa o lojista. Continua
[[ARQ - Cardapio compravel na pagina publica 14092026]].

## Arquivos

| Repositorio | Arquivo | Marca | Tipo |
|---|---|---|---|
| moviki-robo | `lib/checkout.js` | 2026-09-15-aviso | SUBSTITUI |

Nenhuma env nova: o `RESEND_API_KEY` ja esta no projeto.

## O buraco

Pedido novo **nao avisava ninguem**. O unico Telegram do arquivo e o do DONO do
Moviki, e so para troca de chave Pix. No Pix direto quem confirma o pagamento e
o lojista, olhando o proprio extrato — sem aviso, a venda so anda se ele
estiver com o painel aberto no momento exato. E a tela do comprador expira o
pedido em 30 minutos.

## Por que e-mail, e nao WhatsApp

O pedido do Paulo era WhatsApp. Nao da, hoje, sem violar regra:

- **API oficial (Meta Cloud API)** exige conta business verificada, numero
  proprio e **template aprovado pela Meta** para qualquer mensagem iniciada pela
  empresa, com custo por conversa. E um projeto proprio, com aprovacao de
  terceiro no meio do caminho.
- **Atalhos nao-oficiais** (bots que abrem sessao de WhatsApp pessoal) sao
  violacao dos Termos da Meta e custam o numero do lojista.

E-mail chega em todo lojista, hoje, sem cadastro nenhum e sem depender de
aprovacao. O WhatsApp oficial fica como projeto proprio, para quando o volume
justificar o custo por conversa.

O e-mail sai da conta do lojista no **Authentication**, nao de um campo que ele
digita: campo digitado erra, envelhece e e editavel por quem invadir o painel.
Sem e-mail na conta, cai no cadastro do negocio.

## Os tres momentos

| Quando | Assunto |
|---|---|
| Pedido criado | Novo pedido de R$ X |
| Comprador toca em "Ja paguei" (Pix direto) | Pagamento avisado — R$ X |
| Banco confirma (modo Asaas, webhook) | Pagamento confirmado — R$ X |

O do meio e o que realmente importa no Pix direto: enquanto o lojista nao
confere o extrato e confirma, o pedido nao anda.

## O que o e-mail NAO leva

Nome, telefone, endereco e a lista de itens do comprador **nao vao no e-mail**.
Ele diz o valor, quantos itens, se e retirada ou entrega, e manda abrir o
painel. Dado pessoal de terceiro fica atras do login, nao numa caixa de entrada
que o lojista abre no meio da rua — minimizacao, na letra da LGPD. Coberto por
teste: o corpo do e-mail e vasculhado atras do nome, do telefone, do endereco e
do CPF do comprador.

## Duas travas que nao estavam no pedido

- **Teto de 15 avisos por hora por negocio.** O freio de pedidos ja segura 40
  por hora; sem este teto, um lojista debaixo de pedido falso levaria ate 80
  e-mails e o provedor comecaria a marcar o dominio do Moviki como spam — o que
  derrubaria TODO o e-mail do produto, inclusive o de cadastro. Estourado o
  teto, o aviso para; o painel continua mostrando tudo.
- **O envio e AGUARDADO, com tempo limite de 2,5 s.** Promessa solta em funcao
  serverless e cortada no instante em que a resposta sai — o e-mail
  simplesmente nao chegaria. E o limite existe porque o comprador esta parado na
  tela esperando o Pix: se o Resend demorar, o aviso morre e a venda segue.
  Prender a venda esperando e-mail seria trocar o certo pelo acessorio.

Falha de aviso **nunca** derruba pedido nem pagamento: todo caminho de erro sai
em silencio e o painel continua sendo a fonte.

## Conferido fora do ar

45 verificacoes num Firestore e um Resend de mentira: origem do e-mail (Auth,
cadastro, invalido), teto por hora e sua virada, conteudo dos tres assuntos,
singular/plural de item, retirada x entrega, trilha do envio, e os quatro
caminhos de falha (sem chave, Resend em 500, rede caida, lojista sem e-mail) —
nenhum deles derrubando a venda. Mais a leitura do proprio arquivo: os quatro
disparos existem e **todos sao aguardados**.

## Pendente

- Som e contador no titulo da aba do painel, para quem esta com ele aberto.
  Depende do `moviki-app/index.html`.
- WhatsApp oficial pela Cloud API da Meta, se o volume justificar.
