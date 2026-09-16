---
type: recurso
status: referencia
area: "[[A4 - Financeiro]]"
tags: [marcas-de-versao, upload, painel-do-dono, custos, margem, firestore]
atualizado: 2026-09-16
---

# R - Marcas de versao - Aba de custos 16092026

Pacote `MOVIKI-SUBIR-aba-custos-16092026.zip`. Um arquivo, um repositorio.

| Repo | Pasta | Arquivo | Acao | Marca | Montado sobre |
|---|---|---|---|---|---|
| `moviki-app` | raiz | `eikoadm01.html` | SUBSTITUI | `2026-09-16-custos1` | `2026-09-16-consumo3` |

**Nenhuma regra nova do Firestore. Nenhuma funcao nova na Vercel. Nenhum arquivo
novo.** Sobe sozinho, em qualquer hora.

---

## A DECISAO QUE VALE MAIS QUE A TELA - onde o dado mora

O dado de custos fica no campo **`custos` dentro de `configuracoes/sistema`**.
Nao e documento novo, e isso e proposital.

> **O match de `configuracoes` nas regras e POR DOCUMENTO, nao curinga.**
> Existem `match /configuracoes/liveTermos` e `match /configuracoes/sistema`, e
> mais nada. Um `configuracoes/custos` **nasceria sem regra nenhuma**: a escrita
> seria negada e a tela salvaria no vazio, calada. Regra do Firestore nao tem
> "deny" e tambem nao tem "permit por engano" - o que nao tem match, nao existe.

O bloco de `configuracoes/sistema` valida **tipo** e **nao tem `hasOnly`** — a
licao da v15, quando o `hasOnly` impediu o proprio dono de desligar a aprovacao
automatica. Por isso campo novo passa sem regra nova, e o `vikPadraoLigado` ja
tinha provado isso na pratica antes deste.

### A trava que vem junto

> **Escrita nesse documento e SEMPRE `merge`.** Ele carrega tambem
> `aprovacaoAutomaticaParceiros` e `vikPadraoLigado`. Sobrescrever inteiro
> desliga a aprovacao automatica de parceiros e o padrao do Vik, sem aviso e sem
> erro. O codigo entregue usa `setDoc(..., {merge:true})` e tem comentario
> dizendo exatamente isso, em cima da linha.

Formato guardado: `{ dolar, aliquota, comissao, asaas, minLive, itens:[{n,c,v,m}] }`
— no maximo 120 itens, nome de ate 60 caracteres, moeda so `BRL` ou `USD`,
categoria conferida contra a lista. Lixo digitado nao vira lixo gravado.

---

## O que a aba faz

Menu **Custos e margem**, entre Relatorios e Lives.

1. **Onde voce esta hoje** — conta com os lojistas que **existem no banco agora**,
   nao com estimativa: pagantes, receita bruta, margem depois de tudo, custo da
   empresa, resultado do mes e quantos Premium faltam para empatar. Chip diz
   "no azul" ou "no vermelho".
2. **Custos mensais** — uma linha por despesa, com categoria, valor e moeda.
   Linha em USD converte pelo dolar do topo. Acrescentar e tirar linha na tela.
   16 linhas ja vem escritas, inclusive as que hoje valem zero — **a linha fica,
   para nao esquecer dela quando o valor existir**.
3. **Imposto, comissao e tarifa** — aliquota efetiva do Simples (o Paulo confirmou
   em 16/09: **6%**, Anexo III), percentual de comissao, tarifa do Asaas e minutos
   de live por lojista.
4. **Quanto sobra de cada cliente** — por plano, com a coluna extra
   **"Sem parceiro"**: a diferenca entre as duas colunas e exatamente o que o
   Programa de Parceiros custa, em reais, por cliente.
5. **Quanto da para gastar para conquistar um cliente** — teto com payback em 3 e
   em 6 meses, e quantos clientes empatam o custo do mes.
6. **O que so o contador responde** — as tres perguntas, na tela, para nao se
   perderem num documento.

### O botao que usa dado real

**"Usar o consumo real de video"** chama a mesma medicao do card de consumo
(`adm_consumo`, analytics do Cloudflare), divide os minutos do ciclo pelos
lojistas em plano com live e escreve o resultado no campo. Com medicao zerada ou
nenhum lojista com live, ele diz isso e **nao muda o numero** — nunca troca um
valor bom por zero.

---

## Os numeros com 6%, conferidos na tela

| Plano | Mensalidade | Imposto | Comissao | Tarifa | Video | Margem | Sem parceiro |
|---|---:|---:|---:|---:|---:|---:|---:|
| Pro | R$ 37,90 | R$ 2,27 | R$ 5,69 | R$ 2,00 | - | **R$ 27,94** | R$ 33,63 |
| Premium | R$ 49,90 | R$ 2,99 | R$ 7,49 | R$ 2,00 | R$ 6,48 | **R$ 30,94** | R$ 38,43 |
| Enterprise | R$ 99,90 | R$ 5,99 | R$ 14,99 | R$ 2,00 | R$ 6,48 | **R$ 70,44** | R$ 85,43 |

Teto por cliente novo, payback em 3 meses: **Pro R$ 83,81 · Premium R$ 92,81 ·
Enterprise R$ 211,31**.

> Isso muda a recomendacao do [[P39 - Remuneracao do influenciador e midia dos parceiros]]:
> o cache de **R$ 150 por peca continua acima do teto** de aquisicao, o que
> confirma trata-lo como **compra de acervo**, nao como custo de cliente. O bonus
> de ativacao de R$ 50 fica confortavelmente dentro.

---

## Conferido antes de entregar

- `node --check` limpo nos **4 blocos de script** do arquivo, inclusive o modulo
- Chromium, com o Firebase trocado por dublê: a secao abre, as 16 linhas
  aparecem, editar um custo recalcula tudo na hora, trocar o dolar reconverte as
  linhas em USD, acrescentar e tirar linha funciona
- **Salvar grava em `configuracoes/sistema`, com `{merge:true}`, e o unico campo
  de raiz enviado e `custos`** — conferido no dublê, que registra o que foi
  gravado
- As outras secoes continuam abrindo, e o `lvConsumoCard` continua no arquivo
- Zero erro de JavaScript
- UTF-8 sem BOM, LF, zero byte de controle

## Conferir depois de subir

1. Abrir o painel, menu **Custos e margem**.
2. Preencher contador, pro-labore, energia e o que mais existir. **Salvar tudo.**
3. Recarregar a pagina e voltar na aba: os valores tem que voltar do banco.
4. Ir em **Configuracoes** e conferir que a chave de **aprovacao automatica de
   parceiros** continua como estava. Se ela tiver mudado, o merge falhou e isso e
   incidente, nao ajuste.
5. Tocar em **Usar o consumo real de video** — com a medicao em zero, ele deve
   dizer que nao ha o que puxar e deixar o campo como estava.

## A planilha morre aqui

A `MOVIKI - Custos da empresa e simulador.xlsx` serviu para levantar os numeros.
Com a aba no ar, **o painel e a fonte** — ele tem o que a planilha nunca teria: a
receita dos lojistas que existem de verdade e o consumo medido do Cloudflare.
Manter as duas cria duas verdades e, em dois meses, ninguem sabe qual esta certa.

## Ligacoes

[[A4 - Financeiro]] · [[P39 - Remuneracao do influenciador e midia dos parceiros]] ·
[[R - Teto de gasto de video no Cloudflare]] · [[R - Planos e precos]] ·
[[R - Custos e cotas]]
