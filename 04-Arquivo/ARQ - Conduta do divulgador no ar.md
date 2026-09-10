---
type: arquivo
status: concluido
area: A10 - Conformidade e LGPD
tags: [conar, parceiros, conformidade, aceite, regra-firestore]
atualizado: 2026-09-10
---

# ARQ - Conduta do divulgador no ar

Entregue em 05/09/2026 e **no ar** — conferido no repositorio em 10/09: o
`parceiro.html` publicado carrega `aceiteConduta`, e as regras estao na v21 (hoje
v22, aditiva).

## As duas pecas

1. **Videoaula P10** — "Como falar do Moviki sem prometer o que nao pode",
   YouTube `T5QdBjl9Y1k`, 2:29, chave `mod-parc-conduta`, no modulo "Comece por
   aqui". Entrou em 04/09 e levou o painel do parceiro a **11 aulas**.
2. **Aceite versionado** — campo `aceiteConduta { versao, em }` em
   `parceiros/{uid}`, com o texto do compromisso de tres linhas ao lado do botao
   "Li e concordo", na aba Divulgacao.

## Por que o aceite existe, e nao so a aula

O **Guia CONAR 2026** trata conteudo **comissionado** como publicidade e poe sobre
o **anunciante** o dever de informar o divulgador das normas e de monitorar o que
ele publica, sob risco de **responsabilizacao solidaria**. Todo parceiro daqui e
comissionado.

**A aula ensina; o aceite prova.** Visualizacao de video nao e prova de que o
dever de informar foi cumprido. Se um parceiro postar "ganhe tanto por mes
indicando", quem responde nao e so ele — e a Eiko Sistemas.

A **versao** na chave existe para o dia em que o compromisso mudar: quem aceitou
a 1.0 nao conta como tendo aceitado a 2.0, e o painel volta a pedir.

## Regras v21

Uma mudanca so: `aceiteConduta` entrou no `hasOnly` do `allow update` de
`parceiros/{uid}`, **opcional** e com **forma fechada** (`versao` e `em`, tamanhos
limitados), para o campo nao virar deposito de texto qualquer dentro do cadastro.

**Nao afrouxa nada:** dinheiro, status e slug continuam fora do `hasOnly`. O
maximo que um parceiro esperto consegue forjando o campo e liberar os proprios
botoes de copiar link e baixar cracha — material de apoio, nao valor. E, ao
forjar, ele grava a declaracao de que se comprometeu: **contra ele, nao a favor**.

## A ordem que nao pode inverter

**Regras ANTES do `parceiro.html`.** Sem o campo no `hasOnly`, a gravacao e negada
e o botao "Li e concordo" responde "Nao deu certo" para sempre. Mesma armadilha da
v18.

## O que o aceite NAO faz

**Nao retranca nada.** Ele so desabilita, ate um clique, os botoes que levam link
e cracha para fora do painel. A trava das aulas segue intacta por cima.

## A armadilha do dia

`conduta()` roda **tres vezes** no `parceiro.html`. **Funcao de painel chamada
mais de uma vez nao pode guardar estado em variavel local**: um `var` local fez o
aceite gravar no banco e a tela voltar a pedir aceite. O estado vive na ponte
`window.__mvParceiroTut`.

## Ligacoes

[[A10 - Conformidade e LGPD]] · [[A5 - Programa de Parceiros]] ·
[[P18 - Aula de conduta do divulgador]] · [[R - Regras de ouro]] ·
[[R - Historico de regras do Firestore]]
