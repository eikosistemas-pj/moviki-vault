---
type: incidente
status: concluido
area: A2 - Infraestrutura e Deploy
tags: [armadilha, deploy, parceiros, painel]
atualizado: 2026-09-10
---

# ARQ - Incidente - colisao de entregas no painel do parceiro

Em 10/09/2026 **quatro conversas diferentes** entregaram o mesmo
`moviki-app/parceiro.html` no mesmo dia. Quem subiu por ultimo apagou o trabalho
dos outros — e ninguem percebeu na hora, porque o arquivo abre normal.

## As quatro entregas

| Marca | O que trazia | Destino |
| --- | --- | --- |
| `2026-09-10-foto-parceiro` | o parceiro escolhe a propria foto | absorvida |
| `2026-09-10-niveis` | card "Seu nivel" | absorvida |
| `2026-09-10-niveis-olhinhos` | os tres olhinhos, refeito como juncao | **e o que esta no ar** |
| `2026-09-10-linkfechado` | conserto do player + avisos de link fechado | **PERDIDO** |

Conferido no repositorio em 10/09: o `parceiro.html` no ar e o
`niveis-olhinhos`, e ele **nao tem** `acabou`, `matar(`, `__contado` nem
`mvSelinho`. Ver [[P20 - Conserto do player e liberacao do link]].

O mesmo aconteceu, com final feliz, no `moviki-app/index.html`: a entrega da
galeria de videos (`2026-09-10-videos`) foi montada por cima da versao com o
conserto do player, entao as duas coisas sobreviveram. Foi sorte de ordem, nao
processo.

E no `moviki-robo/api/novo-parceiro.js`: a versao no ar e a da foto do parceiro;
a da aprovacao por aulas concluidas se perdeu.

## A regra que fica

> **Antes de entregar arquivo grande, ler a marca de versao que esta no GitHub e
> montar a entrega SOBRE ela.** Duas conversas no mesmo arquivo no mesmo dia se
> atropelam, e o sintoma e silencio: a tela abre, o recurso simplesmente nao
> esta la.

Corolario pratico, ja aplicado uma vez neste incidente: quando duas entregas do
mesmo arquivo existirem, a segunda nao e "entregar de novo" — e **juncao**, e
precisa ser refeita sobre o publicado.

## Como conferir em 30 segundos

`F12` > Console > `MOVIKI_VERSAO`, ou abrir o arquivo no GitHub e procurar a
marca. Tela antiga quase sempre e cache: `Ctrl+Shift+R`.

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[R - Marcas de versao no ar]] ·
[[R - Regras de ouro]] · [[P20 - Conserto do player e liberacao do link]] ·
[[ARQ - Tres olhinhos no painel do parceiro]]
