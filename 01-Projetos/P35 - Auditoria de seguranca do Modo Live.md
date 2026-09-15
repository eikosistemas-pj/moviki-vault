---
type: projeto
status: bloqueado
area: A13 - Modo Live
tags: [live, seguranca, red-team, dinheiro, lgpd, armadilha]
prioridade: 1
prazo: antes de soltar o Modo Live
atualizado: 2026-09-15
---

# P35 — Auditoria de seguranca do Modo Live

Varredura adversarial de 15/09/2026, lendo os cinco repositorios e as regras
v23 — **nao a memoria das rodadas anteriores**. Tres frentes em paralelo:
transmissao e pagina publica · estudio, painel do dono e regras · caminho do
dinheiro. Os achados abaixo foram **reconferidos no codigo**, linha por linha.

**Veredito: o Modo Live nao pode sair do beta fechado com os itens do Bloco A
abertos.** Dois deles nao sao da live — sao do dinheiro do Moviki inteiro, e um
lojista Enterprise ja consegue explorar hoje.

---

## O padrao que explica quase tudo

> **Toda decisao que importa mora num documento que o proprio vigiado escreve.**

`negocios/{uid}/estado/live` nao tem regra propria: cai no curinga
`match /{documento=**} { allow write: if request.auth.uid == uid }`, sem
`hasOnly`, sem validacao de campo. E e esse documento que decide **se a live
esta no ar**, **qual video toca**, **qual preco vale** e **o que a moderacao ve**.

O `api/live.js` esta bem feito — confere plano, bloqueio, beta, aceite e termos
no servidor. **Mas ele so guarda a porta de entrada do WHIP.** A pagina publica
nunca fala com ele: ela le o Firestore e acredita.

Sete dos achados abaixo sao a mesma doenca.

---

## BLOCO A — trava o lancamento

### A1. CRITICA · O token do webhook e entregue a cada lojista Enterprise

`mr/lib/checkout.js:316-325` grava o webhook **dentro da subconta Asaas do
lojista** usando `ASAAS_WEBHOOK_TOKEN_PEDIDOS`. A subconta e aberta com o nome,
o CPF e **o e-mail dele** (`checkout.js:293-298`) — ele entra no Asaas pelo
proprio e-mail e le o token em Integracoes → Webhooks.

`mr/api/webhook.js:585-591` aceita **os tres tokens no mesmo endpoint, para
qualquer evento**, sem escopo.

**Ataque:** com o token na mao, ele faz
`POST /api/webhook` com `{event:'PAYMENT_RECEIVED', payment:{id:'x', externalReference:'<uid>', value:99.90}}`
→ `webhook.js:534-547` liga `assinaturas/{uid}` por 34 dias. **De graca, para
sempre, para a conta dele ou a de qualquer outro uid.** Com `TRANSFER_DONE`
fecha saque; com `PAYMENT_REFUNDED` derruba pedido pago alheio.

**Pior:** `acumularComissoes` (`webhook.js:191-195`) usa `Number(pay.value)` do
proprio payload. Um evento com `value: 20000` gera comissao de R$ 3.000 para o
parceiro que ele escolher — **sacavel por Pix**.

**Correcao:**
1. token **unico por subconta**, gerado no `lojaCriar` e guardado cifrado em
   `checkout_contas`;
2. no `webhook.js`, o token de pedidos so vale para o ramo `pedido:`;
3. no ramo que LIGA assinatura, **reconferir no Asaas** (`GET /payments/{id}`
   com a chave-mae) e usar valor e status que o Asaas devolver, descartando o
   payload — e exatamente o que o caminho de pedido ja faz em
   `checkout.js:1241` e o caminho da mensalidade nao faz.

⚠️ Confirmar no painel do Asaas se o titular da subconta enxerga mesmo o
`authToken`. O codigo prova que o token **e enviado** para la; a leitura pelo
lojista nao foi testada contra a API real. **Se enxergar, e a falha mais grave
do sistema** — e existe desde antes da live.

### A2. CRITICA · Retransmitir a live de outro lojista dentro da propria marca

`m/live.html:396` le `negocios/{uid}/estado/live` e `:413` decide
`ativa===true && whepOk(whep) && pulso < 3 min`. **`whepOk()` so confere o
formato da URL.** E `negocios/*` e `read: true`.

**Ataque:** um lojista em **teste gratis** (que entra como Premium,
`api/live.js:226`) le o `whep` de uma live de verdade e escreve no proprio
`estado/live`: `{ativa:true, pulso:agora, whep:<whep alheio>, titulo:…, sacola:[…]}`.
Fica AO VIVO em `moviki.com.br/live/<apelido dele>` transmitindo a imagem do
outro, **com o WhatsApp dele, os produtos dele e o Pix dele** — sem aceitar as
Regras da Live, sem passar pelo beta, sem filtro de termos e **sem o
`api/live.js` ser chamado uma unica vez**.

**Correcao: A4 (abaixo) resolve este e mais seis.**

### A3. CRITICA · "Encerrada pelo Moviki" so existe no navegador do lojista

O painel grava `encerradaPor:'moviki'` em `estado/live`
(`ma/eikoadm01.html:3835`). Quem le esse campo: **so o estudio do proprio
lojista** (`ma/live.html:541`). `grep encerradaPor` nos repos `m/` e `mr/`
devolve **zero** — a pagina publica e o `api/live.js` ignoram.

`adm_encerrar` (`m/api/live.js:307-324`) apaga a entrada do Cloudflare **e nada
mais**: nao grava `live_bloqueios`, nao marca nada no servidor.

**Ataque:** encerrado no meio de uma live proibida (ou com o castigo "so
encerrar, sem bloquear"), ele roda `updateDoc(estado/live,{encerradaPor:null})`
no console, clica em Entrar ao vivo e **o `iniciar` cria uma entrada nova**. De
volta ao ar em 20 segundos.

**Correcao imediata (5 linhas):** `adm_encerrar` grava `live_bloqueios/{uid}`
na mesma operacao, mesmo que por 24 h — o `iniciar` ja respeita esse documento
em `live.js:361-364`.

### A4. CRITICA · A correcao estrutural: tirar a autoridade da mao do lojista

Nao adianta remendar A2 e A3 separados. **Separar CONTEUDO de AUTORIDADE:**

| Documento | Quem escreve | O que guarda |
| --- | --- | --- |
| `negocios/{uid}/estado/live` | lojista (como hoje) | titulo, sacola, fixado, oferta, cupom, brinde — **conteudo** |
| `negocios/{uid}/estado/liveSessao` | **so o robo** (Admin SDK) | `ativa`, `whep`, `inicioEm`, `entradaId`, `encerradaPor`, `limiteMin` — **autoridade** |

- a pagina publica passa a decidir "esta no ar" e **de onde vem o video** pelo
  `liveSessao`; `estado/live` vira so texto na tela, ja filtrado;
- regra: `liveSessao` com `allow write: if false` (cliente nao toca);
- o **pulso vira um POST ao robo** a cada 45 s, em vez de escrita direta. Barato,
  e passa a ser o batimento que aplica **o teto de minutos** e **a cota de lives
  do teste gratis** de [[P34 - Travas contra abuso do teste gratis]].

**Isto conserta de uma vez:** A2, A3, B1, B2, B3, B6 e a pendencia antiga do
teto de minutos. **E o item de maior retorno da lista inteira.**

### A5. CRITICA · Auto-indicacao: o parceiro ganha comissao da propria mensalidade

`indicacoes/{uid}` e criado pelo proprio usuario (`ma/index.html:2841`, a partir
do `?ref=` da URL) e `mr/api/webhook.js:198-226` credita **sem nunca comparar
`p1.uid` com `lojistaUid`**. A trava equivalente **existe** na cadeia de
parceiros (regra de `parceiros`: `indicadoPor != slug`) e **falta** aqui.

**Ataque:** o parceiro aprovado abre a propria conta de lojista com
`?ref=<slug dele>`, assina Enterprise e recebe 15-18% de volta todo mes, para
sempre. O upline dele ainda leva N2 e N3.

**Correcao:** `if (p1.uid === lojistaUid) return;` em `acumularComissoes`, e o
mesmo para p2 e p3.

---

## BLOCO B — antes de sair do beta fechado

**B1. O endereco WHIP e eterno.** `m/api/live.js:250-291` reaproveita a entrada
`mv-<uid>` "para sempre". O lojista copia o WHIP do DevTools na unica vez que
precisa do `iniciar` e publica por OBS/ffmpeg **depois do teste gratis vencer**.
→ entrada por **sessao**, apagada no encerrar; ou cron do robo varrendo
`live_inputs` e apagando as de quem esta inativo. Resolvido junto com A4.

**B2. Transmitir invisivel para a moderacao.** O painel lista lives por
`collection('lives') where ativa==true` (`eikoadm01.html:3706`), e esse
documento e escrito pelo lojista — `updateDoc(lives/<id>,{ativa:false})` some
da lista, dos KPIs e do varredor de termos, **e a transmissao continua** (quem
a alimenta e `estado/live`). O `setDoc` de `lives` ainda esta dentro de um
`try{}catch(_){}` (`ma/live.html:683-687`): basta nao executar. → a lista de
moderacao precisa vir do `liveSessao` (A4), nunca de declaracao voluntaria.

**B3. Limite de 60/180 min so no relogio da tela.** `ma/live.html:706-710`.
`nivel.limiteMin=99999` no console, ou mexer no relogio do aparelho, e a live
de 60 min vira 12 h. → servidor guarda `inicioEm` (A4) e derruba a entrada.

**B4. WHEP publico e permanente, sem URL assinada.** `m/api/live.js:285` cria a
entrada sem `requireSignedURLs`. Qualquer um le `estado/live.whep` e abre 500
conexoes headless — **cada minuto entregue e faturado**, e o endereco serve
para todas as lives futuras daquele lojista. → `requireSignedURLs:true` + token
curto por espectador; entrada por sessao ja invalida o WHEP antigo.

**B5. Sem limite de chamadas: um uid derruba a live de todos.** `api/live.js`
nao tem throttle; cada `iniciar` que erra o cache faz um `GET /live_inputs` da
conta inteira. Em laco, estoura o teto global do token Cloudflare (429) e
**nenhum lojista consegue comecar uma live**. → throttle por uid (1 a cada 30 s,
20/dia) antes de tocar no Cloudflare.

**B6. Corrida cria entradas duplicadas e o encerrar so apaga uma.**
`api/live.js:256-291` cria sem lock e `acharEntrada` guarda so o ultimo id de
cada nome. 30 `iniciar` em paralelo = 30 entradas com o mesmo nome, 29 delas
invisiveis ao painel. → id da entrada guardado pelo robo (A4) e `adm_encerrar`
apagando **todas** as entradas com aquele `meta.name`.

**B7. Presenca e escrita livre, por qualquer um, em qualquer negocio.** A regra
de `livepresenca/{sid}` nao exige `request.auth` nem `liveNoAr(uid)`, e o `sid`
vem do cliente. 500 documentos = "500 assistindo" na tela publica; o laco
tambem roda contra uid que nem esta ao vivo, so para gerar escrita paga.
→ exigir `liveNoAr(uid)` (funcao que ja existe, usada no chat) e `sid`
com formato fixo.

**B8. `tipo:'venda'` forjavel — o unico tipo que a pagina nao filtra.**
`m/live.html:516`: `if(m.tipo!=='venda' && mvProibido(...))`. O dono do negocio
escreve na propria `livechat` pelo curinga. → "Ana comprou <conteudo proibido>",
sem filtro, sem limite de tamanho, **e com prova social de uma venda que nunca
existiu**. → filtrar `venda` igual aos outros e criar match explicito de
`livechat` acima do curinga.

**B9. Oferta, cupom e brinde nao passam por filtro em lugar nenhum.**
`m/live.html:610-641` renderiza sem `mvProibido` (ao contrario de `fixado` e
`sacola`), o varredor do painel nao olha esses campos, e o servidor so confere
titulo e produtos **uma vez, no `iniciar`** — a oferta entra depois. → entrar
limpo e lancar o proibido na faixa de maior destaque da tela e trivial hoje.

**B10. Denuncia anonima como arma.** `denuncias` create sem auth, sem teto, com
o `lojistaUid` escolhido por quem denuncia; o painel escuta **sem `limit()`** e
poe "menor" no topo. 5.000 denuncias contra um concorrente afogam a fila e
enterram a denuncia verdadeira do dia. → freio por IP (o `checkout_freio` ja
existe) e agregacao por lojista na tela.

**B11. `saques.pedidoEm` e escrito pelo cliente e anula a retencao de 7 dias.**
A regra so exige que o campo exista — nem `is timestamp`. Em
`mr/api/pagar-saque.js:88-93`, `ms()` devolve `null` para string, e o corte
some: **todas as comissoes em retencao entram no pagamento**, inclusive as da
assinatura que sera estornada em seguida. → `pedidoEm == request.time` na regra
e `Timestamp.now()` como corte no servidor.

**B12. Saque avulso pago em dobro.** `pagar-saque.js:319-329` cria um saque novo
a cada chamada com `externalReference` diferente — a trava de duplicidade do
Asaas nao pega. Dois cliques, dois Pix. → id deterministico com `.create()`.

**B13. O Pix sai antes da baixa, e a baixa pode falhar.** `pagar-saque.js:355`
transfere e so depois quita num `db.batch()`, que estoura acima de 500
operacoes. Parceiro com muitas comissoes: **o Pix sai, o commit falha, o
proximo clique paga tudo de novo.** → lotes de 400, marcados **antes** da
transferencia.

---

## BLOCO C — corrigir, sem travar o lancamento

- **C1. LGPD: e-mail de todo lojista que fez live e publico.** `ma/live.html:1024`
  grava `email` em `estado/liveAceite`, e o curinga deixa **qualquer um ler**.
  `slugs` → uid → lista a subcolecao `estado`. → parar de gravar o e-mail (o uid
  ja identifica) ou tirar o aceite de dentro de `negocios/`.
- **C2. `RECEIVED_IN_CASH` conta como pago** (`checkout.js:112`). E um marcador
  manual do painel do Asaas, **sem dinheiro trafegando** — e vira pedido pago,
  baixa de estoque e prova social no chat.
- **C3. Estorno nao desfaz nada:** `oferta.vendidos` nao volta, a mensagem
  "comprou" fica no chat e o lojista **nao e avisado** — ele ja pode ter entregue.
- **C4. Teto de 10 unidades furado:** ate 20 linhas com o mesmo produto = 200
  unidades. E o estoque so cai no pagamento, entao N pedidos simultaneos de uma
  oferta com estoque 1 passam todos.
- **C5. Injecao de CSS pelo campo `foto`** (`m/live.html:575`): o `esc()` troca
  a aspa por `&quot;`, **mas o parser decodifica dentro do atributo** e a aspa
  volta, fechando o `url()`. Da para cobrir a tela inteira do espectador — o QR
  do Pix incluido — com uma imagem propria. → montar pelo CSSOM, nao por string.
- **C6. CSP com `'unsafe-inline'`** na pagina que pede CPF, nome e WhatsApp
  (`m/live.html:7`): qualquer escape que falhe no futuro vira execucao de JS.
- **C7. `api/og.js` e um oraculo de apelidos:** 200 x 404 por palpite, sem
  limite, com conta de servico, e a `og:description` devolve o titulo da live.
  Monta-se a lista de apelidos do Moviki em minutos, e cada palpite custa
  leitura paga.
- **C8. `X-Forwarded-Host` decide de onde vem o HTML** (`api/og.js:202,124-138`)
  quando o arquivo local falta. Vira pagina do atacante **sob o dominio
  moviki.com.br**.
- **C9. O filtro "do servidor" no chat e 1/5 do filtro do codigo.** A regex da
  regra tem ~31 termos; `MV_TERMOS` tem ~150. Passam `acompanhante`, `viagra`,
  `cassino`, `cnh falsa`, `piramide financeira`, entre outros — e a regra nao faz
  leet nem normalizacao. **Os `extras` do painel nao valem para o chat**, embora
  a tela diga que valem.
- **C10. A chave-mestra pode falhar na emergencia.** A regra de
  `configuracoes/liveTermos` exige `extras is list` no update; se `extras` nunca
  tiver sido salvo, **desligar a live e editar a lista beta sao negados**. E o
  mesmo defeito que a v16 ja corrigiu em `configuracoes/sistema`. → validar tipo,
  nunca exigir presenca.
- **C11. `configuracoes/liveTermos` e publico** — entrega os uid do beta fechado
  e **a lista de termos extras**, ou seja, o gabarito do filtro.
- **C12. `checkout_publico` e listavel** por anonimo: enumera todo lojista com
  Pix ligado.
- **C13. Token aceito por ate 1 h depois de a conta ser desativada**
  (`api/live.js:142-163`: sem `email_verified`, sem revogacao).
- **C14. `pedido` no modo 'asaas' nunca pode ser confirmado:**
  `confirmarNoAsaas` le sempre `checkout_contas`, que nao existe nesse modo —
  **o comprador paga e o pedido fica `aguardando` para sempre**.
- **C15. Exclusao de conta nao apaga pedido, comprovante nem chave** —
  `comprador.nome`, WhatsApp e endereco ficam, com `expiraEm` de 5 anos.

---

## Ordem de execucao

| Fase | O que | Por que agora |
| --- | --- | --- |
| 0 | **A1** (token do webhook) e **A5** (auto-indicacao) | nao sao da live: exploraveis hoje, mexem em dinheiro |
| 1 | **A4** (`liveSessao` no servidor) | derruba A2, A3, B1, B2, B3, B6 e o teto de minutos |
| 2 | **A3 imediato** (`live_bloqueios` no `adm_encerrar`) | 5 linhas, enquanto A4 nao fica pronto |
| 3 | B4, B5, B7, B8, B9, B10 | custo e moderacao |
| 4 | B11, B12, B13 | dinheiro do parceiro |
| 5 | Bloco C | antes de divulgar a live em anuncio |

**Nenhuma peca de divulgacao da live sai da gaveta com a fase 1 aberta.**

---

## Ressalvas honestas

1. **As regras auditadas sao o arquivo `claude/moviki-regras-firestore-v23.txt`,
   nao o Console.** A hierarquia de verdade do projeto poe o Console acima. A2,
   A3, B7, B8, B11 dependem disso — **conferir no Console antes de fechar cada
   um**.
2. Nada foi testado contra o ambiente real: sem envs do Cloudflare e do Firebase,
   o comportamento exato (entrada duplicada, teto de `live_inputs`) e inferido do
   codigo e da documentacao da API.
3. **A1 depende de o painel do Asaas mostrar o `authToken` ao titular da
   subconta.** O envio esta provado no codigo; a leitura, nao.
4. As politicas de TTL de `livechat`, `livepresenca` e `checkout_freio` sao
   descritas como opcionais nas proprias regras. **Se nao foram criadas no Google
   Cloud, a promessa de "guardado por ate 30 dias" nao existe** e o custo de B7
   e permanente.

## Ligacoes

[[A13 - Modo Live]] · [[A4 - Financeiro]] · [[P24 - Modo Live - lancamento]] ·
[[P34 - Travas contra abuso do teste gratis]] ·
[[R - Live - Arquitetura e arquivos]] · [[R - Live - Checkout Pix e subcontas Asaas]]
