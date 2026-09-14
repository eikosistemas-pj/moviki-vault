---
type: area
status: ativo
area: A13 - Modo Live
tags: [live, live-commerce, checkout, pix, cloudflare, asaas]
atualizado: 2026-09-14
---

# A13 - Modo Live

Área dedicada à transmissão ao vivo do lojista (live commerce) e ao pagamento
dentro dela. **Toda nota da live começa com `Live` no nome ou está ligada aqui.**
Nasceu em 11/09/2026.

## Situação em 14/09/2026

**No ar, em beta fechado.** O módulo subiu em 12/09/2026 — 15 arquivos nos três
repositórios, marca `2026-09-12-beta1`, regras do Firestore v23 publicadas. O
beta está limitado ao próprio negócio do Paulo: ninguém mais vê o botão
**Fazer live**. O lançamento aberto está **bloqueado** pelo teto de 10 subcontas
do período de avaliação do Asaas — ver [[P29 - Teto de 10 subcontas no Asaas]].

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
| [[ARQ - Modo Live no ar em beta fechado 12092026]] | o registro da subida |

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

Toda escrita do painel do dono usa `merge` — armadilha consertada antes de subir:
`setDoc` sem merge apagaria os outros dois campos.

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

## Em aberto

- [ ] Abrir o beta depende da homologação do Asaas ([[P29 - Teto de 10 subcontas no Asaas]])
- [ ] TTL no Google Cloud para `livechat`, `livepresenca`, `checkout_freio`, `pedidos`
- [ ] Teto de minutos no servidor (hoje só na tela)
- [ ] Alerta de cobrança no Cloudflare (WebRTC cobra a partir de 15/10/2026)

## Ligações

[[A1 - Produto e Paineis]] · [[A4 - Financeiro]] · [[A10 - Conformidade e LGPD]] ·
[[A7 - Aquisicao e Midia Paga]] · [[A14 - Material de apoio do parceiro]] ·
[[P28 - Videoaulas do Modo Live]] · [[R - Regras de ouro]] ·
[[R - Marcas de versao no ar]] · [[ARQ - Live escondida durante o beta 14092026]]
