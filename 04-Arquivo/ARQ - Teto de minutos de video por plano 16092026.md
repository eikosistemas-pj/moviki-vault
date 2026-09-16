---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, custo, cloudflare, plano, teto]
atualizado: 2026-09-16
---

# ARQ - Teto de minutos de video por plano 16092026

No ar em 16/09/2026: `moviki-robo/lib/livesessao.js`, `moviki/api/live.js` e
`moviki-app/live.html`, todos marcados **`2026-09-16-tetoplano`**.

## O que existia e nao bastava

Uma parede so: `configuracoes/liveTermos.tetoMinutosMes` (12.000, ciclo dia 12),
medida na analytics do Cloudflare, valida para a **conta inteira**. Ela protege
a fatura do Moviki e **nao protege mais nada**: um lojista com publico grande
consome os 12.000 sozinho e a live de **todos os outros** para — sem aviso, sem
culpado, sem nada na tela de quem ficou de fora. Quem pagou Premium descobre
que nao tem live porque o vizinho transmitiu.

## Os tetos

| Plano | Minutos de video por ciclo |
| --- | --- |
| Premium | 1.500 |
| Enterprise | 5.000 |
| Teste gratis | 300 |

Padrao no codigo (`TETO_VIDEO_PADRAO`), com override em
`configuracoes/liveTermos`: `tetoVideoPremium`, `tetoVideoEnterprise`,
`tetoVideoTrial`. **`0` = sem teto**, igual ao teto global e a lista do beta.
Ciclo no mesmo dia de virada do teto global (`cicloDia`, padrao 12).

## Minuto de VIDEO nao e minuto de LIVE

O Cloudflare cobra por minuto **entregue** — espectadores x duracao. Live de 30
min com 20 pessoas sao **600 minutos**. Por isso este teto nao e o relogio da
live (`limiteMin`, 60 no Premium e 180 no Enterprise, que continua valendo):
sao **duas paredes diferentes**, e so esta fala de dinheiro. O estudio passou a
dizer qual delas bateu — dizer "limite do seu plano" nas duas fazia o lojista
achar que a live de 10 minutos durou uma hora.

## Por que a conta e nossa, e nao do Cloudflare

A analytics deles agrega por conta, demora minutos e **a entrada de video e
apagada e recriada a cada live** (achado B4) — nao da para atribuir minuto a
lojista por la. A conta sai do nosso proprio dado: a cada pulso (45 s) o
servidor **conta** a presenca em `negocios/{uid}/livepresenca` — a mesma
consulta que o estudio ja faz — e multiplica pelo tempo desde o pulso anterior.

**O servidor conta; o estudio nao manda.** Numero de espectadores virou
dinheiro: bastaria declarar zero assistindo para transmitir de graca para
sempre.

O acumulado vive em `live_cota/{uid}`: `cicloVideo` e `minutosVideo`. Ciclo
diferente do gravado e balde novo — nenhuma rotina precisa zerar nada.

## Onde a parede fica

- **`reservar()`**, antes do Cloudflare — mesmo motivo da cota do teste gratis:
  recusar depois deixaria a entrada de video ja criada e a cota ja consumida por
  uma live que nao vai acontecer.
- **`abrir()`**, de novo — seguranca em profundidade, 1 leitura por live.
- **`pulso()`**, a cada 45 s — e o unico lugar que derruba live em andamento.

## O que falha aberto e o que falha fechado

- **Contagem falhou** -> o minuto nao e cobrado e a live segue. O relatorio erra
  para baixo; derrubar transmissao por causa de um `count()` e pior.
- **Acumulado ja estourou** -> a live cai. Esse numero ja esta no banco e nao
  depende de ninguem responder.
- **Pulso atrasado** -> cobra no maximo `DELTA_MAX_MS` (150 s). Pulso que chega
  40 minutos depois e aba dormindo, nao publico assistindo.
- **Live vazia nao gasta teto**: sem espectador o Cloudflare nao entrega nada.

## Testado fora do ar

15 verificacoes num Firestore de mentira: rotulo do ciclo (virada de mes e de
ano), teto por plano e override, consumo de ciclo anterior, 20 espectadores x
45 s = 15 minutos, live vazia, estouro derrubando a sessao, pulso atrasado,
Enterprise passando onde o Premium barra, trial em 300, e recusa no `reservar`.

## Fica em aberto

- **O painel do dono nao tem campo para os tres tetos.** Hoje o override so pela
  `configuracoes/liveTermos` no Console. Os padroes valem sem configurar nada.
- O painel tambem nao mostra o consumo POR LOJISTA — o dado existe em
  `live_cota/{uid}.minutosVideo` e ninguem le.

## Regras de ouro

1. **Teto global protege a fatura, nao os clientes.** Recurso pago em comum
   precisa de parede por assinante, ou o primeiro que crescer derruba o resto.
2. **Cobrar por entrega significa contar espectador, nao relogio.**
3. **Numero que vira dinheiro nao vem do navegador** — nem o de espectadores.
4. **Parede nova entra ANTES do recurso caro**, nao depois dele criado.
5. **Duas paredes diferentes precisam de duas mensagens diferentes**, senao o
   lojista aprende a coisa errada sobre o proprio plano.

## Ligacoes

[[A13 - Modo Live]] · [[P - Abertura da live para lojista pagante]] ·
[[ARQ - Teto de gasto de video no ar 16092026]] · [[R - Marcas de versao no ar]]
