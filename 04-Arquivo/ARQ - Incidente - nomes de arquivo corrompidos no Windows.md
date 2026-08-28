---
type: incidente
status: concluido
data: 2026-08-28
area: A2 - Infraestrutura e Deploy
tags: [armadilha]
atualizado: 2026-08-28
---

# ARQ - Incidente: nomes de arquivo corrompidos no Windows

## Sintoma
No GitHub, `000 Moviki — Home (MOC).md` apareceu como **`000 Moviki ÔÇô Home (MOC).md`**. **59 dos 71 arquivos** do vault subiram com o nome quebrado.

## Causa real
O travessão `—` é `0xE2 0x80 0x94` em UTF-8. **O Explorer do Windows não lê UTF-8 nos nomes de arquivo dentro de um `.zip`** — interpreta os bytes como **cp850**, e cada travessão vira três caracteres de lixo.

Não é problema do GitHub nem do zip: a corrupção acontece **na descompactação**, e o que foi para o repositório já estava errado.

## Por que era grave, e não cosmético
Todo wikilink do vault aponta pelo **nome do arquivo** — um wikilink para "R — Regras de ouro" procura um arquivo com exatamente esse nome. Com o nome corrompido no disco, **o Obsidian não resolve nenhum link** — o cofre abre como 71 notas soltas, sem grafo. O vault perderia exatamente o que o justifica.

## Conserto
Travessão eliminado dos **nomes** (` — ` → ` - `), em 59 arquivos, com os wikilinks reescritos junto. **O conteúdo manteve os travessões** — dentro do arquivo é UTF-8 normal e nada quebra.

Repositório apagado e recriado, porque renomear 59 arquivos pela interface web é pior que refazer.

## A regra
**Nome de arquivo só com ASCII.**

É a mesma família da regra que já existia — *"nome de arquivo entregue no chat não pode depender de hífen, mas o nome vira o endereço na Vercel"*. O nome do arquivo atravessa sistemas que não combinaram codificação entre si: navegador, Explorer, zip, git, Vercel. **O conteúdo é UTF-8 em todo lugar; o nome, não.**

## Também aconteceu na mesma subida
O próprio `movikivaultrepo.zip` foi commitado dentro do repositório. Pacote de entrega não é conteúdo do repositório.

→ [[ARQ - Incidentes e cacadas de bug]] · [[R - Regras de ouro]]
