---
type: projeto
status: aberto
area: A13 - Modo Live
tags: [live, lancamento, fila, seguranca]
prioridade: alta
prazo: 2026-09-30
atualizado: 2026-09-16
---

# P - Abertura da live para lojista pagante

Substitui a versao anterior, que estava errada: ela dava os lotes **1B, 1C e
1D como pendentes**. Conferido **clonando os quatro repositorios publicos em
16/09/2026**, depois da subida do `exclusao2` — os tres ja estavam no ar.

## Estado

- A live **funciona ponta a ponta**: transmitida de verdade em 16/09, com
  espectadores, oferta relampago, chat e **um Pix pago com dinheiro na conta**.
- **Clientes pagantes reais: zero.** As 6 contas do painel sao de teste.
- O que impedia abrir **nao e mais codigo de saque** — o bloco do dinheiro do
  parceiro esta fechado. Falta **executar** a limpeza e confirmar as regras.

## O que ja esta no ar e a nota anterior dava como pendente

| Lote | Onde | Marca |
| --- | --- | --- |
| **1D** — B11, B12, B13 | `moviki-robo/api/pagar-saque.js` | `2026-09-16-saque1` |
| **1C** — B4, B7 | `moviki/api/live.js` | `2026-09-16-teto3` |
| **1B** — B2, B10 | `moviki-app/eikoadm01.html` | `2026-09-16-exclusao2` |
| **Buracos da exclusao** | `moviki-robo/api/exclusoes.js` | `2026-09-16-exclusao2` |

## A fila, em ordem

### 🔴 Trava a abertura

1. **Confirmar as regras v25 no Console do Firebase.** Nenhum repositorio
   guarda as regras — **so o Console prova**. Tem que valer:
   `livepresenca` com `create` exigindo `liveNoAr(uid)` e presenca expirando em
   10 min · `denuncias` com `create` exigindo `liveNoAr(lojistaUid)` ·
   `saques` com `pedidoEm == request.time`.
2. **Limpar as 6 contas de teste.** O roteiro de quatro passos morreu: o robo
   faz a ordem segura sozinho. Basta excluir pela tela e **ler o resumo**:
   `assinaturaCancelada` verdadeiro · `comissoesGeradasEstornadas` batendo com o
   que o parceiro tinha · nenhum aviso de acesso so desativado. Se aparecer
   **"a assinatura NAO foi cancelada"**, nada foi apagado — resolver no Asaas e
   repetir.
3. **Os testes que ficaram de fora.** Live em **4G** fora de casa · limite de
   **3 h** · cota do teste gratis (2 lives, carencia de 15 min) · card
   **"Pedidos pagos hoje"** depois do fluxo Recebi · carga real de 30
   espectadores.

### 🟠 Antes de reabrir a midia

4. **Teto de minutos POR PLANO.** Hoje so existe a parede **global**
   (`configuracoes/liveTermos.tetoMinutosMes` = 12.000, ciclo dia 12). Um
   lojista consome sozinho e trava a live de todos, sem aviso. Proposta:
   Premium 1.500 · Enterprise 5.000 · teste gratis 300.
5. **`MARCAS_CONFERIDAS` do Vik divergente.** `moviki-ai/lib/catalogoPainel.js`
   espera lojista `asaasconta` e parceiro `trilha`; no ar estao os dois em
   `preco1`. **O Vik esta em modo cauteloso agora, sem aviso na tela** — ele
   atende os lojistas novos assim.
6. **Esvaziar `liveBeta`** (`configuracoes/liveTermos.liveBeta`).
7. **Disparar o `Lead` da CAPI no cadastro de parceiro.** `lib/meta.js` exporta
   `lead()` e **`api/novo-parceiro.js` nao importa `lib/meta`** — a campanha de
   parceiros otimiza sem sinal de conversao.
8. **TTL no Google Cloud** para `livechat`, `livepresenca`, `checkout_freio` e
   `pedidos`. Enquanto nao existir, **"guardado por ate 30 dias" nao e verdade**
   e o custo da presenca e permanente.
9. **Gargalo da aquisicao:** cadastro real vindo de anuncio ainda e **ZERO** —
   215 visitas para 5 na `comerciantes.html`.

### 🟡 Produto, nao trava

- O **mapa da home** nao marca quem esta transmitindo (`moviki/index.html` nao
  le `live_sessoes`)
- O **painel do lojista** nao avisa quando a live dele esta no ar
- O lojista **nao ve o limite de duracao** antes de comecar
- Com a folha aberta no estudio, o chat flutuante fica atras dela
- **"Recebi" mede a diligencia do lojista, nao a venda** — "Vendido pelo Pix"
- Bloco C da auditoria (C1-C4, C7-C9, C12-C15)

### 📄 Documentacao

- **Tres apendices de regras de ouro sem fusao**: 11 a 14/09, 16/09 e o desta
  rodada, em [[ARQ - Buracos da exclusao de conta fechados 16092026]]
- **`MAPA-MESTRE.md` secao 8 esta errada**: da 1B, 1C, 1D e a exclusao como
  pendentes. Secao 5A: v25 ainda marcada "pendente"
- Producao de videos V1 a V5 e 8 avatares — so depois da live abrir

## Ligacoes

[[A13 - Modo Live]] · [[ARQ - Buracos da exclusao de conta fechados 16092026]] ·
[[R - Marcas de versao no ar]] · [[P35 - Auditoria de seguranca do Modo Live]]
