---
type: decisao
status: concluido
data: 2026-09-04
area: A6 — Medicao e Analytics
tags: [medicao, meta-ads, capi, lgpd]
atualizado: 2026-09-04
---

# ARQ — Atribuicao do Lead ao anuncio: fbc, fbp e IP

## O furo

A CAPI estava no ar desde 27/08. O `Lead` chegava na Meta e era marcado como
**processado**, com quatro chaves de correspondencia reconhecidas. Mesmo assim a
campanha de Joao Pessoa marcava **zero conversao**.

Motivo: o `user_data` ia sem **`fbc`** — o identificador do clique de anuncio.
Sem ele a Meta recebe o cadastro, aceita, e nao tem como saber de qual anuncio
ele veio. O evento nao credita campanha nenhuma e o algoritmo otimiza no escuro.

Um evento aceito nao e um evento atribuido. **"Processado" no Gerenciador de
Eventos nao significa que a campanha esta medindo.**

Havia ainda tres buracos menores na mesma cadeia:

- `client_ip_address` nunca era preenchido, embora `lib/meta.js` ja aceitasse
  `o.ip`. E uma das chaves de correspondencia mais fortes e esta de graca no `req`.
- `event_source_url` do `Lead` estava fixo em `https://app.moviki.com.br/`.
- `comerciantes.html` manda para `https://app.moviki.com.br` **puro**, sem
  repassar `fbclid` nem UTM. A origem morria no salto entre os dominios.

## A decisao: sessionStorage, nao cookie

O `privacidade.html`, secao 9, diz que o site **nao usa cookie de publicidade** —
foi essa frase que decidiu, em 27/08, pela CAPI em vez do pixel. Gravar o cookie
`_fbc` contradiria a mesma politica e reabriria a discussao do banner.

`sessionStorage` nao e cookie: nao viaja em requisicao automatica, morre ao
fechar a aba, e cobre o cadastro feito na mesma sessao — que e a quase totalidade
de quem chega por anuncio. **A politica publicada continua verdadeira.**

O custo: quem clica no anuncio hoje e so cria a conta amanha, em outra aba, perde
a atribuicao. Aceito — esse caso e minoria e o preco alternativo era um banner de
consentimento na frente de todo visitante.

## O salto entre dominios

`sessionStorage` de `moviki.com.br` **nao** e visivel em `app.moviki.com.br`.
Solucao: o `mvmetrica.js` decora os links que levam ao painel com `mvfbc`,
`mvfbp` e as UTMs, e o painel le da URL na chegada. **Conserta o buraco do
`comerciantes.html` sem tocar no HTML dele** — e link novo ja nasce corrigido.

## Por que o wrapper de fetch, e nao o index.html

Existem **cinco pontos de criacao de conta** no painel, todos chamando
`/api/novo-cliente` ou `/api/novo-parceiro` de dentro de um arquivo enorme.
Envolver o `window.fetch` no `mvmetrica.js` cobre os cinco de uma vez, num
arquivo pequeno. Falha no wrapper = a chamada original segue intacta.
**Cadastro nunca quebra por causa de medicao.**

## Regras que nascem daqui

- **`fbc` e `fbp` vao em TEXTO PURO.** Manda-los em SHA-256 faz a Meta aceitar o
  evento e ignorar o parametro, em silencio — o pior tipo de falha.
- **Formato errado suja tanto quanto campo vazio.** O `lib/meta.js` valida
  `fb.<n>.<ts>.<valor>` e descarta o que nao casar.
- **Cadastro organico chega sem `fbc` e o `Lead` vai do mesmo jeito**, so sem
  credito de campanha. Nenhum dos tres campos novos pode barrar um cadastro.

## Arquivos

- `mvmetrica.js` — repos `moviki` e `moviki-app`, SUBSTITUI (identico nos dois)
- `lib/meta.js` — repo `moviki-robo`, SUBSTITUI
- `api/novo-cliente.js` — repo `moviki-robo`, SUBSTITUI

Bonus do `novo-cliente.js`: o aviso do Telegram passa a dizer **"Origem: anuncio
da Meta"** quando o cadastro veio de campanha, e `avisos_cliente/{uid}` guarda
`origemAnuncio`. Da pra saber se a campanha entrega gente sem abrir o Gerenciador.

## Testes

18 casos no `lib/meta.js` e 17 no `mvmetrica.js`, todos passando: formato de
`fbc`/`fbp`, `fbclid` cru rejeitado, IP invalido descartado, lista de proxy
pegando so o primeiro, visita organica sem gravar nada, link organico intacto,
heranca pelo salto de dominio, corpo nao-JSON passando sem lancar, e `fetch`
lancando excecao devolvendo `false` sem propagar.

## Pendencia que fica aberta

O `Purchase` continua sem `fbc`. `lib/meta.js` **ja aceita** o campo — falta o
`criar-assinatura.js` gravar o `fbc` em `faturamento/{uid}`, junto do `client_id`
do GA, e o `webhook.js` repassar. Enquanto isso, a venda e medida mas nao e
atribuida ao anuncio.

→ [[ARQ - Meta CAPI]] · [[ARQ - Anuncios com marcacao vazada no ar]] · [[A6 - Medicao e Analytics]]
