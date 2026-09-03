---
type: incidente
status: concluido
area: A3 — Dados e Regras
tags: [seguranca, regra-firestore, armadilha, dinheiro]
atualizado: 2026-09-03
---

# ARQ — Auditoria de segurança, 03/09/2026

Primeira varredura completa do projeto: os 5 repositórios por clone anônimo, as regras do Firestore e as do Storage.

**Nada permitia tirar dinheiro, ler dado de terceiro ou virar admin.** O que havia era um endpoint aberto e falhas de integridade de dado público.

## O que foi consertado no mesmo dia

### 1. O robô de WhatsApp estava no ar com a porta destrancada

O `assinaturaValida()` do `moviki-ai/api/atendimento.js` fazia `if (!secret) return true` — **sem a env `WHATSAPP_APP_SECRET`, liberava geral**. E o `moviki-ai` estava publicado, ao contrário do que o mapa dizia.

Qualquer um que descobrisse a URL mandava um POST forjado, o Claude respondia e **queimava crédito da conta Anthropic, em laço, sem login**. Nenhum cliente recebia nada errado (faltava o `WHATSAPP_TOKEN`); o prejuízo era custo e lixo no banco.

**Conserto:** `return false` + tranca de stand-by. O endpoint agora responde **503 `{standby:true}`** e não gasta chamada de IA. Conferido de fora no mesmo dia.

### 2. Regras v19 publicadas — três apertos

- **A nota das avaliações podia ser inventada.** O `create` de `resumo/avaliacoes` aceitava `n` até 100.000 de **visitante anônimo**: dava para um negócio nascer com 5,0 e "2.000 avaliações", ou derrubar um concorrente a 1,0, sem uma avaliação real no banco. Agora anônimo só cria com a primeira avaliação (`n ≤ 1`, `soma ≤ 5`); semear o resumo inteiro é direito do dono do negócio.
- **Comentário sem limite de tamanho.** A tela limitava a 300, a regra não. Agora 300 na regra também.
- **Pedido de saque sem teto.** Agora R$ 5.000. O dinheiro nunca esteve em risco — o `pagar-saque.js` recalcula pelo ledger e ignora o `valorSolicitado`. Era o painel exibindo número mentiroso.

### 3. Chave de administrador em Preview

`FIREBASE_SERVICE_ACCOUNT` do `moviki-ai` saiu de "Production and Preview" e ficou **só em Production**. Antes, toda deployment de branch carregava a chave de administrador do Firebase.

## Efeito colateral conhecido da v19, e é só custo

Negócio antigo sem o documento `resumo` e com mais de uma avaliação continua lendo a lista inteira a cada visita, até o próprio lojista abrir a página pública dele logado. **A nota na tela continua certa** — a página cai sozinha no caminho antigo. Na prática quase não existe caso: todo negócio visitado desde 26/08 já tem o resumo gravado.

## Menores, registrados e não consertados

- **`indicacoes/{uid}` tem leitura pública** e o campo `ref` é texto livre: dá para ver quem indicou quem, e um lojista pode se auto-atribuir ao apelido de qualquer parceiro.
- **Reserva de apelido em lote:** qualquer conta logada cria documentos em `slugs/` e `parceiro_slugs/` sem limite — dá para sequestrar apelidos bons. Agravante: em `parceiro_slugs`, `update` e `delete` são só do admin, então parceiro que errar o slug depende de intervenção manual.
- **`novo-parceiro.js` aceita o `CRON_SECRET` por query string** (`?secret=`), que fica em log de servidor. Preferir só o cabeçalho `Authorization`.

## O que a auditoria confirmou que está sólido

- **Nenhum segredo nos repositórios.** A única chave em código é a `apiKey` do Firebase, pública por natureza.
- **Preço vem do servidor** (tabela `PLANOS` no `lib/asaas.js`) — não dá para assinar Premium por R$ 1,00.
- **Todos os endpoints do `/api` conferem o `idToken`**, e os de admin leem `/admins/{uid}` **no servidor**.
- **Webhook do Asaas** compara o token em tempo constante e recusa quando não bate.
- **Pix de comissão** calcula pelo ledger, tem teto, é idempotente e recupera transferência já criada.
- **Storage fechado** fora de `documentos/{uid}` e das pastas públicas.
- **Mensagem não se edita** depois de enviada; `'bot'` só entra pelo Admin SDK.
- **Chave Pix de parceiro não é pública.**
- **CORS por lista de origens**, nunca `*`.
- **XSS escapado** na página pública, e URL de foto filtrada por domínio.

## A regra de ouro que nasceu daqui

> **Conferência de assinatura NUNCA pode falhar aberto.** `if (!secret) return true` transforma uma env esquecida em porta destrancada, e ninguém percebe — o endpoint responde 200 normalmente. Sem o segredo, ninguém entra.

## Ligações

[[A3 - Dados e Regras]] · [[A9 - IA e Atendimento Vik]] · [[P15 - Enforcement do App Check]] · [[R - Historico de regras do Firestore]] · [[R - Regras de ouro]] · [[ARQ - Incidentes e cacadas de bug]]
