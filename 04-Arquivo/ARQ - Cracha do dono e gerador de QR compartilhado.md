---
type: arquivo
status: concluido
area: A5 - Programa de Parceiros
tags: [cracha, qr-code, painel-dono, prospeccao]
atualizado: 2026-09-10
---

# ARQ - Cracha do dono e gerador de QR compartilhado

No ar em 04/09/2026: `moviki-app/eikoadm01.html` (`2026-09-04-cracha-busca`) e
`moviki-app/mvqr.js` (`2026-09-04-mvqr1`, arquivo NOVO).

## Por que existe

O Paulo vai a campo cadastrar lojista pessoalmente em Joao Pessoa. O painel do
dono ganhou **cracha com QR** e atalho na Visao geral.

## A regra de funil declarada por ele

> **O QR nunca leva direto ao formulario.** Leva a `/v/{apelido}`, onde a pessoa
> le quem esta na frente dela e escolhe entre dois botoes — conhecer o Moviki ou
> se cadastrar com a indicacao. Vale para o cracha do parceiro e para o do dono.

Mais adiante ele quer video dentro dessas paginas.

## O que o cracha exige

Cadastro de parceiro **aprovado** — quem a `/v/` le e o espelho
`parceiros_publicos`. Por isso o cracha do dono nao montava: **o Paulo nao tinha
cadastro de parceiro**. Ele criou o dele pela conta `eikosistemas@gmail.com`,
apelido **`paulopj`**, e o cracha passou a funcionar.

## A busca, e por que o campo as cegas nao servia

Digitar o apelido no escuro nao resolvia: o espelho `parceiros_publicos` **nao
guarda e-mail**. Virou busca na colecao `parceiros` por **nome, e-mail, apelido e
@**, mostrando o status de cada um.

## O gerador de QR virou arquivo proprio

`mvqr.js` foi extraido do `parceiro.html` e conferido **saida a saida em 403
apelidos**. Motivo: aquele codigo **ja teve um bug** — os 15 modulos do format
info escritos transpostos, e nenhum leitor abria. Ter isso em dois arquivos de
tres mil linhas seria ter dois lugares para consertar o mesmo defeito.

**O `parceiro.html` ficou com a copia interna de proposito** — nao se mexe no que
acabou de ser validado. **Divida registrada:** trocar pela `mvqr.js` quando for
mexer nele por outro motivo.

## Ligacoes

[[A5 - Programa de Parceiros]] · [[A11 - Marca e Design System]] ·
[[P14 - Verificacao de parceiro]] · [[R - Regras de ouro]]
