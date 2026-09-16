---
type: decisao
status: concluido
area: A13 - Modo Live
tags: [live, seguranca, moderacao, firestore]
atualizado: 2026-09-15
---

# ARQ - Fase 2 da seguranca da live 15092026

Avaliação crítica da lista de pendências de segurança da live montada por outra
sessão (arquivo `FASE2.txt`), em 15/09/2026. **Metade da lista já estava no ar ou
era maior no papel do que na realidade.**

## O veredito item a item

| Item | Veredito |
| --- | --- |
| **B5** | **Já no ar** — `api/live.js`, marca `2026-09-15-b5a` |
| **B7** | **Superestimado.** O App Check está enforçado no Cloud Firestore desde 05/09/2026; o cenário que o item descrevia já não é alcançável |
| **B8** | **Real.** Fechado nesta rodada |
| **B9** | **Já filtrado** |

## A regra que esta rodada confirma

> **Lista de pendências herdada de outra sessão se confere no código, nunca no
> texto da lista.** Item escrito antes de uma entrega continua escrito depois
> dela.

## O pacote `lote1a` — filtro de conteúdo

Conferido linha a linha e **reproduzido em navegador**, não lido no diff.

O item **C5** era o mais delicado: o aviso do filtro na versão que estava no ar
subia como `position: fixed`, 400x700, `z-index: 99999` — **cobria a tela
inteira do estúdio durante a transmissão**. No pacote novo o mesmo aviso ocupa
62x62 e fica contido. Diferença que só aparece abrindo, porque o CSS do diff não
diz onde o elemento cai.

**Compatibilidade cruzada verificada:** a prévia do `og.js` continua funcionando
com a casca nova do `live.html` — um `<title>`, uma `description`, cifrão
literal preservado.

Marca no ar: `moviki/live.html` = `2026-09-15-filtro`.

## O que isto libera

Com **B8** e **B9** fechados, o motivo técnico que segurava a live em beta
fechado deixa de existir. O que resta é decisão de exposição, não de código:
a lista `configuracoes/liveTermos.liveBeta`.

## Ligações

[[A13 - Modo Live]] · [[R - Live - Relatorio de seguranca]] ·
[[R - Live - Moderacao e regras de conteudo]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[P24 - Modo Live - lancamento]] · [[R - Marcas de versao no ar]]
