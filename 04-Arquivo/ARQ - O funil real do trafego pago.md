---
type: decisao
status: concluido
area: A7 - Aquisicao e Midia Paga
tags: [moviki, meta-ads, google-ads, ga4, aquisicao, conversao, medicao]
atualizado: 2026-09-11
---

# ARQ - O funil real do trafego pago

> Com o GA4 conectado, o funil apareceu inteiro pela primeira vez. **O gargalo nao
> e o quiz nem o cadastro: e a propria comerciantes.html.** De 215 pessoas que
> chegaram pelo anuncio, 5 clicaram no botao. E os 2 unicos sign_up atribuidos ao
> Meta sao os testes do dia 05/09.

Relacionado: [[A7 - Aquisicao e Midia Paga]] · [[A6 - Medicao e Analytics]] ·
[[ARQ - Anuncio do Meta caia na tela de login]] · [[R - Eventos GA4 dicionario]]

---

## 1. O funil, em pessoas (14 dias ate 11/09/2026)

Origem `facebook / cpc`:

| Etapa | Pessoas | Do passo anterior |
| --- | --- | --- |
| Chegaram na `comerciantes.html` | **215** | — |
| Chegaram a 90% da pagina (evento `scroll`) | 9 | 4,2% |
| Clicaram no CTA (`cta_click`) | **5** | **2,3% do total** |
| Abriram o painel (`cta_painel`) | 5 | 100% |
| Entraram no quiz (`quiz_etapa`) | 3 | 60% |
| `sign_up` | 2 | 67% |

Origem `google / cpc`: **16 pessoas, zero clique no CTA, zero quiz, zero cadastro.**
Coerente com os termos de GPS e satelite que a campanha comprava antes do conserto.

## 2. Os 2 sign_up nao sao clientes

Ambos caem em **05/09** — o mesmo dia do cadastro de teste "Eiko Jato", feito com
fbclid manual na URL, e das 2 conversoes Lead que a CAPI confirmou as 07:27.

**Cadastro real vindo de anuncio pago: zero.** A base continua sem lojista de verdade.

## 3. Onde o dinheiro some

**215 chegaram, 5 clicaram.** 210 pessoas viram a pagina e sairam sem tocar em nada.

Tudo o que vem depois funciona bem: quem clica, abre o painel (100%); quem abre,
entra no quiz (60%); quem entra, termina (67%). **O quiz nao pode ser o culpado de
um problema que so 3 pessoas chegaram a ver em 14 dias.**

Duas rodadas foram gastas investigando quiz, tela de login e medicao. O gargalo
estava no primeiro passo o tempo todo.

**Licao de metodo:** funil se le de cima para baixo. Investigar a etapa funda antes
de medir a etapa rasa custa tempo e leva a conserto no lugar errado.

## 4. O que isso faz com a campanha nova

A campanha criada em 11/09 otimiza por evento **Lead**, que nunca aconteceu de
verdade. A Meta precisa de sinal de conversao para aprender; com zero, ela tende a
entregar pouco e ficar em aprendizado.

Isso e consequencia direta de trocar o objetivo antes de consertar o gargalo. A
ordem correta era: **primeiro fazer a pagina converter, depois pedir conversao ao
algoritmo.** A campanha fica de pe, mas nao se deve esperar volume dela enquanto o
topo do funil estiver em 2,3%.

## 5. Regra de ouro que nasce daqui

> **Antes de consertar uma etapa do funil, meca quantas pessoas chegaram nela.**
> Etapa que quase ninguem alcanca nao explica resultado nenhum, por pior que pareca.

> **Objetivo de conversao exige conversao existente.** Pedir ao algoritmo um evento
> que nunca aconteceu e pedir no vazio: consertar a pagina vem antes de trocar o
> objetivo.

Entram em [[R - Regras de ouro]].

## 6. O que fica

- [ ] Trabalhar o topo da `comerciantes.html` — os primeiros segundos decidem 210 das 215 saidas
- [ ] Registrar o parametro `etapa` como dimensao personalizada no GA4 (Admin →
      Definicoes personalizadas), para o `quiz_etapa` poder ser quebrado por tela
- [ ] Reavaliar a campanha de Lead depois que a pagina converter
- [ ] Apagar a conta de teste "Eiko Jato", que ainda contamina o `sign_up`
