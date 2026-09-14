---
type: arquivo
status: concluido
area: "[[A13 - Modo Live]]"
tags: [seguranca, dinheiro, webhook, asaas, vercel, marcas]
atualizado: 2026-09-14
---

# Blindagem do caminho do dinheiro — 14/09/2026

Primeira rodada de execucao da [[R - Doutrina de seguranca financeira]]. Fecha
cinco dos achados de [[ARQ - Auditoria de seguranca do dinheiro 14092026]],
antes de comecar a [[P31 - Financeiro e cardapio compravel]].

Vercel Pro assinado por Paulo em 14/09 na equipe eikosistemas-pj — o teto de 12
funcoes do Hobby deixou de existir.

## O que mudou

### 1. Falha fechada no Asaas (achado A5)
`lib/asaas.js` e `lib/checkout.js` caiam no SANDBOX quando `ASAAS_BASE_URL`
faltava. Em producao isso e pior que um erro: as telas continuam normais, as
cobrancas viram cobranca de mentira e ninguem paga nada — sem log e sem
sintoma. Agora, em producao, falta da variavel OU variavel apontando para
sandbox derruba a chamada com mensagem clara. Fora de producao, o sandbox
segue como padrao.

O `lib/asaas.js` e o que cobra as MENSALIDADES — estava exposto desde sempre,
nao so a live.

### 2. A fila do webhook nao pode mais pausar (achados A3 e A4)
O desenho antigo devolvia 500 para o Asaas tentar de novo. Isso resolve uma
falha isolada e e o pior caminho possivel para uma falha sistematica: 15
eventos seguidos com erro PAUSAM a fila inteira, e os eventos somem em 14 dias.

Agora o `api/webhook.js`:
- grava o evento BRUTO em `webhook_eventos/{id}` antes de qualquer regra;
- responde 200 na hora se o evento ja foi processado com sucesso;
- processa, e se falhar marca `status: 'erro'`, avisa o dono no Telegram na
  hora e **ainda responde 200**;
- exporta `processarEvento`, que o reprocessador reaproveita.

Quem tenta de novo virou o `api/webhook-reprocessa.js` (NOVO), cron aos 20
minutos de cada hora, protegido por `CRON_SECRET`: pega os eventos com erro e
os travados em `processando`, reprocessa ate 20 por rodada, desiste depois de 6
tentativas e avisa o que precisa de olho humano. Reprocessar e seguro porque
toda gravacao de dinheiro ja e idempotente por id deterministico.

Token invalido continua respondendo 401 — essa e a barreira, nao um erro de
processamento.

### 3. HSTS e frame-ancestors (achados A1 e A2)
Os dois `vercel.json` ganharam `Strict-Transport-Security` (1 ano,
includeSubDomains, sem preload — reversivel) e
`Content-Security-Policy: frame-ancestors 'self'`.

`frame-ancestors` so funciona em CABECALHO; a CSP do projeto vive em meta tag,
onde essa diretiva e ignorada. Como o cabecalho novo declara apenas essa
diretiva, as CSP em meta das paginas continuam valendo integralmente — nao ha
conflito com `script-src`, inclusive o `'none'` do regras-da-live.html.

## Marcas de versao no ar

| Repositorio | Arquivo | Marca | Tipo |
|---|---|---|---|
| moviki-robo | `api/webhook.js` | 2026-09-14-fila1 | SUBSTITUI |
| moviki-robo | `api/webhook-reprocessa.js` | 2026-09-14-repro1 | NOVO |
| moviki-robo | `lib/asaas.js` | 2026-09-14-falhafechada | SUBSTITUI |
| moviki-robo | `lib/checkout.js` | 2026-09-14-falhafechada | SUBSTITUI |
| moviki-robo | `vercel.json` | cron do reprocessamento | SUBSTITUI |
| moviki | `vercel.json` | HSTS + frame-ancestors | SUBSTITUI |
| moviki-app | `vercel.json` | HSTS + frame-ancestors | SUBSTITUI |

## Colecao nova

`webhook_eventos/{id}` — copia crua de cada evento do Asaas, com status,
tentativas e erro. So o Admin SDK escreve e le; sem match nas regras do
Firestore, portanto nao precisa de regra nova.

## Conferir depois de subir

1. Login com Google no painel continua abrindo (o `frame-ancestors 'self'`
   cobre o iframe do Firebase Auth, que e same-origin pelo rewrite — mas e o
   unico ponto que merece teste).
2. Pagina publica de negocio, live e crachas abrem normal.
3. `/api/webhook-reprocessa?secret=...&dry=1` responde `ok: true`.
4. Um pagamento de teste cria documento em `webhook_eventos` com `status: ok`.
5. O cron aparece na aba Cron Jobs do projeto moviki-robo.

## Fica para a proxima rodada

- A6 freio por conta e por negocio (entra junto da P31).
- A8 reescrita do `lib/checkout.js` nos dois modos de recebimento.
- A10 segundo fator na conta do dono.
- A11 monitoramento diario do caminho do dinheiro.
