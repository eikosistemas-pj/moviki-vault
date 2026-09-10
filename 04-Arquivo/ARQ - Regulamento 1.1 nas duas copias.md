---
type: arquivo
status: concluido
area: A10 - Conformidade e LGPD
tags: [regulamento, parceiros, conformidade, armadilha]
atualizado: 2026-09-10
---

# ARQ - Regulamento 1.1 nas duas copias

**No ar em 10/09/2026** — conferido nos dois repositorios: as duas copias tem as
clausulas 4.6 a 4.11 e nenhuma menciona "minuta".

## A descoberta do dia

**Existem DOIS `regulamento.html`**: um no repo **moviki**
(`moviki.com.br/regulamento.html`) e outro no repo **moviki-app**
(`app.moviki.com.br/regulamento.html`). O link dentro do painel do parceiro e
relativo, entao **quem esta logado le o do moviki-app** — e essa copia estava
parada na versao 1.0, sem os niveis e sem o telefone.

> **Mexeu num, tem que mexer no outro.**

## O que foi feito

- **Nota interna removida.** A frase "este documento e uma minuta preparada para
  uso comercial e deve passar por revisao de um advogado" so existia na copia do
  moviki-app e estava **aparecendo para o parceiro**
- As duas copias igualadas na **versao 1.1**, com as clausulas 4.6 a 4.11: tabela
  das faixas, percentual so sobre o nivel 1, apuracao a cada mensalidade paga,
  queda de nivel sem aviso previo, comissao ja creditada nao e retirada, bonus de
  marco uma vez por nivel
- No moviki-app os links de voltar apontam para `parceiro.html` — o app nao tem
  `parceiros-ganhos.html` e o link dava erro
- **Bug antigo corrigido:** as tabelas empurravam a pagina de lado no celular
  (scrollWidth 460 numa tela de 360). Agora cada tabela fica num container com
  rolagem propria

## Ordem que foi respeitada

O regulamento subiu **antes** do `webhook.js`: percentual de comissao e contrato
do programa, e a regra escrita precisa estar no ar antes de o robo pagar
diferente.

## O que continua em aberto

**A revisao juridica.** A nota da minuta saiu da tela, mas o texto continua sem
ter passado por advogado — e agora ele **fixa percentual de comissao e bonus em
dinheiro**, ou seja, gera obrigacao financeira.

## Ligacoes

[[A10 - Conformidade e LGPD]] · [[A5 - Programa de Parceiros]] ·
[[P19 - Plano de niveis do parceiro]] · [[P04 - Decisao fiscal do Programa de Parceiros]]
