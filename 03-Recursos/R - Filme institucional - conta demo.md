---
type: recurso
status: referencia
area: A8 - Conteudo e Social
tags: [video, produto, lgpd]
atualizado: 2026-08-31
---

# R — Filme institucional: conta demo

A conta de demonstracao de onde saem as capturas de tela de C08, C09 e C10.
Projeto: [[P13 - Video institucional da landing]].

## Por que existe uma conta demo

O opt-in `autorizaDivulgacao` do produto **nao cobre o filme**: ele promete ao
lojista *"Nunca publicamos seu endereco exato — so a cidade"*, e o filme mostra
o mapa. **Nenhuma captura sai de cliente real.** A conta demo resolve o
bloqueador de LGPD por inteiro.

## Contas avaliadas

| Slug | Veredito |
| --- | --- |
| `movikiapp` | ❌ descartada — vazia **e** o negocio se chama "moviki.app", o que viola a regra de nao usar o nome MOVIKI como nome do estabelecimento. No filme o cliente precisa encontrar **um negocio**, nao a plataforma. |
| `hamburguermaster` | ✅ escolhida — plano enterprise ativo, GPS definido, logo enviada, cardapio iniciado |

## Identificadores

| Campo | Valor |
| --- | --- |
| Slug | `hamburguermaster` |
| `uid` | `rjESfrCf8NPiQBNyDwxnP4BzAzd2` |
| Plano | `enterprise`, ativo, origem trial, vence 2026-09-29 |
| GPS | -6.9825203 / -34.8295697 (Joao Pessoa/PB) |

Plano enterprise ativo libera **tudo**: fotos, cardapio, promocoes, eventos,
logo no pino, multi-ponto.

## Como auditar sem depender da pagina

**A pagina publica nao pode ser lida por fetch simples** — o conteudo vem do
Firestore por JavaScript, e o HTML estatico contem os blocos ocultos, o que faz
uma leitura crua parecer preenchida ou vazia sem relacao com a realidade.
**A leitura confiavel e a REST do Firestore**, que e publica em `/negocios`:

```
https://firestore.googleapis.com/v1/projects/moviki-app/databases/(default)/documents/slugs/<slug>
https://firestore.googleapis.com/v1/projects/moviki-app/databases/(default)/documents/negocios/<uid>
https://firestore.googleapis.com/v1/projects/moviki-app/databases/(default)/documents/assinaturas/<uid>
```

`projectId` = `moviki-app`. `updateTime` do documento diz se a edicao no painel
foi realmente salva. **Esta e a forma de conferir preenchimento, nao a pagina.**

## Checklist de preenchimento

| Campo | Exigido | Estado em 2026-08-31 23:37 |
| --- | --- | --- |
| `fotos` | 6 — a 1ª vira a capa | 🔴 0 |
| `cardapio` | 5 itens em 2 categorias, todos com foto, descricao e preco | 🟠 2 itens, 0 fotos |
| `promocoes` | 1, sem promessa agressiva | 🔴 0 |
| `endereco` | rua + bairro | 🔴 vazio |
| `horario` | preenchido | 🔴 vazio |
| `entrega` | preenchido | 🔴 vazio |
| `precoMedio` | > 0 | 🔴 0 |
| `cor` | fora da faixa ciano/azul da marca | 🔴 `#00f2fe` |
| `recado` | curto, sem exclamacao tripla | 🟠 "Seja Bem vindo!!!" |
| `whatsapp` | numero de demonstracao | 🟠 `4120186848` — conferir se e pessoal |
| `nome` | ficticio, sem colidir com marca real | 🟠 "Hamburguer Master" e generico |

## Tres consequencias que quebram o filme

1. **`fotos: []` mata a capa.** `aplicarCapa()` so usa foto da galeria; sem ela
   a pagina cai em `capaVazia` = **arte de marca MOVIKI**. A pagina do negocio
   abriria com a marca da plataforma no lugar da marca dele.
2. **Cardapio sem foto nao rende destaque.** `montarDestaques()` so usa o
   caminho com imagem quando ha **3 ou mais** produtos com foto.
3. **`cor: "#00f2fe"` e erro de posicionamento.** E praticamente o ciano da
   MOVIKI e pinta os destaques da pagina publica: em tela, o negocio fica com a
   identidade da plataforma e o espectador nao distingue os dois.

## Ordem de preenchimento

1. Nome + cor
2. Galeria de 6 fotos (a melhor primeiro — vira a capa)
3. Cardapio: 5 itens com foto, descricao e preco
4. 1 promocao com capa
5. Informacoes: horario, entrega, preco medio, endereco
6. Recado curto
7. WhatsApp de demonstracao

**Avaliacoes** nao entram no gate. Se aparecerem em quadro, apenas com nomes
claramente ficticios — nunca avaliacao redigida para parecer real.

## Ligacoes

[[R - Filme institucional - gate de assets]] · [[P13 - Video institucional da landing]] ·
[[R - Colecoes do Firestore]] · [[A10 - Conformidade e LGPD]]
