---
type: arquivo
status: concluido
data: 2026-09-04
area: A4 — Programa de Parceiros
tags: [conformidade, videoaula, parceiro, conar, aceite]
atualizado: 2026-09-04
---

# ARQ — Conduta do divulgador: aula P10, aceite e aviso — 04/09/2026

## O trio, e por que nenhum dos tres sozinho resolve

**A aula ensina. O aceite registra. O aviso chega a tempo.**

- A aula so alcanca quem assiste — e influenciador quer o link, nao o curso.
- Se der problema com a Meta ou com um parceiro que se sentiu enganado, o que
  vale e o **aceite com versao e data**, nao a visualizacao.
- O aviso de tres linhas fica no ponto exato onde ele pega o link e o cracha.

## O furo que ninguem tinha no radar: CONAR e responsabilidade solidaria

O Guia CONAR 2026 trata conteudo **comissionado** como publicidade, e exige
identificacao **ostensiva, em primeiro plano, visivel sem clicar em "ver mais"**.
Todo parceiro do Moviki e comissionado — logo **todo post de parceiro sobre o
Moviki e publicidade e precisa de `#publi`**.

E o guia poe sobre o **anunciante** o dever de informar o influenciador das
normas e de **monitorar ativamente** o que ele publica, sob risco de
**responsabilizacao solidaria**. Se um parceiro postar "ganhe R$ 500 por mes
indicando" sem `#publi`, quem responde nao e so ele — e a Eiko Sistemas.

A aula e o aceite deixam de ser zelo e viram a prova de que o dever de informar
foi cumprido.

## P10 no ar

`P10-conduta-divulgador` · **2:29** · YouTube **T5QdBjl9Y1k** · chave
`mod-parc-conduta` · modulo **"Comece por aqui"**, logo depois da abertura.

Titulo no painel: **"Como falar do Moviki sem prometer o que nao pode"** —
"conduta do divulgador" soa a manual de RH e ninguem clica com vontade.

Mora em "Comece por aqui" e nao em Divulgacao de proposito: e a aula que diz o
que NAO pode ser falado, e isso precisa ser sabido antes de qualquer coisa
sobre como divulgar.

**Conteudo:** as tres frases proibidas (ganho, garantido, prazo) escritas na
tela em vermelho com o X; o que PODE ser dito (a regra da comissao); a ressalva
sobre o produto — nao prometer que os clientes acham o negocio pelo mapa,
porque ainda ha cidade com pouca gente; e o `#publi` obrigatorio.

**Nenhum valor, percentual, prazo ou quantidade de aulas na narracao.**

## O gate: proporcional, e nao retranca ninguem

O aceite **nao cobre a secao** e **nao mexe na trava das aulas**. O unico efeito
e segurar os botoes que levam o material PARA FORA — copiar link, WhatsApp,
Facebook, compartilhar, copiar link de parceiro e baixar o cracha — ate um
clique em "Li e concordo".

Quem ja divulga mantem o painel inteiro e precisa de um clique. Isso respeita a
regra de que **aula nova nao retranca parceiro**.

## Armadilha paga nesta rodada

`conduta()` e chamada tres vezes (na entrada, no timeout de 1400 ms e no evento
`mv-parceiro-pronto`). Com um `var aceito` **local**, cada chamada criava um
escopo novo: o listener do clique fechava sobre o escopo VELHO enquanto o
repintar do clique global lia o NOVO. Resultado no teste: **o aceite gravava no
banco e a tela voltava a pedir aceite.**

Conserto: o estado mora num lugar so — a ponte `window.__mvParceiroTut`. A
funcao le sempre de la, nunca de copia local.

**Regra que nasce daqui:** *funcao de painel que e chamada mais de uma vez nao
pode guardar estado em variavel local — o estado vive na ponte.*

## Testado com Playwright e Firestore de mentira

- Parceiro aprovado sem aceite: bloco laranja, os sete botoes bloqueados.
- Clique em "Li e concordo": grava `aceiteConduta {versao, em}` em
  `parceiros/{uid}`, bloco fica verde, botoes liberam.
- Parceiro que ja aceitou: entra verde, com a data do aceite.
- Parceiro que nunca viu aula: cadeado das aulas continua funcionando por cima.
- Parceiro nao aprovado: bloco escondido pelo `soAprovado`.
- Nenhum erro de pagina em nenhum cenario.

## BLOQUEIO — a regra do Firestore precisa entrar ANTES

`aceiteConduta` e campo NOVO. Enquanto ele nao estiver no `hasOnly` que o
cliente atravessa em `parceiros/{uid}`, **a gravacao e negada** e o botao
responde "Nao deu certo — tentar de novo".

Entra como **opcional**, pela regra de ouro: campo novo nunca e exigido antes
de o codigo que grava estar no ar.

## Arquivo

`parceiro.html` — repo `moviki-app`, raiz, **SUBSTITUI**.
Marca de versao: `2026-09-04-conduta`.

→ [[P15 - Aula de conduta do divulgador]] · [[ARQ - Atribuicao do Lead ao anuncio - fbc e fbp]] · [[R - Regras de ouro]]
