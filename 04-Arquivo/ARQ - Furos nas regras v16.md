---
type: incidente
status: ativo
area: A3 - Dados e Regras
tags: [regra-firestore, armadilha, conformidade]
atualizado: 2026-08-31
---

# ARQ — Furos encontrados na leitura das regras v16

Achados da revisao das regras publicadas em 31/08/2026. **Nenhum destes quebrou
nada ainda** — sao brechas abertas, nao incidentes. Ordenados por gravidade.

## 1. 🔴 Nota media falsificavel antes da primeira avaliacao

`/negocios/{uid}/resumo/avaliacoes` — o `create` e **anonimo** e aceita
qualquer par dentro dos limites:

```
allow create: if request.resource.data.keys().hasOnly(['n','soma'])
              && ... n >= 0 && n <= 100000
              && soma >= n && soma <= n * 5;
```

Quem chegar primeiro num negocio **que ainda nao tem resumo** cria o documento
com `n: 100000, soma: 500000` — e a pagina publica passa a exibir **5,0 com
100 mil avaliacoes**, sem uma avaliacao real existir. O `update` esta bem
travado (+1 por escrita); o furo e so na criacao, e **todo negocio sem avaliacao
esta com ele aberto agora.**

**Conserto sugerido:** o resumo nasce com a primeira avaliacao, nao antes.

```
allow create: if ( request.auth != null && request.auth.uid == uid )
              || ( request.resource.data.keys().hasOnly(['n','soma'])
                   && request.resource.data.n == 1
                   && request.resource.data.soma >= 1
                   && request.resource.data.soma <= 5 );
```

O dono continua reescrevendo o resumo inteiro quando quiser (ja previsto no
`update`).

**Por que isso importa para P13:** o filme decidiu nao exibir nota nem contador
por falta de base real auditavel. Este furo mostra que a decisao estava certa —
e que a base **nao e auditavel** enquanto o create anonimo existir.

## 2. 🟠 `comentario` da avaliacao entra sem tipo e sem tamanho

```
hasOnly(['nota','nome','comentario','criadoEm'])
```

`nota` e `nome` sao validados. **`comentario` nao tem nem `is string` nem
`.size()`.** Aceita mapa, lista, ou string ate o teto de 1 MiB do documento.
A unica defesa contra HTML na pagina publica e o `esc()` no cliente — regra de
ouro do projeto, mas defesa em camada unica.

**Conserto:** `(!('comentario' in d) || (d.comentario is string && d.comentario.size() <= 500))`.

## 3. 🟠 Avaliacao anonima sem qualquer limite de volume

`/negocios/{uid}/avaliacoes` — `create` sem `request.auth`. Um script grava
milhares de avaliacoes em qualquer negocio. Reputacao e inflavel **e**
atacavel, e cada escrita e custo.

**Conserto possivel sem quebrar o fluxo anonimo:** mover a criacao para um
endpoint no robo (que ja e o padrao do projeto para dinheiro e status), ou
exigir App Check com enforcement ligado.

## 4. 🟡 Squatting de apelido

`/slugs/{slug}` e `/parceiro_slugs/{slug}`: qualquer conta autenticada cria
quantos slugs quiser, um por escrita, sem teto. Uma conta pode reservar todos os
apelidos bons antes de existir demanda.

Agravante em `parceiro_slugs`: `update, delete` sao **so do admin**. Parceiro
que errar o slug depende de intervencao manual.

## 5. 🟡 `match /{documento=**}` publica toda subcolecao futura

Dentro de `/negocios/{uid}` o curinga da `allow read: if true` para **qualquer
subcolecao que venha a existir**. Foi exatamente por isso que `metricas` virou
colecao de topo. **Toda subcolecao nova nasce publica por acidente.**

Regra derivada: **subcolecao nova de negocio nasce publica — decidir antes de
criar, nao depois.**

## Regra de ouro que veio da v16

> **`hasOnly` em colecao que so o admin escreve e seguranca de mentira.**
> Nao barra ninguem que ja nao esteja barrado e quebra o painel a cada campo
> novo. Validar **tipo**, nunca conjunto fechado.
>
> E: **`allow write` cobre delete, e em delete `request.resource` e nulo** — a
> expressao erra e nega. Separar `create, update` de `delete` sempre.

## Ligacoes

[[A3 - Dados e Regras]] · [[R - Regras de ouro]] · [[R - Colecoes do Firestore]] ·
[[R - Historico de regras v7 a v15]] · [[ARQ - Incidentes e cacadas de bug]] ·
[[R - Filme institucional - conta demo]]
