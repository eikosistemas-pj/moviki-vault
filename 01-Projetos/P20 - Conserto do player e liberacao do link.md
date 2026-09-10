---
type: projeto
status: ativo
prioridade: 1
prazo: 2026-09-12
area: A1 - Produto e Paineis
tags: [videoaulas, parceiros, painel, player, aprovacao, armadilha]
atualizado: 2026-09-10
---

# P20 - Conserto do player e liberacao do link

> Era `P15` na entrega original de 10/09. Renumerado: `P15` ja existe no vault
> desde 03/09 ([[P15 - Enforcement do App Check]]). Ver
> [[ARQ - Incidente - colisao de entregas no painel do parceiro]].

Quatro frentes: o player parou de cortar o fim do video, o contador parou de
travar, adiantar o video deixou de valer, e a aprovacao do parceiro ganhou uma
segunda porta — quem termina as aulas entra na hora.

## ESTADO REAL EM 10/09 — conferido nos repositorios

| Arquivo | Repo | Deveria estar | Esta no ar | Situacao |
| --- | --- | --- | --- | --- |
| `index.html` | moviki-app | `2026-09-10-player` | `2026-09-10-videos` | **OK** — a entrega da galeria de videos foi montada por cima e carrega `acabou()`, `matar()` e `__contado` |
| `parceiro.html` | moviki-app | `2026-09-10-linkfechado` | `2026-09-10-niveis-olhinhos` | **PERDIDO** — zero ocorrencia de `acabou`, `matar(`, `__contado` e `mvSelinho` |
| `novo-parceiro.js` | moviki-robo | 5 min + aulas | `DELAY_MIN_MINUTOS = 10`, sem `aprovarParceiro` | **PERDIDO** — o que subiu foi a versao da foto do parceiro |

**Consequencia, e ela e grave:** o painel do parceiro tem **11 aulas** e e onde o
defeito do contador e fatal — a Divulgacao so abre com TODAS vistas. O conserto
esta no painel do lojista (4 aulas, onde quase nao aparece) e **nao esta** no do
parceiro. O sintoma que segurou o link do amigo do Paulo continua no ar.

## O que refazer

- [ ] `parceiro.html` — reaplicar o conserto do player e os avisos de link
      fechado **sobre o `2026-09-10-niveis-olhinhos` que esta no ar** (nunca
      sobre a copia antiga). Marca alvo: `2026-09-10-linkfechado`
- [ ] `novo-parceiro.js` — reaplicar `DELAY_MIN_MINUTOS = 5`, `aprovarParceiro()`
      e a porta por `aulasEm`, **sobre a versao com foto que esta no ar**
- [ ] Robo primeiro, painel depois
- [ ] Conferir `aprovacaoAutomaticaParceiros` ligado em `configuracoes/sistema`

## 1. O video parava alguns segundos antes de acabar

Aos 90% a aula era marcada e, 1,1 s depois, a proxima entrava no palco — e por a
proxima no palco APAGA o iframe da que ainda tocava. Aula de 1:46 perdia 10 s.
**Conserto:** a troca saiu do `marcar()` e virou `acabou()`, chamada so no estado
`ENDED` da API do YouTube.

## 2. O contador travava da segunda aula em diante

O `YT.Player` antigo nunca era destruido. Ao apagar o iframe, a API continua
falando com uma janela morta e **para de entregar eventos aos players
seguintes**: `onStateChange` nunca mais dispara e a aula nunca fica verde.

Tres camadas: `matar(iframe)` com `player.destroy()` · relogio proprio que
comeca no `onReady` e no `PLAYING` · `f.__contado` para nao gravar duas vezes.

## 3. Nao vale mais adiantar o video

Vale o CAMINHO PERCORRIDO, nao a posicao da agulha. A cada 500 ms anota-se o
segundo que toca, e so conta se o salto couber no tempo real
(`pulo <= real * 1,6 + 0,6`). Fecha com 90% de segundos distintos. Arrastar a
barra: 0 aulas. Rever o comeco em laco: 0 aulas. 2x continua valendo de
proposito — apertar mais geraria falso negativo em celular lento.

## 4. As duas portas do parceiro

| Porta | Abre com | Libera |
| --- | --- | --- |
| Aprovacao | 5 minutos, ou concluir as aulas | o painel |
| Aulas | assistir TODAS as publicadas | o link de indicacao |

`DELAY_MIN_MINUTOS` cai de 10 para 5 porque a varredura do GitHub Actions roda
de 5 em 5 — esperar 10 fazia a aprovacao cair entre 10 e 15 minutos reais.

A segunda porta reaproveita a chamada que o painel ja faz a
`api/novo-parceiro?espelho=1` quando a ultima aula fecha: se o parceiro esta
`pendente`, a auto-aprovacao esta ligada e o `aulasEm` esta carimbado **no
banco**, aprova ali e responde `{aprovado:true}`. A varredura tambem passa a
aceitar `aulasEm`, como rede de seguranca. Status continua escrito so pelo Admin
SDK, e `aulasEm` e lido do banco, nunca do navegador. Telegram distingue os dois
casos; `aprovadoPor` grava `automatico` ou `automatico-aulas`.

## 5. "Aprovado" nao e "link liberado"

Aprovar em 5 minutos poe o parceiro num painel liberado sem ter assistido nada —
e o painel nao dizia isso. O aviso morava so na Visao geral, e o cartao de
situacao sumia na aprovacao dizendo *"Tudo certo! Divulgue seu link"* com o link
ainda borrado atras do cadeado.

Passa a existir: aviso laranja pulsante em TODAS as secoes (menos a Divulgacao,
que ja tem o cadeado) · cadeadinho `.mvSelinho` no menu lateral e no do celular ·
o cartao de situacao FICA, com selo **"Aprovado - link fechado"** e botao "Ver as
aulas e liberar meu link" · o painel le `{aprovado:true}` e repinta sem F5.

## Atencao — sao 11 aulas de parceiro, nao 8

`MIN_AULAS = 8` e so o piso para a trava existir; destravar exige ver **todas**
as publicadas. Confirmado no repo: o `parceiro.html` no ar mantem `MIN_AULAS=8`.

## Validacao feita (na entrega original)

Playwright com a API do YouTube simulada nos dois paineis. Arrastar a barra: 0
marcadas. Rever o comeco 12x: 0. Assistir inteiro: marcada, 1 gravacao. Parceiro
com 11 aulas: 11 de 11, `aulasEm` carimbado, Divulgacao aberta, 10 players
destruidos. `node --check` em todos os blocos.

## Em aberto

- [ ] Gravar as 3 videoaulas do lojista que faltam: Primeiros passos, Seu
      desempenho, Seu dia a dia
- [ ] Arredondar para cima as duracoes exibidas no painel — quase toda aula
      mostra 1 segundo a menos que o YouTube
- [ ] Decidir se o antifraude vale para as boas-vindas do lojista se elas
      virarem obrigatorias

## Ligacoes

[[A1 - Produto e Paineis]] · [[A5 - Programa de Parceiros]] ·
[[ARQ - Incidente - colisao de entregas no painel do parceiro]] ·
[[P19 - Plano de niveis do parceiro]] · [[R - Marcas de versao no ar]]
