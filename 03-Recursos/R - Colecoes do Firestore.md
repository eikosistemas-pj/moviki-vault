---
type: recurso
status: referencia
area: A3 — Dados e Regras
tags: [regra-firestore, dados]
atualizado: 2026-08-28
---

# R — Coleções do Firestore

| Coleção | O que é | Leitura | Escrita |
| --- | --- | --- | --- |
| `negocios/{uid}` | dados do lojista; sinal de "é lojista" | pública | lojista (`hasOnly`) · `markerLogo` só servidor |
| `negocios/{uid}/avaliacoes/{id}` | avaliação anônima (nota 1–5, nome 2–60, comentário) | pública | visitante |
| `negocios/{uid}/resumo/avaliacoes` | `{n, soma}` — a nota média sai daqui | pública | servidor |
| `metricas/{uid}/dias/{AAAA-MM-DD}` | contador por negócio, TTL 13 meses (`expiraEm`) | dono do negócio + admin | página pública (`increment(1)`) |
| `conversas/{uid}` | caixa de mensagens; **o id É o uid** | aquele lojista + admin | idem |
| `conversas/{uid}/mensagens/{id}` | `de: 'lojista' \| 'admin' \| 'bot'` | idem | **não pode ser editada** |
| `vik_memoria/{uid}` | o que o Vik aprendeu | **só admin** | **só Admin SDK** |
| `newsletter/{id}` | e-mails do rodapé | **só admin** | anônimo só CRIA; update só para `ativo:false` |
| `saques/{id}` | pedido de saque | parceiro + admin | parceiro (≥R$20) ou robô |
| `comissoes/{payId_nN}` | ledger idempotente | | servidor |
| `pontos/{pid}` | unidade Enterprise | pública | só `api/pontos.js` |
| `faturamento/{uid}` | ids do Asaas + `gaClientId`/`gaSessionId` | **privado, sem match** | servidor |
| `faturamento/{uid}/ga/{payId}` | trava de dedup do `purchase` | | servidor |
| `atendimentos_bot/{telefone}` | WhatsApp | **`if false` para o app** | só `moviki-ai` |
| `assinaturas/{uid}` · `slugs/` · `ponto_slugs/` · `parceiro_slugs/` · `indicacoes/{lojistaUid}` (imutável) · `parceiros/{uid}` · `admins/{uid}` · `configuracoes/sistema` | | | |

## `negocios` — campos no `hasOnly` de `negocioValido`
`nome`, `status`, `recado`, `cardapio`, `promocoes`, `eventos`, `fotos`, `atualizadoEm`, `lat`, `lng`, `slug`, `whatsapp`, `markerLogo`, `cor`, `whiteLabel`, `segmento`, `segmentoMacro`, `autorizaDivulgacao`, `horario`, `endereco`, `entrega`, `precoMedio`.

## `conversas` — campos
`uid`, `nome`, `email`, `ultimaMsg`, `ultimaEm`, `ultimoDe`, `vistoLojistaEm`, `vistoDonoEm`, `docsLiberado`, `docsPedido`, `criadoEm` — e desde a **v14**: `botLigado`, `botRespondeuAte`, `botDia`, `botUsos`.

**A trava:** `docsLiberado` fica **fora** da lista de campos que o lojista pode alterar. É só isso que impede o lojista de liberar o próprio anexo — e a mesma trava está no Firestore **e** no Storage.

## `metricas` — campos
`views` · `whats` · `rota` · `cardapio` · `b0…b11` (12 faixas de 2h → horário de pico) · `expiraEm`.

⚠️ **`expiraEm` é derivado da DATA DO PRÓPRIO DOCUMENTO, em UTC — nunca do relógio do visitante.** Relógios diferentes mandariam valores diferentes, o campo contaria como alterado, a escrita passaria do teto e seria **recusada**.

## Storage — `moviki-app.firebasestorage.app`
`logos/{uid}` e `produtos/{uid}` (robô, **`read: if true`** — sem isso, publicar regras apaga logos e fotos da tela) · `documentos/{uid}` (anexos da caixa de mensagens, privado).
