---
type: arquivo
status: concluido
area: A14 - Material de apoio do parceiro
tags: [material-de-apoio, parceiro, qr, panfleto, conferencia, cache]
atualizado: 2026-09-16
---

# ARQ - Conferencia do material de apoio 16092026

Conferencia dos quatro pacotes entregues por outra conversa (o acervo que levou
o material de 17 para **81 pecas**), feita contra o GitHub e testada em
Chromium em 16/09/2026.

## O pacote passou

- 126 arquivos novos (63 capas, 31 stories, 29 feed, 1 panfleto, 2 videos) mais
  o `catalogo.json`. **Zero `.html`, zero `.js`** — o pacote nao toca em codigo.
- Catalogo: JSON valido, **81 itens**, 12 categorias, zero id repetido, zero
  categoria invalida, zero legenda vazia, **todas comecando com `#publi`**.
- Zero referencia quebrada, zero arquivo orfao, dimensoes e peso batendo em
  100% dos itens.
- Conformidade: zero promessa quantificada, zero URL escrita na legenda, zero
  "trial", zero "PRO" sem acento.

## O achado que mudou o plano: a pendencia P-2 nao existia

O handoff dizia que o `parceiro.html` ainda precisava ganhar a navegacao por
categoria. **Ela ja estava no ar desde 15/09**, dentro da marca
`2026-09-15-aulatrava`: `barras()`, `CATEG`, `matCats`, `data-matcat`, a
leitura de `j.categorias` e a rede de seguranca que joga categoria desconhecida
na primeira da lista.

Provado em Chromium, servindo o `parceiro.html` do ar contra o catalogo novo:
**11 categorias na faixa, soma exata de 81 cards, zero erro de JavaScript.**
"Feira, rua e delivery", com zero peca, se esconde sozinha.

**Consequencia:** o material subiu sem tocar em uma linha de HTML, e o risco de
colisao no `parceiro.html` — a maior preocupacao dos dois lados — deixou de
existir.

> **Regra de ouro:** pendencia herdada de outra sessao se confere **no codigo**,
> nunca no texto da lista. Item escrito antes de uma entrega continua escrito
> depois dela.

## A faixa de categorias escondia categoria

Com 11 categorias a faixa rolava na horizontal com a barra de rolagem escondida
(`scrollbar-width:none`): a ultima aparecia cortada na borda e **nao havia
pista nenhuma** de que existia mais coisa para o lado. Quem procurava a propria
categoria concluia que ela nao existia.

**Conserto:** no desktop a faixa quebra em duas linhas (`flex-wrap:wrap`). No
celular duas linhas virariam sete — um terco da tela —, entao ali ela continua
rolando, **com um esmaecido na borda direita** dizendo que tem mais. O
esmaecido so aparece quando ha mesmo o que rolar: a classe `temMais` e posta
medindo, depois de pintar.

> **Regra de ouro:** faixa que rola sem dizer que rola esconde conteudo.

## O QR do panfleto: o defeito era cache, nao coordenada

O QR saia cortado no panfleto A5. As coordenadas foram remedidas **pixel a
pixel na arte real** — o quadrado branco vai de x 1289 a 1624 (centro 1456) e a
faixa do texto de 1235 a 1678 — e corrigidas para `qr {x:1312, y:1841, l:288}`
e `texto {x:1456, y:2162, w:420}`.

Depois da correcao o Paulo disse que **continuava torto**. Em vez de mexer nas
coordenadas de novo, o compositor real foi rodado no navegador com o catalogo
que estava no ar e o QR gerado foi **lido com OpenCV**: devolveu
`https://moviki.com.br/v/luciano?utm_source=panfleto&utm_medium=qr`,
perfeitamente posicionado. Era **cache do navegador**. `Ctrl+Shift+R` resolveu.

> **Regra de ouro:** antes de corrigir a segunda vez, **gerar o artefato com o
> codigo que esta no ar e medir**. Duas correcoes seguidas no mesmo numero
> quase sempre significam que a primeira nunca chegou a ser vista.

O mesmo aconteceu com "a pagina esta do jeito antigo": o repositorio estava
certo, era cache.

## Ligacoes

[[A14 - Material de apoio do parceiro]] · [[A5 - Programa de Parceiros]] ·
[[P33 - Material de apoio organizado por categoria]] ·
[[R - Regras de ouro]] · [[R - Marcas de versao no ar]] ·
[[ARQ - Icones 3D das categorias e da live 16092026]] ·
[[ARQ - Aba Material de apoio do parceiro]]
