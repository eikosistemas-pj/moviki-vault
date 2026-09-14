---
type: projeto
status: em-andamento
area: "[[A13 - Modo Live]]"
tags: [financeiro, checkout, pix, cardapio, asaas, seguranca]
prioridade: alta
prazo: 2026-09-30
atualizado: 2026-09-14
---

# P31 — Financeiro e cardapio compravel

Nota unica do projeto. As entregas concluidas viram nota em `04-Arquivo`; esta
aqui guarda a decisao, o estado e o que falta.

Normativa: [[R - Doutrina de seguranca financeira]].
Entregas: [[ARQ - Auditoria de seguranca do dinheiro 14092026]] ·
[[ARQ - Blindagem do caminho do dinheiro 14092026]] ·
[[ARQ - Checkout em dois modos 14092026]] ·
[[ARQ - Portas separadas do checkout 14092026]] ·
[[ARQ - Aba Financeiro no painel 14092026]]

## Por que existe

O suporte do Asaas nao respondeu sobre o teto de 10 subcontas. Em 14/09 o Paulo
decidiu nao esperar: **"temos que fazer o que puder"**. O projeto tira o Asaas do
caminho critico e, de quebra, abre a venda pelo cardapio — que vende 24h, sem
depender de o lojista fazer live.

## Decisoes fechadas em 14/09

- Cardapio compravel no **Premium e Enterprise**. Live continua so no Enterprise.
- **Pix direto do lojista e o modo PADRAO** — sem Asaas, sem tarifa, sem teto.
  Asaas conectado e upgrade opcional.
- **A responsabilidade pelo pedido e do LOJISTA**, com termo versionado, canal
  de denuncia e bloqueio do reincidente.
- Um unico modulo de checkout serve live e cardapio.
- A aba Financeiro entra no menu lateral **e** como cartao em Ferramentas.

## Os tres modos de recebimento

| Modo | Como funciona | Tarifa | Piso | Confirmacao |
| --- | --- | --- | --- | --- |
| `pix` (padrao) | chave Pix do lojista, copia-e-cola montado no servidor | zero | R$ 5 | o lojista confere o extrato pelos centavos unicos |
| `asaas` (upgrade) | conta Asaas DO LOJISTA por chave de API | R$ 1,99/Pix | R$ 20 | automatica, por webhook |
| `subconta` (legado) | subconta criada pela conta-mae | R$ 1,99/Pix | R$ 20 | automatica |

Um modo ativo por vez. Quem ja tinha subconta ligada cai no legado sozinho.

## No ar em 14/09/2026

**moviki-robo** — `lib/pix.js` (NOVO), `lib/checkout.js` `2026-09-14-aceite`,
`lib/asaas.js` `2026-09-14-falhafechada`, `api/webhook.js` `2026-09-14-fila1`,
`api/webhook-reprocessa.js` (NOVO), `api/pedido.js` (NOVO), `api/financeiro.js`
(NOVO), `vercel.json` com o cron do reprocessamento.

**moviki-app** — `index.html` `2026-09-14-financeiro` com a aba Financeiro
inteira; `vercel.json` com HSTS e `frame-ancestors`.

**moviki** — `vercel.json` com HSTS e `frame-ancestors`.

## Firestore

**Nenhuma regra nova.** Confirmado lendo a v23 publicada, linha a linha:

- `cardapio` e validado so como `is list && size() <= 60` — a regra nao entra nos
  itens, entao o `sku` passa;
- `pedidos/{id}` ja da leitura ao lojista dono, com escrita negada;
- `checkout_publico` ja tem `read: true`;
- `recebimento`, `financeiro_trilha` e `webhook_eventos` nao tem match, de
  proposito.

⚠️ **O `hasOnly` de `negocioValido()` nao conhece campo do Financeiro.** Campo
fora do `hasOnly` faz TODO save do painel ser negado — cardapio, fotos,
promocoes, tudo. Por isso a aba Financeiro **nao grava nada em `negocios/{uid}`**.

## Falta para fechar a Fase 1

1. **Cardapio compravel na pagina publica** (`moviki/404.html`, hoje em
   `2026-09-11-live1`): botao de adicionar por produto vendavel, sacola, tela de
   pedido, QR desenhado pelo `mvqr.js` a partir do copia-e-cola do servidor, e o
   nome e documento do recebedor visiveis para conferencia no banco.
2. **`sku` nos produtos** ao salvar o cardapio no painel.
3. **Icones PNG 3D** de Financeiro, Vender e Vendas — hoje caem no emoji por
   `onerror`, que e degradacao limpa, mas destoa dos outros.
4. **Aulas 07R, 08R e 14**, que so podem ser gravadas com as telas no ar.

## Dividas registradas

- Lista de vendas consulta so por igualdade com `limit(200)` e ordena no
  navegador. Acima de 200 pedidos por negocio, criar indice composto no console.
- Segundo fator na conta do dono (Identity Platform) antes do primeiro lojista
  real vender.
- Monitoramento diario do caminho do dinheiro (fila do webhook, pedido preso,
  pico num negocio so).
- App Check no Authentication.
- Teto de 10 subcontas no Asaas — **agora sem bloquear nada**.
