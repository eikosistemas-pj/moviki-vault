---
type: incidente
status: concluido
area: A7 - Aquisicao e Midia Paga
tags: [moviki, performance, aquisicao, conversao, armadilha, design]
atualizado: 2026-09-11
---

# ARQ - O favicon de 949 KB

> A `comerciantes.html` carregava **1,44 MB**, e **949 KB disso era o favicon** —
> um PNG de 1254x1254 servido como icone de aba. Depois da otimizacao a mesma
> pagina carrega **104 KB**, 14x mais leve, com o pixel identico na tela.

Relacionado: [[ARQ - O funil real do trafego pago]] · [[A7 - Aquisicao e Midia Paga]] ·
[[A11 - Marca e Design System]] · [[R - Regras de ouro]]

---

## 1. Como chegamos aqui

O funil apontou que 215 pessoas chegaram na pagina e apenas 5 clicaram no botao.
A primeira hipotese foi que o topo da pagina era fraco. **Era falso** — a pagina foi
renderizada num viewport de celular (390x844) e o topo esta correto: titulo claro,
subtitulo claro, botao visivel sem rolar, prova "30 dias gratis, sem cartao" e o
mockup logo abaixo.

A medicao de peso e que mostrou o problema.

## 2. O que a pagina carregava

| Recurso | Peso | Observacao |
| --- | --- | --- |
| `favicon512.png` | **949 KB** | PNG 1254x1254 usado como icone de aba |
| `app-mockup.png` | 360 KB | mockup do hero |
| `logo.png` | 68 KB | |
| `comerciantes.html` | 17 KB | |
| `mvmetrica.js` | 13 KB | |
| icones do hero | ~35 KB | |
| **Total do 1o carregamento** | **1,44 MB** | 66% disso e o favicon |

Num 4G brasileiro real, 1,44 MB sao 3 a 4 segundos so de download; em sinal fraco,
10 segundos ou mais. Quem vem de anuncio no celular nao espera isso — e o
`page_view` do GA4 ja disparou, entao a saida nem aparece como falha de carregamento.

**O arquivo nem tinha 512 pixels.** O nome diz 512, a imagem tinha 1254x1254.

## 3. O conserto

Reamostragem para 512x512 no favicon e requantizacao com paleta adaptativa de 256
cores preservando o canal alfa, em todo o pacote de imagens dos dois repositorios.
Comparacao visual lado a lado: **sem diferenca perceptivel**.

| | Antes | Depois |
| --- | --- | --- |
| `comerciantes.html` (1o carregamento) | 1.442 KB | **104 KB** |
| `favicon512.png` (site e painel) | 949 KB | 10 KB |
| `app-mockup.png` | 360 KB | 49 KB |
| `logo.png` | 68 KB | 11 KB |
| Pacote de imagens do site | 1.842 KB | 527 KB |
| Pacote de imagens do painel | 2.113 KB | 768 KB |

Nenhuma linha de HTML mudou: os nomes dos arquivos sao os mesmos, entao **todas as
paginas dos dois repositorios ficam mais leves de uma vez**.

## 4. Regra de ouro que nasce daqui

> **Favicon nao e arte — e icone de aba.** Nenhuma imagem servida como favicon passa
> de 512x512, e o peso vive em dezenas de KB, nunca em centenas.

> **Antes de reescrever uma pagina que nao converte, pese a pagina.** Copy e layout
> so importam para quem esperou o carregamento terminar.

Entram em [[R - Regras de ouro]].

## 5. O que fica

- [ ] Subir os dois pacotes de imagem e conferir no ar que nada quebrou visualmente
- [ ] Reler o funil do Meta 48h depois: `cta_click` sobre `page_view` deve subir dos 2,3% atuais
- [ ] Avaliar `fundo.jpg` (88 KB) e os `.webp` do Vik na proxima passada
- [ ] Se o CTR interno nao subir com a pagina leve, ai sim o problema e a copy
