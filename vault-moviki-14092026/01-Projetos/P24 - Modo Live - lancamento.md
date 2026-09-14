---
type: projeto
status: bloqueado
area: A13 - Modo Live
tags: [live, checkout, pix, asaas, cloudflare, beta]
atualizado: 2026-09-14
prioridade: 1
prazo: 2026-09-30
---

# P24 - Modo Live - lançamento

## Resultado esperado

Lojista Premium/Enterprise faz live pelo painel; cliente assiste em
`moviki.com.br/live/{apelido}`. No Enterprise, o cliente **paga por Pix dentro da
live** e o dinheiro cai na conta Asaas do lojista.

## Onde está hoje (14/09/2026)

**No ar em beta fechado.** A subida aconteceu em 12/09/2026: 15 arquivos nos três
repositórios na marca `2026-09-12-beta1` e regras do Firestore v23 publicadas.
O beta está limitado ao próprio negócio do Paulo pelo campo `liveBeta` em
`configuracoes/liveTermos`.

**O lançamento aberto está BLOQUEADO.** O Asaas está em período de avaliação
regulatória: **10 subcontas, R$ 2.000 em cobranças por subconta, 60 dias**.
Abrir a live para a base estoura o teto — ver
[[P29 - Teto de 10 subcontas no Asaas]].

## Já feito

- [x] Cloudflare: conta, Stream ligado, `CF_ACCOUNT_ID` e `CF_STREAM_TOKEN` na Vercel (projeto do site)
- [x] `FIREBASE_SA_LEITURA` (projeto moviki), `CHECKOUT_CHAVE` e `ASAAS_WEBHOOK_TOKEN_PEDIDOS` (projeto moviki-robo) — feitas em 11/09
- [x] Firestore: regras v23 publicadas sobre a v22 de 10/09
- [x] **moviki-robo**, sozinho e primeiro: `lib/checkout.js` (NOVO)
- [x] **moviki-robo**: `api/pontos.js`, `api/webhook.js` (SUBSTITUI)
- [x] **moviki**, textos primeiro: `regras-da-live.html` (NOVO), `termos.html`, `privacidade.html` (SUBSTITUI)
- [x] **moviki**: `api/live.js`, `live.html` (NOVO), `vercel.json`, `404.html` (SUBSTITUI)
- [x] **moviki-app**: `live.html` (NOVO), `eikoadm01.html`, `index.html`, `vercel.json` (SUBSTITUI), `icones/live.png` (NOVO)
- [x] Beta fechado no painel do dono: Lives > "Quem pode fazer live" > só o próprio negócio

## Para abrir o beta

- [ ] Falar com o gerente do Asaas: homologação para sair do teto de 10 subcontas, custo por subconta e confirmação da tarifa do Pix recebido
- [ ] Teste real: live pelo celular + outro aparelho no 4G em `moviki.com.br/live/apelido` — vídeo, chat, selo AO VIVO na página
- [ ] Aba **Receber no Pix**: abrir a subconta com o CPF do Paulo, enviar documentos, esperar aprovação, ligar
- [ ] Compra real de R$ 20,00 de outro banco: QR, pagamento, "Pagamento confirmado", pedido pago no estúdio, estoque da oferta baixando, saque no app do Asaas
- [ ] premium.html, enterprise.html e comparativo: live no Premium, Pix na live no Enterprise (descrever a ferramenta, nunca venda)
- [ ] Página de venda da live ([[P25 - Pagina de venda da live]])
- [ ] Vik: ensinar o que a live e o Pix fazem e em qual plano estão
- [ ] Videoaulas "Sua primeira live" e "Receber no Pix pela live" ([[P28 - Videoaulas do Modo Live]])
- [ ] GA4: `purchase_live` e `live_pix_gerado` como conversão
- [ ] Decidir o domínio antes de divulgar o link da live ([[P30 - Decisao de dominio apex ou www]])

## Não bloqueia, mas fica

- [ ] TTL no Google Cloud (`expiraEm`) em `livechat`, `livepresenca`, `checkout_freio`, `pedidos`
- [ ] Alerta de cobrança no Cloudflare (WebRTC cobra a partir de 15/10/2026)
- [ ] Teto de minutos no servidor (hoje só na tela)
- [ ] Histórico de pedidos no painel (hoje: pedidos de hoje, no estúdio)
- [ ] Aviso ao lojista de pedido pago também por e-mail/Telegram

## Fase 3

Compra em grupo · seguir o negócio + aviso de "entrou ao vivo" · replay por
produto · anúncio que leva direto à live · Vik no chat · roteiro pelo Vik · OBS
com retransmissão · co-live · apresentador virtual rotulado · cartão no Pix.

## Riscos e armadilhas

- `lib/checkout.js` depois dos `api/*`: derruba o webhook das assinaturas. Por
  isso ele subiu sozinho e primeiro.
- `CHECKOUT_CHAVE` trocada depois de criar subconta: chaves ilegíveis, Pix para.
  **Nunca trocar essa env.**
- Regras depois dos arquivos: chat "Não foi", contador zero e pedidos invisíveis
  para o lojista — o pagamento em si funciona.
- Webhook da subconta não configurado: o pedido ainda vira pago pela tela do
  comprador ou pelo botão **Conferir pagamento** do lojista.
- Abrir o beta sem homologação do Asaas: o 11º lojista não consegue abrir conta.

## Registro

| Data | O que aconteceu |
| --- | --- |
| 2026-09-11 | Live: pesquisa, planos, arquivos e regras v23. Checkout Pix decidido (0%, Enterprise, só Pix, sem frete). Nada no ar |
| 2026-09-11 | Envs criadas no Cloudflare, na Vercel do site e na do robô |
| 2026-09-12 | Módulo sobe inteiro e invisível: 15 arquivos, marca `2026-09-12-beta1`, regras v23 publicadas, beta fechado no próprio negócio do Paulo |
| 2026-09-12 | Custos confirmados: Cloudflare US$ 0/mês pague-pelo-uso, Asaas R$ 1,99 fixos por Pix. Pedido mínimo sobe de R$ 5 para R$ 20 |
| 2026-09-14 | Live escondida durante o beta ([[ARQ - Live escondida durante o beta 14092026]]) |

## Ligações

[[A13 - Modo Live]] · [[R - Live - Arquitetura e arquivos]] ·
[[R - Live - Checkout Pix e subcontas Asaas]] · [[R - Live - Ferramentas de transmissao]] ·
[[R - Live - Regras legais e conformidade]] · [[R - Live - Exposicao e interruptores do beta]] ·
[[P29 - Teto de 10 subcontas no Asaas]] · [[R - Checklist de deploy]] ·
[[ARQ - Modo Live no ar em beta fechado 12092026]] · [[R - Retomada live parte 02]]
