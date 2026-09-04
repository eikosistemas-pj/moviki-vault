---
type: incidente
status: concluido
area: A1 — Produto e Painéis
tags: [moviki, videoaulas, armadilha, incidente]
atualizado: 2026-09-03
---

# ARQ — O visto verde que só valia na primeira aula

Encontrado pelo Paulo em 03/09, testando o painel do parceiro: **a partir da
segunda videoaula, o vídeo terminava e a aula não ficava verde.** Só a primeira
contava.

**Estava nos DOIS painéis** — o do parceiro e o do lojista. No lojista o efeito
era pior e ninguém tinha notado: as boas-vindas mostravam **"1 de 4"** para
sempre e **a faixa laranja piscando nunca sumia**, porque o lojista nunca
conseguia concluir as quatro.

## A causa

`iframe(v)` chama `vigiar(f, v)` e **só depois** quem chamou anexa o elemento na
página.

- **Primeira aula:** a API do YouTube ainda estava carregando, então o callback
  do `carregarYT` caía tarde — e o elemento já estava no documento. Funcionava
  **por acidente**.
- **Da segunda em diante:** a API já está pronta, o callback roda **na hora**, e
  `new YT.Player(f.id)` procura um id que ainda não existe na página. A API não
  cria player nenhum, `onStateChange` nunca dispara, o contador de 90% nunca
  roda, a aula nunca fica verde.

## Como foi provado

Com um **stub da API do YouTube** que registra se o elemento existia no
documento no instante em que o `YT.Player` foi construído — e que, como a API
real, **não liga nada quando o elemento não existe**.

| | Aula 1 | Aula 2 | Aula 3 | Aula 4 |
| --- | --- | --- | --- | --- |
| Antes | ✅ verde | ❌ | ❌ | ❌ |
| Depois | ✅ | ✅ | ✅ | ✅ |

Contador do parceiro: **"1 de 9" → "4 de 9"** nas quatro aulas tocadas.
Contador do lojista: **"1 de 4" → "4 de 4"**.

## O conserto

`vigiar()` passou a esperar o elemento aparecer no documento antes de montar o
player — teto de 3 segundos, falha calada. Tutorial não derruba painel.

## A regra de ouro que nasce daqui

> **Callback que às vezes é assíncrono e às vezes não é uma armadilha.** Quando
> o caminho lento esconde uma dependência de ordem, o caminho rápido a expõe — e
> o defeito aparece só a partir da segunda vez, que é justamente quando ninguém
> está mais olhando.

> **API que precisa de um elemento no documento tem que conferir se ele está
> lá.** Não confie na ordem em que quem chamou faz o `appendChild`.

## Efeito colateral bom

Quem ficou preso pelo bug **não perde nada**: o progresso vive em
`parceiros/{uid}.aulasVistas`, e as aulas que não contaram simplesmente ainda
não estão lá. Assistindo de novo, contam. Ninguém precisa de migração.

## Ligações

[[A1 - Produto e Paineis]] · [[P17 - Videos novos do parceiro]] · [[R - Regras de ouro]] · [[ARQ - Incidentes e cacadas de bug]]
