---
type: guia
status: ativo
area: A13 - Modo Live
tags: [handoff, live, seguranca, fase-2, lancamento]
prioridade: 1
prazo: antes de abrir o Modo Live
atualizado: 2026-09-16
---

# HANDOFF — Fechar a fase 2 e por o Modo Live no ar

**Cole este arquivo no inicio do chat que vai continuar.** E autocontido: traz
o estado do ar conferido, o que ja foi entregue, **o que esta pronto e ainda
nao subiu**, a fila em ordem de urgencia e as armadilhas que ja custaram tempo.

Detalhamento por achado: [[P35 - Auditoria de seguranca do Modo Live]].

---

## 1. Onde o trabalho parou (16/09/2026, madrugada)

O **Bloco A inteiro** da auditoria esta fechado e no ar. A **fase 2** comecou:
**B5, B8, B9 e C5 fechados e no ar**, conferidos byte a byte.

O objetivo agora e um so: **fechar o que trava a abertura da live** e por no ar.
Nao e fechar os 30 achados.

## 2. O QUE ESTA NO AR — conferido byte a byte no GitHub

| Repositorio | Arquivo | Marca |
| --- | --- | --- |
| moviki-robo | `lib/livesessao.js` | `2026-09-15-b5b` |
| moviki-robo | `lib/checkout.js` | `2026-09-15-whtoken` |
| moviki-robo | `api/webhook.js` | `2026-09-15-escopo` |
| moviki-robo | `api/pontos.js` | `2026-09-15-livesessao` |
| moviki | `api/live.js` | `2026-09-15-b5a` |
| moviki | `live.html` | `2026-09-15-filtro` |
| moviki-app | `live.html` (estudio) | `2026-09-15-sessao5` |
| moviki-app | `index.html` | `2026-09-15-aulatrava` |
| moviki-app | `parceiro.html` | `2026-09-15-aulatrava` |
| moviki-app | `eikoadm01.html` | `2026-09-15-conferir` |

**Regras do Firestore: v24 publicada** no Console e provada contra o ar.
**Envs:** `LIVE_SEGREDO` existe nos dois projetos da Vercel.
⚠️ **So em `Production`, nao em `All Environments`.** Producao funciona; um
deploy de **Preview nao tem o segredo** e a live nao comeca (falha fechada).

## 3. ✅ LOTE 1A — NO AR E TESTADO (16/09, madrugada)

`moviki/live.html`, marca **`2026-09-15-filtro`**. Conferido byte a byte contra
o GitHub: identico ao entregue.

**Testado na live real** (`moviki.com.br/live/karina`), com o Paulo
transmitindo: video, oferta relampago com contador, cupom `LIVE10`, sacolinha
com dois produtos, chat com duas mensagens — **e as FOTOS aparecendo**, que era
o unico risco de regressao do C5. Veredito do Paulo: "tudo ok".

**O que este lote mudou — para nao ser desfeito por engano:**

1. **B8, na exibicao do chat.** Era
   `if(m.tipo!=='venda' && mvProibido(m.texto)) return;` — tudo que fosse
   `venda` entrava sem filtro. Passa a ser
   `if(mvProibido(m.texto) || mvProibido(m.nome)) return;`.
2. **B8, no envio.** `mvProibido` tambem no nome, ao salvar o nome
   (`btnSalvarNome`) e dentro de `gravarChat`.
3. **B9.** `ofertaAtiva()` devolve null se `mvProibido(o.nome)`; o brinde so
   aparece se `!mvProibido(b.texto)`; o cupom so existe se codigo e texto
   passarem (`cupomOk`).
4. **C5.** `fotoOk()` passa a recusar aspa, apostrofo, parentese, espaco, barra
   invertida e `<`/`>`, com o dominio ancorado; `fotoDiv()` devolve
   `<div class="cpFoto" data-mvfoto="1">` **sem `style=`**, e a imagem entra
   depois por `el.style.backgroundImage` (CSSOM), nos dois lugares que usam
   `fotoDiv` (produto em destaque e sacolinha).

⚠️ **Nao afrouxar `fotoOk()` sem olhar a URL.** A validacao e estrita de
proposito: e ela que fecha o C5. Se um dia sumir a foto de algum lojista, pedir
**a URL** antes de mexer — no teste real as fotos apareceram normalmente.

## 4. FILA — em ordem de urgencia real, nao pela numeracao

> O criterio e um so: **o que um estranho explora no dia em que a live abrir.**
> Dois itens do Bloco C sao mais graves que metade do Bloco B.

| Lote | Achados | Arquivos | Por que |
| --- | --- | --- | --- |
| ~~**1A**~~ | ~~B8, B9, C5~~ | `moviki/live.html` | ✅ **no ar e testado** |
| **1B** | **B2**, **B10** | `moviki-app/eikoadm01.html` | abrir a live com a moderacao cega e o pior cenario |
| **1C** | **B4**, **B7** | `moviki/api/live.js` + regras v25 | custo faturado por qualquer um |
| **1D** | **B11, B12, B13** | `moviki-robo/api/pagar-saque.js` + regras | nao e da live: **saque pago em dobro, hoje** |
| 2 | C9, C1, C2–C4, C7, C8, C12–C15 | varios | nao trava a abertura |

### O que cada um do lote 1B e 1C exige

- **B2 — a moderacao nao pode depender de declaracao voluntaria.**
  `eikoadm01.html:3706` lista lives com
  `collection('lives') where ativa==true`, e esse documento **e escrito pelo
  proprio lojista** — um `updateDoc(ativa:false)` some da lista, dos KPIs e do
  varredor de termos **com a transmissao no ar**. A acao `live_adm_noar` **ja
  existe no robo** (`lib/livesessao.js`): e so a lista passar a vir dela.
- **B10 — a denuncia vira arma.** `denuncias` aceita create sem auth e sem
  teto, com o `lojistaUid` escolhido por quem denuncia, e o painel escuta
  **sem `limit()`**, poe "menor" no topo. 5.000 denuncias contra um concorrente
  afogam a fila e enterram a denuncia verdadeira. Precisa de `limit()` e
  agregacao por lojista na tela, mais freio no create.
- **B4 — o WHEP e publico e eterno.** `moviki/api/live.js` cria a entrada sem
  `requireSignedURLs`. Qualquer um le o endereco e abre centenas de conexoes —
  **cada minuto e faturado** — e o mesmo endereco serve para todas as lives
  futuras daquele lojista.
- **B7 — presenca forjavel.** A regra de `livepresenca/{sid}` nao exige
  `request.auth` nem `liveNoAr(uid)`, e o `sid` vem do cliente: 500 documentos
  viram "500 assistindo", e o laco roda ate contra uid que nem esta ao vivo, so
  para gerar escrita paga.
  ⚠️ **Cuidado no desenho:** por `liveNoAr(uid)` no create E no update faz cada
  batida de presenca (uma por espectador por minuto) pagar um `get()`. Exigir
  **so no create** mata o ataque contra quem nao esta no ar sem criar custo
  recorrente. O `expiraEm` hoje e de 2 dias — para presenca, deveria ser
  minutos.

### Fechados por reavaliacao, nao por conserto

- **C10** ja estava resolvido na v24: a regra da chave-mestra valida **tipo**
  em vez de exigir presenca do campo.
- **C11** perde a urgencia **se a live abrir para todos**: ele vaza os uid do
  beta fechado, e com `liveBeta` vazia nao ha o que vazar.

## 5. ARMADILHAS — ja custaram tempo, nao repetir

1. **Regra do Firestore nao tem "deny".** Varios `match` que casam somam
   permissoes. Colecao de autoridade vai para a **raiz**, nunca dentro de
   `negocios/{uid}` (la o curinga da escrita ao dono).
2. **O Console nao tem mais simulador de regras.** Para provar uma regra,
   subir uma pagina temporaria que tente escrita e leitura logado — **com App
   Check inicializado**, senao tudo e negado pelo motivo errado.
3. **Validar a sintaxe do JavaScript DENTRO dos `.html`**, nao so dos `.js`.
   Identificador repetido derruba o arquivo inteiro e a tela fica "Carregando".
4. **Conserto num painel tem que ser conferido no outro na mesma rodada** —
   `index.html` e `parceiro.html` carregam o mesmo motor de aulas, copiado.
5. **Arquivo de codigo so com texto imprimivel.** Byte de controle no lugar do
   escape roda igual, **some do diff do Git** e morre no primeiro editor.
6. **Conferir sempre o GitHub antes de montar.** O Paulo trabalha so pela
   interface web; montar sobre uma base velha e subir **apaga** o que estava la,
   e o sintoma e silencio.

Lista completa: [[R - Regras de ouro novas de 15092026]] e [[R - Regras de ouro]].

## 6. METODO DE CONFERENCIA (vale a pena repetir)

- **Clonar e comparar.** `moviki`, `moviki-robo` e `moviki-app` sao publicos e
  podem ser clonados direto; comparar o arquivo do GitHub **byte a byte** com o
  que foi entregue. Foi assim que apareceram os bytes de controle.
  ⚠️ **`moviki-vault` e privado** — nao da para clonar.
- **Testar em navegador de verdade.** Chromium com Playwright ja resolveu duas
  cacadas: o dube da API do YouTube (visto verde) e a prova do ataque de CSS do
  C5 — que **funciona** no arquivo que esta no ar e para de funcionar no 1A.

## 7. LIMPEZAS PENDENTES (nao sao da fase 2, mas vao doer depois)

- [ ] A conta de teste (Karina) esta **Enterprise por edicao manual no Console**.
      Reverter ou marcar `origem: teste` quando os testes acabarem.
- [ ] O painel do dono conta **pedido de teste como venda**: "Vendido pelo Pix
      R$ 25,41", "Pedidos pagos 1", "Conversao 50%". Marcar ou apagar **antes**
      de olhar qualquer relatorio de faturamento.
- [ ] Testar no ar o **freio B5a** (entrar, 10 s, encerrar, entrar de novo: tem
      que abrir) e a **trava do cursor** das videoaulas.
- [ ] **Fundir** `R - Regras de ouro.md` e `R - Marcas de versao no ar.md` com os
      apendices de 11–14/09 e de 15/09. Os apendices existem porque o vault e
      privado e o arquivo integral nunca chegou — substituir sem ele apagaria
      historico.

## 8. Notas geradas nesta linha de trabalho

[[ARQ - Token de webhook por subconta e valor reconferido]] ·
[[ARQ - Sessao da live no servidor]] · [[ARQ - Freio do api live - B5]] ·
[[ARQ - Ajuste do freio da live - B5a]] ·
[[ARQ - Bytes de controle no livesessao]] ·
[[ARQ - Incidente - estudio preso em carregando]] ·
[[ARQ - Trava do cursor nas videoaulas]] ·
[[P34 - Travas contra abuso do teste gratis]] ·
[[P35 - Auditoria de seguranca do Modo Live]] ·
[[R - Regras de ouro novas de 15092026]] ·
[[R - Marcas de versao no ar em 15092026]]

## Ligacoes

[[P35 - Auditoria de seguranca do Modo Live]] · [[A13 - Modo Live]] ·
[[P24 - Modo Live - lancamento]] · [[R - Live - Arquitetura e arquivos]]
