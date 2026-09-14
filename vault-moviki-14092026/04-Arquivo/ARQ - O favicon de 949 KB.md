---
type: incidente
status: concluido
area: A7 - Aquisicao e Midia Paga
tags: [moviki, performance, aquisicao, conversao, armadilha, design]
atualizado: 2026-09-11
---

# ARQ - O favicon de 949 KB

> A `comerciantes.html` carregava **1,44 MB**, e **949 KB disso era o favicon** — um
> PNG de **1254x1254** servido como ícone de aba. Depois da otimização a mesma página
> carrega **104 KB**, 14x mais leve, com o pixel idêntico na tela.

---

## 1. Como chegamos aqui

O funil apontou que 215 pessoas chegaram na página e apenas 5 clicaram no botão. A
primeira hipótese foi que o topo da página era fraco. **Era falso** — a página foi
renderizada num viewport de celular (390x844) e o topo está correto: título claro,
subtítulo claro, botão visível sem rolar, prova "30 dias grátis, sem cartão" e o
mockup logo abaixo.

A medição de **peso** é que mostrou o problema.

## 2. O que a página carregava

| Recurso | Peso | Observação |
| --- | --- | --- |
| `favicon512.png` | **949 KB** | PNG 1254x1254 usado como ícone de aba |
| `app-mockup.png` | 360 KB | mockup do hero |
| `logo.png` | 68 KB | |
| `comerciantes.html` | 17 KB | |
| `mvmetrica.js` | 13 KB | |
| ícones do hero | ~35 KB | |
| **Total do 1º carregamento** | **1.442 KB** | 66% disso é o favicon |

Num 4G brasileiro real, 1,44 MB são 3 a 4 segundos só de download; em sinal fraco,
10 segundos ou mais. Quem vem de anúncio no celular não espera isso — e o `page_view`
do GA4 já disparou, então a saída nem aparece como falha de carregamento.

**O arquivo nem tinha 512 pixels.** O nome diz 512, a imagem tinha 1254x1254.

## 3. O conserto

Reamostragem para 512x512 no favicon e requantização com paleta adaptativa de 256
cores preservando o canal alfa, em todo o pacote de imagens dos dois repositórios.
Comparação visual lado a lado: **sem diferença perceptível**.

| | Antes | Depois |
| --- | --- | --- |
| `comerciantes.html` (1º carregamento) | 1.442 KB | **104 KB** |
| `favicon512.png` (site e painel) | 949 KB | 10 KB |
| `app-mockup.png` | 360 KB | 49 KB |
| `logo.png` | 68 KB | 11 KB |
| Pacote de imagens do site | 1.842 KB | 527 KB |
| Pacote de imagens do painel | 2.113 KB | **768 KB** |

**Nenhuma linha de HTML mudou.** Os nomes dos arquivos são os mesmos, só os arquivos
de imagem foram trocados — então todas as páginas dos dois repositórios ficam mais
leves de uma vez.

## 4. Regras de ouro que nascem daqui

> **Favicon não é arte — é ícone de aba.** Nenhuma imagem servida como favicon passa
> de 512x512, e o peso vive em dezenas de KB, nunca em centenas.

> **Antes de reescrever uma página que não converte, pese a página.** Copy e layout
> só importam para quem esperou o carregamento terminar.

## 5. O que fica

- [ ] Subir os dois pacotes de imagem e conferir no ar que nada quebrou visualmente
- [ ] Reler o funil do Meta 48h depois: `cta_click` sobre `page_view` deve subir dos 2,3% atuais
- [ ] Avaliar `fundo.jpg` (88 KB) e os `.webp` do Vik na próxima passada
- [ ] Se o CTR interno não subir com a página leve, aí sim o problema é a copy

## Ligações

[[ARQ - O funil real do trafego pago]] · [[A7 - Aquisicao e Midia Paga]] ·
[[A11 - Marca e Design System]] · [[A2 - Infraestrutura e Deploy]] ·
[[R - Design system e icones]] · [[R - Regras de ouro]] ·
[[R - Marcas de versao no ar]]
