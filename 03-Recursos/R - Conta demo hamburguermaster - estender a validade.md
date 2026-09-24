---
type: recurso
status: ativo
area: A3 - Dados e Regras
tags: [firebase, firestore, conta-demo, assinatura, hamburguermaster]
atualizado: 2026-09-22
---

# R - Conta demo hamburguermaster - estender a validade

Como empurrar a data de vencimento da conta demo no Console do Firebase, e o que conferir junto para as capturas de tela funcionarem.

## Estado atual — 22/09/2026

Já executado. O documento está assim:

| Campo | Valor |
| --- | --- |
| `ativo` | true |
| `plano` | `enterprise` |
| `periodo` | `mensal` |
| `origem` | `trial` |
| `vence_em` | 30/12/2030 (timestamp) |
| `atualizadoEm` | 30/08/2026 |

**Nada mais a fazer neste documento.** As duas observações que sobram:

- `origem` continua `trial` com vencimento em 2030. É dado incoerente para qualquer relatório futuro de conversão de teste grátis — a demo vai aparecer como trial que nunca acabou. Trocar para `demo` custa um clique e limpa a base.
- `atualizadoEm` ficou em 30/08. O Console não carimba esse campo sozinho; quem carimba é o código. Não quebra nada, mas a data não corresponde à última edição real.

## Identificadores

| Campo | Valor |
| --- | --- |
| Projeto Firebase | `moviki-app` |
| Slug | `hamburguermaster` |
| uid | `rjESfrCf8NPiQBNyDwxnP4BzAzd2` |
| Documento | `assinaturas/rjESfrCf8NPiQBNyDwxnP4BzAzd2` |

## Os campos que mandam

O documento de assinatura é criado assim pelo `api/ativar-trial.js`:

| Campo | Tipo | Para que serve |
| --- | --- | --- |
| `ativo` | boolean | **É este que libera o plano.** `lib/contextoUsuario.js` e o painel olham `ativo === true` |
| `vence_em` | timestamp | data de validade. `api/criar-assinatura.js` compara com o relógio: `ativo === true && vence_em > agora` |
| `plano` | string | `basico` · `pro` · `premium` · `enterprise` |
| `periodo` | string | `trial` · `mensal` · `anual` |
| `origem` | string | de onde veio (`trial`, Asaas…) |
| `atualizadoEm` | timestamp | carimbo da última escrita |

**`vence_em` tem que ser do tipo `timestamp`.** Se for salvo como string, a comparação `vence_em.toMillis()` quebra e o comportamento fica imprevisível — é o erro mais comum nessa edição.

## Passo a passo

1. Abrir `console.firebase.google.com` e entrar no projeto **`moviki-app`**.
2. Menu lateral: **Build → Firestore Database**.
3. Na coluna das coleções, escolher **`assinaturas`**.
4. Na coluna do meio, achar o documento **`rjESfrCf8NPiQBNyDwxnP4BzAzd2`**. A lista é grande: use o campo de busca de id no topo da coluna em vez de rolar.
5. Na coluna da direita, passar o mouse no campo **`vence_em`** e clicar no lápis.
6. Conferir que o **tipo continua `timestamp`**. Escolher a data nova no calendário e a hora.
7. **Atualizar.**
8. Na mesma tela, conferir os outros três antes de sair:
   - `ativo` = **true**
   - `plano` = **enterprise**
   - `periodo` — pode continuar `trial`, não atrapalha
9. Sair do painel do lojista e entrar de novo. O painel lê a assinatura no carregamento; sem recarregar, a tela continua mostrando o estado velho.

**Que data pôr:** para conta de demonstração, use algo bem à frente — **31/12/2027**. Não faz sentido repetir essa edição toda vez que a gravação atrasa. Se quiser deixar explícito que não é cliente, mude também `origem` para `demo`.

**Fuso:** o console grava em UTC. Evite `23:xx` do dia limite, que em UTC já é o dia seguinte — ou o contrário, dependendo do campo. Com a data em 2027 isso deixa de importar.

## O que NÃO fazer

- **Não apagar o documento `assinaturas/{uid}`.** Apagar não "reseta o trial": o `trials_usados` guarda o hash do e-mail e continua lá de propósito. O que some é o plano.
- **Não mexer em `trials_usados`.** É a memória do teste grátis. Mexer ali reabre o ciclo de conta nova para burlar o trial.
- **Não fazer isso em conta de lojista real.** Numa conta com assinatura recorrente no Asaas, o `api/webhook.js` reescreve `ativo` e `vence_em` no próximo evento e a edição manual se perde — pior, fica um estado divergente entre o Asaas e o Firestore até lá. A demo não tem Asaas, por isso a edição manual é segura **nela**.

## Conferir também, antes de gravar

O plano ativo não é a única trava da live. O painel decide se mostra o botão **Fazer live** assim:

```
configuracoes/liveTermos → liveBeta (array) e liveDesligada (boolean)
```

O botão só aparece se `liveBeta` estiver **vazio** (live aberta a todos) **ou** se o uid da demo estiver dentro dele — e se `liveDesligada` não for `true`. Enquanto o beta estiver fechado, plano Enterprise ativo não basta: o botão simplesmente não existe na tela.

Confira esse documento no mesmo Console, coleção `configuracoes`, documento `liveTermos`. Se `liveBeta` tiver itens e o uid da demo não estiver lá, acrescente o uid.

## Por que isso importa agora

As cenas 3 e 7 do vídeo convite do criador dependem de live funcionando na conta demo. Sem Enterprise ativo e sem o botão Fazer live, as capturas não existem e o vídeo fica só com as artes.

Relacionado: [[R - Roteiro de captura de tela para o video do criador]] · [[R - Filme institucional - conta demo]] · [[R - Colecoes do Firestore]]
