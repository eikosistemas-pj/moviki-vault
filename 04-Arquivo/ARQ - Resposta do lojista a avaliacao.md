---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [avaliacoes, pagina-publica, painel-lojista, regra-firestore]
atualizado: 2026-09-10
---

# ARQ - Resposta do lojista a avaliacao

No ar em 05/09/2026: `moviki-app/index.html` e `moviki/404.html`, ambos
`2026-09-05-resposta`.

O lojista responde a avaliacao do cliente, como no Google. Campos `resposta` e
`respostaEm` no proprio documento da avaliacao.

## Por que NAO precisou de regra nova

Duas coisas que ja existiam, juntas:

1. Dentro de `negocios/{uid}` existe `match /{documento=**}` que ja da escrita ao
   dono do negocio.
2. A regra de **create** da avaliacao tem
   `hasOnly(['nota','nome','comentario','criadoEm'])` — visitante nenhum consegue
   nascer com o campo `resposta`.

**E isso que garante que a assinatura "Resposta de <negocio>" na pagina publica e
verdade do banco, e nao promessa de tela.** A garantia nao esta no HTML: esta na
regra que impede qualquer outro autor de escrever ali.

## O que ficou de fora, e por que

**O "curtir" na avaliacao.** Abriria porta de escrita anonima nova justamente na
vespera do enforcement do App Check, e nao muda a decisao de ninguem.

## Pendencia que este trabalho revelou

**A regra deixa o dono do negocio editar nota e comentario do cliente**, nao so
responder. Ja era assim antes desta rodada. O conserto natural e limitar o update
do dono a `resposta` e `respostaEm` com `affectedKeys().hasOnly()`.

Enquanto isso nao entra, a integridade da avaliacao depende de boa-fe do lojista
— e avaliacao que o avaliado pode reescrever nao serve de prova para ninguem.

## Ligacoes

[[A1 - Produto e Paineis]] · [[A3 - Dados e Regras]] ·
[[ARQ - Incidente - carregando avaliacoes eterno]] · [[R - Regras de ouro]]
