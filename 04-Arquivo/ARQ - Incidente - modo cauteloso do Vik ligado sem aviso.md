---
type: incidente
status: aberto
area: A9 - IA e Atendimento Vik
tags: [vik, catalogo, versao, armadilha, silencio]
atualizado: 2026-09-16
---

# ARQ - Incidente - modo cauteloso do Vik ligado sem aviso

## O mecanismo

`moviki-ai/lib/catalogoPainel.js` guarda `MARCAS_CONFERIDAS`: a marca de versao
de cada painel que foi **lida** para escrever o catalogo do Vik. O
`api/chat.js` recebe a marca real do painel a cada mensagem e compara. Divergiu,
o Vik entra em **modo cauteloso**: continua atendendo, mas fica proibido de
dizer que algo "nao existe".

O desenho esta certo. O problema e outro: **ele e silencioso**. Nao avisa o
usuario, nao avisa o dono, nao aparece em lugar nenhum do painel.

## Duas vezes em dois dias

| Quando | Tabela apontava | Painel no ar estava | Quanto tempo |
| --- | --- | --- | --- |
| 15/09 | `2026-09-13-vikpainel` | `liveaulas2` / `aulatrava` | um dia inteiro |
| 16/09 | `2026-09-15-aulatrava` | `2026-09-16-wafoto` | o dia inteiro |

Em 16/09 o `parceiro.html` subiu **tres vezes** (`matfaixa`, `wafoto`,
`caticones`) e a tabela ficou parada em `aulatrava`.

Nos dois casos ninguem percebeu. O Vik atendeu o dia todo mais humilde do que
precisava, e o unico sintoma era uma resposta um pouco pior.

## A regra

> **Painel que sobe, tabela de marca do Vik sobe junto, na MESMA rodada.**
> Marca velha ali nao quebra nada — ela **degrada tudo, devagar e sem ruido**.

> **Trava silenciosa precisa de tela.** Mecanismo que se protege sozinho sem
> mostrar que se protegeu e indistinguivel de mecanismo quebrado. Vale para o
> modo cauteloso do Vik e valeu para o teto de video
> ([[ARQ - Teto de gasto de video no ar 16092026]]).

## Fica em aberto

- [ ] O modo cauteloso **nao tem indicador**. Precisa aparecer em algum lugar —
      no painel do dono, ou num aviso do proprio Vik ao time — senao o terceiro
      episodio ja esta contratado.

## Ligacoes

[[A9 - IA e Atendimento Vik]] · [[R - Vik - catalogo do painel]] ·
[[R - Marcas de versao no ar]] · [[R - Regras de ouro]] ·
[[P36 - Memoria da live no Vik]] ·
[[ARQ - Teto de gasto de video no ar 16092026]]
