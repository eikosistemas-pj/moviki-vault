---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, aquisicao, vitrine, home, moderacao]
atualizado: 2026-09-16
---

# ARQ - Vitrine de lives no ar 16092026

No ar em 16/09/2026: `moviki/mvaovivo.js` (novo), `moviki/api/vitrine.js`,
`moviki/index.html`, `moviki/aovivo.html`, `moviki-robo/lib/livesessao.js` e
`moviki-app/eikoadm01.html`.

## O buraco

Ate hoje **nenhuma superficie publica do Moviki mostrava quem estava
transmitindo**. A live so era descoberta pelo link que o proprio lojista
mandava no WhatsApp.

Ou seja: **o Moviki nao entregava um unico espectador.** O lojista trazia a
audiencia que ja tinha, e a promessa da landing — "venda em tempo real para
quem esta perto" — nao se cumpria em lugar nenhum do produto. E isso que
decide se o Premium vale a **segunda** mensalidade.

De quebra, o item do mapa mestre estava mal escrito: dizia "o mapa da home nao
marca quem esta transmitindo". **Nao existe mapa de negocios na home** — os
pinos de la sao ilustracao.

## Como foi feito

| Peca | O que faz |
| --- | --- |
| `livesessao.js` | `abrir()` grava o **cartao** da live na sessao: slug, nome, segmento e logo. **Uma** leitura de `negocios/{uid}` por live aberta, em vez de uma por lojista cada vez que alguem abre a home |
| `api/vitrine.js` | ganhou `?modo=aovivo`. **Nao foi criada funcao nova** — a que ja existia foi estendida |
| `mvaovivo.js` | busca, pinta e revalida o bloco. Estatico, nao conta no teto de funcoes |
| `index.html` · `aovivo.html` | `<div id="mvAoVivo">` + o script |
| `eikoadm01.html` | interruptor proprio da vitrine |

## As decisoes que valem mais que o codigo

**Nada de SDK do Firebase na landing.** A home so baixa o Firebase quando
alguem encosta na newsletter, para continuar leve — e essa leveza e o funil de
aquisicao. A lista vem de um fetch JSON com **20 s de cache na CDN**: mil
visitantes na home custam **uma** leitura do Firestore.

**Vazio some.** Sem ninguem no ar, o bloco nao aparece. "Nenhuma live agora"
num produto novo nao e transparencia — e cartaz de loja fechada na vitrine.

**Pulso de menos de 3 minutos**, igual ao painel do dono. Aba fechada no meio
da feira deixaria um "AO VIVO" eterno na home, pior que nao ter vitrine.

**Falha aberta aqui, fechada la.** A `vitrine.js` do robo social devolve 502
quando o Firestore cai, de proposito — lista vazia faria o robo publicar
institucional caladinho todo dia. A vitrine da home faz o **oposto**: sem
lista, o bloco some e a home segue inteira. Dar erro na cara do visitante para
proteger um bloco seria trocar o silencio por um estrago maior.

## O risco que a entrega abriu, e a trava

A vitrine **muda o perfil de risco do Modo Live**: antes, uma live impropria
ficava no link que o lojista distribuia; agora ela aparece na **home**. A
moderacao encerra a live e ela some em 20 s, mas incidente nao espera ninguem
estar acordado para subir arquivo.

Por isso nasceu junto o **interruptor da vitrine**
(`configuracoes/liveTermos.vitrineDesligada`), com botao proprio no painel do
dono e registro em `moderacao`. E **separado da chave-mestra de proposito**:

> **Tirar o cartaz da frente da loja nao e fechar a loja.** Derrubar todas as
> transmissoes do Moviki porque UM lojista passou do ponto seria punir os
> outros pelo incidente dele.

A chave-mestra tambem apaga a vitrine — sem live acontecendo, nao pode haver
cartaz dizendo que ha.

## Regras de ouro

1. **Recurso que ninguem descobre nao e recurso.** O Modo Live estava tecnico
   inteiro e comercialmente pela metade.
2. **Pendencia mal escrita esconde trabalho maior.** "O mapa nao marca quem
   transmite" virou "nao existe mapa, e nao existe descoberta".
3. **Vitrine vazia nao se anuncia.**
4. **Toda superficie publica nova precisa do proprio interruptor**, no banco,
   separado dos interruptores que ja existem.
5. **Cache de CDN e trava de custo**, nao so velocidade: e a diferenca entre
   uma leitura e mil.

## Ligacoes

[[A13 - Modo Live]] · [[P - Abertura da live para lojista pagante]] ·
[[R - Marcas de versao no ar]] · [[R - TTL de retencao no Firestore]]
