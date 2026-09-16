---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [videos, capa, galeria, instagram, tiktok, pagina-publica]
atualizado: 2026-09-16
---

# ARQ - Capa do video escolhida pelo lojista 16092026

Pedido do Paulo: *"na parte dos vídeos do Instagram, deixar escolher a capa
pra não ficar feio na página pública do cliente"*.

## O problema

Instagram e TikTok **não entregam miniatura** para fora do aplicativo deles.
O cartão dessas duas redes nascia só com a arte de fundo — no meio de cartões
do YouTube, que têm miniatura automática, parecia defeito.

## A solução

Campo **`capa`** (URL de imagem) **dentro de cada item do array `videos`**.

> **Por que dentro do item, e não um campo novo em `negocios/{uid}`:**
> a regra v25 valida `videos` só como `d.videos is list && size() <= 6`, sem
> entrar nos itens — conferido linha a linha na regra publicada. Campo novo
> solto cairia fora do `hasOnly` de `negocioValido()` e faria **todo** o
> "Salvar tudo" do painel ser negado: cardápio, fotos, promoções, tudo.
> Mesmo caminho do `sku` dentro de `cardapio`. **Sem regra nova.**

### No painel

Botão **Escolher capa** / **Trocar capa** em cada vídeo, com três saídas:

1. **Usar uma foto da galeria** — grade clicável, instantâneo, sem upload.
   É o caminho principal: quem tem vídeo quase sempre já tem foto boa.
2. **Enviar uma imagem** — mesmo `comprimirProporcional(1080)` e mesmo
   `/api/upload-imagem` das fotos. Nada de caminho novo para o mesmo problema.
3. **Tirar a capa** — volta ao automático.

A miniatura do painel mostra a capa escolhida, na mesma ordem da página
pública: **capa escolhida > miniatura do YouTube > arte de fundo**. O lojista
vê o que o cliente dele vai ver, antes de salvar.

### Na página pública

`vidInfo()` passou a ler `capa`, validada pelo **mesmo `fotoOk()`** da galeria
(só `firebasestorage` e `ibb.co`). `cartaoVideo()` usa a capa antes da
miniatura do YouTube. A arte de fundo continua embaixo de tudo: imagem que não
carrega deixa o cartão bonito em vez de cinza.

⚠️ **A validação da origem não é firula.** `capa` é texto guardado no banco e
vai direto para um `src` na página do cliente. Sem a lista fechada, qualquer
endereço entraria. Testado: `capa: "javascript:alert(1)"` é **descartado nas
duas pontas** — não chega ao banco pelo painel e não vira `src` na página.

## Achado de quebra: a CSP barrava foto antiga

O `fotoOk()` da página pública aceita `ibb.co`, mas o `img-src` da CSP **não
tinha** esse domínio. Foto hospedada lá era aceita pela validação e bloqueada
pelo navegador — sumia sem erro visível. `i.ibb.co` e `*.ibb.co` entraram no
`img-src`. Vale a regra: **origem aceita pela validação tem que estar na CSP.
Divergência entre as duas é falha silenciosa.**

## Arquivos

| Repo | Arquivo | Ação | Marca nova | Montado sobre |
| --- | --- | --- | --- | --- |
| moviki-app | `index.html` | SUBSTITUI | `2026-09-16-capavideo` | `2026-09-16-trilha` |
| moviki-app | `parceiro.html` | SUBSTITUI | `2026-09-16-trilha` | `2026-09-16-liveparc2` |
| moviki | `404.html` | SUBSTITUI | `2026-09-16-capavideo` | `2026-09-15-compra4` |
| moviki-ai | `lib/catalogoPainel.js` | SUBSTITUI | `2026-09-16-6` | `2026-09-16-5` |

**Ordem:** app → site → Vik por último.
O `index.html` deste pacote **já contém** a trilha das aulas: se o pacote
`2026-09-16-trilha` ainda não subiu, este substitui os dois.

## Testado em Chromium

**Painel:** capa válida preservada na leitura e na gravação · `javascript:`
descartado · botão em todos os cartões · miniatura mostrando a capa · folha
abrindo com as fotos da galeria · escolha aplicando, fechando e avisando para
salvar · campo vazio **não** é gravado.

**Página pública:** YouTube sem capa usa a do YouTube · YouTube com capa usa a
escolhida · Instagram com capa mostra a capa · Instagram sem capa cai na arte
de fundo · TikTok com endereço inválido não vira imagem.

`node --check` limpo nos 9 blocos de script do painel e no da página pública.
BOM e CRLF preservados no `index.html`; zero byte de controle no `404.html`.

## Ligações

[[A1 - Produto e Paineis]] · [[R - Regras de ouro]] ·
[[ARQ - Trilha da aula e medidor visivel 16092026]]
