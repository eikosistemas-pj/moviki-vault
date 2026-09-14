---
type: projeto
status: ativo
area: A7 - Aquisicao e Midia Paga
tags: [aovivo, live, landing, conversao, csp, video]
atualizado: 2026-09-14
prioridade: 1
prazo: 2026-09-30
---

# P25 — Página de venda da live

A página `/aovivo` é a camada de ação do funil e é ela que destrava tornar o
filme hero público no YouTube. Está na **V2**, entregue em 13/09/2026 à tarde.

## Estado

| Item | Valor |
| --- | --- |
| Arquivo | `moviki/aovivo.html` |
| Rota | `/aovivo`, via `rewrites` do `vercel.json` do site |
| Marca de versão V1 | `2026-09-13-aovivo1` |
| Marca de versão V2 (vigente) | `2026-09-13-aovivo4` |
| Imagens | `livehero.webp` (103 KB) e `livehero.jpg` (140 KB, reserva do `<picture>`) |
| Peso do HTML | 50 KB |

## Decisão de arquitetura: dois níveis, não repaginar o site

O funil de 11/09 mostrou 215 pessoas na `comerciantes.html` e 5 cliques no CTA
(2,3%). Reescrever as quatro landings ao mesmo tempo apaga a única linha de base
que existe, e não há volume para um A/B significativo.

| Nível | Onde | Promessa |
| --- | --- | --- |
| Guarda-chuva | `index.html`, `comerciantes.html` | ser encontrado hoje |
| Camada de ação | `/aovivo` | o palco onde a venda acontece |

Live é upsell e retenção, não porta de entrada. Só vira topo do `index.html` se
a `/aovivo` converter melhor que a `comerciantes.html`.

## O que a V2 mudou sobre a V1

- **O vídeo muda com o dispositivo.** Até 760 px o palco é 9:16 e toca o corte
  vertical de 60 s; acima, o palco é 16:9 e toca o filme de 2:38
  (`n2nmTfGY_mo`). Um palco, um `iframe`, nenhum player concorrendo. No celular
  um botão discreto abaixo do palco abre o filme inteiro. Motivo: o tráfego pago
  chega no celular, e filme horizontal de 2:38 em tela de celular é abandono.
- Short do corte vertical publicado em 13/09 no canal **Moviki App**, id
  `3Q5b0Q0PPh4`, título *MOVIKI AO VIVO | Mostre. Responda. Venda em tempo real.*
  Confirmado público por oembed.
- `video_play` distingue `corte_vertical_60s` de `filme_hero`.
- Título da seção, selo e linha de apoio trocam por `soMob` / `soDesk`.
- **A arte do Paulo foi corrigida sem pedir:** o contador de "1,4 mil" assistindo
  virou **12**. "1,4 mil" contradiz a decisão D1 do filme hero e, em peça de
  campanha, funciona como claim de alcance automático. Inpaint + badge
  redesenhado em Poppins Bold; a página diz, sob a imagem, que os números são
  exemplo.

## Player em fachada e CSP por arquivo

- Player em **fachada**: capa em CSS, `iframe` de `youtube-nocookie` criado só
  no clique. Sem miniatura externa.
- **A CSP mora dentro do próprio HTML.** No repo `moviki` a política é
  `<meta http-equiv="Content-Security-Policy">` **por arquivo** (igual
  `enterprise.html`, `404.html`, `v.html`). O `vercel.json` do site só tem
  `rewrites` e `functions` — **nenhum header de CSP**. Página nova sem a meta
  fica sem CSP nenhuma, porque não há header de servidor para herdar.
- A meta libera apenas `frame-src https://www.youtube-nocookie.com`. Como a
  fachada não usa miniatura externa, **não** é preciso
  `img-src https://i.ytimg.com` — a V1 ainda liberava. Conferido no navegador
  com a CSP ligada: iframe nasce, zero recurso recusado.
- Sem a meta certa o player **não abre e não dá erro visível**.

## Preço e conformidade

- **O preço não aparece na página.** Fica em `/premium.html` e
  `/enterprise.html`. A `/aovivo` traz a tabela comparativa Premium x Enterprise
  sem valores.
- Gatilhos usados: dor identificável, contraste antes x depois, novidade,
  curiosidade, redução de atrito, quebra de objeção em bloco próprio,
  reciprocidade (Academia), prova de mecanismo, ancoragem por comparação,
  autoridade por transparência ("O que a gente não faz"), CTA progressivo em
  5 pontos.
- Gatilhos recusados: depoimento e "X lojistas já usam" (base real de pagante
  vindo de anúncio é zero), contador regressivo e vagas limitadas, "até 40% de
  conversão", qualquer promessa de faturamento. A FAQ responde "vender ao vivo
  garante mais vendas?" com um **não** explícito.

## Medição

- Padrão `mvmetrica.js` + `data-ev`. O valor de `data-ev` é o nome do CTA; o
  evento enviado é `cta_click` com `{cta, pagina:'aovivo'}` via `window.mvEv`.
- `chegou_por_indicacao` com `?ref=`.

## Layout e bugs virados regra

- CTA acima da dobra medido no navegador em 375x667, 360x740 e 390x844. No
  celular a arte vem antes do texto, com altura em `vh` e breakpoint por
  `max-height`.
- Em `display:flex`, cada `<b>`/`<span>` do item vira flex item e o texto se
  reordena.
- `.avTrocar{display:block}` depois de `.soMob{display:none}` reacendia o
  elemento escondido no desktop — ordem das regras importa.

## Beta: a página está com noindex

Durante o beta fechado a `/aovivo` está com `noindex` — ver
[[ARQ - Live escondida durante o beta 14092026]]. A página já fala em nome do
recurso para quem se cadastrar, e nenhuma live real rodou fora da conta do Paulo.

## Aberto

- [ ] Conferir o player no celular com a página no ar
- [ ] Conferir os destinos dos CTAs — a V1 apontava para `/comerciantes.html`;
      a `enterprise.html` usa `https://app.moviki.com.br?plano=enterprise`
- [ ] Revisar a copy da página
- [ ] Apontar a descrição do Short e do filme longo para `/aovivo`
- [ ] Conferir no YouTube Studio se o Short `3Q5b0Q0PPh4` está com o embed liberado
- [ ] Apex x www — cada CTA novo herda o salto de redirecionamento
- [ ] Trocar a dobra da `comerciantes.html` (210 das 215 saídas)
- [ ] Tirar o `noindex` quando o beta fechar

## Ligações

- [[A13 - Modo Live]]
- [[A7 - Aquisicao e Midia Paga]]
- [[P24 - Modo Live - lancamento]]
- [[P26 - Cortes do filme hero - vertical e pago]]
- [[P27 - Publicacao do filme hero no YouTube]]
- [[P30 - Decisao de dominio apex ou www]]
- [[ARQ - Live escondida durante o beta 14092026]]
- [[ARQ - Filme hero v6 aprovado 13092026]]
- [[ARQ - Cortes do filme hero vertical e pago 13092026]]
- [[R - Live - Exposicao e interruptores do beta]]
- [[R - Retomada live parte 02]]
- [[R - Planos e precos]]
- [[R - Checklist conformidade Meta e Google]]
- [[R - Eventos GA4 dicionario]]
- [[R - Marcas de versao no ar]]
