---
type: incidente
status: concluido
area: A3 - Conteudo e Videoaulas
tags: [videoaulas, trava, parceiro, lojista, medidor, localstorage]
atualizado: 2026-09-16
---

# ARQ - Trilha da aula e medidor visivel 16092026

Relato do Paulo em 16/09, com print: *"mesmo assistindo, a aula não fica verde"*
— na aula nova do parceiro, com o painel mostrando 12 de 13.

## A investigação, em ordem

1. Reproduzido em Chromium com dublê da API do YouTube, contra o
   `parceiro.html` que está no ar: assistindo do começo ao fim **a aula fecha,
   fica verde, salva e o contador vai a 13 de 13**. O motor estava correto.
2. Confirmado com ele que o medidor rodava (a porcentagem subia). Isso descartou
   bloqueio da API do YouTube e vídeo com incorporação desativada.
3. Sobrou a única diferença entre o teste e a vida real: **o teste assiste de
   uma vez só.**

## A causa

O percurso assistido vivia **só em memória**. Fechar o painel, recarregar a
página ou voltar no dia seguinte começava do zero. Quem assiste uma aula de
2:23 em dois pedaços nunca junta os 90% — e a aula nunca fica verde, por mais
vezes que a pessoa assista.

Não era defeito do vídeo nem do catálogo: era o desenho da medição.

## O conserto

1. **O percurso passou a sobreviver ao recarregamento.** Fica no próprio
   navegador (`localStorage`), por conta e por aula, gravado de 2 em 2 segundos,
   ao sair da tela e no `pagehide` (fechar a aba ou recarregar — o único evento
   que também funciona no iPhone). Aula concluída apaga o rascunho.
   **Não vai para o banco:** medição é local; o que o banco guarda continua
   sendo a aula CONCLUÍDA.
   Falha calado: aba anônima ou armazenamento bloqueado volta ao comportamento
   antigo, sem quebrar nada.
2. **O medidor ficou visível.** No lugar da linha miúda embaixo do vídeo, uma
   faixa com barra de progresso, a porcentagem em corpo grande e a meta escrita:
   *"a aula fica verde quando chegar em 90%"*. Três estados: assistindo (ciano),
   concluída (verde, "Pode passar para a próxima") e adiantou o vídeo (laranja,
   "Não contou — assista do ponto onde parou").
3. **A lista mostra onde parou:** cada aula não concluída exibe
   "Assistido 36% · 2:23" em vez de "Aula 3 · 2:23".

Os três valem para o **parceiro e para o lojista** — os dois carregam o mesmo
motor, copiado.

## A regra que fica

> **Trava que mede tem que guardar o que mediu.** Medição em memória transforma
> "assisti em dois dias" em "nunca assisti" — e o usuário só enxerga que o
> sistema não reconhece o esforço dele.

E a segunda, que o Paulo apontou:

> **Trava só é justa se a pessoa vê o quanto falta, com destaque.** Medidor
> discreto é indistinguível de defeito.

## Arquivos

| Repo | Arquivo | Ação | Marca nova | Montado sobre |
| --- | --- | --- | --- | --- |
| moviki-app | `parceiro.html` | SUBSTITUI | `2026-09-16-trilha` | `2026-09-16-liveparc2` |
| moviki-app | `index.html` | SUBSTITUI | `2026-09-16-trilha` | `2026-09-16-aulafinanceiro` |
| moviki-ai | `lib/catalogoPainel.js` | SUBSTITUI | `2026-09-16-5` | `2026-09-16-4` |

## Prova

Duas sessões separadas em Chromium, com o navegador fechando entre elas:
a primeira assiste metade e sai (rascunho guardado, medidor em 50%); a segunda
abre mostrando o progresso na lista, continua de onde parou, **fecha a aula,
pinta verde, salva e limpa o rascunho**. Contagens de não-regressão idênticas ao
que está no ar nos dois arquivos; BOM e CRLF preservados no `index.html`;
`node --check` limpo nos 9 blocos de script de cada um.

Um defeito encontrado durante a própria correção: a variável do topo da faixa
nasceu sem `var` e, em modo estrito, derrubava a montagem da tela de aulas em
silêncio — o `try/catch` de `abrirTutoriais` engolia o erro. **Bloco novo em
arquivo com `use strict` se testa abrindo a tela, não só com `node --check`.**

## Ligações

[[ARQ - Entrega aula de live do parceiro 16092026]] ·
[[R - Live - Videoaulas do modulo]] · [[R - Regras de ouro]]
