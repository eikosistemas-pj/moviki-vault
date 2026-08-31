---
type: incidente
status: referencia
area: A8 - Conteudo e Social
tags: [armadilha, video, ia]
atualizado: 2026-08-31
---

# ARQ — Armadilhas de geracao por IA

Tudo que ja custou credito, rodada ou take na producao do filme institucional.
**Ler antes de gerar qualquer coisa no Kairogen.** `#armadilha`
Projeto: [[P13 - Video institucional da landing]].

## 1. Direcao de arte mandada gerar sem validacao

As tres primeiras variacoes de C01 foram rejeitadas em bloco. Causa: a direcao
de arte foi escrita e enviada para geracao sem aprovacao humana previa.
**Conserto permanente:** nenhuma geracao antes de biblia escrita e aprovada.

## 2. Fisica nao se conserta por prompt

Em C01 a bandeja atravessou o poste em tres takes seguidos. **Modelo de video
nao tem simulacao de corpo rigido** — nenhuma redacao de prompt evita
interpenetracao. A unica solucao foi **remover a bandeja da cena**.

**Regra derivada:** objeto manipulado fica abaixo da linha do balcao, ou nao
entra na cena.

## 3. `nano-banana-pro` rejeita `negative_prompt`

Devolve `[VALIDATION_ERROR] 400`. As negativas entram dentro do proprio prompt
como bloco `STRICTLY AVOID: ...`.

## 4. Timeout do MCP com a geracao seguindo e sendo cobrada

O MCP estoura em 60 s enquanto a geracao continua rodando no servidor — e e
cobrada. **Retry cego cobra duas vezes.**

**Conserto:** `wait_for_completion: false` + `get_generation`, e conferir por
`get_credits` + `list_my_gallery` **antes** de qualquer retentativa.

## 5. `GENERATION_QUOTE_MISMATCH`

Aconteceu ao tentar `reference-to-video`: 61 creditos cobrados contra 31
esperados. **Conserto:** keyframe + image-to-video, 37 creditos por cena — 24 a
menos por cena.

## 6. Limite de videos simultaneos

"Limite de videos simultaneos atingido (4)" no plano PRECISION. Disparar em
ondas de 4 e so entao a quinta.

## 7. Veo nao aceita 5 segundos

As duracoes possiveis sao **4, 6 e 8**. Toda duracao fracionada do roteiro tem
que ser arredondada e reajustada na montagem — foi o que encurtou o corte de
78 s para 74,1 s.

## 8. `first_frame` governa posicao, prompt governa movimento

Em image-to-video o prompt **nao** reposiciona nada. Enquadramento errado se
conserta no keyframe, nunca no texto.

## 9. CDN do Kairogen bloqueado para download

`curl` devolve HTTP 000 — o proxy de egresso nega o host. **Contorno:**
`get_generation` devolve a imagem inline. **MP4 continua sem caminho
automatico** — o Paulo baixa e reanexa para extracao de quadro com ffmpeg.

## 10. `moviki.com.br` inalcancavel pelo ambiente do Claude

O proxy nega `CONNECT` para o dominio; so o WebFetch passa, e ele nao executa
JavaScript. Playwright headless nao abre a pagina.
**Consequencia:** auditoria de conta se faz pela REST do Firestore, e **captura
de tela e sempre manual**.

## 11. Pagina publica lida sem JavaScript engana

O HTML estatico carrega todas as secoes, inclusive as ocultas, e os textos de
estado vazio. Uma leitura crua pode parecer preenchida ou vazia sem relacao com
o Firestore. **Fonte de verdade: `updateTime` do documento.**

## 12. Autenticidade confundida com precariedade

A primeira versao de C12 foi rejeitada por mostrar negocios com aparencia
improvisada. **Regra:** autenticidade nao significa precariedade.

## Ligacoes

[[R - Filme institucional - biblia visual e continuidade]] ·
[[R - Filme institucional - inventario de takes]] ·
[[ARQ - Incidentes e cacadas de bug]] · [[R - Regras de ouro]] ·
[[P13 - Video institucional da landing]]
