---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [videoaulas, parceiros, painel, player, aprovacao, entrega]
atualizado: 2026-09-10
---

# ARQ - Player e liberacao do link no ar

**No ar em 10/09/2026, 16h11** — conferido clonando os repositorios:
`parceiro.html` na marca `2026-09-10-linkfechado`, `novo-parceiro.js` com
`DELAY_MIN_MINUTOS = 5` e `aprovarParceiro()`. Fecha
[[P20 - Conserto do player e liberacao do link]].

## O que estava errado

O `parceiro.html` no ar era o `2026-09-10-niveis-olhinhos`, montado sobre a
versao da foto e nao sobre a do player: o conserto tinha sido atropelado por
outra entrega do mesmo dia. Resultado: o painel do lojista (4 aulas) tinha o
conserto e o do parceiro (11 aulas) — onde o defeito e fatal — nao tinha.
Ver [[ARQ - Incidente - colisao de entregas no painel do parceiro]].

Esta entrega foi montada **sobre o arquivo publicado**, e por isso niveis,
olhinhos, foto, cracha e aceite de conduta continuam todos la.

## Os quatro consertos

1. **O video nao morre antes do fim.** A troca de aula saiu do `marcar()` e
   virou `acabou()`, chamada so no estado `ENDED`. Por a proxima no palco apaga
   o iframe da que ainda esta tocando — era isso que cortava os ultimos
   segundos, e aparecia mais no painel do parceiro por ter mais aulas.
2. **O contador nao trava mais da segunda aula em diante.** `matar()` chama
   `player.destroy()` de verdade: sem isso a API do YouTube continua falando
   com uma janela morta e para de entregar eventos aos players seguintes. Mais
   duas camadas: relogio proprio que comeca no `onReady` E no `PLAYING`, e
   `f.__contado` para nao gravar a mesma aula duas vezes.
3. **Nao vale adiantar.** Vale o caminho percorrido, nao a posicao da agulha: a
   cada 500 ms anota-se o segundo que toca, e so conta se o salto couber no
   tempo real (`pulo <= real * 1,6 + 0,6`). Fecha com 90% de segundos
   distintos. 2x continua valendo de proposito.
4. **"Aprovado" deixou de significar "link liberado".** Aviso laranja pulsante
   em TODAS as secoes menos a Divulgacao (que ja tem o cadeado), cadeadinho
   `.mvSelinho` nos dois menus, e o cartao de situacao que FICA na tela com o
   selo **"Aprovado - link fechado"** enquanto as duas portas nao abrem.

## As duas portas

| Porta | Abre com | Libera |
| --- | --- | --- |
| Aprovacao | 5 minutos, ou concluir as aulas | o painel |
| Aulas | assistir TODAS as publicadas | o link de indicacao |

`DELAY_MIN_MINUTOS` caiu de 10 para 5 porque a varredura do GitHub Actions roda
de 5 em 5 — esperar 10 fazia a aprovacao cair entre 10 e 15 minutos reais.

A segunda porta reaproveita a chamada que o painel ja fazia a
`api/novo-parceiro?espelho=1` quando a ultima aula fecha. `aprovarParceiro()`
virou funcao unica usada pelos dois gatilhos — status escrito so pelo Admin SDK,
`aulasEm` lido do banco, nunca do navegador. `aprovadoPor` grava `automatico` ou
`automatico-aulas`, e o Telegram distingue os dois casos. O painel le
`{aprovado:true}` e repinta sem F5.

**Se `aprovacaoAutomaticaParceiros` estiver desligada em
`configuracoes/sistema`, nenhuma das duas portas abre** — continua manual.

## Validacao antes de subir

Chromium com a API do YouTube simulada: arrastar a barrinha ate o fim **0 aulas
marcadas** · rever so o comeco 20 vezes **0** · pausado **0** · assistir do
inicio ao fim **1 aula, 1 gravacao** · player destruido na troca · aviso em 7
secoes, 2 cadeadinhos, cadeado e blur na Divulgacao · zero erro de JavaScript.

Robo com Firestore simulado, 6 de 6: concluiu as aulas aprova na hora · sem
aulas continua pendente · auto desligada nao abre nada · quem ja esta aprovado
nao e tocado · a varredura aprova por tempo **ou** por aulas · e-mail de
boas-vindas e espelho publico saem em toda aprovacao.

## Sem regra nova

Nenhuma regra do Firestore mudou, nenhuma variavel de ambiente nova, nenhum
arquivo novo em `api/` — as 12 funcoes do plano Hobby continuam sendo as mesmas.

## Detalhe que fica

`MIN_AULAS = 8` e so o piso para a trava existir. **Hoje sao 11 aulas
publicadas**, e e o numero real que aparece no aviso — se subir aula nova, o
texto muda sozinho.

## Em aberto

- [ ] Conferir `aprovacaoAutomaticaParceiros` ligada no painel do dono
- [ ] Gravar as 3 videoaulas do lojista que faltam: Primeiros passos, Seu
      desempenho, Seu dia a dia
- [ ] Arredondar para cima as duracoes exibidas no painel (hoje quase toda aula
      mostra 1 segundo a menos que o YouTube)
- [ ] Decidir se o antifraude vale para as boas-vindas do lojista se elas
      virarem obrigatorias

## Ligacoes

[[A1 - Produto e Paineis]] · [[A5 - Programa de Parceiros]] ·
[[ARQ - Incidente - colisao de entregas no painel do parceiro]] ·
[[R - Marcas de versao no ar]] · [[P19 - Plano de niveis do parceiro]]
