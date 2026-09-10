---
type: decisao
status: concluido
area: A6 - Medicao e Analytics
tags: [meta-ads, capi, medicao, atribuicao, armadilha]
atualizado: 2026-09-10
---

# ARQ - Atribuicao do Lead ao anuncio - fbc e fbp

Rodada de 05/09/2026. No ar e conferido no repositorio em 10/09.

## O que faltava

O evento `Lead` chegava a Meta pela API de Conversoes, mas **sem os campos que
dizem de qual anuncio a pessoa veio**. Sem `fbc`, a Meta recebe uma conversao que
nao consegue amarrar a nenhum clique — e campanha que nao recebe conversao
atribuida nunca sai do aprendizado.

## A cadeia, ponta a ponta

1. `mvmetrica.js` (identico nos repos `moviki` e `moviki-app`) captura o
   **`fbclid`** da URL e guarda
2. o salto de dominio (`moviki.com.br` para `app.moviki.com.br`) preserva o valor
3. o wrapper de fetch leva o campo ate o robo
4. `api/novo-cliente.js` repassa e `lib/meta.js` monta **`fbc`, `fbp` e IP** no
   evento

**Sem pixel no navegador, de proposito:** o `privacidade.html` declara que o site
nao usa cookie de publicidade, e subir o pixel contradiria a politica publicada.
O evento nasce no servidor.

## A prova

05/09, 02:06 — cadastro de teste "Eiko Jato" (`eikovida2021@gmail.com`) feito com
`fbclid` manual na URL, e o aviso do Telegram veio com **"Origem: anuncio da Meta"**.
Isso prova que o valor atravessou a landing, o salto de dominio, o wrapper de
fetch e chegou ao `novo-cliente.js`.

05/09, 07:27 — **CAPI confirmada funcionando**: 2 eventos `Lead` recebidos no
conjunto `2114417739495816`, qualidade de correspondencia **7,7/10**. Nunca esteve
quebrada.

## As armadilhas que custaram a madrugada

- **Lead de teste com `fbclid` inventado NAO aparece em `actions_lead` da
  campanha** — so no Gerenciador de Eventos do conjunto. Confundir os dois faz
  parecer que falhou.
- **A Visao geral do Gerenciador de Eventos demora HORAS**, apesar de a propria
  tela prometer 30 minutos. Duas horas olhando tela vazia levaram a um
  diagnostico errado. Para conferir envio na hora, usar a aba **Eventos de teste**.
- **Log sem erro e ambiguo.** O `lib/meta.js` so grava `console.error` em falha:
  silencio significa sucesso **ou** envio nao tentado. Foi o que motivou a linha
  de resultado da medicao no aviso do Telegram (`enviada`, `sem env`,
  `recusada HTTP xxx`, `tempo esgotado`).
- **Nunca reusar nome de variavel ja usado no escopo.** Um `let corpo` colidiu com
  o corpo do POST e teria derrubado **todos** os eventos em producao, com sintoma
  identico ao bug que estava sendo cacado. Pego no teste.

## Timeout: dois numeros diferentes de proposito

O `Lead` subiu de 2,5 s para **6 s** — cadastro nao tem a pressa do webhook. O
`Purchase` **fica em 2,5 s**: o contrato do webhook do Asaas nao pode ser
esticado. `lead()` e `purchase()` seguem devolvendo booleano e nunca lancam —
**medicao nunca derruba cobranca**.

## Em aberto

- [ ] `Purchase` sem `fbc`: o `lib/meta.js` ja aceita o campo — falta o
      `criar-assinatura.js` gravar em `faturamento/{uid}` e o `webhook.js` repassar
- [ ] Tirar o `META_TEST_CODE` da Vercel: enquanto existir, o evento nao conta
      como conversao de verdade
- [ ] Apagar a conta de teste `eikovida2021@gmail.com` pelo `eikoadm01.html`

## Ligacoes

[[A6 - Medicao e Analytics]] · [[A7 - Aquisicao e Midia Paga]] ·
[[P17 - Descobrir o CPA real do lojista]] · [[R - Regras de ouro]]
