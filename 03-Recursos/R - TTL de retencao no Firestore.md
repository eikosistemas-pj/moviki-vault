---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [lgpd, firestore, ttl, retencao, custo]
atualizado: 2026-09-16
---

# R - TTL de retencao no Firestore

**Nao ha codigo a escrever.** Conferido nos repositorios em 16/09/2026: as
quatro colecoes ja gravam o campo `expiraEm`. O que falta e ligar as politicas
de TTL no Console do Google Cloud — **quatro cliques, uma vez**.

Enquanto elas nao existirem, **"guardado por ate 30 dias" nao e verdade** na
privacidade do Moviki: nada e apagado, nunca. E o custo da presenca da live
(um documento por aba de espectador, por live) e permanente.

## ⚠️ O erro que apaga tudo

O TTL do Firestore apaga o documento quando **a data no campo ja passou**.
Apontar a politica para `criadoEm` — que e sempre uma data no passado —
**apaga a colecao inteira na primeira varredura**. O campo e sempre
`expiraEm`, nunca `criadoEm`.

## As quatro politicas

| Escopo | Nome do grupo | Campo | Retencao gravada hoje |
| --- | --- | --- | --- |
| **Grupo de colecoes** | `livechat` | `expiraEm` | 30 dias |
| **Grupo de colecoes** | `livepresenca` | `expiraEm` | minutos (`PRESENCA_VIDA_MS`) |
| Colecao | `pedidos` | `expiraEm` | `PEDIDO_RETENCAO_MS` · pago: `PEDIDO_RETENCAO_PAGO_MS` |
| Colecao | `checkout_freio` | `expiraEm` | 24 h |

`livechat` e `livepresenca` sao **subcolecoes** de `negocios/{uid}` — no
Console eles entram como **grupo de colecoes** (collection group), nao como
colecao de topo. E a mesma escolha que o campo "Escopo" oferece.

## Passo a passo

1. Console do Google Cloud, projeto **moviki-app**.
2. **Firestore > TTL** (menu da esquerda, dentro do banco `(default)`).
3. **Criar politica**. Escopo: colecao ou grupo de colecoes, conforme a tabela.
4. Nome do grupo/colecao e **campo `expiraEm`**. Confirmar.
5. Repetir para as quatro. O estado fica "Criando" por alguns minutos e depois
   "Ativa".

## O que esperar depois

- **A exclusao nao e instantanea.** O Firestore apaga em geral **dentro de
  24 h** depois do vencimento. A politica de privacidade deve dizer "ate 30
  dias", nunca "em 30 dias exatos".
- **Documento antigo nao some.** O que foi gravado antes de o campo `expiraEm`
  existir nao tem o campo, e **TTL sem campo nao apaga nada**. Os registros de
  testes de 11 a 16/09 ficam la para sempre. Se incomodar, a limpeza deles e
  manual, uma vez.
- **A exclusao por TTL conta como operacao de escrita** na fatura. Para
  `livepresenca`, que e o volume real, ainda sai muito mais barato que guardar.
- TTL **nao dispara gatilho** e nao aparece no historico: e faxina silenciosa.

## Por que isto e prioridade

Nao e arrumacao. Sao tres coisas ao mesmo tempo:

1. **LGPD:** a pagina de privacidade promete prazo de retencao que hoje nao
   acontece. Promessa escrita e nao cumprida e o pior tipo de exposicao —
   documentada por nos mesmos.
2. **Custo permanente:** presenca de live e um documento por aba por live. Sem
   TTL, o banco so cresce.
3. **Exclusao de conta:** o `exclusoes.js` de 16/09 apaga as subcolecoes de um
   lojista excluido, mas o chat de uma live de um lojista **ativo** fica para
   sempre sem o TTL.

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[P - Abertura da live para lojista pagante]] ·
[[ARQ - Buracos da exclusao de conta fechados 16092026]]
