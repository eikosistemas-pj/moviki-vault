---
type: arquivo
status: concluido
area: A14 - Material de apoio do parceiro
tags: [material-de-apoio, parceiro, categoria, icone-3d, kairogen, conformidade]
atualizado: 2026-09-16
---

# ARQ - Categoria Fotografia e eventos 16092026

Lote de quatro artes de fotografia entregue pelo Paulo em 16/09/2026. Tres
aprovadas, uma recusada, categoria nova aberta e um achado que vale mais que o
lote: **os icones 3D das categorias nao estao aparecendo no ar.**

Entrega: `moviki-material-fotografia-16092026.zip` — versao
`2026-09-16-fotografia`, 84 pecas, 13 categorias.

## O lote

| Arte | Formato | Destino |
| --- | --- | --- |
| Rafael Mendes, 1254x1254 | Feed 1:1 | `feed-fotografia-talento` |
| Rafael Mendes, 941x1672 | Story 9:16 | `story-fotografia-talento` |
| Luz & Afeto, 941x1672 | Story 9:16 | `story-fotografia-talento-2` |
| Luz & Afeto, 1254x1254 | Feed 1:1 | **RECUSADA** |

As duas de story vieram em 941x1672 — proporcao 16:9 exata, mas abaixo do
minimo. Ampliadas em dois passos Lanczos com mascara de nitidez entre eles.
A de feed veio acima do alvo e so foi reduzida.

### A recusa

A versao 1:1 da Luz & Afeto tem **dois defeitos de texto na propria arte**:

1. `CONTRATAÇCÕES` no quarto item da lista — cedilha dobrada.
2. `30 DIAS DE PRO`, **sem acento**, no selo do rodape.

O segundo e violacao direta da regra de ouro: e sempre `30 DIAS DE PRÓ`, com
acento, nunca "trial". A gemea de story da mesma dupla esta correta nos dois
pontos, o que mostra que o gerador errou so nessa passada. Pedir de novo.

> **Regra de ouro:** o selo do rodape se confere **letra por letra, com zoom**,
> em toda arte do lote. `PRO` e `PRÓ` sao indistinguiveis a olho no tamanho em
> que a arte chega no chat.

## A categoria nova: `eventos` — "Fotografia e eventos"

Fotografo nao cabe em `servicos`. "Servicos e reparos" le como conserto: o
parceiro que procura material para prospectar fotografo, DJ ou buffet nao
abriria aquela aba. **E o mesmo erro da autopeca**, que nasceu `automotivo`
justamente por isso.

Aberta como `eventos` e nao como `fotografia` de proposito: cobre videomaker,
DJ, buffet, decoracao e festa infantil sem precisar de outra categoria depois.
Vertical inteira de profissional itinerante — o publico central do produto.

Posicionada **antes de `servicos`**, com `geral` continuando em primeiro.

## O icone 3D

Gerado no Kairogen, `seedream-v4` 2048x2048, **2 creditos**. Saldo depois: 198.

Camera 3D, azul-royal com faixa ciano, lente **opaca** (vidro transparente vira
buraco no recorte), botao dourado, flutuando sem chao.

**O chroma saiu imperfeito e isso rendeu conserto novo.** O fundo veio como um
degrade roxo com vinheta, nao magenta chapado, e a IA desenhou uma **sombra
projetada** apesar do `no cast shadow` no prompt. A sombra era roxa e saturada,
entao o filtro de luminancia baixa e saturacao baixa da rotina **nao pegou** —
ela sobreviveu ao recorte e aparecia como um risco escuro embaixo do icone,
gritante em fundo claro.

Conserto que entrou na rotina: depois do chroma, **rotular os componentes
conexos e manter so o maior**. Sombra projetada e sempre um blob separado do
objeto. Pegou de primeira, e e independente da cor da sombra.

> **Regra de ouro:** sombra que o chroma nao pega se tira por **componente
> conexo**, nao por cor. O filtro de luminancia so resolve sombra cinza; sombra
> colorida passa batido e so aparece em fundo claro, depois de publicada.

Despill de magenta feito por `min(R,B) - G`, que preserva azul-royal (R baixo)
e ciano (G alto) por construcao — despill ingenuo destruiria os dois, que sao
justamente a paleta da marca.

## O achado: o campo `ico` sumiu do catalogo no ar

O `parceiro.html` le **`c.ico`** na funcao `barras()` e monta
`icones/<c.ico>` com `onerror` caindo no emoji.

**Nenhuma das 12 categorias do catalogo no ar tem o campo `ico`.**

A entrega `2026-09-16-caticones`, da mesma manha, subiu os 12
`icones/cat-<id>.png` e um catalogo com `ico` preenchido. O catalogo que esta
no ar hoje carrega **a mesma string de versao** e nao tem o campo. Outro lado
entregou um catalogo montado sobre base anterior e sobrescreveu o campo,
mantendo a marca.

**O sintoma foi silencio, como sempre:** a aba abre normal, as 12 categorias
aparecem, ninguem ve erro. O `onerror` fez o trabalho dele e mostrou o emoji —
exatamente o comportamento que a faixa tinha antes dos icones existirem. A
entrega de 16/09 foi desfeita sem deixar rastro.

`catalogo.json` deste pacote **devolve `ico` as 12** e acrescenta a 13a.

> **Regra de ouro:** marca de versao igual nao prova conteudo igual. Campo que
> uma entrega acrescenta se confere **no campo**, na proxima rodada, nao na
> marca.

> **Regra de ouro:** rede de seguranca que degrada bem **esconde a regressao**.
> O `onerror` salvou a tela e apagou o sintoma. Todo recurso com fallback
> silencioso precisa de uma conferencia explicita do campo que o alimenta.

## Conferencia programatica

Zero id repetido · zero categoria invalida · zero legenda vazia · todas
comecando com `#publi` e terminando em `{link}` · zero URL escrita · zero
"trial" · zero `PRO` sem acento · zero promessa quantificada · dimensoes e peso
batendo em 100% · zero arquivo orfao · `geral` em primeiro.

### O defeito que a conferencia pegou em mim

Na primeira montagem as capas foram nomeadas pelo nome do arquivo de origem, e
a arte de feed e a de story do mesmo par **caiam na mesma capa** —
`fotografia-mostre-talento-01.webp`. A segunda gravacao sobrescreveu a
primeira, e o card de feed ficaria com capa de story, esticada. A varredura de
arquivo orfao **nao pega isso**, porque o arquivo existe e esta referenciado.

Refeito com a convencao de id do repositorio: `<id>.jpg` e `<id>.webp`. Como o
id ja e unico, a colisao deixa de ser possivel.

> **Regra de ouro:** nome de capa sai do **id do item**, nunca do nome do
> arquivo de origem. Peca do mesmo par colide, a gravacao vence em silencio e a
> varredura de orfao nao acusa.

## Estado das categorias

`geral` 24 · `naturais` 10 · `moda` 9 · `automotivo` 8 · `alimentacao` 7 ·
`servicos` 5 · `pet` 4 · `eletronicos` 4 · `papelaria` 4 · `beleza` 3 ·
`artesanato` 3 · **`eventos` 3** · `feira` **0**

`feira` segue com zero peca e por isso nao aparece na faixa. **E o caso de uso
central do produto e continua a unica categoria sem material** — pendencia
aberta desde 16/09 de manha.

`beleza`, `artesanato` e `eventos` estao nos 3, no limite de baixo.

## Pendencias que ficam

- Pedir de novo a arte 1:1 da Luz & Afeto, sem `CONTRATAÇCÕES` e com `PRÓ`.
- Conferir no GitHub se os 12 `icones/cat-<id>.png` continuam la. Se algum
  sumiu junto com o campo, a faixa cai no emoji so naquele botao.
- `feira` continua com zero peca.

## Ligacoes

[[A14 - Material de apoio do parceiro]] ·
[[ARQ - Icones 3D das categorias e da live 16092026]] ·
[[ARQ - Conferencia do material de apoio 16092026]] ·
[[R - Regras de ouro]] · [[R - Marcas de versao no ar]]
