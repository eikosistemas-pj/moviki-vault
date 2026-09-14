---
type: incidente
status: ativo
area: A2 - Infraestrutura e Deploy
tags: [vault, armadilha, numeracao]
atualizado: 2026-09-14
---

# ARQ - Faxina de notas órfãs do vault

Achado em 14/09/2026, lendo o vault publicado pela Base de Conhecimento do
Project. **Três notas antigas continuam no repositório com nomes que foram
aposentados na renumeração de 10/09.** O `SincronizarVaultMoviki.bat` commita e
faz push — ele **não apaga** o arquivo antigo quando a nota é renomeada.

## As três órfãs

| Arquivo no repositório | Substituída por | Ação |
| --- | --- | --- |
| `01-Projetos/P14 - App Check enforcement.md` (04/09) | [[ARQ - App Check enforcement ligado]] | **apagar** |
| `01-Projetos/P14 - Descobrir o CPA real do lojista.md` (04/09) | [[P17 - Descobrir o CPA real do lojista]] | **apagar** |
| `01-Projetos/P15 - Aula de conduta do divulgador.md` (05/09) | [[P18 - Aula de conduta do divulgador]] | **apagar** |

## Por que não é cosmético

1. **A colisão de numeração continua viva no disco.** Existem hoje três arquivos
   começando por `P14` e dois por `P15`. O `_Indice de Projetos` não os lista —
   quem lê o índice acha que está resolvido, e quem abre a pasta vê o contrário.
2. **Elas afirmam um estado falso.** A `P14 - App Check enforcement` está com
   `status: ativo` e descreve o enforcement como pendente. Ele foi ligado em
   05/09. Qualquer retomada que caia nesse arquivo começa errada.
3. **Os wikilinks delas apontam para nomes mortos** — `A7 — Midia paga` com
   travessão, `P15 - Aula de conduta do divulgador` — e poluem o grafo com
   links não resolvidos.

## Como apagar

O `.bat` não resolve: ele só sabe adicionar. Apagar pela interface web do GitHub,
em `eikosistemas-pj/moviki-vault/01-Projetos/`, um arquivo por vez — ou apagar no
Obsidian e deixar o plugin Git sincronizar a remoção.

## A regra que fica

> **Renomear nota é uma operação de duas pontas: criar a nova e apagar a velha.**
> A ferramenta de sync só faz a primeira. Renumeração sem faxina deixa duas
> versões da mesma verdade no cofre, e a errada é sempre a que alguém abre.

## O registro que estava errado

Três documentos de retomada (10/09, 13/09) afirmam que "a fila de notas do vault
de 04–06/09 segue sem subir". **Está errado:** aquelas 13 notas subiram no pacote
`vault-moviki-10092026.zip` e estão no repositório com `atualizado: 2026-09-10`.
O texto foi copiado de uma retomada para a seguinte sem reconferência. O que
sobrou pendente era só esta faxina.

> **Pendência herdada por cópia não é pendência conferida.** Antes de repetir um
> item de "ainda em aberto" numa retomada nova, abrir a fonte.

## Ligações

[[A2 - Infraestrutura e Deploy]] · [[R - Protocolo Claude e vault]] ·
[[R - Sync do vault Obsidian Git]] · [[_Indice de Projetos]] ·
[[R - Retomada live parte 02]]
