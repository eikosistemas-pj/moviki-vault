---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, seguranca, custo, cloudflare, freio, cota]
atualizado: 2026-09-15
---

# O freio do api/live.js — B5 — 15/09/2026

Primeiro item da **fase 2** de [[P35 - Auditoria de seguranca do Modo Live]].
Entrega: `moviki-b5-freio-15092026.zip` — tres arquivos.

---

## 1. O defeito

`moviki/api/live.js` **nao tinha limite de chamadas**. Um lojista rodando
"Entrar ao vivo" em laco fazia, a cada erro de cache, um **GET da lista inteira
de entradas do Cloudflare**. Estourado o teto do token da conta, o Cloudflare
responde **429** — e a partir dai **nenhum lojista consegue comecar uma live**.

**Um uid derrubava o Modo Live inteiro**, com a fatura do Firestore subindo
junto. E nao exigia nenhuma malicia sofisticada: um script de dez linhas.

## 2. Duas barreiras, as duas ANTES do Cloudflare

| # | Onde | Teto | Pega |
| --- | --- | --- | --- |
| 1 | memoria do `api/live.js` | 1 `iniciar` a cada 20 s por lojista | a rajada do mesmo processo, **sem custar leitura nenhuma** |
| 2 | robo, `live_throttle/{uid}` | 3/min, 20/hora, 60/dia | a rajada espalhada por varias instancias frias da Vercel |

A barreira 1 sozinha nao bastaria: a Vercel abre instancias novas, e cada uma
teria o proprio contador zerado. A barreira 2 sozinha custaria uma leitura por
tentativa, inclusive nas rajadas. **Juntas, a rajada barata morre de graca e a
distribuida morre no contador duravel.**

Janelas **fixas**, nao deslizantes: uma leitura e uma escrita por chamada, sem
guardar lista de horarios. Em freio de abuso, simples e melhor que exato.

## 3. A chamada cara sumiu do caminho normal

O robo **ja guardava** o id da entrada do Cloudflare em `live_sessoes/{uid}`
(veio de graca com a [[ARQ - Sessao da live no servidor]]). Agora ele devolve
esse id no `live_reservar`, e o `api/live.js` busca a entrada **direto por id**.

**A listagem da conta inteira so acontece para quem nunca fez live.** Era
exatamente ela a chamada que estourava o teto.

## 4. De quebra: a cota foi para o lugar certo

A cota do teste gratis era contada no `live_abrir` — ou seja, **depois** de
criar a entrada no Cloudflare. Cota estourada ja tinha gasto chamada. Agora ela
e consumida no `live_reservar`, antes de tocar no Cloudflare.

⚠️ O `live_abrir` passou a receber **`jaReservado`** e nao conta de novo. Sem
esse cuidado, uma unica live comeria **duas** da cota.

## 5. Tetos — onde mexer

| O que | Onde | Valor |
| --- | --- | --- |
| memoria | `MEM_JANELA_MS` em `moviki/api/live.js` | 20 s |
| duravel | `FREIO = { minuto:3, hora:20, dia:60 }` em `lib/livesessao.js` | — |

Generosos para uso real (queda de sinal, reconexao, lojista indeciso) e
apertados o suficiente para um laco nao chegar perto do teto do Cloudflare.

## 6. Entrega

| Arquivo | Acao | Marca |
| --- | --- | --- |
| `moviki-robo/lib/livesessao.js` | SUBSTITUI | `2026-09-15-b5` |
| `moviki/api/live.js` | SUBSTITUI | `2026-09-15-b5` |
| `moviki-app/live.html` | SUBSTITUI | `2026-09-15-sessao4` |

⚠️ O `live.html` **substitui o conserto `sessao3`** entregue minutos antes (o do
botao "encerrada pelo Moviki"): e a mesma base, com a mensagem do freio a mais.

**Envs:** nenhuma nova. **Regras:** nenhuma mudanca — `live_throttle` nao tem
match, entao so o Admin SDK escreve, que e o padrao do projeto para colecao de
controle.

## 7. Testes — 11/11

freio de minuto (3 passam, a 4a barra) · um lojista nao afeta o outro · cota de
2 no teste gratis · carencia de 15 min nao consome · plano pago sem cota ·
`live_abrir` com `jaReservado` nao conta de novo · `reservar` devolve o
`entradaId` guardado. Mais a checagem de sintaxe do JavaScript dos `.html`.

## 8. Conferir depois de subir

1. entrar ao vivo normalmente — tem que funcionar igual;
2. encerrar e tentar entrar de novo **4 vezes seguidas, rapido** — a partir da
   segunda: *"Você tentou começar várias vezes seguidas..."*;
3. Firestore > `live_throttle/{uid}` — `nMin`, `nHora` e `nDia` subindo.

## Fila da fase 2, depois deste

- [ ] **B7** presenca forjavel (audiencia falsa e escrita paga)
- [ ] **B8 e B9** filtro de conteudo: `tipo:'venda'` escapa; oferta, cupom e
      brinde nao passam por filtro nenhum
- [ ] **B2** lista "Lives no ar" do painel passa a usar `live_adm_noar`
- [ ] **B4** WHEP sem URL assinada · **B10** denuncia como arma
- [ ] **B11 a B13** dinheiro do parceiro (saque)

## Ligacoes

[[P35 - Auditoria de seguranca do Modo Live]] ·
[[ARQ - Sessao da live no servidor]] ·
[[P34 - Travas contra abuso do teste gratis]] · [[A13 - Modo Live]]
