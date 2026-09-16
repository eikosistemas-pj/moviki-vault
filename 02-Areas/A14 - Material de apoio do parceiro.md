---
type: area
status: ativo
area: A14 - Material de apoio do parceiro
tags: [parceiro, material-de-apoio, conteudo, panfleto, qr, conar, categoria]
atualizado: 2026-09-16
---

# A14 — Material de apoio do parceiro

Responsabilidade contínua: manter a aba **Material de apoio** do painel do
parceiro abastecida com artes, panfletos, vídeos e textos prontos para divulgar.

> **Numeração:** esta área nasceu como "A13" no documento de 11/09/2026. Houve
> colisão: a **A13** ficou com o **Modo Live** e o material de apoio passou a ser
> a **A14**. Qualquer referência a "A13 — Material de apoio" está errada.

## Situação em 16/09/2026

**81 peças, 12 categorias, navegação em dois níveis no ar.** O acervo saiu de 17
para 81 em quatro dias. `catalogo.json` na versão `2026-09-16-qr`.

## Como funciona

| Peça | Onde vive |
| --- | --- |
| Aba Material de apoio | `moviki-app/parceiro.html` — destaque na Visão geral, item no menu lateral e no menu Mais |
| Catálogo | `moviki-app/material/catalogo.json`, estático. **Nada no Firestore** |
| Arquivos | `material/` com `capas/`, `feed/`, `panfletos/`, `stories/`. Vídeo fica solto em `material/`, com a capa junto |
| Ícones das categorias | `moviki-app/icones/cat-<id>.png`, PNG 3D 256×256 (16/09) |

### Navegação em dois níveis

**Nível 1 — categoria de comércio.** Faixa no topo, lida do campo `categorias`
do catálogo. Só aparece categoria que tem peça. Cada botão mostra um ícone 3D,
com o emoji escondido atrás como reserva.

**Nível 2 — tipo de mídia.** Panfletos, Feed, Stories, Vídeos, Textos. Só
mostra o que existe dentro da categoria escolhida.

Estado inicial: **Para qualquer negócio**.

### As 12 categorias

`geral` · `alimentacao` · `moda` · `beleza` · `naturais` · `pet` ·
`artesanato` · `eletronicos` · `papelaria` · `automotivo` · `servicos` ·
`feira`

**`feira` tem zero peça e por isso não aparece** — ver
[[P37 - Acervo de feira rua e delivery e correcoes do material]].

### Outras regras da aba

- Panfleto com QR: **uma arte só**; o QR do parceiro
  (`/v/apelido?utm_source=panfleto&utm_medium=qr`) é desenhado por cima no
  navegador dele. As coordenadas vivem no próprio item do catálogo.
- Botões **Instagram, Facebook e WhatsApp** em cada material. **O share do
  WhatsApp leva só o arquivo** — arquivo mais texto faz o WhatsApp descartar a
  imagem sem avisar. Ver
  [[ARQ - Previa de link e compartilhamento no WhatsApp 16092026]].
- Baixar e postar obedecem às portas do link: aprovado, aulas concluídas,
  compromisso aceito. **Todo mundo VÊ.**
- Não criar subpasta nova pelo GitHub web.

## Fluxo para material novo

1. O Paulo manda a arte ou o vídeo no chat.
2. O Claude confere a conformidade (`#publi`, sem promessa de ganho, sem
   "trial"), otimiza o arquivo (JPG 88 / MP4 até 20 MB), gera a capa WebP de
   320 px e escreve a legenda.
3. Entrega um zip para a pasta que **já existe** no GitHub + `catalogo.json`
   (SUBSTITUI) com o `versao` trocado — é isso que acende o **NOVO**.
4. O `parceiro.html` não muda.

**Vídeo acima de 25 MB não passa pelo chat nem pelo GitHub web.** O caminho é o
anexo de Release — ver [[ARQ - Video do influencer pelo Release do GitHub]].

## Regras

- Toda legenda começa com `#publi` (Guia CONAR 2026).
- Descrever o que a ferramenta faz; nunca prometer ganho, venda, "garantido",
  "sem risco".
- "Teste grátis" ou "plano Básico", nunca "trial".
- Mockup de celular precisa dizer "Atualizado agora", nunca "há 7 dias".
- **Número em mockup é promessa.** Contador inventado sai.
- O `parceiro.html` é disputado por várias conversas: entrega que encoste nele
  se monta sobre a marca que está no GitHub **naquele momento**.

## Pendências

Consolidadas em
[[P37 - Acervo de feira rua e delivery e correcoes do material]]:
peças de Feira/rua/delivery, cinco artes com erro de ortografia, "Atualizado há
7 dias" no panfleto A5 antigo e no vídeo 1, varredura de números inventados.

## Ligações

[[A5 - Programa de Parceiros]] · [[A8 - Conteudo e Social]] ·
[[A10 - Conformidade e LGPD]] · [[A13 - Modo Live]] ·
[[P37 - Acervo de feira rua e delivery e correcoes do material]] ·
[[ARQ - Aba Material de apoio do parceiro]] ·
[[ARQ - Botoes de postar no material de apoio]] ·
[[ARQ - Conferencia do material de apoio 16092026]] ·
[[ARQ - Icones 3D das categorias e da live 16092026]] ·
[[ARQ - Incidente - aba de material apagada pela aula P11]] ·
[[ARQ - Video do influencer pelo Release do GitHub]] ·
[[R - Marcas de versao no ar]]
