---
type: incidente
status: concluido
area: A13 - Modo Live
tags: [git, arquivo, armadilha, regra-de-ouro, livesessao]
atualizado: 2026-09-15
---

# Tres bytes invisiveis que deixaram um arquivo binario — 15/09/2026

Achado na conferencia de subida pedida pelo Paulo, depois do B5a.
Entrega: `moviki-livesessao-b5b-15092026.zip` — um arquivo.

---

## 1. O sintoma

Conferindo se os uploads bateram, o `grep` respondeu:

```
grep: robo/lib/livesessao.js: binary file matches
```

Os outros 71 arquivos dos tres repositorios estavam limpos. So esse.

## 2. A causa

Dentro da funcao que higieniza texto do lojista existe:

```
.replace(/[\x00-\x1f\x7f<>]/g, ' ')
```

No arquivo, `\x00`, `\x1f` e `\x7f` estavam gravados como os **bytes de verdade**
(posicoes 6190, 6192 e 6193), e nao como o texto que os representa. Veio da
geracao do arquivo, nao do upload do Paulo — o arquivo que saiu daqui ja tinha.

## 3. Por que isso importa, mesmo funcionando

O JavaScript aceita caractere de controle literal dentro de classe de regex.
**Nada quebrou, e nada ia quebrar sozinho.** O estrago e em outro lugar:

1. **O Git marca o arquivo como binario.** No GitHub ele nao mostra diff nenhum:
   toda alteracao futura vira "arquivo binario alterado". O Paulo trabalha **so
   pela interface web do GitHub** — o diff e a unica conferencia visual que ele
   tem, e ela tinha sido desligada sem ninguem notar.
2. **Qualquer editor que limpe caracteres invisiveis apaga os tres.** A regra que
   tira caractere estranho do texto do lojista para de funcionar — **calada**,
   sem erro, num arquivo que continua "parecendo certo".

## 4. A REGRA DE OURO

> **Arquivo de codigo so pode conter texto imprimivel.** Um byte de controle
> gravado no lugar do seu escape roda igual, some do diff do Git e morre no
> primeiro editor que passar. Antes de entregar qualquer arquivo, varrer os
> bytes abaixo de 0x09, entre 0x0e e 0x1f, e 0x7f.

Vale para os cinco repositorios, nao so para este arquivo.

## 5. O conserto

Os tres bytes viraram o texto `\x00`, `\x1f` e `\x7f`. Comportamento provado
identico. **Nada mais mudou** — diff conferido linha por linha contra o que
estava no ar.

| Arquivo | Acao | Marca |
| --- | --- | --- |
| `moviki-robo/lib/livesessao.js` | SUBSTITUI | `2026-09-15-b5b` |

Sem env, sem regra. **Ja esta no ar e conferido:** 20.609 bytes, zero bytes de
controle.

## Ligacoes

[[ARQ - Ajuste do freio da live - B5a]] · [[ARQ - Freio do api live - B5]] ·
[[R - Regras de ouro]] · [[A13 - Modo Live]]
