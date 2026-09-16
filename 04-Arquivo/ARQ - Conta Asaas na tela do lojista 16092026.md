---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [financeiro, asaas, seguranca, indicacao, painel]
atualizado: 2026-09-16
---

# Conta Asaas na tela do lojista — 16/09/2026

Pergunta do Paulo: a parte do Asaas na aba Financeiro esta em aberto para o
cliente, e faltava videoaula. **A aula sozinha nao resolvia** — a tela tinha
tres buracos que nenhum video conserta. Consertados nesta rodada.

Continua [[P31 - Financeiro e cardapio compravel]] ·
[[ARQ - Portas separadas do checkout 14092026]] ·
[[ARQ - Decisao sobre o BaaS do Asaas 15092026]].

## Arquivos

| Repositorio | Arquivo | Marca | Tipo |
| --- | --- | --- | --- |
| moviki-app | `index.html` | 2026-09-16-asaasconta | SUBSTITUI |
| moviki-robo | `lib/checkout.js` | 2026-09-16-asaasconta | SUBSTITUI |
| moviki-ai | `lib/catalogoPainel.js` | 2026-09-16-8 | SUBSTITUI |

Montados sobre o que estava no GitHub em 16/09 as 15h: lojista
`2026-09-16-quadro`, checkout `2026-09-16-subfechada`, catalogo
`2026-09-16-7`.

## O que a tela tinha de errado

1. **Nao dizia o que a chave e.** No Asaas a chave de API vale para a conta
   INTEIRA. A tela falava em "guardada criptografada" e nao falava do poder da
   chave — e chave poderosa que parece inofensiva e a que vai parar num grupo
   de WhatsApp.
2. **Nao existia caminho para quem nao tem conta.** O campo comecava do fim:
   "cole sua chave". Quem nao tinha conta olhava a tela e fechava.
3. **Nao havia volta.** Conectou, conectou. Sem botao de desconectar, a unica
   saida era o suporte.
4. **Conta em analise passava batido.** O `lojaAsaasConectar` so perguntava
   `/myAccount/commercialInfo`, que responde antes da aprovacao. Resultado:
   chave guardada, venda ligada, e o comprador com um Pix que nao cai.

## O que passou a valer

### Servidor — tres portas antes de guardar a chave

1. **Chave de homologacao nao entra** (`_hmlg_` no valor) — erro
   `chave_sandbox`. Era o unico jeito de o lojista emitir QR de mentira com a
   tela dizendo que estava tudo certo.
2. **`GET /myAccount/status` precisa voltar `general: APPROVED`** — erro
   `conta_pendente`, com a lista do que falta (dados da empresa, conta
   bancaria, documentos). **Nada e guardado** enquanto nao aprovar.
3. **`/myAccount/commercialInfo`** continua como prova de vida e traz nome e
   documento para a tela.

Novos: `lojaAsaasDesconectar` (apaga a chave e, se a venda estava ligada no
modo `asaas`, **desliga a venda na mesma escrita** e reespelha o
`checkout_publico`) e `avisarContaAsaas` (Telegram na troca e na remocao,
igual ao que ja existia para a troca de chave Pix). Trilha nova:
`asaas_trocado`, `asaas_desconectado`, `asaas_indicacao_clique`.

`situacaoRecebimento` passou a devolver `asaas.status` e `asaas.em`.

### Tela — o caminho inteiro, nao so o campo

- Passo a passo de quatro passos, com a espera da aprovacao dita **antes**, nao
  descoberta depois.
- Botao **"Abrir minha conta no Asaas"** apontando para o link de indicacao do
  Moviki: `https://www.asaas.com/r/0ab6b815-4cf9-415f-8ad2-c495ad6efe87`.
- Alerta ambar sobre o poder da chave, com a frase que corta o golpe mais
  provavel: **o suporte do Moviki nunca pede essa chave**.
- Conectada: cartao verde com o nome do titular, para o lojista conferir que a
  conta e a dele, e botao **Desconectar esta conta** — com aviso de que a
  venda cai junto, dito ANTES de confirmar.
- Mensagens novas para `conta_pendente` e `chave_sandbox`.

### Medicao do link de indicacao

O clique e contado em dois lugares de proposito: GA (`asaas_abrir_conta`,
funil) e **trilha do Financeiro** (`asaas_indicacao_clique`, por lojista). O
relatorio do Asaas conta conta aberta; a trilha conta intencao. A diferenca
entre os dois numeros e a taxa de abandono no cadastro do Asaas — que e o que
diz se o passo a passo esta bom.

### Vik

`MARCAS_CONFERIDAS.lojista` foi para `2026-09-16-asaasconta` na mesma rodada.
Sem isso o Vik entra em modo cauteloso silencioso — ja aconteceu duas vezes em
16/09. O catalogo ganhou o fluxo novo e os dois avisos novos, e a regra de que
**o Vik nunca pede chave de API**.

## Regra de ouro que nasceu aqui

> **Credencial de terceiro so entra depois de a conta estar aprovada na
> origem, e toda tela que guarda credencial precisa ter a porta de saida na
> mesma tela.** Guardar chave de conta pendente e guardar risco sem receber
> uma venda em troca.

⚠️ **Falta levar esta regra para `R - Regras de ouro.md`.** O conteudo
integral daquela nota nao e legivel desta conta (o vault chega so por RAG, em
trechos) e substituir sem o original apagaria linhas.

## Conferido

- `node --check` no `checkout.js`, no `catalogoPainel.js` e nos nove blocos de
  script do `index.html`: sem erro.
- Balanceamento de `<div>` identico ao do arquivo original (mesma diferenca de
  1, que ja existia — vem de uma string dentro do JS).
- Renderizado em Chromium a 390 px nos dois estados (sem conta e conectada):
  sem rolagem lateral, `scrollWidth` 390.
- `index.html` entregue com **BOM + CRLF**, como exige o navegador do Paulo.

## Ligacoes

[[P36 - Videoaula da conta Asaas]] · [[R - Aula - Conta Asaas do lojista]] ·
[[R - Marcas de versao no ar]] · [[R - Doutrina de seguranca financeira]]
