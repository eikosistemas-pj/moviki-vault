---
type: projeto
status: ativo
prioridade: 2
prazo: 2026-09-30
area: A10 - Conformidade e LGPD
tags: [parceiros, conar, conformidade, videoaula, aceite]
atualizado: 2026-09-10
---

# P18 - Aula de conduta do divulgador

> Era `P15` na fila represada de 05/09. Renumerado: `P15` ja existe no vault desde
> 03/09 ([[P15 - Enforcement do App Check]]).

## Por que existe

O **Guia CONAR 2026** trata conteudo **comissionado** como publicidade e poe sobre
o **anunciante** o dever de informar o divulgador das normas e de monitorar o que
ele publica, sob risco de **responsabilizacao solidaria**. Todo parceiro do Moviki
e comissionado — logo todo post de parceiro sobre o Moviki e publicidade.

**A aula ensina; o aceite prova.** Visualizacao de video nao e prova de que o
dever de informar foi cumprido.

## O que ja esta no ar

- **Videoaula P10** — "Como falar do Moviki sem prometer o que nao pode",
  `T5QdBjl9Y1k`, 2:29, chave `mod-parc-conduta`, modulo "Comece por aqui". Entrou
  em 04/09 e levou o parceiro a 11 aulas
- **Regras v21** publicadas em 05/09: campo `aceiteConduta { versao, em }`
  opcional no `hasOnly` do update de `parceiros/{uid}`, com forma fechada
- **`parceiro.html`** com o aceite — conferido no repositorio em 10/09:
  `aceiteConduta` esta no arquivo no ar

## Como o aceite se comporta

**Nao retranca nada.** So desabilita, ate um clique, os botoes que levam link e
cracha para fora. A trava das aulas segue intacta por cima.

A **versao** existe para o dia em que o compromisso mudar: quem aceitou a 1.0 nao
conta como tendo aceitado a 2.0, e o painel volta a pedir.

**O que um parceiro esperto consegue forjando o campo** e liberar os proprios
botoes de copiar link e baixar cracha — material de apoio, nao valor. E, ao
forjar, ele grava a declaracao de que se comprometeu: contra ele, nao a favor.

## Ordem de publicacao, para nao repetir

**Regras ANTES do painel.** Sem o campo no `hasOnly` a gravacao e negada e o botao
"Li e concordo" responde "Nao deu certo" para sempre. Mesma armadilha da v18.

## Armadilha registrada

`conduta()` roda **tres vezes** no `parceiro.html`. Funcao de painel chamada mais
de uma vez **nao pode guardar estado em variavel local**: um `var` local fez o
aceite gravar no banco e a tela voltar a pedir aceite. O estado vive na ponte
`window.__mvParceiroTut`.

## Pendencias

- [ ] Monitorar o que os parceiros publicam — o dever do CONAR nao acaba no
      aceite, inclui **acompanhar**
- [ ] Texto do compromisso revisado junto com o Regulamento 1.1
- [ ] Aula de etiqueta por rede (onde o `#publi` fica em cada formato) — esta como
      modulo 2 em [[P16 - Perfil do criador de conteudo no quiz]]

## Ligacoes

[[A10 - Conformidade e LGPD]] · [[A5 - Programa de Parceiros]] ·
[[P16 - Perfil do criador de conteudo no quiz]] · [[R - Regras de ouro]]
