---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, arquitetura, firestore, vercel, webrtc, arquivos]
atualizado: 2026-09-14
---

# R - Live - Arquitetura e arquivos

## O caminho de uma live

1. Lojista abre `app.moviki.com.br/live.html` (botão **Fazer live** no painel).
2. O estúdio chama `moviki.com.br/api/live` com `acao:'nivel'` — o servidor confere
   o token e lê `assinaturas/{uid}` pela conta de serviço só-leitura
   (`FIREBASE_SA_LEITURA`). Sem plano: página de venda da live.
3. **Entrar ao vivo** chama `acao:'iniciar'`: o servidor cria (uma vez por
   lojista, nome `mv-{uid}`) ou reaproveita a entrada no Cloudflare e devolve
   WHIP (segredo) e WHEP (público).
4. O navegador do lojista manda o vídeo por WHIP e grava
   `negocios/{uid}/estado/live` com `ativa:true`, `whep`, produtos e ferramentas.
5. O cliente abre `moviki.com.br/live/{apelido}`: lê o `slugs`, o estado e a
   assinatura; toca o vídeo por WHEP; comenta em `livechat`; carimba
   `livepresenca` a cada 60 s.
6. O estúdio carimba `pulso` a cada 45 s e conta a presença a cada 30 s. Sem
   pulso há 3 min, a página pública considera a live encerrada.

## Arquivos — os 15 que subiram em 12/09/2026

| Repo | Arquivo | Ação | Papel |
| --- | --- | --- | --- |
| moviki-robo | `lib/checkout.js` | NOVO | checkout Pix (subcontas Asaas). Módulo, não conta no teto de 12 funções. **Subiu sozinho e primeiro** |
| moviki-robo | `api/pontos.js` | SUBSTITUI | recebe as ações `loja_*` e `compra_*` |
| moviki-robo | `api/webhook.js` | SUBSTITUI | desvia `pedido:<id>` antes de tudo e aceita `ASAAS_WEBHOOK_TOKEN_PEDIDOS` |
| moviki | `regras-da-live.html` | NOVO | regras de conteúdo da transmissão |
| moviki | `termos.html` | SUBSTITUI | cláusulas da live e do checkout |
| moviki | `privacidade.html` | SUBSTITUI | chat, presença, CPF no checkout |
| moviki | `api/live.js` | NOVO | porta: token, plano, Cloudflare. 3ª função do projeto do site |
| moviki | `live.html` | NOVO | página vertical de quem assiste |
| moviki | `vercel.json` | SUBSTITUI | rota `/live/:slug` antes do curinga de apelido |
| moviki | `404.html` | SUBSTITUI | selo AO VIVO na página do negócio |
| moviki-app | `live.html` | NOVO | estúdio do lojista |
| moviki-app | `eikoadm01.html` | SUBSTITUI | painel do dono: Lives, chave-mestra, Conferir no Asaas |
| moviki-app | `index.html` | SUBSTITUI | botão Fazer live (Ação rápida e Ferramentas) |
| moviki-app | `vercel.json` | SUBSTITUI | rota do estúdio |
| moviki-app | `icones/live.png` | NOVO | ícone 3D, 256x256 |
| Firestore | regras v23 | publicada | `livechat`, `livepresenca`, `pedidos`, `checkout_publico`, `liveTermos` |

Ordem obrigatória do upload: regras > `lib/checkout.js` sozinho > `api/*` do robô >
textos do site > páginas do site > painel. Invertido, o `require` de um módulo
inexistente derruba a função do dinheiro.

## Dados

`negocios/{uid}/estado/live` (sem regra nova — o match recursivo dá escrita ao
dono e leitura a todos): `ativa`, `titulo`, `inicio`, `pulso`, `fim`, `whep`,
`nivel`, `assistindo`, `sacola[]`, `fixado`,
`oferta{nome,precoDe,precoPor,fimEm,estoque,vendidos}`,
`cupom{codigo,texto,minutos}`, `brinde{texto,primeiros}`, `local`,
`agendada{em,titulo}`.

`negocios/{uid}/livechat/{id}`: `nome`, `texto`, `tipo` (`msg`, `quero`, `dono`),
`criadoEm`, `expiraEm` (30 dias).

`negocios/{uid}/livepresenca/{aba}`: `em`, `expiraEm` (2 dias).

`configuracoes/liveTermos`: `liveBeta` (array de uid), `liveDesligada`
(chave-mestra) e `extras` (termos proibidos). Toda escrita com `merge`.

O checkout Pix está detalhado em [[R - Live - Checkout Pix e subcontas Asaas]].

## Travas

- Endereço WHIP só sai do servidor, para o dono da conta, com plano.
- Ferramenta do Enterprise só é pintada na página pública se `assinaturas/{uid}`
  disser Enterprise — estado forjado por lojista de outro plano não aparece.
- WHEP só toca se casar com `customer-*.cloudflarestream.com/<32 hex>/webRTC/play`;
  link de produto só se for `https://`; foto só do Storage/ibb; todo texto com `esc()`.
- Chat anônimo só enquanto `ativa:true` (regra), 140 caracteres, 1 mensagem a
  cada 3 s na tela; lojista apaga qualquer mensagem.
- CSP das páginas novas inclui `*.cloudflarestream.com` no `connect-src`.
  App Check inicializado nas duas (Firestore enforçado desde 05/09).

## Testes antes da entrega (Playwright + Firebase de mentira)

- Entrega de 11/09: estúdio Enterprise e Premium com câmera falsa e WebRTC real
  em laço local (servidor recebeu áudio e vídeo, `connected`), sacolinha,
  destaque, chat, fila, oferta, cupom, brinde, local, corte de 2 s, contagem de
  presença, encerrar e resumo. Página pública nos quatro níveis, agendada, sem
  pulso, WHEP com recusa e nova tentativa. `api/live.js` em 14 casos.
  `404.html` com e sem live.
- Rodada de 12/09, antes de subir: **48 casos no robô, 26 na API do live** e a
  suíte de browser inteira (estúdio, público, checkout, painel do dono,
  segurança, chave-mestra, beta). Zero erro de console. Regras v23 balanceadas.

**O que só o teste real prova:** o Cloudflare de verdade, o 4G da feira e o
Safari do iPhone.

## Ligações

[[A13 - Modo Live]] · [[P24 - Modo Live - lancamento]] ·
[[R - Live - Ferramentas de transmissao]] · [[R - Live - Checkout Pix e subcontas Asaas]] ·
[[R - Live - Relatorio de seguranca]] · [[R - Colecoes do Firestore]] ·
[[R - Historico de regras do Firestore]] · [[R - Stack e repositorios]] ·
[[R - Marcas de versao no ar]]
