---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, videoaulas, estudio, tutoriais]
atualizado: 2026-09-14
---

# R - Live - Videoaulas do modulo

Documento do módulo de videoaulas do Modo Live: o que cada aula cobre, onde ela
aparece e como o progresso é medido. Estado em 13/09/2026: **estrutura pronta e
conferida no navegador, vídeos ainda não produzidos**. A produção é o
[[P28 - Videoaulas do Modo Live]].

## A decisão: uma aula por aba

Treze aulas curtas, de 25 segundos a um minuto e meio, em vez de dois vídeos
longos. O motivo é mecânico: **o motor de tutoriais embute um vídeo por
seletor**. Aula por aba faz cada uma nascer onde a dúvida acontece — quem abre
"Oferta relâmpago" vê a aula de oferta relâmpago no fim daquela aba. Vídeo longo
obrigaria o lojista a procurar o minuto certo no meio de uma transmissão.

Três aulas são de contexto: a abertura, as regras de conteúdo e a primeira
transmissão.

## Catálogo

Arquivo: **`moviki-app/liveaulas.js`**, lido pelo painel e pelo estúdio.

| # | Chave | Título | Duração | Onde embute | Plano |
| --- | --- | --- | --- | --- | --- |
| 1 | `mod-live-abertura` | Live no Moviki: o que é e como funciona | 1:20 | só biblioteca | todos |
| 2 | `mod-live-regras` | O que pode e o que não pode na live | 1:05 | tela de aceite (`#aulaRegras`) | todos |
| 3 | `mod-live-primeira` | Sua primeira live: título, câmera e entrar ao vivo | 1:15 | `#boxAntes` | todos |
| 4 | `mod-live-sacolinha` | Sacolinha e produto em destaque | 1:05 | aba Produtos | Premium+ |
| 5 | `mod-live-chat` | Chat da live: responder e apagar | 0:45 | aba Chat | Premium+ |
| 6 | `mod-live-agendar` | Agendar a próxima live e divulgar o link | 0:50 | aba Agendar | Premium+ |
| 7 | `mod-live-pix` | Receber no Pix dentro da live | 1:30 | aba Receber no Pix | Enterprise |
| 8 | `mod-live-pedidos` | Pedidos pagos: conferir, combinar e entregar | 0:55 | só biblioteca | Enterprise |
| 9 | `mod-live-oferta` | Oferta relâmpago e estoque ao vivo | 1:00 | aba Oferta relâmpago | Enterprise |
| 10 | `mod-live-cupom` | Cupom, brinde e "Estou aqui agora" | 1:00 | aba Cupom e brinde | Enterprise |
| 11 | `mod-live-fila` | Fila de pedidos | 0:35 | aba Fila de pedidos | Enterprise |
| 12 | `mod-live-dados` | Dados ao vivo e o resumo da live | 0:45 | aba Dados | Enterprise |
| 13 | `mod-live-cortes` | Cortes para Reels e Status | 0:45 | aba Cortes | Enterprise |

Total previsto: 12 a 13 minutos de vídeo. As cenas são numeradas de
`L00-live-abertura` a `L12-cortes`.

**A aula de ferramenta do Enterprise aparece para quem é Premium**, com o selo
`Enterprise` no cartão. Ela descreve a ferramenta e nunca promete resultado —
então passa na conformidade e funciona como vitrine. Esconder a aula esconderia
justamente o motivo pelo qual as ferramentas foram divididas assim.

A cobertura foi conferida lendo o `live.html` do estúdio, o `live.html` público,
o `api/live.js` e o `lib/checkout.js` — não a memória de rodadas anteriores.
Nenhuma funcionalidade ficou sem aula.

## Onde as aulas aparecem

**No painel (`index.html`).** As treze entram na biblioteca *Tutoriais*, no fim
da lista, com rótulo `Live — …`. Os seletores de aba não existem no painel,
então nada é embutido lá. A sequência de boas-vindas **não muda**: ela tem lista
fixa de quatro chaves.

**No estúdio (`live.html`).** Motor próprio:

- botão **Aulas** no topo, com contador, que abre a biblioteca;
- caixa da aula no fim da aba correspondente;
- a aula das regras dentro da própria tela de aceite;
- faixa de convite na primeira visita, enquanto a abertura e a primeira live não
  forem vistas — **insistência, nunca bloqueio**: o estúdio segue aberto;
- visto verde por aula, medido em **90% de reprodução real** pela API do YouTube.

## A trava que vale por si: aula não toca com a live no ar

Com `<body class="noAr">` o clique vira aviso e nenhum vídeo abre, nem na
biblioteca nem na aba. **O áudio da aula sairia dentro da transmissão**, pelo
microfone do celular. E ao tocar em *Entrar ao vivo*, tudo que estiver tocando é
parado e a biblioteca fecha.

## Progresso

`negocios/{uid}/estado/liveaulas` → `{ vistas: [], em: '' }`.

**Não exigiu regra nova**: cai no `match /negocios/{uid}/{documento=**}`, que já
dá escrita ao dono. Essa subcoleção é de **leitura pública** — por isso só entram
chaves de aula, nada pessoal. O `em` é carimbado uma única vez, na primeira
conclusão, pelo mesmo motivo do `aulasEm` do parceiro.

## Regras dos roteiros

Valem para os treze:

- conversa, não manual; fala com quem trabalha, não com quem programa;
- descreve a **regra**, nunca o **resultado**;
- nunca diz quantas aulas ou quantas ferramentas existem — a lista cresce e o
  vídeo não se corrige com um deploy;
- nada de valor, nome ou documento real no quadro quando a aula mostra o Pix.

Único número falado em todo o módulo: a tarifa fixa do Asaas por Pix recebido,
na aula 7. Está lá porque sem ele o pedido mínimo de vinte reais não se explica.
É também a única frase que envelhece se a tarifa mudar.

## Produção

- **Voz Malu** (`fhtZMBwha5du5OxuvexO`), Kairogen. Falas curtas: bloco longo
  engasga nessa voz. Grafia para o motor: **Mo-víki**; a legenda e o `.srt`
  mantêm "Moviki".
- O estúdio Playwright das videoaulas grava o painel real contra um Firebase de
  mentira. Para a live ele precisa de peças novas, e **essa é a maior parte do
  trabalho**: câmera falsa no Chromium
  (`--use-fake-device-for-media-stream`), `api/live.js` de mentira devolvendo
  nível e endereços, um vídeo local no lugar do WebRTC do Cloudflare, e uma
  **segunda aba** gravando a tela de quem assiste — metade das aulas mostra os
  dois lados.

## Para publicar

1. Produzir os treze `.mp4` e `.srt`.
2. Paulo sobe no YouTube, **não listados**, e manda os links.
3. Cada link vira `id` e `d` em `liveaulas.js` — só esse arquivo muda.
4. Atualizar o documento de videoaulas no ar na mesma entrega.
5. Conferir no ar: contador certo no botão Aulas, caixa em cada aba, visto verde
   na segunda aula (o defeito clássico) e nenhuma aula abrindo com a live no ar.

**Enquanto os vídeos não existirem, nada aparece e nada quebra** — aula sem `id`
não é exibida em lugar nenhum. Foi assim que a estrutura foi conferida no
navegador antes de entregar.

Durante o beta as aulas obedecem ao interruptor da live: só aparecem para quem
está na lista `liveBeta`. Ver
[[R - Live - Exposicao e interruptores do beta]].

## Ligações

[[A13 - Modo Live]] · [[A14 - Material de apoio do parceiro]] ·
[[P28 - Videoaulas do Modo Live]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[R - Live - Moderacao e regras de conteudo]] ·
[[R - Live - Ferramentas de transmissao]] ·
[[R - Voz oficial das videoaulas]] · [[R - Regras de conteudo e tom]]
