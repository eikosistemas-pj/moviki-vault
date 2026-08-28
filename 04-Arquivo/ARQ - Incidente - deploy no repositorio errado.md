---
type: incidente
status: concluido
data: 2026-08-28
area: A2 - Infraestrutura e Deploy
tags: [deploy, armadilha]
atualizado: 2026-08-28
---

# ARQ - Incidente: deploy no repositorio errado

## Sintoma
O botão do padrão global "não aparecia" no painel do dono e a marca de versão continuava a antiga — **mas o mesmo texto aparecia em `moviki.com.br/eikoadm01.html`**.

## Causa
`index.html`, `parceiro.html` e `eikoadm01.html` foram subidos no repositório **`moviki`** em vez de **`moviki-app`**.

Consequência: **`moviki.com.br` passou a servir o painel do lojista** e a landing pública saiu do ar por alguns minutos. O painel do dono ficou acessível publicamente em `moviki.com.br/eikoadm01.html`.

## Conserto
1. Restaurar a landing primeiro — a página pública fora do ar é o dano maior.
2. Apagar os dois arquivos intrusos do `moviki`.
3. Subir os três no `moviki-app`.

## Lição 1 — entregar em pasta nomeada não bastou
Os arquivos foram entregues em pastas com o nome do repositório de destino e **ainda assim** foram para o repo errado. O que pegou o erro não foi o processo de entrega: foi **conferir o conteúdo publicado no domínio**, e a **marca de versão** foi o que provou.

> Nunca confiar no "já subi". A verdade é o domínio, e a prova é a marca de versão.

## Lição 2 — o deploy da Vercel demora, e isso custou duas rodadas
Duas vezes o arquivo estava **certo no GitHub** e o domínio ainda servia o anterior. Inclusive um erro *"Não consegui ler as conversas"* que era só o deploy trocando o arquivo no meio do caminho — **sumiu sozinho**.

> Arquivo certo no GitHub + comportamento errado no domínio = **esperar e conferir de novo** antes de concluir que deu errado. Caçar bug durante um deploy em andamento é caçar fantasma.

## Família
É o mesmo gênero de [[ARQ - Incidente - nomes de arquivo corrompidos no Windows]] e do `catch` que inventou erro em [[ARQ - Incidentes e cacadas de bug]]: **a tela deixou de refletir a realidade**, e o tempo foi gasto consertando o que não estava quebrado.

## Também nesta rodada
A **CSP mordeu pela terceira vez**: o `connect-src` do `eikoadm01.html` liberava `moviki-robo.vercel.app` mas não `moviki-ai.vercel.app`. Foi pega antes de subir. Fetch bloqueado por CSP **não aparece no Network** — só no Console.

→ [[R - Regras de ouro]] · [[R - Checklist de deploy]] · [[R - Marcas de versao no ar]] · [[A2 - Infraestrutura e Deploy]]
