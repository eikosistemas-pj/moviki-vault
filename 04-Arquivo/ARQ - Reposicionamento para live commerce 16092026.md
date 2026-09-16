---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [marca, posicionamento, landing, live, home, medicao]
atualizado: 2026-09-16
---

# ARQ - Reposicionamento para live commerce 16092026

Decisao do Paulo em 16/09/2026: **a imagem da empresa passa a ser venda ao vivo
e live commerce, com localizacao em tempo real junto** — o mesmo eixo do
panfleto novo. O site inteiro foi refeito nesse eixo na mesma madrugada.

## O eixo

> **"Seu negocio no mapa. E em video."**

A frase abre as duas paginas. Localizacao deixa de ser o produto e passa a ser
**metade** dele; a outra metade e vender pela camera do celular.

## Papel de cada pagina — decisao fechada

| Pagina | Papel |
| --- | --- |
| `index.html` (home) | **vitrine** — mostra o que o Moviki e, para quem chega frio |
| `comerciantes.html` | **conversao** — para quem ja entendeu e quer criar a pagina |

Nao sao a mesma pagina com palavras diferentes. A home explica; a de
comerciantes fecha.

## `comerciantes.html` — `2026-09-16-filmelive`

- Hero: **"Seu negocio no mapa. E em video."**
- Bloco **"O que vem junto"** com os sete blocos do panfleto novo, **na mesma
  ordem e com as mesmas palavras**. Papel e site tem que dizer a mesma coisa: o
  lojista recebe o panfleto do parceiro na rua e abre o link em seguida.
- Secao `data-sec="live"` com o player do filme hero.

## `index.html` — `2026-09-16-ctavideo`

- Hero: **"Seu negocio no mapa. / E em video."**
- Secao `#aovivo` nova: tres cartoes, a arte da live e o filme.
- **A home ganhou medicao de rolagem, que ela nunca teve.** Onze `data-sec` e um
  IntersectionObserver disparando `secao_vista`. A `comerciantes.html` tinha
  isso desde 11/09; a home, a pagina que recebe mais gente, era cega.
- Os botoes **Comecar gratis** e **Ver o Modo Live** foram para **depois do
  player**, centralizados — pedido do Paulo, e faz sentido: o CTA chega quando
  a pessoa acabou de ver o que o produto faz.

## Arte da live

`livehero.webp/png/jpg`, 800x1421. O `.jpg` foi para 1200x630 para servir de
imagem de previa (Open Graph).

**O contador da arte dizia "1,4 mil".** Terceira reincidencia do mesmo defeito
em pecas do projeto: numero inventado em mockup e promessa de resultado
implicita. Corrigido para **"12"** sem pedir autorizacao — o Paulo deu
autorizacao permanente para corrigir violacao de regra da Meta e do Google
direto.

> **Regra que fica:** numero em mockup e promessa. Mockup usa numero pequeno e
> plausivel, ou nenhum.

## Fica em aberto

- [ ] `premium.html` e `enterprise.html` **nao citam a live em lugar nenhum** —
      conferido, zero mencao. E `premium.html` e a landing que recebe trafego
      pago.
- [ ] As duas continuam **sem marca de versao**.

## Ligacoes

[[A1 - Produto e Paineis]] · [[A7 - Aquisicao e Midia Paga]] ·
[[A13 - Modo Live]] · [[P24 - Modo Live - lancamento]] ·
[[P25 - Pagina de venda da live]] ·
[[R - Regras de conteudo e tom]] · [[R - Eventos GA4 dicionario]] ·
[[R - Marcas de versao no ar]] ·
[[ARQ - Posicionamento e home reescrita 07092026]]
