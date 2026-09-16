---
type: projeto
status: aberto
area: "[[A7 - Aquisicao e Midia Paga]]"
tags: [seo, search-console, conteudo, palavras-chave]
prioridade: alta
prazo: 2026-10-15
atualizado: 2026-09-16
---

# P38 - Search Console e conteudo de intencao

Nasce de [[ARQ - SEO reposicionado e sitemap de negocios 16092026]]. A parte
tecnica esta feita; falta a operacao e o conteudo.

## Logo depois do upload

- [ ] Reenviar `https://www.moviki.com.br/sitemap.xml` no Search Console, na
      propriedade do **www** (conferir que a propriedade monitorada e a do www,
      e nao a do apex).
- [ ] Conferir `X-Moviki-Negocios` em `/sitemap-negocios.xml`: e o primeiro
      numero real de quantas paginas de lojista passam no portao de qualidade.
      Se vier baixo demais, o gargalo nao e SEO — e cadastro pela metade.
- [ ] Teste de Resultados Aprimorados na home, `/premium.html` e numa pagina de
      negocio.
- [ ] Marcar a data: a curva de "Paginas indexadas" do Search Console a partir
      daqui e a unica medicao honesta desta entrega.

## Em duas semanas

- [ ] Ler quais consultas aparecem no Search Console. **Antes disso, qualquer
      escolha de palavra-chave e chute** — nao ha ferramenta de volume neste
      ambiente, e o Planejador do Google Ads exige campanha ativa para mostrar
      faixa fechada.
- [ ] Se as paginas de negocio comecarem a receber impressao local
      ("food truck em <cidade>", "<segmento> perto de mim"), o caminho e
      reforcar o conteudo DELAS — nao a home.

## Conteudo de intencao — a fila, quando houver autoridade

Termos de cauda longa onde o diferencial e nosso e a concorrencia e fraca:

1. receber Pix na live / vender ao vivo e receber na hora
2. cardapio digital com Pix sem taxa / cardapio que recebe Pix
3. vender ao vivo pelo celular sem loja
4. vender sem maquininha e sem comissao

**Nao disputar** *live commerce*, *como fazer live para vender* e *cardapio
digital* no genérico: a primeira pagina e de Nuvemshop, Stone, Cielo, Sebrae,
Cardapio Web, OlaClick e Saipos.

## Aberto de antes, que continua

- [ ] Arte de previa 1200x630 (hoje o `og:image` da home aponta para o
      `favicon512.png`; as paginas de negocio ja usam `ogmoviki.jpg`)
- [ ] Os QR dos crachas e os links dos parceiros ainda apontam para o apex —
      ver [[P30 - Decisao de dominio apex ou www]]. O codigo do site foi
      corrigido nesta rodada; os QR ja impressos, nao.
- [ ] Pontos do Enterprise (`ponto_slugs`) ficaram FORA do sitemap de negocios.
      Cada ponto tem pagina propria e slug proprio. Entram numa rodada propria,
      depois de conferir como o `og.js` monta o portao de qualidade deles.
