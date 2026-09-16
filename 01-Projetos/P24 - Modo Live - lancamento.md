---
type: projeto
status: ativo
area: A13 - Modo Live
tags: [live, checkout, pix, asaas, cloudflare, beta, lancamento]
atualizado: 2026-09-16
prioridade: 1
prazo: 2026-09-30
---

# P24 - Modo Live - lançamento

## Resultado esperado

Lojista Premium/Enterprise faz live pelo painel; cliente assiste em
`moviki.com.br/live/{apelido}`. No Enterprise, o cliente **paga por Pix dentro
da live** e o dinheiro cai na conta Asaas do lojista.

## Onde está em 16/09/2026

**No ar, em beta fechado — e tecnicamente pronto para abrir.** A fase 2 da
auditoria de segurança foi concluída, as regras do Firestore estão na **v25**, o
teto de gasto de vídeo existe e o módulo de aulas está publicado.

**O que ainda segura:** o teto de 10 subcontas do período de avaliação do Asaas
([[P29 - Teto de 10 subcontas no Asaas]]) e o **teste de fumaça**, que nunca foi
feito.

## Já feito

- [x] Infra, envs, regras v23 (12/09) → **v24** (15/09) → **v25** (16/09)
- [x] Módulo no ar em beta fechado desde 12/09
- [x] Sessão da live no servidor, `live_sessoes/{uid}` na raiz (15/09)
- [x] Fase 2 da segurança: B2, B4, B7, B10, B11, B12, B13
      ([[ARQ - Fase 2 da seguranca da live concluida 16092026]])
- [x] **Teto de gasto de vídeo**, 50.000 min, ciclo dia 12
      ([[ARQ - Teto de gasto de video no ar 16092026]])
- [x] 14 videoaulas com trava de 3 aulas antes de transmitir (15/09)
- [x] Página de venda `/aovivo` pública, sem `noindex`, com o JSON-LD corrigido
      ([[ARQ - Violacao de FAQPage na pagina aovivo 16092026]])
- [x] Site reposicionado para live commerce
      ([[ARQ - Reposicionamento para live commerce 16092026]])
- [x] Material de apoio do parceiro com 81 peças e peças de Modo Live

## O que falta para abrir — nesta ordem

### 1. Teste de fumaça (nunca feito)

- [ ] **Presença** — entrar na live por outro aparelho e conferir que o contador
      sobe. Regra v25 mudou o `create` de `livepresenca`
- [ ] **Denúncia** — enviar uma denúncia com live no ar e conferir que grava;
      com live fora do ar, conferir que a regra v25 recusa
- [ ] **Vik** — perguntar sobre a live e conferir que ele responde com o
      catálogo novo, fora do modo cauteloso
- [ ] **Card de consumo** — conferir os minutos do ciclo e a linha
      "Próxima live: LIBERADA/BARRADA"
- [ ] Teste de teto com **duas pessoas assistindo** e `tetoMinutosMes = 1`, para
      ver a live ser barrada de verdade

### 2. Asaas

- [ ] Falar com o gerente: homologação para sair do teto de 10 subcontas, custo
      por subconta, tarifa do Pix recebido
- [ ] Compra real de R$ 20,00 de outro banco, ponta a ponta

### 3. Abrir

- [ ] **Esvaziar `liveBeta`** no painel do dono. É o passo que abre o produto
- [ ] Tirar `noindex,follow` do `regras-da-live.html`
- [ ] Acrescentar `/aovivo` ao `sitemap.xml`
- [ ] Tornar o filme hero **público** no YouTube
- [ ] **Citar a live no `premium.html` e no `enterprise.html`** — conferido em
      16/09: **zero menção** nas duas, e a `premium.html` é a landing que recebe
      tráfego pago
- [ ] GA4: `purchase_live` e `live_pix_gerado` como conversão

## Não bloqueia, mas fica

- [ ] TTL no Google Cloud (`expiraEm`) em `livechat`, `livepresenca`,
      `checkout_freio`, `pedidos` — sem ele, "guardado por até 30 dias" não é
      verdade
- [ ] Bloco C da auditoria (C1–C4, C7–C9, C12–C15)
- [ ] O **modo cauteloso do Vik não tem indicador**
      ([[ARQ - Incidente - modo cauteloso do Vik ligado sem aviso]])
- [ ] Histórico de pedidos no painel
- [ ] Aviso ao lojista de pedido pago por e-mail/Telegram
- [ ] `WmpIQr36b2o` — aula 08 antiga, com fala errada, ainda publicada como não
      listada no YouTube
- [ ] Conta **Karina** está Enterprise por edição manual no Console, e o pedido
      de teste de R$ 25,41 conta como venda no painel. Mantido de propósito,
      para demonstração — reverter depois

## Riscos e armadilhas

- `lib/checkout.js` depois dos `api/*`: derruba o webhook das assinaturas
- `CHECKOUT_CHAVE` trocada depois de criar subconta: Pix para. **Nunca trocar**
- `LIVE_SEGREDO` está só em **Production** na Vercel. Deploy de Preview não tem
  o segredo e a live não começa — falha fechada, sem erro visível
- Escrita em `configuracoes/liveTermos` é sempre `merge`. Sobrescrever inteiro
  **desliga o teto de vídeo e abre o beta sem querer**
- Abrir o beta sem homologação do Asaas: o 11º lojista não abre conta

## Registro

| Data | O que aconteceu |
| --- | --- |
| 2026-09-11 | Pesquisa, planos, arquivos, regras v23. Checkout Pix decidido |
| 2026-09-12 | Módulo sobe inteiro e invisível, marca `2026-09-12-beta1` |
| 2026-09-14 | Live escondida durante o beta |
| 2026-09-15 | Sessão da live no servidor; fase 1 da auditoria; aulas com trava |
| 2026-09-16 | Fase 2 fechada, regras **v25**, teto de vídeo no ar, site reposicionado, `/aovivo` pública, material com 81 peças, ícones 3D |

## Ligações

[[A13 - Modo Live]] · [[P25 - Pagina de venda da live]] ·
[[P28 - Videoaulas do Modo Live]] · [[P29 - Teto de 10 subcontas no Asaas]] ·
[[P30 - Decisao de dominio apex ou www]] ·
[[P35 - Auditoria de seguranca do Modo Live]] · [[P36 - Memoria da live no Vik]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[R - Teto de gasto de video no Cloudflare]] · [[R - Marcas de versao no ar]]
