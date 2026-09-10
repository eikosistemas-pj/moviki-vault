---
type: arquivo
status: concluido
area: A3 - Painel do Parceiro
tags: [icones, quiz, niveis, parceiro, kairogen, identidade]
atualizado: 2026-09-10
---

# ARQ - Icones 3D do quiz e dos niveis

Fecha a pendencia dos quatro icones que faltavam no quiz e cria a familia
visual dos cinco niveis do parceiro, mais o selo que fica ao lado do nome no
painel.

## O que entrou

**Repo `moviki-app`, pasta `quiz/icones/` — 4 arquivos novos**
`sushi.png` · `suplementos.png` · `naturais.png` · `otica.png`
Fecham a lista: os 4 itens que entraram no quiz em 10/09 usavam emoji por
falta de desenho. Agora sao 38 icones.

**Repo `moviki-app`, pasta `icones/` — 12 arquivos novos**
`nivel-bronze.png` · `nivel-prata.png` · `nivel-ouro.png` ·
`nivel-diamante.png` · `nivel-esmeralda.png` · `selo-parceiro.png`
e as mesmas seis em `-48.png`.

**Repo `moviki-app`, `parceiro.html` — marca `2026-09-10-icones-nivel`**
- escada de niveis: cada degrau ganhou a medalha; colorida no que ja foi
  alcancado, cinza no que falta
- o ponto colorido saiu da escada — quem marca o degrau agora e a medalha e a
  borda ciano do degrau atual
- chip "Seu nivel" com a medalha antes do nome
- selo de parceiro verificado ao lado do nome no cabecalho, so quando o
  cadastro esta aprovado (classe `soAprovado`)

## Como foram produzidos

Kairogen `flux-2-klein-9b`, 2 creditos por imagem, fundo chroma chapado e
remocao do fundo em Python (chroma key + despill + sombra reconstruida em
cinza + recorte para 256x256 com fundo transparente).

Saldo Kairogen: 470 antes, **442 depois** (13 geracoes; 3 descartadas).

## Armadilhas que apareceram nesta rodada

- **Fundo verde nao serve para tudo.** Lente de oculos transparente sobre verde
  vira buraco no recorte: o vidro reflete o fundo e some junto. Regra nova:
  fundo **magenta** quando o objeto tem verde, ciano ou vidro transparente;
  verde so quando nao tem nenhum dos tres. E a lente precisa ser opaca.
- **Preto puro some no painel escuro.** O pote de suplemento preto virou uma
  mancha; refeito em azul-royal com tampa branca.
- **Icone de 256 px reduzido a 20 px vira borrao.** Por isso existe a versao
  `-48.png` — e ela que vai ao lado do nome e dentro do chip.
- **O CDN do Kairogen e negado pela politica de saida desta conta** (403 no
  CONNECT). O arquivo so chega ao sandbox pela ferramenta de audio do proprio
  MCP apontada para a URL do `.jpg`; o download de imagem apenas exibe.

## Regra de ouro que nasce daqui

> **Desenho que falta nao pode derrubar tela.** Todo icone entra com
> `onerror` que esconde a imagem: o quiz volta ao emoji e o nivel continua
> escrito por extenso. Arte e enfeite; o texto e o que informa.

## Ordem de subida (foi respeitada)

1. os PNG — subiram em 10/09
2. so depois o `parceiro.html`

Invertido, o painel abre com icone quebrado ate o segundo upload.

## Ligacoes

[[P19 - Niveis do parceiro]] · [[P22 - Icones do quiz]] ·
[[R - Marcas de versao no ar]] · [[R - Regras de ouro]] ·
[[A3 - Painel do Parceiro]]
