---
type: incidente
status: concluido
area: A13 - Modo Live
tags: [live, freio, teste-real, ux, custo]
atualizado: 2026-09-15
---

# O freio barrou um caso legitimo — B5a — 15/09/2026

Ajuste de [[ARQ - Freio do api live - B5]], disparado pelo **teste real do
Paulo**, poucos minutos depois de subir o B5.

Entrega: `moviki-b5a-freio-ajuste-15092026.zip` — tres arquivos.

---

## 1. O que o Paulo viu

> "Eu abri a live e com uns 10 segundos eu encerrei. Quando eu fui abrir de
> novo, ja apareceu a mensagem. Ai nao mostra quanto tempo e o cliente vai ter
> que esperar. Mas na segunda ja apareceu, nao foi na quarta nao."

Duas coisas erradas, as duas dele, as duas certas.

## 2. Quem barrou nao era quem eu disse

A mensagem falava em "varias tentativas seguidas" — linguagem do contador do
robo (3 por minuto). **Mas quem barrou foi a barreira em memoria do
`api/live.js`**, que era uma trava seca: **1 chamada a cada 20 segundos, sem
excecao**. Abrir, encerrar em 10 s e reabrir cai dentro dos 20 s.

⚠️ A licao vale alem deste caso: **duas barreiras com a mesma mensagem escondem
qual das duas disparou.** O diagnostico so saiu porque o Paulo contou o numero
da tentativa ("na segunda"), que nao batia com o teto de 3 do robo.

## 3. Os tres consertos

### 3.1 Encerrar zera o minuto

`fechar()` agora grava `nMin: 0` em `live_throttle/{uid}`.

**Quem encerra de proposito nao esta abusando** — esta usando o produto. Hora e
dia continuam somando, entao o laco que abre-e-fecha mil vezes ainda morre; o
que morreu foi a punicao de quem fez a coisa certa.

### 3.2 A barreira em memoria virou surto, nao trava seca

| Antes | Agora |
| --- | --- |
| 1 a cada 20 s, seca | **2 na janela de 20 s** (`MEM_SURTO = 2`) |

Reabrir depois de encerrar passa. O laco de script, que dispara dezenas por
segundo, morre na terceira — de graca, sem custar leitura nenhuma.

### 3.3 A mensagem passou a dizer quanto esperar

Nova `esperaAte(escala, agora)` calcula os segundos ate a janela virar e devolve
`esperaSeg` na recusa, do robo ate a tela: **"Tente de novo em N segundos"**.

Antes o lojista via uma porta fechada sem relogio — e a reacao natural a isso e
clicar mais, que e exatamente o que o freio quer evitar.

## 4. Detalhe que evita punicao dupla

**Tentativa barrada nao conta para a hora nem para o dia.** Se contasse, quem
esbarrasse no freio do minuto teria o teto da hora consumido pelas proprias
batidas na porta fechada — o castigo cresceria sozinho.

## 5. Tetos atuais

| O que | Onde | Valor |
| --- | --- | --- |
| surto em memoria | `MEM_JANELA_MS` / `MEM_SURTO` em `moviki/api/live.js` | 2 em 20 s |
| duravel | `FREIO` em `moviki-robo/lib/livesessao.js` | 3/min · 20/hora · 60/dia |
| zera o minuto | `fechar()` em `livesessao.js` | ao encerrar |

## 6. Entrega

| Arquivo | Acao | Marca |
| --- | --- | --- |
| `moviki-robo/lib/livesessao.js` | SUBSTITUI | `2026-09-15-b5a` |
| `moviki/api/live.js` | SUBSTITUI | `2026-09-15-b5a` |
| `moviki-app/live.html` | SUBSTITUI | `2026-09-15-sessao5` |

**Envs:** nenhuma. **Regras:** nenhuma.

## 7. Testes — 8/8

encerrar libera o minuto · hora e dia continuam somando · tentativa barrada nao
conta para a hora · laco sem encerrar morre na 4a · espera calculada por escala
· surto de 2 passa · 3a no mesmo instante barra · sintaxe do JavaScript do
`.html`.

## 8. Conferir depois de subir

1. entrar ao vivo -> 10 s -> encerrar -> entrar de novo: **tem que abrir**;
2. clicar varias vezes **sem encerrar**: na 3a, *"Tente de novo em N segundos"*;
3. Firestore > `live_throttle/{uid}`: `nMin` volta a 0 depois do encerramento,
   `nHora` e `nDia` seguem subindo.

## Ligacoes

[[ARQ - Freio do api live - B5]] · [[P35 - Auditoria de seguranca do Modo Live]] ·
[[ARQ - Sessao da live no servidor]] · [[A13 - Modo Live]]
