---
type: decisao
status: concluido
area: A7 - Aquisicao e Midia Paga
tags: [moviki, meta-ads, google-ads, ga4, funil, conversao]
atualizado: 2026-09-11
---

# ARQ - O funil real do tráfego pago

> Com o GA4 conectado, o funil apareceu inteiro pela primeira vez. **O gargalo não é
> o quiz nem o cadastro: é a própria `comerciantes.html`.** De 215 pessoas que
> chegaram pelo anúncio, 5 clicaram no botão. E os 2 únicos `sign_up` atribuídos ao
> Meta são testes do próprio Paulo, de 05/09.

---

## 1. O funil, em pessoas — 14 dias até 11/09/2026

Origem `facebook / cpc`:

| Etapa | Pessoas | Do passo anterior |
| --- | --- | --- |
| Chegaram na `comerciantes.html` | **215** | — |
| Chegaram a 90% da página (`scroll`) | 9 | 4,2% |
| Clicaram no CTA (`cta_click`) | **5** | **2,3% do total** |
| Abriram o painel (`cta_painel`) | 5 | 100% |
| Entraram no quiz (`quiz_etapa`) | 3 | 60% |
| `sign_up` | 2 | 67% |

Origem `google / cpc`, mesmos 14 dias: **16 pessoas, zero clique no CTA, zero quiz,
zero cadastro.** Coerente com os termos de GPS e satélite que a campanha comprava
antes do conserto de 11/09.

## 2. Os 2 sign_up não são clientes

Ambos caem em **05/09** — o mesmo dia do cadastro de teste feito pelo próprio Paulo
com `fbclid` manual na URL, e das 2 conversões Lead que a CAPI confirmou às 07:27.

**Cadastro real vindo de anúncio pago: ZERO.** A base continua sem lojista de verdade.

## 3. Onde o dinheiro some

**215 chegaram, 5 clicaram.** 210 pessoas viram a página e saíram sem tocar em nada.

Tudo o que vem depois funciona bem: quem clica abre o painel (100%); quem abre entra
no quiz (60%); quem entra termina (67%). **O quiz não pode ser o culpado de um
problema que só 3 pessoas chegaram a ver em 14 dias.**

Duas rodadas foram gastas investigando quiz, tela de entrada e medição. O gargalo
estava no primeiro passo o tempo todo.

**Lição de método:** funil se lê de cima para baixo. Investigar a etapa funda antes
de medir a etapa rasa custa tempo e leva a conserto no lugar errado.

## 4. Dois diagnósticos errados, corrigidos

Duas notas foram produzidas em 11/09 a partir de premissa errada. Ficam registradas
aqui como correção, e **não** como arquivo próprio.

### 4.1 "Medição cega no Meta por código de teste esquecido" — premissa falsa

A tese era que o `META_TEST_CODE` tinha ficado ligado na Vercel desde 05/09 e jogava
todo evento para a aba "Testar eventos", tornando `actions_lead = 0` indistinguível
de um problema de medição.

**Não procede.** O print das variáveis de ambiente do `moviki-robo` em 11/09 mostra
**16 envs e nenhuma delas é o `META_TEST_CODE`**. A medição não estava cega: o zero
era real, e o funil do GA4 confirma por outro caminho (5 cliques no CTA, 2 sign_up
de teste).

Fica de pé apenas o achado de leitura: `actions_lead` mede **formulário nativo do
Facebook**, não evento server-side. O campo da CAPI é
`actions_offsite_conversion_fb_pixel_lead`. Os quatro campos de conversão foram
conferidos e todos estavam em zero.

> **Lição:** campo de métrica com nome parecido mede coisa diferente. E pendência
> anotada numa rodada anterior não vira diagnóstico sem conferência da fonte.

### 4.2 "Anúncio do Meta caía na tela de login" — premissa falsa

A tese era que o CTA "Começar grátis" entregava `app.moviki.com.br` com a aba
**Entrar** ativa por padrão, pedindo uma senha que o visitante nunca criou.

**Não procede.** O `app.moviki.com.br` abre **no quiz**, não no login. A porta de
entrada nunca foi o furo, e o funil mostra isso: dos 5 que abriram o painel, 3
entraram no quiz e 2 terminaram. Quem chega no painel passa.

O que sobra do caso é o furo real de objetivo de campanha, tratado em
[[ARQ - Reestruturacao da campanha do Meta]]: a campanha antiga otimizava por
`LANDING_PAGE_VIEWS`, ou seja, comprava visita, não cadastro.

## 5. O que isso faz com a campanha nova

A campanha criada em 11/09 otimiza por evento **Lead**, que nunca aconteceu de
verdade. A Meta precisa de sinal de conversão para aprender; com zero, tende a
entregar pouco e ficar em aprendizado.

A ordem correta era: **primeiro fazer a página converter, depois pedir conversão ao
algoritmo.** A campanha fica de pé, mas não se deve esperar volume dela enquanto o
topo do funil estiver em 2,3%.

## 6. Regras de ouro que nascem daqui

> **Antes de consertar uma etapa do funil, meça quantas pessoas chegaram nela.**
> Etapa que quase ninguém alcança não explica resultado nenhum, por pior que pareça.

> **Objetivo de conversão exige conversão existente.** Pedir ao algoritmo um evento
> que nunca aconteceu é pedir no vazio: consertar a página vem antes de trocar o
> objetivo.

> **Diagnóstico se confirma na fonte, não na anotação anterior.** Duas rodadas
> inteiras foram gastas em duas premissas que um print de variáveis e uma abertura
> da página derrubariam em um minuto.

## 7. O que fica

- [ ] Trabalhar o topo da `comerciantes.html` — os primeiros segundos decidem 210 das 215 saídas
- [ ] Registrar o parâmetro `etapa` como dimensão personalizada no GA4 (Admin → Definições personalizadas), para o `quiz_etapa` poder ser quebrado por tela
- [ ] Reavaliar a campanha de Lead depois que a página converter
- [ ] Apagar a conta de teste de 05/09, que ainda contamina o `sign_up`

## Ligações

[[A7 - Aquisicao e Midia Paga]] · [[A6 - Medicao e Analytics]] ·
[[A1 - Produto e Paineis]] · [[ARQ - O favicon de 949 KB]] ·
[[ARQ - Reestruturacao da campanha do Meta]] ·
[[ARQ - Vazamento de trafego no Google Ads e conserto]] ·
[[ARQ - Pulso das campanhas 12 e 13092026]] ·
[[R - Eventos GA4 dicionario]] · [[R - Regras de ouro]]
