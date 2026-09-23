---
type: arquivo
status: concluido
area: A5 - Programa de Parceiros
tags: [vik, criadores, moviki-ai, entrega]
atualizado: 2026-09-23
---

# Vik em modo criador — 22/09/2026

## O que mudou
- **Catálogo** (`moviki-ai/lib/catalogoPainel.js` `2026-09-22-1`): bloco novo `CRIADOR` com a Área do criador — abas, botões, situações das peças, as duas chaves, formatos, erros comuns. Entra no prompt **só** de quem tem `parceiros/{uid}.criador == true` e está no lado parceiro.
- **Dados da conta** (`lib/contextoUsuario.js`): para a criadora, uma consulta agregada em `criador_pecas` — enviadas, em análise, aprovadas, recusadas, suspensas, autorizadas em vigor, liberadas e os 3 últimos motivos de recusa. Nunca a URL do arquivo. Parceiro não marcado recebe "CRIADOR: não — o acesso é liberado pela equipe".
- **Comportamento** (`lib/promptPainel.js`):
  - revisa legenda ou roteiro colado pela criadora e aponta o que o Moviki não publica **pela posição, sem repetir a palavra proibida** (o filtro `segurancaVik` descartaria a resposta);
  - **não** escreve a legenda por ela e **não** dá dica de alcance, horário ou hashtag;
  - nunca promete aprovação nem data de publicação;
  - **passa para o time**: pedido de tirar do ar post já publicado com peça dela, e qualquer pergunta de bônus, cachê ou condição de criador.
- **Lista do que não existe**: editar peça enviada, escolher dia e hora de publicação, conta só de criador.
- `api/chat.js`: passa `criador` ao prompt (nunca no painel do lojista).

## Ajuste de 23/09 — "minha peça saiu?"
- Primeiro teste real: o Vik respondeu "liberadas para sair" a quem já tinha story publicado, e pediu para ela abrir a tela e ler para ele.
- Causa: o histórico do robô mora em `moviki-assistente-social/estado/historico.json` (GitHub), não no Firestore — o Vik não via.
- Conserto (`catalogoPainel.js` `2026-09-23-1` + `contextoUsuario.js`): o contexto da criadora lê esse histórico (cache de 5 min, limite de 3 s) e traz quantos posts saíram, formato, rede e data. O catálogo manda responder primeiro com o que já saiu e proíbe pedir que ela leia a tela para o Vik.

## Ajuste de 23/09 — data e palavra
- O Vik disse "story em 23/09" para o publicado às 23h26 de 22/09. Causa antiga, de todo o Vik: `dataBrMs` usava o relógio do servidor (UTC). Tudo entre 21h e meia-noite saía com o dia seguinte — também liberação de comissão, saque e conclusão das aulas. Agora a data é sempre de Brasília (`catalogoPainel.js` `2026-09-23-2`).
- O Vik escreveu "o robo escolhe". Passa a dizer "sistema de publicação do Moviki".

## Incidente junto
A marca do parceiro no Vik ficou em `2026-09-19-menucateg` enquanto o `parceiro.html` subia até `2026-09-22-criador4`: o Vik ficou em **modo cauteloso para todos os parceiros** desde a subida da Área do criador. Mesma causa de 16/09 — painel subiu sem a tabela do Vik na mesma rodada. Corrigido nesta entrega (`MARCAS_CONFERIDAS.parceiro = 2026-09-22-criador4`).

## Testes
- Sintaxe de todos os arquivos; `segurancaVik.test.js` e `tetoDia.test.js` passando.
- Teste offline com banco simulado: criadora com 3 peças gera o resumo certo; bloco do criador entra só com `criador: true`; modo cauteloso desligado com a marca atual.

## Regra
Painel que sobe, `MARCAS_CONFERIDAS` do Vik sobe junto, na mesma rodada — **inclusive** quando a mudança é num menu que só parte dos usuários vê.

## Ligações
- [[ARQ - Area do criador no painel do parceiro]]
- [[ARQ - Oferta do criador por porta de entrada - decisao 22092026]]
- [[R - Regras de ouro novas de 22092026]]
