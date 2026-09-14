---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, cloudflare, webrtc, whip, whep, custos]
atualizado: 2026-09-14
---

# R - Live - Ferramentas de transmissão

## Escolhida: Cloudflare Stream por WebRTC (WHIP/WHEP)

- O lojista transmite **do navegador do celular**, dentro do painel. Sem app,
  sem inscritos, sem OBS. Só APIs nativas do navegador — nenhuma biblioteca.
- Atraso abaixo de 1 segundo: o chat conversa de verdade com quem está ao vivo.
- Milhares de espectadores simultâneos pela rede do Cloudflare.
- **Limites a lembrar:** WebRTC não grava no servidor, não tem HLS e não dá
  contagem de espectadores pela API. Por isso a contagem é nossa (presença no
  Firestore) e os cortes são gravados no celular do lojista.
- **Porta de entrada:** só o `api/live.js` sabe criar a entrada e entregar o
  endereço de transmissão — e só para quem tem plano.

## Custo (confirmado em 12/09/2026)

| Item | Valor |
| --- | --- |
| Plano Cloudflare Images & Stream | **US$ 0/mês**, pague-pelo-uso |
| Entrada e codificação | grátis |
| Entrega por WebRTC | grátis até 14/10/2026; **US$ 1 por 1.000 minutos assistidos a partir de 15/10/2026** |
| Starter Bundle US$ 5/mês | **não é necessário** — corrige a estimativa de 11/09 |

Exemplo depois de 15/10: live de 30 min com 20 pessoas = 600 min = US$ 0,60.

## Descartadas

| Ferramenta | Por que não |
| --- | --- |
| YouTube Live embutido | 50 inscritos para live pelo celular, até 24 h para ativar e público limitado até 1.000 inscritos. Barra quase todo feirante |
| Instagram / TikTok Live | não dá para embutir na página do Moviki; o cliente sai do link do lojista |
| Amazon IVS | bom e com região São Paulo, mas exige conta AWS, IAM e assinatura de requisição — mais peças para o Paulo manter |
| Mux | sem transmissão pelo navegador |
| LiveKit Cloud | precificação hoje voltada a agentes de voz; custo por participante |

## Plano B

Se o Cloudflare cair ou encarecer, o estúdio e a página só conhecem "um endereço
WHIP e um WHEP". Trocar de fornecedor é trocar o `api/live.js` e o filtro
`whepOk()` da `live.html` — o resto não muda.

## Em aberto

- [ ] Criar alerta de cobrança no Cloudflare antes de 15/10/2026
- [ ] Teto de minutos de transmissão conferido no servidor (hoje só na tela)

## Ligações

[[A13 - Modo Live]] · [[R - Live - Arquitetura e arquivos]] · [[R - Custos e cotas]] ·
[[R - Variaveis de ambiente]] · [[P24 - Modo Live - lancamento]]
