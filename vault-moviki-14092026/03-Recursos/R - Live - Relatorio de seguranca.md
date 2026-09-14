---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, seguranca, auditoria, firestore]
atualizado: 2026-09-14
---

# R - Live - Relatorio de seguranca

Relatório que destravou a subida do Modo Live. Regra fechada na rodada de
12/09/2026: **o módulo só sobe depois do relatório de segurança**. O relatório
foi feito, o módulo subiu.

## O que o relatório cobre

| Camada | Onde mora | O que garante |
| --- | --- | --- |
| Chave de API | só no servidor (`api/live.js`, `lib/checkout.js`) | nenhuma credencial no navegador |
| Webhook do Asaas | token + `confirmarNoAsaas()` | pagamento só vira "pago" depois de conferido na API |
| Preço | calculado no servidor | valor não vem do navegador do comprador |
| Transporte | HTTPS / TLS 1.2+, HSTS pela Vercel | — |
| Chat | escape de XSS | mensagem não injeta código na tela |
| CORS | lista fixa de origens | script de terceiro não chama a API |
| Rate limiting | chat 3 s · checkout 30 por IP a cada 10 min · login pelo Firebase | freio contra abuso automatizado |
| Multitenant | isolamento por `uid` | um lojista não alcança dado de outro |
| Senha | Firebase Auth | hash fora do nosso código |
| Consentimento | Termos, Privacidade e caixa obrigatória no checkout | LGPD |

## Confirmação do pagamento

`confirmarNoAsaas()` confere `externalReference` e valor (tolerância de
R$ 0,01) antes de marcar o pedido como pago. Webhook que não confirma responde
**200** e grava `alerta: divergente` — não libera nada. Responder 200 evita
reentrega infinita; a divergência fica registrada para análise.

## Cabeçalhos de segurança

No `vercel.json` dos dois sites: `X-Content-Type-Options`, `Referrer-Policy`,
`Permissions-Policy` (site sem câmera e microfone; app com), e
`Cross-Origin-Opener-Policy`. HSTS já é enviado pela Vercel.

## Regras do Firestore v23

Publicadas sobre a v22 de 10/09/2026. Nove mudanças, e só elas:

| # | Alvo | Para quê |
| --- | --- | --- |
| 1 | `negocios/{uid}/livechat/{mid}` | visitante anônimo comenta, com filtro de termos graves |
| 2 | `negocios/{uid}/livepresenca/{sid}` | contagem de quem está assistindo |
| 3 | `pedidos/{id}` | o lojista lê os próprios; ninguém escreve pelo app |
| 4 | `checkout_publico/{uid}` | leitura pública, só leitura |
| 5 | match recursivo de `negocios/{uid}` | o admin também escreve — é o que deixa o dono encerrar live alheia |
| 6 | `lives/{id}` | sessão de live, campos fechados |
| 7 | `denuncias/{id}` | denúncia anônima |
| 8 | `live_bloqueios/{uid}` | quem está proibido de transmitir |
| 9 | `moderacao/{id}` e `configuracoes/liveTermos` | registro e termos extras |

Duas funções novas: `liveNoAr(uid)` e `liveCampos(d)`.

Travas que importam:

- Pedido nasce só pelo Admin SDK. `write: false` para todo mundo, inclusive o
  dono — status "pago" nunca nasce no navegador.
- `checkout_contas/{uid}` (chave da subconta, cifrada) **não tem match nenhum**.
  Não é esquecimento, é a trava: ninguém lê nem escreve pelo app.
- Chat só grava com a live no ar (`liveNoAr`, 1 leitura por mensagem). Impede o
  chat de virar mural de spam fora da transmissão.
- `livepresenca` guarda só hora do servidor e validade. Sem nome, sem IP.
- `moderacao` não aceita update nem delete: registro não se reescreve.

Conferência do arquivo: 70/70 chaves, 531/531 parênteses, 27/27 colchetes,
profundidade final zero, 31 correspondências, sem duplicata.

## Discordância dos dois PDFs de referência

Três recomendações foram recusadas, com motivo:

- **Cloudflare como proxy na frente da Vercel.** A Vercel já entrega anti-DDoS,
  WAF e TLS na borda, e não existe IP de origem para esconder porque não há
  servidor próprio. Pôr Cloudflare na frente acrescenta salto, quebra o cache da
  Vercel e cria risco de laço. Cloudflare entra só no Stream, para o vídeo.
- **Formulário obrigatório antes de assistir.** Derruba conversão e cria base de
  dados pessoais sem finalidade — o oposto da minimização que a LGPD exige. Dado
  pessoal só é pedido na compra.
- **"Até 40% de conversão" e "se paga com 1 ou 2 vendas".** Promessa de
  resultado. Não vai para anúncio nem para página de vendas: viola política do
  Meta e do Google e o art. 37 do CDC. Fica como estimativa interna.

Itens que **não se aplicam** e por isso não viraram tarefa: SQL Injection
(Firestore não é SQL), token CSRF (não há cookie de sessão; o idToken vai no
corpo), tokenização de cartão e PCI-DSS (só Pix).

## Riscos residuais aceitos

| Risco | Mitigação aceita |
| --- | --- |
| Lojista adultera as estatísticas da própria sessão | só afeta o relatório dele; KPI de dinheiro vem de `pedidos`, escrito só pelo servidor |
| Filtro de palavra é burlável por gíria nova | denúncia + termos extras pelo painel + encerramento manual |
| Limite de minutos por plano só na tela | custo baixo (US$ 1 por 1.000 min); revisar se houver abuso |
| 2FA do admin não é do sistema | 2FA na conta Google + `emailVerified`; TOTP exigiria Identity Platform |
| App Check ainda não cobre o Auth | rodada própria, fora deste módulo |

## Evidência de teste

- `t_api.js` — 23 casos: sem aceite, título proibido, produto proibido, sacola
  proibida vinda do estado, lojista bloqueado, `adm_encerrar` por não admin, uid
  inválido, encerrar e encerrar de novo.
- `t_seg_est.js` (estúdio) e `t_seg_pub.js` (público, modo normal e modo
  bloqueado) — zero erro de console.
- `t_checkout.js` — 40 casos no robô.
- Regressão verde: `t_webhook.js`, `t_adm.js`, `t_estudio.js`, `t_publico.js`,
  `t_ck_pub.js`, `t_ck_est.js`, `t_404.js`.

## Em aberto

- [ ] Validação dos Termos e da Privacidade por advogado.
- [ ] App Check cobrindo o Auth.
- [ ] Revisar limite de minutos por plano se aparecer abuso.

## Ligações

[[A13 - Modo Live]] · [[A3 - Dados e Regras]] · [[A10 - Conformidade e LGPD]] ·
[[R - Live - Moderacao e regras de conteudo]] ·
[[R - Live - Arquitetura e arquivos]] ·
[[R - Live - Checkout Pix e subcontas Asaas]] ·
[[R - Live - Regras legais e conformidade]] ·
[[R - Historico de regras do Firestore]] · [[R - Colecoes do Firestore]] ·
[[P15 - Enforcement do App Check]] ·
[[ARQ - Modo Live no ar em beta fechado 12092026]]
