---
type: incidente
status: concluido
area: A7 - Aquisicao e Midia Paga
tags: [moviki, meta-ads, google-ads, aquisicao, conversao, armadilha]
atualizado: 2026-09-11
---

# ARQ - Anuncio do Meta caia na tela de login

> **275 pessoas chegaram na pagina em 14 dias e nenhuma se cadastrou.** Nao era
> medicao: eram dois furos empilhados — a campanha pedia visita em vez de
> cadastro, e o botao "Comecar gratis" entregava uma tela pedindo senha.

Relacionado: [[A7 - Aquisicao e Midia Paga]] · [[A6 - Medicao e Analytics]] ·
[[A1 - Produto e Paineis]] · [[R - Regras de ouro]]

---

## 1. O numero que abriu o caso

Conta Meta 920636768619509, 14 dias ate 11/09/2026:

| | Total |
| --- | --- |
| Gasto | R$ 118,02 |
| Cliques no link | 372 |
| **Visualizacoes de pagina** | **275** |
| Leads (todos os campos de conversao) | **0** |

Taxa de conversao: **0%**.

## 2. Dois diagnosticos errados no caminho

**Errado 1 — "e o META_TEST_CODE".** A pendencia anotada em 10/09 mandava remover
essa env da Vercel. O print das variaveis do `moviki-robo` mostrou **16 envs e
nenhuma delas e o META_TEST_CODE**. A pendencia estava errada e foi repetida sem
conferencia.

**Errado 2 — "a CAPI nao registra".** O campo lido era `actions_lead`, que mede
**formulario nativo do Facebook**, nao evento server-side. O campo certo para CAPI
e `actions_offsite_conversion_fb_pixel_lead`. Conferidos os quatro campos de
conversao: todos zero. Entao a medicao estava certa — nao houve cadastro mesmo.

**Licao:** campo de metrica com nome parecido mede coisa diferente. Antes de
declarar medicao quebrada, conferir se o campo lido e o campo do evento.

## 3. Furo 1 — a campanha pedia a coisa errada

| Campanha | Objetivo | Otimizando por |
| --- | --- | --- |
| Moviki \| Cadastro de lojista \| Joao Pessoa \| set-2026 | `OUTCOME_TRAFFIC` | **LANDING_PAGE_VIEWS** |
| Post do Instagram (impulsionado) | `LINK_CLICKS` | LINK_CLICKS |

O algoritmo da Meta otimiza **literalmente** para o que se pede. Pedindo
visualizacao de pagina, ele aprende a achar quem clica e carrega — o publico mais
barato e menos comprometido que existe. Entregou 237 visitas por R$ 103, a R$ 0,44
cada. Ele fez o trabalho certo para a pergunta errada.

## 4. Furo 2 — o botao entregava uma porta trancada

Cadeia real do visitante:

1. Anuncio diz **"Comecar gratis"**
2. Cai em `moviki.com.br/comerciantes.html` — pagina certa, tráfego frio na pagina
   que apresenta o produto
3. Clica em **"Comecar gratis →"**
4. Cai em `app.moviki.com.br` com a aba **Entrar** ativa por padrao
   (`<button id="abaEntrar" class="ativa">`), pedindo e-mail, senha e com
   "Esqueci minha senha" logo abaixo

Quem nunca ouviu falar do Moviki chega numa tela que pede uma senha que ela nunca
criou. O botao "Criar conta" existe, ao lado, sem destaque nenhum.

**A cadeia tecnica estava toda certa** — `mvmetrica.js` captura o `fbclid`, guarda
em sessionStorage, injeta `mvfbc` no salto entre dominios e na chamada de cadastro.
O elo que faltava nao era tecnico: era a porta de entrada.

## 5. O conserto (11/09/2026)

**`moviki/comerciantes.html`** (`2026-09-11-criarconta`): os dois CTAs passaram a
apontar para `https://app.moviki.com.br/?criar=1`. O `mvmetrica.js` ja trata href
com query existente, entao o `mvfbc` continua sendo injetado normalmente.

**`moviki-app/index.html`** (`2026-09-11-criarconta`): nasce `mvAbaInicial()`, que
le `?criar=1` (aceita tambem `novo=1` e `cadastro=1`) e devolve qual aba abrir. A
branch de "nao logado" do boot, que chamava `trocarAba('entrar')` fixo, passou a
chamar `trocarAba(mvAbaInicial())`.

O parametro vale **uma vez por carregamento**: logout de verdade continua caindo em
Entrar mesmo com o parametro ainda na barra de endereco.

Conferido por diff: tres mudancas em cada arquivo, nada mais tocado. Sintaxe dos
13 blocos de script inline validada.

## 6. Regra de ouro que nasce daqui

> **O que o anuncio promete, a primeira tela entrega.** Anuncio que diz "comecar
> gratis" nao pode cair em tela de login. Todo CTA de aquisicao carrega o estado
> da tela de destino, nunca confia no padrao dela.

> **Objetivo de campanha e o que voce esta comprando.** Otimizar por visita compra
> visita. Quem quer cadastro pede cadastro, mesmo que o volume caia.

Entram em [[R - Regras de ouro]].

## 7. O que fica

- [ ] Subir os dois arquivos e conferir no ar que `?criar=1` abre a aba certa
- [ ] Recriar a campanha do Meta com objetivo de **conversao/Lead**, nao trafego
      (objetivo nao e editavel na Meta — exige campanha nova)
- [ ] Desligar o impulsionamento "Post do Instagram" (LINK_CLICKS, R$ 14,78, 0 lead)
- [ ] Aplicar o mesmo `?criar=1` nos demais CTAs do site (`index.html`,
      `premium.html`) numa rodada propria
- [ ] So julgar a campanha do Meta depois de 48h com a porta consertada
