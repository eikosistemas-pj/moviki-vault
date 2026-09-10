---
type: incidente
status: concluido
area: A1 - Produto e Paineis
tags: [armadilha, pagina-publica, avaliacoes]
atualizado: 2026-09-10
---

# ARQ - Incidente - carregando avaliacoes eterno

Achado em 04/09/2026 na pagina publica `moviki.com.br/karina`, corrigido em 05/09
(`moviki/404.html`, marca `2026-09-05-resposta`).

## O sintoma

A pagina exibia a nota **5,0** e "Avaliacoes 1" no topo, e logo abaixo
**"Carregando avaliacoes..." para sempre**. Nenhum erro no console.

Os dois numeros vem de lugares diferentes: a nota sai do documento
`negocios/{uid}/resumo/avaliacoes`; a **lista** e outra leitura.

## A causa

A lista so era pedida **no clique da aba**. Negocio sem fotos liberadas, sem
promocao e sem evento cai no fallback do `montarAbas` e **abre ja na aba
Avaliacoes**, sem clique nenhum — entao ninguem pedia a lista.

Atingia qualquer lojista do plano Basico que tivesse avaliacao. Nao tinha relacao
com o App Check, que estava sendo ligado nos mesmos dias — **por isso o incidente
foi investigado antes de virar a chave**, para os dois sintomas nao se
confundirem.

## O conserto

Quem pede a lista passou a ser o `pintarAba`, e o estado virou `avEstado` com
quatro valores: `nao` / `carregando` / `pronto` / `erro`. Leitura negada mostra
mensagem com botao **Tentar de novo** em vez de "Carregando" eterno.

## A licao

> **Estado de carregamento precisa de um valor para "nem comecou".** Um booleano
> `carregando` nao distingue *pedindo* de *nunca pedido*, e o "nunca pedido"
> aparece na tela exatamente igual a uma requisicao travada.

E a irma dela: **a tela tem que refletir a realidade nos dois sentidos** — falha
de leitura vira mensagem com saida, nunca silencio infinito.

## Ligacoes

[[A1 - Produto e Paineis]] · [[R - Regras de ouro]] ·
[[ARQ - Resposta do lojista a avaliacao]]
