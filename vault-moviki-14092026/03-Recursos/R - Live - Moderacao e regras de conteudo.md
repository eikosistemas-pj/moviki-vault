---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, moderacao, denuncia, painel-do-dono]
atualizado: 2026-09-14
---

# R - Live - Moderacao e regras de conteudo

Como o Moviki impede, detecta e interrompe conteúdo proibido dentro da live.
Quatro camadas: regra escrita, aceite, filtro automático e mão humana.

## 1. Regras da Live 1.0

Página pública `moviki/regras-da-live.html`. Lista o que é proibido:

- droga, arma e munição
- conteúdo sexual
- exposição de menor
- medicamento de receita e anabolizante
- tabaco e vape
- rifa, sorteio e aposta
- produto roubado ou falsificado
- animal silvestre
- promessa de lucro
- discurso de ódio

Mais as regras de venda: preço anunciado é oferta e tem de ser cumprido,
escassez tem de ser real, brinde é por ordem de chegada (sorteio comercial
depende de autorização do Ministério da Fazenda), conteúdo comissionado leva
`#publi`. A página traz **190** e **Disque 100** na tela.

## 2. Aceite versionado

`negocios/{uid}/estado/liveAceite` com `versao: '1.0'`.

- Modal obrigatório no estúdio antes da primeira transmissão.
- **`api/live.js` confere no servidor**: sem aceite, o endereço de transmissão
  não é gerado. A tela sozinha não seria trava.
- Mudou o texto das regras, sobe a versão e todo lojista aceita de novo — mesma
  lógica do `aceiteConduta` do parceiro.

## 3. Filtro de termos proibidos

Nove grupos: drogas, armas, sexual, medicamentos, tabaco, fraude, apostas,
animais, golpe.

- Lista de exceções para não derrubar termo inocente: pistola de água, de cola,
  de pintura, de ar e de solda; sexo do bebê; beijo roubado; bingo de sabores.
- Normalização de acento e de leet.
- **Dígito só vira letra depois de uma letra** — senão `bet365` quebraria.

Cinco cópias, todas geradas do mesmo arquivo-fonte: estúdio, página pública,
painel do dono, `api/live.js` e `lib/checkout.js`. **As duas últimas são a
barreira real**, porque rodam no servidor; as três primeiras são conforto de
tela. As regras do Firestore repetem os termos mais graves, em expressão
regular, na criação de `livechat` — quem escreve por fora da página também
esbarra.

Termos extras ficam em `configuracoes/liveTermos.extras` (até 300 itens),
editáveis pelo dono no painel, **sem deploy**.

## 4. Denúncia anônima

Botão na tela pública de quem assiste. Seis motivos (`proibido`, `sexual`,
`menor`, `violencia`, `golpe`, `outro`) e detalhe de até 300 caracteres.

- "Criança ou adolescente em risco" sobe ao topo da fila e mostra 190 e
  Disque 100.
- Grava em `denuncias/{id}`: qualquer um cria, só o admin lê, resolve ou apaga.
- **Não guarda quem denunciou.**

## 5. Painel do dono — aba Lives (`eikoadm01.html`)

- KPIs: ao vivo, assistindo, lives hoje, vendido hoje, denúncias abertas,
  bloqueados, pedidos hoje, pedidos 7 dias.
- Lives ativas com alerta de denúncia e de termo proibido.
- **Encerrar live**: motivo + castigo (só encerrar, 1, 7, 30 dias ou
  definitivo). Chama `adm_encerrar`, que apaga a entrada no Cloudflare — o
  endereço de transmissão morre na hora, não depende de o lojista colaborar.
- Fila de denúncias, análise de 30 dias (12 KPIs, barras de 14 dias, top 5,
  tabela de 60 lives), lista de bloqueados com Liberar, campo de termos extras,
  log de moderação.
- Correção de segurança da mesma rodada: `naLista` passou a exigir
  `emailVerified === true`.

## 6. Efeito do bloqueio

`live_bloqueios/{uid}` — leitura pública, escrita só do admin. Bloqueado:

- não consegue transmitir;
- não consegue vender pelo Pix;
- tem a página pública derrubada em tempo real, com o aviso "suspensa pela
  equipe do Moviki";
- tem a câmera do estúdio parada.

## 7. Registro

`moderacao/{id}` — só o admin cria e lê. Update e delete proibidos pela regra:
registro que pode ser reescrito não serve de registro.

## Em aberto

- [ ] Revisar a lista-base de termos depois das primeiras lives reais.
- [ ] Definir prazo de guarda do log de moderação.

## Ligações

[[A13 - Modo Live]] · [[A10 - Conformidade e LGPD]] ·
[[R - Live - Relatorio de seguranca]] ·
[[R - Live - Regras legais e conformidade]] ·
[[R - Regras de conteudo e tom]] · [[R - Colecoes do Firestore]] ·
[[R - Live - Videoaulas do modulo]] ·
[[ARQ - Modo Live no ar em beta fechado 12092026]]
