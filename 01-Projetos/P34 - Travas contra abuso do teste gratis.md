---
type: projeto
status: ativo
area: A4 - Financeiro
tags: [teste-gratis, fraude, trava, live, lgpd, armadilha]
prioridade: 1
prazo: antes de o Modo Live sair do beta
atualizado: 2026-09-15
---

# P34 — Travas contra abuso do teste gratis

Fechar o ciclo *"vendo 30 dias de graca, abro outra conta, vendo mais 30"*.
Diretriz do Paulo em 15/09/2026, que passa a valer para todo o produto:

> Travas de e-mail, de numero de telefone e de aparelho. E a live no teste
> gratis liberada **por quantidade de lives**, nao por dias — duas, no maximo.

Continua [[A13 - Modo Live]] e [[P24 - Modo Live - lancamento]].
Muda o que [[P33 - Aulas do Modo Live para o parceiro]] manda o parceiro falar.

---

## 1. O buraco, conferido no codigo em 15/09

`moviki-robo/api/ativar-trial.js`, versao no ar:

```
const snap = await ref.get();
if (snap.exists) return res.status(200).json({ ok:true, jaExiste:true });
```

**A unica trava era "ja existe `assinaturas/{uid}`".** O uid nasce junto com a
conta. Logo: **conta nova = teste gratis novo, sem limite e sem registro.**

Pior: o `index.html` chama a rota **dentro do `createUserWithEmailAndPassword`**,
no mesmo segundo. **O e-mail nem precisava ser confirmado.**

E nada fica registrado: excluida a conta, nao sobra memoria nenhuma de que
aquele e-mail ja consumiu um teste.

### O que o abusador leva hoje, e o que ele nao leva

| Leva | Nao leva |
| --- | --- |
| 30 dias de Pro, quantas vezes quiser | Pix dentro da live (e Enterprise, nunca cai no teste) |
| Live em nivel Premium: 1 h por transmissao, 5 produtos | Avaliacoes, historico, desempenho — zeram a cada conta |
| Quantidade **ilimitada** de lives | O apelido antigo (o link e o QR impresso morrem) |

**O prejuizo direto e pequeno** — Cloudflare Stream custa US$ 1 por 1.000 min de
espectador. Cem abusadores com 4 h/mes dao ~US$ 24. **O prejuizo real e outro:
o lojista que PAGARIA descobrir o truque.** E por isso que a trava importa antes
do lancamento da live, nao depois.

---

## 2. A regra que governa todas as travas

**Trava-se o BENEFICIO, nunca a porta de entrada.**

Aquisicao e o gargalo do Moviki, com campanha paga rodando. Exigir CPF, cartao
ou SMS **no cadastro** derruba conversao de gente honesta para barrar quem nunca
ia pagar. Quem nao passa numa trava vira lojista do plano **Basico** e continua
dentro — nenhuma trava desta nota recusa cadastro.

---

## 3. As cinco camadas

### Camada 1 — E-mail (ENTREGUE em 15/09)

`api/ativar-trial.js` reescrito. Tres travas no servidor:

1. **`email_verified` obrigatorio.** Sem confirmacao, responde
   `{ pendenteVerificacao:true }` e nao concede. **Nao exige mudanca no
   `index.html`**: o painel ja rechama a rota a cada login enquanto nao ha
   assinatura (`onAuthStateChanged`), entao o teste entra sozinho quando ele
   confirmar o e-mail.
2. **`trials_usados/{hash}`**, gravado na mesma transacao e **nunca apagado —
   nem na exclusao de conta**. Guarda so o hash com sal (LGPD: minimizacao).
   O e-mail e **normalizado** antes: no Gmail, `joao.silva+1@`, `joaosilva@` e
   `j.o.a.o.silva@` sao a mesma caixa e hoje valiam tres testes.
3. **Dominio descartavel** barrado — lista base no codigo mais a env
   `TRIAL_DOMINIOS_BLOQUEADOS`, editavel no Vercel **sem deploy**.

Negativas ficam em `trial_negado/{uid}` para o painel do dono.

⚠️ `trials_usados` e `trial_negado` sao escritos **so pelo Admin SDK**.
Conferir nas regras que nao existe curinga permissivo alcancando as duas.

### Camada 2 — Cota de lives no teste gratis

**Decisao: 2 lives no total do periodo de teste.** Nao por mes — o teste dura 30
dias, e cota mensal so ensinaria a esperar virar o mes.

Plano pago (Premium e Enterprise) continua **sem limite de quantidade**.

#### O detalhe tecnico que decide onde isso mora

`moviki/api/live.js` usa a conta de servico **`FIREBASE_SA_LEITURA`, so-leitura,
de proposito**. Ela **nao pode gravar contador.** Entao:

- contador novo em `moviki-robo` (`api/live-cota.js`), que ja tem Admin SDK;
- o `api/live.js` chama esse endpoint **server-to-server, com segredo
  compartilhado**, no momento da acao `iniciar` — nunca no `nivel`, senao abrir
  o estudio para olhar ja gastaria cota;
- documento `live_cota/{uid}` → `{ usadas, sessoes:[], ultimaEm }`.

#### A armadilha que a regra crua cria — e a carencia que resolve

Feira, 4G, celular na mao: **a conexao cai.** Com a regra crua, reabrir a live
consome a segunda cota, e o lojista fica sem teste no primeiro dia por culpa do
sinal. Isso nao e trava, e cancelamento.

**Regra:** reabrir em ate **15 minutos** do encerramento anterior **nao consome
cota** — conta como a mesma sessao.

#### O contador tambem vende

No estudio, em cima: *"Teste gratis: 1 de 2 lives usadas."* Vira gatilho de
assinatura, nao so cadeado. Na segunda, o texto ja oferece o plano.

### Camada 3 — Telefone (a unica trava com custo real para o fraudador)

E-mail e gratis e infinito. **Chip nao.**

- **Nao no cadastro.** Exigido para **liberar a primeira live**, e so.
- `linkWithPhoneNumber` do Firebase Auth: o numero vira identificador do usuario,
  e o proprio Firebase recusa o mesmo numero em duas contas
  (`auth/credential-already-in-use`).
- Apagou a conta antiga, o numero **libera no Firebase** — por isso guardamos
  `telefones_usados/{hash}` do nosso lado, **permanente**, igual ao e-mail.
- **Custo:** SMS de verificacao e cobrado por envio e varia por pais.
  **Confirmar a tabela do Identity Platform antes de ligar** — e o unico item
  desta nota que gasta dinheiro por tentativa.
- Alternativa sem SMS: codigo pelo WhatsApp. Depende do `api/atendimento.js`,
  que esta em **stand-by trancado** por falta de `WHATSAPP_TOKEN`. Fica como
  fase 2.

### Camada 4 — Aparelho: o que da e o que nao da

**Nao existe IMEI no navegador.** O Moviki e web; nao ha app nativo, entao nao ha
Play Integrity nem DeviceCheck. Quem prometer "ID do aparelho" no navegador esta
vendendo fingerprint com outro nome.

O que da para fazer, e o que cada peca vale:

| Sinal | Vale | Fura com |
| --- | --- | --- |
| Id proprio em `localStorage` + IndexedDB | quase nada sozinho | aba anonima, limpar dados |
| **Fingerprint** (canvas, WebGL, fontes, audio, tela, fuso) | sinal bom, estavel no mesmo aparelho | outro navegador, outro aparelho |
| IP do cadastro (**ja capturado** no `api/novo-cliente.js`) | agrupa tentativas | 4G troca IP (CGNAT) |
| Coordenada do negocio | agrupa tentativas | mudar o pino |

**Como usar, sem criar injustica:** fingerprint **nao bloqueia cadastro**.
Fingerprint que ja consumiu teste gratis → **a live no teste nao abre** naquela
conta nova, e a conta acende no painel do dono.

⚠️ **Falso positivo e real:** familia com um celular so, lan house, lojista que
cadastra pelo aparelho do filho, dois feirantes no mesmo balcao. Por isso o
efeito e limitado a live no teste, e o dono consegue **liberar a mao**.

⚠️ **LGPD:** fingerprint e dado pessoal. Precisa entrar na **Politica de
Privacidade** com finalidade *prevencao a fraude* e base legal *legitimo
interesse*, antes de ligar. Nao e opcional.

### Camada 5 — Tornar a troca de conta cara

A trava mais honesta nao e a que impede: e a que faz o truque **nao valer a pena**.

- **Apelido em quarentena permanente.** Hoje a exclusao e um pedido em
  `exclusoes/{uid}`, tratado a mao. Passa a gravar `apelidos_usados/{slug}` e o
  apelido **nunca volta a ser oferecido**. O link no panfleto, o QR impresso e o
  endereco que os clientes salvaram morrem com a conta — e nao renascem.
- **Avaliacoes, historico e desempenho nao migram.** Ja e verdade; passa a ser
  dito com todas as letras na tela de exclusao e na aula do lojista.
- **Aviso no fim do teste** (`api/lembrete-trial.js`, que ja roda) dizendo o que
  ele perde ao nao assinar. Retencao, nao ameaca.

---

## 4. Ordem de execucao

| # | O que | Custo | Efeito |
| --- | --- | --- | --- |
| 1 | `api/ativar-trial.js` endurecido | zero | **feito** — fecha o caso trivial |
| 2 | Cota de 2 lives no teste (`live-cota.js` + `api/live.js`) | baixo | tira o motivo economico do ciclo |
| 3 | Teto de minutos **no servidor** (hoje so na tela) | baixo | pendencia antiga de [[P24 - Modo Live - lancamento]], resolvida na mesma passada |
| 4 | Telefone verificado para liberar a live | **SMS pago** | a trava forte |
| 5 | Fingerprint como sinal + painel de suspeitos | medio | pega o reincidente |
| 6 | Apelido em quarentena | baixo | encarece a troca de conta |
| 7 | Politica de Privacidade: prevencao a fraude | zero | **pre-requisito legal do item 5** |

Itens 1 a 3 **antes** de a live sair do beta. Itens 4 e 5 podem entrar depois,
mas nao muito.

---

## 5. O que muda no discurso do parceiro

A frase de [[P33 - Aulas do Modo Live para o parceiro]] muda:

> **Antes:** "No teste gratis voce faz live, quantas quiser, de ate uma hora."
> **Agora:** "No teste gratis voce faz **duas lives** de ate uma hora, para
> experimentar. Assinando, deixa de ter limite de quantidade."

⚠️ O roteiro de `mod-parc-live` e as pecas da
[[P32 - Material de apoio da live para o parceiro]] **ainda nao foram gravados** —
entao esta mudanca **nao custa regravacao**, desde que entre agora. Se a producao
comecar antes da decisao final da cota, custa.

---

## 6. Pendencias abertas

- [ ] Confirmar o preco do SMS de verificacao na tabela do Identity Platform
- [ ] Definir se o teto de minutos do teste tambem entra (hoje: so quantidade)
- [ ] Conferir nas regras do Firestore que `trials_usados`, `trial_negado`,
      `telefones_usados`, `live_cota` e `apelidos_usados` sao inacessiveis ao cliente
- [ ] Escolher a biblioteca de fingerprint e medir o falso positivo antes de ligar
- [ ] Politica de Privacidade: clausula de prevencao a fraude

## Ligacoes

[[A13 - Modo Live]] · [[A4 - Financeiro]] · [[P24 - Modo Live - lancamento]] ·
[[P33 - Aulas do Modo Live para o parceiro]] ·
[[P32 - Material de apoio da live para o parceiro]] ·
[[R - Live - Arquitetura e arquivos]]
