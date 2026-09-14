---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, entrega, beta, cloudflare, demo]
atualizado: 2026-09-14
---

# ARQ - Modo Live no ar em beta fechado 12092026

Registro da madrugada de 12/09/2026: o Modo Live subiu. **Beta fechado**, com
apenas o negócio do Paulo na lista — nenhum outro lojista via a live.

## O que subiu

**15 arquivos nos três repositórios**, conferidos **byte a byte** contra o que
foi entregue, clonando os repos — não confiando na tela da Vercel.

**Regras do Firestore v23 publicadas sobre a v22 de 10/09.** A ordem foi
respeitada: regras primeiro, depois o `lib/checkout.js` sozinho, depois o resto.

| Repo | Arquivos |
| --- | --- |
| moviki | `api/live.js`, `live.html`, `regras-da-live.html`, `termos.html`, `privacidade.html`, `404.html`, `vercel.json` |
| moviki-app | `live.html`, `eikoadm01.html`, `index.html`, `vercel.json`, `icones/live.png` |
| moviki-robo | `lib/checkout.js`, `api/pontos.js`, `api/webhook.js` |

## Pendência encerrada sem atendente

Painel do dono, botão "Conferir no Asaas": **Liberado, 0 de 10 subcontas**. A
conta da Eiko pode criar subconta por API. O teto de dez virou o
[[P29 - Teto de 10 subcontas no Asaas]].

## O incidente do CORS

O estúdio não abria, só `(rede)`. Causa: na Vercel, `moviki.com.br` está como
**"Redirects to www.moviki.com.br"**, e redirecionamento entre origens troca a
origem por `null` — o navegador então bloqueia por CORS. Consertado nos dois
arquivos que falam com a API: chamada direta ao www, corpo em `text/plain` para
dispensar a checagem prévia, e `www.moviki.com.br` liberado na CSP. O painel do
dono tinha o mesmo defeito no botão "Encerrar live", corrigido junto. Nada mudou
no servidor. Detalhe e decisão pendente em
[[P30 - Decisao de dominio apex ou www]].

## Vídeo demo da tela de venda

Ideia do Paulo, com uma correção: **não é videoaula**. Quem toca em "Fazer live"
sem plano quer ver funcionando, não aprender a usar — videoaula é depois de
assinar.

- **`demo-live-moviki.mp4`** — 58 s, 1080x1350 (4:5), 5,3 MB, narração da Malu
  (voz oficial). Capa `capa-youtube.png`, 1280x720.
- Roteiro: abertura, escolher produto e título, ligar a câmera, entrar ao vivo,
  quem entra vê ao vivo, chat, oferta relâmpago com tempo e estoque reais,
  "Ana comprou", checkout sem sair da live, Pix com QR, pagamento confirmado com
  o dinheiro na conta do lojista, cartão com os dois planos. Trechos do
  Enterprise levam selo dourado.
- **Funciona sem som**: toda mensagem está na legenda, porque navegador não toca
  áudio sozinho.
- Feito **sem gravação de tela e sem filmagem**: saiu do mesmo estúdio Playwright
  que testa a live, com painel e página pública reais contra um Firebase de
  mentira, dirigidos por roteiro com tempos cravados. A "câmera" é a
  `vendedor.jpg` do próprio site com zoom lento. Legendas e cartões renderizados
  no navegador com Poppins e compostos com ffmpeg.
- Duas armadilhas encontradas: o Chromium do Playwright **não toca H.264** (o
  vídeo de entrada tem de ser WebM VP8/VP9), e o `whepOk()` valida o formato do
  endereço do Cloudflare — endereço fora do padrão faz a página achar que a live
  não está no ar.
- O id do vídeo mora em `configuracoes/liveTermos.demoYoutube`, editável no
  painel do dono > Lives. Trocar o vídeo não exige subir arquivo. Sem id, a
  caixa nem aparece. Player `youtube-nocookie`, sem autoplay; a CSP do estúdio
  ganhou `frame-src https://www.youtube-nocookie.com`.
- O vídeo **não é hospedado no Moviki**: 5 MB por visita derrubariam a página no
  4G.

## Também nesta rodada

- Botões da tela de venda: o dourado era `inline-flex` sem largura e encolhia.
  Agora os dois têm a mesma largura, com o Enterprise em cima — a tela termina
  listando o que só o Enterprise tem.
- Selo **AO VIVO** da página pública quebrava em duas linhas em tela estreita.
  Corrigido.

## Infra e variáveis

Cloudflare no plano **Images & Stream**, custo **US$ 0/mês** no volume atual; o
Stream é usado só para o vídeo da transmissão — a Vercel continua sozinha na
frente do site.

Variáveis, só em Production:

| Projeto | Variáveis |
| --- | --- |
| moviki | `CF_ACCOUNT_ID`, `CF_STREAM_TOKEN`, `FIREBASE_SA_LEITURA` |
| moviki-robo | `CHECKOUT_CHAVE` (**nunca trocar**), `ASAAS_WEBHOOK_TOKEN_PEDIDOS` |

## Decisões comerciais da rodada

- Cláusula de tarifa futura: **valor fixo em reais por pedido**, nunca
  percentual, com aviso de **30 dias** por e-mail e no painel e saída sem multa.
  Está nos Termos, §6-C.
- Enterprise fica em **R$ 99,90**, com a live dentro. Taxa do Moviki **0%** no
  lançamento.

## Riscos residuais aceitos

| Risco | Mitigação |
| --- | --- |
| Lojista adultera as estatísticas da própria sessão | só afeta o relatório dele; KPI de dinheiro vem de `pedidos`, escrito só pelo servidor |
| Filtro de palavra é burlável por gíria nova | denúncia + termos extras pelo painel + encerramento manual |
| Limite de minutos por plano só na tela | custo baixo (US$ 1 por 1.000 min); revisar se houver abuso |
| 2FA do admin não é do sistema | 2FA na conta Google + `emailVerified`; TOTP exigiria Identity Platform |
| App Check ainda não cobre o Auth | rodada própria |

Três recomendações dos dois PDFs de referência foram recusadas com motivo
técnico registrado (Cloudflare como proxy na frente da Vercel, formulário
obrigatório antes de assistir, e as promessas de conversão). Estão em
[[R - Live - Relatorio de seguranca]].

## Testes

48 casos no robô, 26 na API e a suíte de navegador inteira — estúdio, público,
checkout, painel do dono, segurança, chave-mestra, beta e tela de venda. Zero
erro de console.

## Marcas de versão

| Repo | Arquivo | Marca |
| --- | --- | --- |
| moviki | `api/live.js` | 2026-09-12-beta1 |
| moviki | `live.html` | 2026-09-12-pill1 |
| moviki | `regras-da-live.html` | 2026-09-11-regras1 |
| moviki | `termos.html` | 2026-09-12-live1 |
| moviki | `privacidade.html` | 2026-09-12-live1 |
| moviki | `404.html` | 2026-09-11-live1 |
| moviki-app | `live.html` | 2026-09-12-demo1 |
| moviki-app | `eikoadm01.html` | 2026-09-12-demo1 |
| moviki-app | `index.html` | 2026-09-11-live1 |
| moviki-robo | `lib/checkout.js` | 2026-09-11-seguranca1 |
| moviki-robo | `api/pontos.js` | 2026-09-11-checkout1 |
| moviki-robo | `api/webhook.js` | 2026-09-11-checkout1 |
| Firestore | regras | v23 |

## Ficou em aberto

- [ ] Ligar 2FA na conta Google antes de abrir o painel de lives.
- [ ] Validação dos Termos e da Privacidade por advogado.
- [ ] Primeira live em conta de teste, com o painel do dono aberto ao lado.

## Ligações

[[A13 - Modo Live]] · [[A2 - Infraestrutura e Deploy]] · [[A4 - Financeiro]] ·
[[R - Live - Relatorio de seguranca]] ·
[[R - Live - Moderacao e regras de conteudo]] ·
[[R - Live - Arquitetura e arquivos]] ·
[[R - Live - Checkout Pix e subcontas Asaas]] ·
[[R - Live - Ferramentas de transmissao]] · [[R - Variaveis de ambiente]] ·
[[R - Custos e cotas]] · [[P24 - Modo Live - lancamento]] ·
[[P25 - Pagina de venda da live]] · [[P29 - Teto de 10 subcontas no Asaas]] ·
[[P30 - Decisao de dominio apex ou www]] ·
[[ARQ - Incidente - webhook do Asaas 401 em producao]] ·
[[ARQ - Live escondida durante o beta 14092026]]
