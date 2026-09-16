---
type: incidente
status: concluido
area: A7 - Aquisicao e Midia Paga
tags: [moviki, google-ads, meta-ads, correspondencia-ampla, falso-alarme, leitura-de-dado]
atualizado: 2026-09-16
---

# ARQ - Falso alarme das amplas e Meta pausada 16092026

> Duas acoes autorizadas pelo Paulo em 16/09. A primeira derrubou um alarme que
> a rotina vinha repetindo havia dias: **as 3 palavras em correspondencia AMPLA
> nunca voltaram**. A segunda pausou a campanha da Meta apos 9 dias sem um unico
> lead.

Relacionado: [[ARQ - Palavras amplas de volta e campanha parada em 14092026]] ·
[[ARQ - Reposicao das palavras positivas do Google Ads]] ·
[[R - Rotina de checagem das campanhas]] · [[R - Regras de ouro]]

---

## 1. O alarme que nao existia

O pulso de 13/09 e de novo o de 15/09 registraram que as tres palavras removidas
no conserto de 11/09 estavam de volta no Grupo de anuncios 1 (`206808639824`):

| Palavra | Correspondencia | criterion_id |
| --- | --- | --- |
| mapa em tempo real | BROAD | 303299890762 |
| mapa tempo real | BROAD | 309090226055 |
| localizacao em tempo real | BROAD | 314042009422 |

Com a autorizacao do Paulo, a remocao foi executada em 16/09 pela ponte do
Windsor. Resposta dos tres ids:

> **"Resource was not found."**

As tres **ja estavam removidas**. Nao voltaram, nao foram reaplicadas por
recomendacao automatica, e ninguem as recriou no painel.

## 2. Por que o alarme se repetiu

A leitura foi feita com `include_inactive: true`, que devolve palavras
**removidas** junto com as ativas, porque elas ainda carregam o dado historico da
janela consultada. As tres aparecem na leitura de 10 a 16/09 com impressao e
gasto — 32 impressoes e R$ 12,84 numa delas — e esse dado e de **10 e 11/09**,
antes do conserto.

Esta e **exatamente** a mesma armadilha descrita em
[[ARQ - Reposicao das palavras positivas do Google Ads]], em 11/09. A licao
estava escrita e a rotina caiu nela duas vezes depois.

### Regra de ouro reforcada

> **No Google Ads, presenca de uma palavra numa leitura com `include_inactive`
> NAO significa que ela esta ativa.** Para saber o estado real, tentar a escrita:
> a recusa e a resposta. E antes de abrir alarme de "palavra voltou", conferir se
> o gasto atribuido a ela cai dentro da janela consultada ou e anterior ao
> conserto.

## 3. Meta pausada

Campanha `Moviki | Cadastro de lojista | Conversao | set-2026`
(`120251233014530770`) **PAUSADA em 16/09**, por decisao do Paulo.

Motivo: nove dias de entrega, zero lead.

| Data | Gasto | Cliques | Impressoes | Leads |
| --- | --- | --- | --- | --- |
| 13/09 | R$ 9,85 | 11 | 640 | 0 |
| 14/09 | R$ 7,36 | 7 | 437 | 0 |
| 15/09 | R$ 8,38 | 17 | 596 | 0 |
| 16/09 | R$ 6,47 | 8 | 353 | 0 |

O gatilho da rotina e 5 dias sem conversao. Foi ultrapassado com folga.

**Criterio de retomada:** so religar depois que a `comerciantes.html`
reposicionada (`2026-09-16-filmelive`) tiver dado de conversao proprio. Objetivo
de conversao exige conversao existente — religar antes repete o vazio.

Reversivel pela acao `enable_campaign`.

## 4. Google Ads segue parado, e o motivo e saldo

| Data | Gasto | Cliques | Impressoes |
| --- | --- | --- | --- |
| 13/09 | R$ 13,06 | 7 | 189 |
| 14/09 | R$ 0,00 | 0 | 4 |
| 15/09 | R$ 0,00 | 0 | 4 |
| 16/09 | R$ 0,00 | 0 | 3 |

Campanha ENABLED, grupos ELIGIBLE, anuncios APPROVED. Saldo esgotado, reposicao
e do Paulo no painel.

**Nao repor antes de conferir a conversao Inscricao.** A consulta de conversoes
por acao nao devolve linha nenhuma desde 09/09 — nem zero Inscricao, zero linha
de qualquer tipo. Repor saldo com medicao cega repete os R$ 99,16 de 09 a 13/09.

## 5. Estado das palavras do Grupo 1

Conferido na mesma leitura: o Grupo 1 tem hoje 20 palavras, todas em FRASE ou
EXATA, todas do nicho itinerante (`sistema para food truck`, `app para feirante`,
`divulgar barraca de feira`, `divulgar quiosque`...). **Zero impressao na
semana.** O grupo continua vivo e mudo — por falta de volume de busca, nao por
estrutura errada.

Decisao em aberto: repovoar com palavra de problema do lojista ou pausar o grupo
para limpar a leitura da conta.
