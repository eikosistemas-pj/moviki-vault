---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, videoaulas, estudio, trava]
atualizado: 2026-09-15
---

# R - Live - Videoaulas do modulo

Documento do módulo de videoaulas do Modo Live. Estado em 15/09/2026:
**catorze aulas produzidas, no ar e com `id`**. Substitui a versão de 13/09, que
descrevia treze aulas ainda não produzidas.

## A decisão: módulo próprio, não mais itens na biblioteca do painel

Desde 15/09 as aulas da live **não são** o fim da lista de tutoriais do painel.
São módulo dedicado, aberto pelo clique em *Fazer live*, com trava de aptidão.
O registro da decisão está em
[[ARQ - Modulo de aulas da live com trava 15092026]].

As aulas do painel continuam exatamente como estão.

## Uma aula por aba

Aulas curtas, de vinte segundos a um minuto e meio, em vez de dois vídeos
longos. O motivo é mecânico: **o motor embute um vídeo por seletor**. Aula por
aba faz cada uma nascer onde a dúvida acontece.

## Catálogo

Arquivo: **`moviki-app/liveaulas.js`**, marca `2026-09-15-liveaulas2`, lido pelo
painel e pelo estúdio.

| # | Chave | Título | Dur | Onde embute | Plano | id |
| --- | --- | --- | ---: | --- | --- | --- |
| 1 | `mod-live-abertura` | Live no Moviki: o que é e como funciona | 1:20 | só biblioteca | todos | `1TqgHffAyYU` |
| 2 | `mod-live-regras` | O que pode e o que não pode na live | 1:04 | tela de aceite | todos | `3WceM12RkWE` |
| 3 | `mod-live-primeira` | Sua primeira live: título, câmera e entrar ao vivo | 1:16 | `#boxAntes` | todos | `sngj1eUC7kU` |
| 4 | `mod-live-sacolinha` | Sacolinha e produto em destaque | 0:55 | aba Produtos | Premium+ | `3Fsofzdj0u4` |
| 5 | `mod-live-chat` | Chat da live: responder e apagar | 0:33 | aba Chat | Premium+ | `V6WZqQ0s-bY` |
| 6 | `mod-live-agendar` | Agendar a próxima live e divulgar o link | 0:31 | aba Agendar | Premium+ | `cWG2cWGMrII` |
| 7 | `mod-live-pix` | Como você recebe o dinheiro | 1:30 | aba Receber no Pix | Enterprise | `hhTBM163vK0` |
| 8 | `mod-live-pedidos` | Pedidos: conferir, confirmar e entregar | 1:00 | `#tab-financeiro` | Enterprise | `qx4dFUC9ORs` |
| 9 | `mod-live-oferta` | Oferta relâmpago e estoque ao vivo | 0:55 | aba Oferta relâmpago | Enterprise | `pbWfLHoKGag` |
| 10 | `mod-live-cupom` | Cupom, brinde e "Estou aqui agora" | 0:50 | aba Cupom e brinde | Enterprise | `BQPflIBLNG0` |
| 11 | `mod-live-fila` | Fila de pedidos | 0:21 | aba Fila de pedidos | Enterprise | `hhooJvRXx2Q` |
| 12 | `mod-live-dados` | Dados ao vivo e o resumo da live | 0:31 | aba Dados | Enterprise | `07rQewrYNaI` |
| 13 | `mod-live-cortes` | Cortes para Reels e Status | 0:24 | aba Cortes | Enterprise | `vzZOyzzfYHM` |
| 14 | `mod-live-cardapio` | Seu cardápio vendendo sozinho | 1:18 | `#tab-cardapio` | Premium+ | `2_ty4YrgZ0I` |

Total: cerca de **12 minutos** de vídeo. Todas **não listadas** no YouTube até a
abertura das portas.

A catorze nasceu depois do projeto: o cardápio comprável virou porta de venda
que funciona **sem live**, e passou a exigir aula própria.

**A aula de ferramenta do Enterprise aparece para quem é Premium**, com o selo
`Enterprise` no cartão. Descreve a ferramenta e nunca promete resultado — passa
na conformidade e funciona como vitrine.

## A trava de aptidão

Três chaves travam o botão *Entrar ao vivo*: `mod-live-abertura`,
`mod-live-regras`, `mod-live-primeira`. São as de **contexto**. As onze de
ferramenta não travam — ferramenta que o lojista não usa não impede transmissão.

A trava age no `btnIniciar`, **antes do aceite dos termos**, e só reabre o que
ela mesma fechou: `travadoPorAula` guarda a autoria e `mestraAtiva()` confere que
o interruptor mestre do painel do dono não é quem está segurando o botão.

## Onde as aulas aparecem

**No painel (`index.html`, `2026-09-15-liveaulas2`).** Card próprio no topo,
espelhando o card das videoaulas do painel: falta assistir · em dia · aula nova.
Pintado dentro do snapshot do `liveTermos` — antes disso o painel não sabe se a
live está liberada. Embute nas abas Financeiro e Cardápio.

**No estúdio (`live.html`, `2026-09-15-liveaulas`).** Botão **Aulas** no topo com
contador, caixa da aula no fim de nove abas, a aula das regras dentro da tela de
aceite, visto verde medido em **90% de reprodução real** pela API do YouTube.

## Função nova ganha aula, e a aula vira alerta

Toda ferramenta nova que entrar no estúdio entra também aqui, com data em `em`.
`novas()` compara a data de conclusão do lojista com a data de cada aula: só
conta como novidade a aula **publicada depois** de ele ter ficado em dia. Quem
nunca assistiu nada não recebe "aula nova" — recebe "falta assistir".

## A trava que vale por si: aula não toca com a live no ar

Com `<body class="noAr">` o clique vira aviso e nenhum vídeo abre. **O áudio da
aula sairia dentro da transmissão**, pelo microfone do celular. Ao tocar em
*Entrar ao vivo*, tudo que estiver tocando é parado e a biblioteca fecha.

Parar o vídeo na troca de aba é feito por **listener de clique** em
`[data-tab], .tab, .aba, [data-fin], .finAba` — o painel re-embrulha `abrirTab`
em `setInterval` e qualquer wrapper posto por cima some sozinho.

## Progresso

`negocios/{uid}/estado/liveaulas` → `{ vistas: [], em: '' }`.

**Não exigiu regra nova**: cai no `match /negocios/{uid}/{documento=**}`. Essa
subcoleção é de **leitura pública** — por isso só entram chaves de aula, nada
pessoal. O `em` é carimbado na primeira conclusão.

## Regras dos roteiros

- conversa, não manual;
- descreve a **regra**, nunca o **resultado**;
- nunca diz quantas aulas ou quantas ferramentas existem;
- nada de valor, nome ou documento real no quadro — telefone e CPF nas gravações
  são **falsos claros**, porque o vídeo vai para o YouTube.

Único número falado no módulo: a tarifa fixa do Asaas por Pix recebido, na aula
7. Sem ele o pedido mínimo de vinte reais não se explica. É a única frase que
envelhece se a tarifa mudar.

## Produção

- **Voz Malu** (`fhtZMBwha5du5OxuvexO`), Kairogen. Falas curtas. Grafia para o
  motor: **Mo-víki**; legenda e `.srt` mantêm "Moviki".
- Captura 1376x774 escala 2, encode 1280x720 H.264 crf 17, legenda queimada mais
  `.srt`.
- Três motores: `gravador.py` (uma tela e duo), **`partes.py`** (bancadas
  costuradas, para aula que percorre painel, página pública e estúdio em dois
  planos) e as bancadas `estudio.py`, `publica.py`, `ponte.py`.
- O relógio da bancada governa câmera e animação desde 15/09 —
  ver [[ARQ - Incidente - camera e animacoes aceleradas na bancada]].

## Pendências

- **Doze aulas foram gravadas antes do conserto do relógio** e estão no ar com a
  câmera acelerada. São legíveis; regravar em lote é decisão aberta. A 01 e a 08
  já saíram consertadas.
- **`WmpIQr36b2o`** — aula 08 antiga, com a fala errada — segue publicada como
  não listada.

Durante o beta as aulas obedecem ao interruptor da live: só aparecem para quem
está na lista `liveBeta`. Ver [[R - Live - Exposicao e interruptores do beta]].

## Ligações

[[A13 - Modo Live]] · [[A14 - Material de apoio do parceiro]] ·
[[ARQ - Videoaulas do Modo Live concluidas 15092026]] ·
[[ARQ - Modulo de aulas da live com trava 15092026]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[R - Live - Moderacao e regras de conteudo]] ·
[[R - Live - Ferramentas de transmissao]] ·
[[R - Voz oficial das videoaulas]] · [[R - Regras de conteudo e tom]]
