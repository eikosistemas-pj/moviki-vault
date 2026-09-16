---
type: area
status: ativo
area: A13 - Modo Live
tags: [live, live-commerce, checkout, pix, cloudflare, asaas]
atualizado: 2026-09-16
---

# A13 - Modo Live

Área dedicada à transmissão ao vivo do lojista (live commerce) e ao pagamento
dentro dela. **Toda nota da live começa com `Live` no nome ou está ligada aqui.**
Nasceu em 11/09/2026.

## Situação em 16/09/2026

**No ar, em beta fechado — e tecnicamente pronto para abrir.** O módulo subiu em
12/09/2026 e desde então passou por três rodadas de endurecimento: sessão da
live no servidor (15/09), fase 2 da auditoria de segurança e **regras v25**
(16/09), e o **teto de gasto de vídeo** (16/09). O beta continua limitado ao
próprio negócio do Paulo.

**O que ainda segura o lançamento aberto:** o teto de 10 subcontas do período de
avaliação do Asaas ([[P29 - Teto de 10 subcontas no Asaas]]) e o **teste de
fumaça**, que nunca foi feito. Ver [[P24 - Modo Live - lancamento]].

## O que é

O lojista Premium ou Enterprise transmite do próprio celular, pelo painel, sem
app e sem seguidores mínimos. O cliente assiste em `moviki.com.br/live/{apelido}`,
vê o produto fixado na tela e compra: no **Enterprise**, paga por **Pix dentro da
live** e o dinheiro cai na conta Asaas do lojista; no Premium, o botão **Quero
este** abre o WhatsApp do lojista com a mensagem pronta. A página pública do
negócio ganha o selo vermelho **AO VIVO**.

**O diferencial que nenhuma live de marketplace tem:** a live é de quem tem
endereço — ou de quem se move. No Enterprise, "Estou aqui agora" põe o botão
Como chegar dentro da live. É o "local life" do Douyin trazido para a feira.

## Mapa da área

| Nota | Para que serve |
| --- | --- |
| [[P24 - Modo Live - lancamento]] | o que já subiu e o que falta para abrir, com checklist |
| [[R - Live - Mercado chines e o que o Moviki copia]] | pesquisa: mecanismos da China e do Brasil, e a divisão Premium x Enterprise |
| [[R - Live - Ferramentas de transmissao]] | por que Cloudflare Stream, custos, alternativas |
| [[R - Live - Arquitetura e arquivos]] | arquivos, dados no Firestore, endpoint, testes |
| [[R - Live - Checkout Pix e subcontas Asaas]] | como o cliente paga dentro da live e o dinheiro cai na conta do lojista |
| [[R - Live - Regras legais e conformidade]] | CDC, sorteio, LGPD, CONAR, texto para termos |
| [[R - Live - Exposicao e interruptores do beta]] | quem enxerga a live hoje e como desligar tudo |
| [[R - Live - Relatorio de seguranca]] | o que foi auditado antes de subir |
| [[R - Live - Moderacao e regras de conteudo]] | filtro de termos e conduta na transmissão |
| [[R - Live - Videoaulas do modulo]] | roteiro das aulas da live |
| [[R - Teto de gasto de video no Cloudflare]] | por que o Cloudflare não tem teto e qual parede o Moviki construiu |
| [[ARQ - Modo Live no ar em beta fechado 12092026]] | o registro da subida |
| [[ARQ - Fase 2 da seguranca da live concluida 16092026]] | B2, B4, B7, B10, B11, B12, B13 e as regras v25 |
| [[ARQ - Teto de gasto de video no ar 16092026]] | a decisão de falhar aberta e o incidente do teste |

## Divisão por plano (decisão do Paulo em 11/09)

Live só no **Premium** e no **Enterprise** (teste grátis entra como Premium). As
ferramentas que mais vendem ficam no **Enterprise, de propósito, para puxar o
cliente para o Enterprise**.

| Premium - Live Essencial | Enterprise - Live Completa |
| --- | --- |
| Transmitir do celular, até 60 min | Tudo do Premium, até 3 h |
| Sacolinha com 5 produtos | Sacolinha com 20 produtos |
| Produto em destaque + Quero este + link | **Pix dentro da live, direto na conta do lojista** |
|  | Oferta relâmpago com contagem regressiva |
| Chat com moderação | Estoque ao vivo "Restam N", que baixa sozinho a cada Pix pago |
| Quem está assistindo (real) | Cupom da live liberado por tempo assistindo |
|  | Pedidos pagos na hora + "Ana comprou" no chat |
| Agendar live + "Lembrar na agenda" | Brinde garantido aos primeiros N pedidos |
| Selo AO VIVO na página | Fila de quem tocou em Quero |
| Avisar clientes (compartilhar) | Dados ao vivo + resumo por produto |
|  | Cortes de 60 s para Reels/Status |
|  | "Estou aqui agora" com Como chegar |

No painel, quem não é Enterprise vê as abas do Enterprise com cadeado e a lista
do que ganha subindo de plano. Quem não tem plano vê a página de venda da live
([[P25 - Pagina de venda da live]]).

## Interruptores (documento `configuracoes/liveTermos`)

| Campo | O que faz |
| --- | --- |
| `liveBeta` | array de uid. Vazio = live aberta. Com alguém = só esses veem o botão, transmitem e abrem conta no Pix |
| `liveDesligada` | chave-mestra: derruba tudo na hora, sem deploy |
| `extras` | termos proibidos que o dono acrescenta ao filtro |
| `demoYoutube` | id do vídeo demo da página de venda |
| `tetoMinutosMes` | **teto de minutos entregues no ciclo do Cloudflare** (hoje 50000) |
| `cicloDia` | **dia da virada do ciclo de faturamento do Cloudflare** (hoje 12) |

Toda escrita do painel do dono usa `merge` — armadilha consertada antes de
subir: `setDoc` sem merge apagaria os outros campos. Desde 16/09 isso ficou
mais grave: sobrescrever o documento inteiro **desliga o teto de vídeo e abre o
beta sem querer**.

## Padrão a manter

- **Número na tela é número contado.** Assistindo, pico, "Restam N" e toques em
  Quero são reais. Escassez inventada é propaganda enganosa (CDC art. 37).
- **Nunca sorteio.** Brinde por ordem de chegada. Sorteio exige autorização do
  Ministério da Fazenda (Lei 5.768/71).
- **O plano decide no servidor.** O endereço de transmissão só sai do
  `api/live.js`; a página pública confere o plano antes de pintar ferramenta do
  Enterprise.
- **Dinheiro da venda nunca passa pela conta da Eiko.** O Pix sai da subconta
  Asaas do lojista. Taxa do Moviki 0% no lançamento (decisão de 11/09).
- **Preço nunca vem do navegador.** O robô lê o preço do estado da live.
- **Live não grava no servidor.** WebRTC do Cloudflare não grava; o corte fica no
  celular do lojista. Nenhum vídeo do cliente mora no Moviki.
- **Módulo novo sobe antes do arquivo que o importa.** `lib/checkout.js` primeiro,
  sozinho; depois `api/pontos.js` e `api/webhook.js`.
- **Autoridade mora fora do alcance do vigiado.** `live_sessoes/{uid}` fica na
  **raiz** do Firestore, escrita só pelo Admin SDK. Dentro de `negocios/{uid}` o
  curinga `match /{documento=**}` daria escrita ao dono e a trava viraria
  enfeite — regra do Firestore não tem "deny".
- **Toda trava do módulo falha fechada, menos uma.** O teto de vídeo falha
  aberta de propósito, porque depende da analytics do Cloudflare, que é um
  terceiro fora do caminho crítico.
- **Trava silenciosa precisa de tela.** O veredito do teto aparece no painel do
  dono como "Próxima live: LIBERADA/BARRADA", com o motivo.

## Em aberto

- [ ] **Teste de fumaça** — presença, denúncia, Vik e card de consumo. Nunca feito
- [ ] Abrir o beta depende da homologação do Asaas ([[P29 - Teto de 10 subcontas no Asaas]])
- [ ] TTL no Google Cloud para `livechat`, `livepresenca`, `checkout_freio`, `pedidos`
- [ ] Bloco C da auditoria (C1–C4, C7–C9, C12–C15)
- [ ] `premium.html` e `enterprise.html` não citam a live em lugar nenhum
- [x] ~~Teto de minutos no servidor~~ — feito em 15/09, no pulso do robô
- [x] ~~Alerta de cobrança no Cloudflare~~ — virou **teto de gasto**, 16/09

## Ligações

[[A1 - Produto e Paineis]] · [[A4 - Financeiro]] · [[A10 - Conformidade e LGPD]] ·
[[A7 - Aquisicao e Midia Paga]] · [[A14 - Material de apoio do parceiro]] ·
[[P28 - Videoaulas do Modo Live]] · [[R - Regras de ouro]] ·
[[R - Marcas de versao no ar]] · [[ARQ - Live escondida durante o beta 14092026]] ·
[[ARQ - Fase 2 da seguranca da live concluida 16092026]] ·
[[ARQ - Teto de gasto de video no ar 16092026]] ·
[[R - Teto de gasto de video no Cloudflare]]
