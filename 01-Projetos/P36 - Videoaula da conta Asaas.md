---
type: projeto
status: em-andamento
area: A13 - Modo Live
tags: [aula, asaas, financeiro, estudio]
prioridade: media
prazo: 2026-09-23
atualizado: 2026-09-16
---

# P36 - Videoaula da conta Asaas

Aberto em 16/09 pela pergunta do Paulo: a parte do Asaas ficou "em aberto"
para o lojista enquanto a homologacao das subcontas nao sai.

A tela ja foi consertada em [[ARQ - Conta Asaas na tela do lojista 16092026]].
Falta o video.

## Decisao que orienta o projeto

**O passo a passo de abrir conta vive na TELA, nao no video.** O Asaas muda o
layout dele quando quiser; texto na tela se corrige em dois minutos, video
exige regravar, subir, trocar o id, atualizar a tabela e so entao apagar o
antigo. O video fica com o que nao desatualiza: a decisao entre os dois modos
e o cuidado com a chave.

## Estado

| Item | Estado |
| --- | --- |
| Tela com passo a passo, alerta e desconectar | **no ar** (aguardando upload) |
| Roteiro da aula | **pronto** — [[R - Aula - Conta Asaas do lojista]] |
| Narracao (voz Malu) | falta gravar |
| Cena `T27-conta-asaas` | falta montar |
| Id do YouTube | falta |
| Entrada no `MOVIKI_TUTORIAIS` do `index.html` | falta |

## Travas antes de gravar

1. **Conferir `claude/moviki-videoaulas-no-ar.md`.** A aula `mod-financeiro`
   saiu de outra frente em 16/09 e esta sem id. Fixar `T27-conta-asaas` e
   `mod-asaas` so depois de ver que nenhum dos dois colidiu.
2. **Gravar com a tela nova ja no ar.** O mockup do video mostra o cartao
   verde e o aviso de conta pendente — filmar antes do upload produz aula que
   nao bate com o painel, que foi o defeito da 07 antiga.
3. **Escrever `Ásaas` no texto do motor de voz.** Sem acento a Malu le
   *asáas*.

## Depois do video

- Trocar o id, a duracao e a chave no `MOVIKI_TUTORIAIS`, embutido no bloco do
  Asaas (`sel` apontando para `#finBlocoAsaas`).
- Atualizar `claude/moviki-videoaulas-no-ar.md` na MESMA entrega.
- So entao apagar qualquer versao antiga no YouTube.

## Ligacoes

[[ARQ - Conta Asaas na tela do lojista 16092026]] ·
[[R - Aula - Conta Asaas do lojista]] · [[P31 - Financeiro e cardapio compravel]]
