---
type: decisao
status: concluido
area: A13 - Modo Live
tags: [live, videoaulas, trava, painel, estudio]
atualizado: 2026-09-15
---

# ARQ - Modulo de aulas da live com trava 15092026

As aulas do Modo Live deixaram de ser "mais treze itens no fim da biblioteca de
tutoriais" e viraram **módulo próprio, com trava de aptidão**. Decidido e
entregue em 15/09/2026.

## A decisão

Três mudanças de conceito, na ordem em que foram pedidas:

1. **Módulo separado dos tutoriais do painel.** As aulas do painel continuam como
   estão. As da live nascem de um gatilho: o lojista clica em **Fazer live**, e é
   esse clique que abre o módulo.
2. **Assistir vem antes de transmitir.** Não é convite, é porta. Enquanto as três
   aulas de contexto não estiverem vistas, o botão *Entrar ao vivo* fica fechado.
3. **Função nova ganha aula, e a aula vira alerta.** Toda ferramenta nova que
   entrar no estúdio entra também no módulo, com data. Quem já estava em dia
   recebe o aviso de que existe aula nova — sem ser tratado como quem nunca
   assistiu nada.

## A trava

Três chaves, e só três: `mod-live-abertura`, `mod-live-regras`,
`mod-live-primeira`. São as aulas de **contexto** — o que é a live, o que pode e
o que não pode, e como entrar no ar. As onze de ferramenta **não** travam:
ferramenta que o lojista não usa não pode impedir que ele transmita.

Onde a trava age:

- **`btnIniciar` no estúdio**, antes do aceite dos termos.
- Só reabre o que ela mesma fechou: a variável `travadoPorAula` guarda a
  autoria, e `mestraAtiva()` confere se o interruptor mestre não é quem está
  segurando o botão. **Sem isso a trava reabriria uma live derrubada de
  propósito pelo painel do dono.**

## O card no painel

Espelha o card das videoaulas do painel: mesmo lugar, mesma linguagem. Três
estados — falta assistir, em dia, aula nova. Pintado dentro do snapshot do
`liveTermos`, não no carregamento: o painel só sabe se a live está liberada
depois que esse documento chega.

## Alerta de aula nova por data, não por contagem

O primeiro desenho dizia "11 aulas novas" para quem tinha visto só as três da
trava — mistura aula nunca vista com aula acrescentada depois. `novas()` passou
a comparar a data de conclusão gravada em `em` com o `em` de cada aula: só conta
como novidade a aula **publicada depois** de o lojista ter ficado em dia.

## Armadilha encontrada no caminho

**O painel re-embrulha `abrirTab` em `setInterval`.** Um wrapper posto por cima
some sozinho em alguns segundos. Parar o vídeo ao trocar de aba virou **listener
de clique** em `[data-tab], .tab, .aba, [data-fin], .finAba` — o DOM não se
reescreve, o wrapper sim.

## Onde embute

Nove abas do estúdio, duas do painel, mais a biblioteca. As duas chaves que não
embutiam em aba nenhuma foram resolvidas: `mod-live-pedidos` passou a
`#tab-financeiro` ("O pedido que vem da live") e `mod-live-cardapio` a
`#tab-cardapio` ("Vender pelo cardápio, sem live").

## Arquivos

| Arquivo | Marca |
| --- | --- |
| `moviki-app/liveaulas.js` | `2026-09-15-liveaulas2` |
| `moviki-app/live.html` | `2026-09-15-liveaulas` |
| `moviki-app/index.html` | `2026-09-15-liveaulas2` |

## Ligações

[[A13 - Modo Live]] · [[R - Live - Videoaulas do modulo]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[ARQ - Videoaulas do Modo Live concluidas 15092026]] ·
[[R - Marcas de versao no ar]]
