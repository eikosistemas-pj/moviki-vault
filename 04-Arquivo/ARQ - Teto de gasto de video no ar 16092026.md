---
type: arquivo
status: concluido
area: A13 - Modo Live
tags: [live, cloudflare, custo, teto, decisao, incidente]
atualizado: 2026-09-16
---

# ARQ - Teto de gasto de video no ar 16092026

## O que se descobriu

**O Cloudflare Stream nao tem teto de gasto.** Os "budget alerts" da conta sao
**so aviso** — mandam e-mail e nada mais. Nao existe botao que pare a entrega
quando o valor estoura. O preco e **US$ 1 por 1.000 minutos entregues**, e
"entregue" conta **por espectador**: uma live de 1 hora com 50 pessoas
assistindo custa 3.000 minutos, nao 60.

Sem parede, uma unica live que viralize — ou um laco malicioso — gera fatura
sem teto.

## A parede que foi construida

`moviki/api/live.js` mede os minutos entregues na analytics do Cloudflare e
**recusa live nova** acima do teto.

- Consulta GraphQL, dataset `streamMinutesViewedAdaptiveGroups`. Exige a
  permissao **Account Analytics** no token.
- `medirConsumo(cicloDia)` soma o ciclo corrente; `inicioDoCiclo()` calcula a
  virada.
- `vereditoTeto(termos)` decide e **diz por que**: `sem_teto`,
  `medicao_falhou`, `teto_atingido`, `medicao_zerada`, `abaixo_do_teto`.

## A decisao que precisa estar escrita

> **Esta trava falha ABERTA de proposito.** Medicao que nao responde **nao**
> impede a live. E a unica trava do projeto assim. Todas as outras — aceite,
> plano, beta, corte de comissao, abertura de sessao — falham fechadas.
>
> O motivo: a analytics do Cloudflare e um terceiro fora do caminho critico.
> Falhar fechada ali significaria **o Modo Live inteiro parar porque um
> endpoint de relatorio ficou lento**. O risco de uma live a mais e dinheiro; o
> risco de falhar fechada e o produto.

## O ciclo NAO e o mes-calendario

O faturamento do Cloudflare vira no dia da assinatura da conta. A do Paulo vira
**dia 12** — o Billing mostra "Sep 12 - Oct 11". Medir do dia 1 daria um numero
errado todo mes. Por isso existe `cicloDia`, configuravel no painel do dono.

## O incidente do teste que "nao travou"

Paulo configurou **teto = 1 minuto** e a live abriu normalmente. A leitura
obvia seria "a trava nao funciona".

**A trava estava certa. A tela e que nao contava.** Com zero minuto medido no
ciclo, `0 >= 1` e falso — e nada barra. E, como nada aparecia na tela, nao
havia como saber se o teto tinha sido lido, se a medicao respondeu, ou se a
conta estava zerada.

O conserto nao foi na trava: foi a linha **"Proxima live: LIBERADA / BARRADA"**
no card de consumo do painel do dono, com o motivo por extenso.

> **Regra de ouro:** trava sem tela que mostre o veredito e indistinguivel de
> trava quebrada. Quem testa precisa ver **o que a trava decidiu e por que**,
> nao so o efeito.

## Configuracao no ar

| Chave em `configuracoes/liveTermos` | Valor |
| --- | --- |
| `tetoMinutosMes` | **50000** |
| `cicloDia` | **12** |

⚠️ `configuracoes/liveTermos` guarda tambem `liveBeta`, `liveDesligada`,
`extras` e `demoYoutube`. **Escrita nesse documento e sempre `merge`.**
Sobrescrever inteiro desliga o teto e abre o beta sem querer.

## Ligacoes

[[A13 - Modo Live]] · [[A4 - Financeiro]] ·
[[R - Teto de gasto de video no Cloudflare]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[R - Live - Ferramentas de transmissao]] ·
[[P35 - Auditoria de seguranca do Modo Live]] · [[R - Regras de ouro]]
