---
type: recurso
status: referencia
area: A8 - Conteudo e Social
tags: [aquisicao, conteudo, video, marca]
atualizado: 2026-08-31
---

# R - Roteiro do video institucional

Documento de producao do filme institucional da Moviki para a landing
`moviki.com.br`. Fonte unica de verdade do roteiro, dos textos de tela, da
narracao e dos prompts de geracao. Projeto que executa: [[P13 - Video institucional da landing]].

> **Estado:** roteiro travado em 2026-08-29. A producao divergiu do plano em
> pontos concretos — ver **secao 15** antes de usar qualquer numero deste
> documento como verdade operacional.

---

## 0. Critica ao briefing original — 8 correcoes estruturais

O briefing pedia um filme. Um filme sozinho nao move metrica. Estas oito
mudancas foram incorporadas ao roteiro abaixo.

1. **O video precisa funcionar mudo.** Autoplay em landing e mudo por padrao no
   navegador. Se a mensagem depende da locucao, ela nao existe para a maioria.
   Correcao: **tipografia cinetica carrega a narrativa inteira sozinha**; a
   locucao e camada de reforco, nao de conteudo. Legenda queimada obrigatoria.
2. **Nao existe "um" video.** Existe um banco de cenas e cinco cortes:
   78 s (master), 30 s (trafego pago), 15 s vertical 9:16 (Reels/Stories),
   **8 s mudo em loop para o heroi** e 6 s (bumper YouTube). Mesmo banco, custo
   marginal quase zero. Detalhe na secao 10.
3. **O video nao entra no heroi como autoplay pesado.** A landing e enxuta
   (~30 KB) e um MP4 no topo destroi o LCP. Correcao: heroi recebe o loop de
   8 s em WebM <= 1,5 MB, sem audio, `preload="none"`, com poster; o filme
   completo abre em lightbox pelo botao **"Ver como funciona"** que ja existe
   na pagina. Especificacao na secao 11.
4. **Vik fica de fora do master.** Mascote cartoon dentro de fotografia
   cinematografica realista quebra a unidade estetica — e o Vik ja tem funcao
   definida (assistente, 404, onboarding, videoaulas). Correcao: **Vik nao
   aparece no institucional**; ganha uma peca propria de explicacao de produto.
5. **Conformidade Meta/Google precisa nascer no roteiro, nao na revisao.** O
   filme sera midia paga. Nenhuma frase pode prometer resultado, ganho, aumento
   de venda ou crescimento. Correcao: o roteiro descreve **a regra e o
   recurso**, nunca o resultado. Lista do que e proibido na secao 12.
6. **Prova social falsa mata a marca.** O "4,8 (128)" da landing e exemplo de
   interface, nao dado real. Correcao: **nenhum numero, nota, contador ou
   depoimento** aparece no filme enquanto nao houver base real auditavel.
7. **A UI nao pode ser inventada.** Interface fake e o item n. 1 que faz um SaaS
   parecer vaporware. Correcao: toda tela do filme e **captura real** de
   `app.moviki.com.br` e `moviki.com.br/apelido`, composta em pos sobre celular
   com tela apagada. A IA nunca gera interface.
8. **Video nao instrumentado e video invisivel.** Correcao: eventos GA4
   definidos na secao 13, no mesmo padrao do funil ja no ar.

**Ganho colateral:** o banco de cenas alimenta o robo social (`moviki-assistente-social`)
por meses e resolve a escassez de criativo institucional dos 11 fundos.

---

## 1. Conceito criativo

### A frase que abre o filme

> **"Onde voces estao hoje?"**

E a pergunta que o dono de negocio itinerante responde trinta vezes por dia no
WhatsApp, no direct e nos comentarios. E a pergunta que o cliente digita e nem
sempre tem resposta. **O filme comeca nessa pergunta e termina resolvendo ela.**

### O conflito central

Um negocio em movimento vive uma contradicao: **ele se move, mas o endereco
nao acompanha.** A rede social parece resolver e nao resolve — feed e fila, nao
e lugar. O post de hoje esta soterrado amanha.

### A tese da marca, dita em uma linha

> **"Um post envelhece em uma hora. Um ponto no mapa, nao."**

Esta e a frase que diferencia a Moviki de "postar no Instagram". Nao promete
resultado, e argumento, e verdadeira, e passa em qualquer revisao de anuncio.

### O gesto de marca

O momento visual que a plateia leva embora: **o pino que acende e se move junto
com o negocio.** Ele nasce na cena 6, se multiplica na 13 e vira o logo na 14.
Um unico gesto grafico atravessa o filme inteiro.

### Tom

Documentario de marca. Nao e comercial de aplicativo, nao e video de tutorial.
E um filme curto sobre duas pessoas que quase nao se encontram — e sobre o que
faz elas se encontrarem.

---

## 2. Estrategia narrativa

| Ato | Tempo | Funcao | Emocao alvo |
| --- | --- | --- | --- |
| I — A pergunta | 0–8 s | Gancho. Reconhecimento imediato. | "isso e comigo" |
| II — O desencontro | 8–21 s | A dor concreta, nao abstrata. | frustracao |
| III — A virada | 21–32 s | O pino. A frase-conceito. | alivio |
| IV — A plataforma | 32–55 s | Prova. Recurso a recurso, sem tutorial. | confianca |
| V — A amplitude | 55–70 s | "Cabe muito mais que food truck." | pertencimento |
| VI — Assinatura | 70–78 s | Logo, slogan, CTA. | acao |

**Duas regras de ritmo:**

- **Nenhum plano passa de 8 s.** Media de 5,6 s. Corte no movimento, nunca no
  repouso.
- **A dor tem 13 s e a solucao tem 23 s.** Inverter isso vira video de
  reclamacao; alongar a dor alem de 15 s perde retencao.

**Regra de retencao (30 s pagos):** o corte de trafego pago comeca na cena 2,
nao na 1. Em feed, o gancho tem 1,5 s.

---

## 3. Roteiro completo — 14 cenas / 78 s

| # | In–Out | Dur | O que se ve | Camera | Grafico |
| --- | --- | --- | --- | --- | --- |
| C01 | 00,0–04,0 | 4,0 | Food truck acendendo as luzes numa rua nova, fim de tarde | dolly lateral lento | — |
| C02 | 04,0–08,0 | 4,0 | Close do celular do lojista, mensagens chegando | macro, camera fixa | baloes de msg |
| C03 | 08,0–13,0 | 5,0 | Cliente na calcada girando, procurando; feed rolando | handheld sutil | feed em pos |
| C04 | 13,0–17,0 | 4,0 | O desencontro: cliente vira a esquina errada | plano alto, estatico | — |
| C05 | 17,0–21,0 | 4,0 | Dona do carrinho olhando a rua vazia. Batida de silencio | close, camera parada | — |
| C06 | 21,0–26,0 | 5,0 | A virada: um ponto de luz acende sobre a cena | push in lento | **pino** |
| C07 | 26,0–32,0 | 6,0 | Cidade do alto ao anoitecer, pinos acendendo | aereo lento | mapa + frase |
| C08 | 32,0–38,0 | 6,0 | Lojista ativa o ponto com um toque | over-the-shoulder | UI real |
| C09 | 38,0–44,0 | 6,0 | Cliente encontra: mapa, pagina, cardapio | macro do celular | UI real |
| C10 | 44,0–49,0 | 5,0 | Promocao e conversa direta no WhatsApp | detalhe de maos | UI real |
| C11 | 49,0–55,0 | 6,0 | O encontro. Cliente chega, e atendido | steadicam frontal | — |
| C12 | 55,0–62,0 | 7,0 | Amplitude: feira, praia, quiosque, van, entrega | montagem 5 planos | pinos |
| C13 | 62,0–70,0 | 8,0 | Cidade a noite, mapa vivo de pinos | aereo ascendente | mapa cheio |
| C14 | 70,0–78,0 | 8,0 | Card final: logo, slogan, CTA | fundo grafico | 100% pos |

---

## 4. Lista de cenas por bloco de producao

- **Bloco A · Rua ao entardecer (lojista):** C01, C05, C11 — mesma personagem,
  mesmo food truck, mesma luz.
- **Bloco B · Cliente na cidade:** C03, C04 — mesmo ator, mesma rua, mesma hora.
- **Bloco C · Celular em macro:** C02, C08, C09, C10 — mesma mao, mesmo aparelho,
  **tela sempre apagada**.
- **Bloco D · Aereo:** C06, C07, C13 — mesma cidade, mesmo horario azul.
- **Bloco E · Montagem de amplitude:** C12 — 5 microplanos.
- **Bloco F · 100% pos:** C14 — nao ha geracao de IA.

**Regra de continuidade:** cada bloco nasce de **um keyframe still aprovado**
(gerado antes, no `nano-banana-pro`), e so depois vai para image-to-video.
Prompt solto por cena devolve rosto diferente a cada take.

---

## 5. Narracao completa

**Cronometrada. 118 palavras. Ritmo de 1,9 palavra/s com respiros.**

| Cena | Locucao | Direcao de leitura |
| --- | --- | --- |
| C01 | *Todo dia, a mesma pergunta.* | baixa, quase sussurrada |
| C02 | *"Onde voces estao hoje?"* | leitura de mensagem, nao de anuncio |
| C03 | *O negocio se move. O endereco, nao acompanha.* | constatacao seca |
| C04 | *O post desce no feed. E o cliente desiste.* | pausa antes de "desiste" |
| C05 | *(silencio — so ambiente)* | — |
| C06 | *E se o seu ponto pudesse se mover com voce?* | primeira subida de energia |
| C07 | *Seu negocio se movimenta. Seu cliente tambem. A Moviki conecta os dois.* | tres frases, tres respiros |
| C08 | *Um toque, e voce esta no mapa. Em tempo real.* | firme, resolvido |
| C09 | *Quem esta perto encontra voce — com cardapio, fotos e horario.* | fluido |
| C10 | *Promocoes, cupons e conversa direta no WhatsApp. Sem comissao por venda.* | "sem comissao" com peso |
| C11 | *Um post envelhece em uma hora. Um ponto no mapa, nao.* | a frase do filme. Desacelerar. |
| C12 | *Food truck, feira, praia, quiosque, entrega. Se o seu negocio se move, ele cabe aqui.* | ritmo de lista, acelerando |
| C13 | *Um mapa vivo do comercio que acontece agora.* | amplo |
| C14 | *Moviki. O mapa inteligente dos negocios em movimento.* | assinatura, sem pressa |

### Direcao de voz

- **Voz recomendada:** feminina, 32–42 anos, timbre medio-grave, portugues do
  Brasil neutro com leve calor paulistano.
- **Referencia:** narracao de documentario de marca, nao de varejo. Zero
  entonacao de locutor de radio. Zero sorriso na voz.
- **Proibido:** exclamacao, aceleracao no CTA, "corre la", "nao perca".
- **Fluxo:** gravar primeiro uma **locucao TTS descartavel** para montar o
  animatic e travar o tempo; so depois contratar o locutor humano.
  **Locutar antes de travar o tempo e retrabalho garantido.**

---

## 6. Textos na tela

Poppins. Caixa alta nas frases-conceito, caixa mista nos descritivos.
Entram por **fade + subida de 12 px em 400 ms**, saem por fade de 250 ms.
Nenhum texto fica menos de 1,6 s em tela.

| Cena | Texto | Peso / corpo (base 1080p) | Cor | Posicao |
| --- | --- | --- | --- | --- |
| C02 | ONDE VOCES ESTAO HOJE? | SemiBold 600 / 64 px | `#F2F5F9` | inferior-esq., safe 8% |
| C03 | O NEGOCIO SE MOVE. | Bold 700 / 72 px | `#F2F5F9` | centro-baixo |
| C04 | O ENDERECO, NAO. | Bold 700 / 72 px | `#00D4FF` | centro-baixo |
| C07 | SEU NEGOCIO SE MOVIMENTA. | Bold 700 / 68 px | `#F2F5F9` | terco superior |
| C07 | SEU CLIENTE TAMBEM. | Bold 700 / 68 px | `#F2F5F9` | terco superior |
| C07 | A MOVIKI CONECTA OS DOIS. | Bold 700 / 68 px | `#00D4FF` | terco superior |
| C08 | Um toque. Voce no mapa. | Medium 500 / 44 px | `#F2F5F9` | canto inf.-dir. |
| C08 | TEMPO REAL | Bold 700 / 30 px, tracking +8% | `#00D4FF` | tag sobre pino |
| C09 | Cardapio · Fotos · Horario | Medium 500 / 40 px | `#F2F5F9` | rodape |
| C09 | moviki.com.br/seuapelido | Medium 500 / 36 px | `#00D4FF` | rodape |
| C10 | Promocoes · Cupons · WhatsApp | Medium 500 / 40 px | `#F2F5F9` | rodape |
| C10 | SEM COMISSAO POR VENDA | Bold 700 / 46 px | `#00D4FF` | centro |
| C11 | UM POST ENVELHECE. UM PONTO NO MAPA, NAO. | Bold 700 / 60 px, 2 linhas | `#F2F5F9` | centro |
| C12 | Feito para quem se move. | Medium 500 / 42 px | `#F2F5F9` | inferior |
| C14 | *(logo oficial Moviki)* | asset vetorial | — | centro |
| C14 | O mapa inteligente dos negocios em movimento | Medium 500 / 38 px | `#F2F5F9` | sob o logo |
| C14 | Comecar gratis agora | SemiBold 600 / 34 px | `#0D1B2A` sobre pilula `#00D4FF` | abaixo |
| C14 | 30 dias gratis · Sem cartao de credito | Medium 500 / 26 px | `#F2F5F9` | sob a pilula |
| C14 | moviki.com.br | Medium 500 / 30 px | `#00D4FF` | rodape |

**Regras nao negociaveis:**

- Todo texto dentro da **safe area de 10%**.
- Nenhum texto sobre area de alto detalhe: se o fundo brigar, entra
  **gradiente `#0D1B2A` a 0–70% de opacidade** por tras, nunca caixa solida.
- Contraste minimo 4.5:1 medido, sempre.
- **Legenda queimada** no corte 9:16 e no de 30 s. No master em lightbox,
  legenda `.vtt` ligavel.

---

## 7. Trilha sonora

| Tempo | Camada | Intencao |
| --- | --- | --- |
| 0–8 s | piano solo, notas espacadas, muito reverb | pergunta suspensa |
| 8–17 s | entra sub-bass em pulso lento | peso, dor |
| 17–21 s | **tudo cai. Quase silencio.** So ambiente de rua | o vazio da cena 5 |
| 21–26 s | arpejo sintetico sobe, filtro abrindo | virada |
| 26–32 s | bateria eletronica entra inteira | primeiro climax |
| 32–55 s | groove estavel, camadas somando | prova, progressao |
| 55–62 s | acelera, percussao dobra | amplitude |
| 62–70 s | cordas quentes + sintetizador | segundo climax, o maior |
| 70–78 s | resolve para pad e piano do inicio | assinatura, circulo fechado |

- **BPM 92.** Tonalidade maior. Sem vocal, sem palmas.
- **Busca (Artlist / Epidemic / Musicbed):** `cinematic corporate uplifting
  minimal piano pulse`, `hopeful technology build no vocals`, `documentary brand
  film emotional strings synth`. Filtrar 90–95 BPM e **faixa com stems**.
- **Licenca:** guardar o certificado junto do projeto. Reivindicacao de direito
  autoral no YouTube derruba anuncio.

### Desenho de som

- ambiente de rua ao entardecer (base continua, -28 dB)
- chapa quente / fritura no bloco A
- notificacoes na C02 — abafadas, tres em rapida sucessao
- clique haptico do toque na C08
- **`pin.wav` — assinatura sonora da marca.** Pop curto de sub + brilho agudo,
  220 ms, toca a cada pino que acende (C06, C07, C12, C13, C14).
  **Produzir uma vez e reaproveitar no app, nos Reels e no bumper.**
- ambiente urbano noturno na C13, reverb longo
- silencio absoluto de 300 ms antes do card final

### Mixagem

- Locucao a -12 LUFS, musica a -22 LUFS sob a locucao, ducking de 4 dB.
- Master a **-14 LUFS integrado, true peak -1 dBTP**.
- Entregar tambem **stem de musica+SFX sem locucao** — permite dublar depois.

---

## 8. Direcao visual

### Fotografia

- **Formato:** 3840x2160, 24 fps, entrega em 1920x1080.
- **Proporcao:** 16:9 limpo. **Nao usar tarja 2.39:1** — em lightbox de 620 px
  de altura a tarja come 30% da tela util.
- **Optica:** primas anamorficas vintage. 35 mm nos planos de rua, 85 mm nos
  closes, 24 mm nos aereos. T2.0–T2.8.
- **Profundidade rasa e constante.** A cidade vira bokeh de pontos de luz — que
  rima visualmente com o mapa de pinos.
- **Movimento:** so tres tipos. Dolly lateral lento, push-in lento e aereo
  ascendente. Zero whip pan, zero camera tremida, zero drone agressivo.

### Cor

| Uso | Hex | Onde |
| --- | --- | --- |
| Ciano de marca | `#00D4FF` | pinos, tags, palavras-chave, pilula do CTA |
| Azul de marca | `#0066FF` | gradiente do mapa, traco de conexao |
| Azul escuro | `#0D1B2A` | sombras, fundo do card final, gradiente de leitura |
| Claro | `#F2F5F9` | texto corrido, logo sobre escuro |

- Sombras puxadas para `#0D1B2A`, meios-tons neutros, **pele quente e
  preservada**. A unica fonte de calor sao as pessoas e as luzes praticas.
- **O ciano nunca vem da fotografia.** So existe na camada grafica. Regra dura:
  **nenhuma luz pratica ciano na cena gerada.**
- Grao filmico leve e uniforme em todo o filme, inclusive nas cenas graficas.
- **Proibido:** o glow laranja da arte original do Vik.

### Camada grafica

- **O pino** e o simbolo oficial, nunca redesenhado. Anima em tres tempos:
  escala 0 -> 110% -> 100% em 500 ms com ease-out; ondas de sinal expandindo em
  loop de 2,4 s, opacidade 40% -> 0%; flutuacao vertical de 4 px em 3 s.
- **Traco de conexao:** linha de 3 px, gradiente `#00D4FF` -> `#0066FF`,
  desenhada da esquerda para a direita em 700 ms.
- **Mapa:** estilo escuro, ruas em `#1A2B3F`, sem nome de rua legivel, sem marca
  de provedor em tela. Se o mapa real aparecer, **conferir a atribuicao antes de
  publicar.**
- **Toda UI e captura real**, composta sobre o celular com corner-pin.
  Nunca reconstruir interface em After Effects.

### Elenco e realismo

- Pessoas comuns, roupa de trabalho real, avental usado, mao com calo.
- **Rostos em plano fechado so quando necessarios.** Nos planos medios, preferir
  contraluz, perfil parcial e maos.
- A dona do carrinho da C01 e a mesma da C05 e da C11 — **e a protagonista.**

---

## 9. Prompts de geracao por cena

**Os prompts estao em ingles** porque os modelos de video respondem melhor a
ingles. Montar sempre como `STYLE BIBLE` + `prompt da cena` + `NEGATIVE`.
Confirmar o custo com `estimate_cost` antes de gerar.

### STYLE BIBLE (prefixo fixo de toda cena)

```
Cinematic live-action brand documentary, shot on ARRI Alexa 35, vintage
anamorphic prime lenses, shallow depth of field, natural film grain, 24fps
motion cadence, high dynamic range. Color grade: deep navy shadows, neutral
midtones, warm preserved skin tones, cool desaturated environment, no cyan
practical lights. Contemporary Brazilian urban setting. Real ordinary working
people, authentic imperfect skin texture, no makeup gloss, documentary
authenticity, unposed. Composition deliberately leaves clean negative space for
graphics to be added in post. Photorealistic, premium technology brand film.
```

### NEGATIVE (sufixo fixo de toda cena)

```
text, letters, words, captions, subtitles, logos, brand names, readable
signage, numbers, phone screen content, app interface, UI, visible map on
screen, cartoon, illustration, 3D render, anime, plastic skin, uncanny face,
deformed hands, extra fingers, warped anatomy, stock-photo smile, neon
overload, magenta or purple cast, orange glow, oversaturated teal-orange,
lens flare spam, whip pan, shaky action cam, motion smear, low resolution,
watermark, split screen, collage
```

> **Atencao:** o `nano-banana-pro` **rejeita o parametro `negative_prompt`**
> (400 VALIDATION_ERROR). Nos stills, o bloco acima entra dentro do proprio
> prompt como `STRICTLY AVOID: ...`. Ver [[ARQ - Armadilhas de geracao por IA]].

---

### C01 · 4,0 s — A rua nova

- **Ambiente:** rua residencial arborizada, calcada larga, fim de tarde, hora azul comecando.
- **Personagem:** mulher, 38 anos, brasileira parda, cabelo preso, avental gasto.
- **Iluminacao:** contraluz quente residual ao fundo; praticas do trailer acendendo durante a tomada.
- **Composicao:** trailer no terco direito, rua vazia nos dois tercos esquerdos — **esse vazio e o espaco grafico.**
- **Camera:** dolly lateral lento esquerda -> direita, 35 mm, altura de peito, T2.0.
- **Continuidade:** **keyframe mestre do Bloco A.**

```
Late golden hour on a quiet tree-lined residential street in Brazil. A compact
white food trailer parked at the curb, its warm tungsten string lights and
service window lights flickering on during the shot, becoming the main light
source as the sky settles into deep blue. A 38-year-old Brazilian woman with
tied-back dark hair, worn work apron over a plain t-shirt, steps back from the
counter and looks down the empty street. Slow lateral dolly left to right, 35mm
anamorphic lens, chest height, T2.0, very shallow depth of field, background
street melting into soft round bokeh. The left two thirds of the frame stay
empty and uncluttered. Warm backlight rim on her shoulders, cool blue ambient
fill. Calm, expectant, the beginning of a shift.
```

- **Edicao:** nao usar o primeiro nem o ultimo 0,3 s do take — e onde a IA deforma.

---

### C02 · 4,0 s — A pergunta

- **Personagem:** so as maos e o antebraco. **Sem rosto.**
- **Tela do celular preta.** A luz fria simula o brilho; a tela real entra em pos.
- **Camera:** macro 85 mm, tripe fixo, T2.2.
- **Continuidade:** mesma mao, mesmo aparelho em C08, C09 e C10.

```
Extreme close-up macro shot of a working woman's hands holding a modern
smartphone with a completely black powered-off screen. Inside a food trailer at
dusk, warm out-of-focus practical lights and metal surfaces reflecting far
behind. Cool soft light falls on her hands and the phone edges as if the screen
were glowing, but the screen itself stays pure black and reflective. Her thumb
scrolls down once. 85mm macro anamorphic, locked-off tripod, T2.2, razor
shallow focus on the device, background dissolved into warm bokeh. Upper third
of frame intentionally empty. Worn nails, small kitchen scar on the index
finger, real hands. Quiet, routine, repetitive.
```

- **Edicao:** baloes em motion, nao print. Texto: `Oi, onde voces estao hoje?` ·
  `To passando ai, ta aberto?` · `Voces vem no bairro hoje?`. Um a cada 400 ms.

---

### C03 · 5,0 s — A busca

- **Personagem:** homem, 27 anos, brasileiro negro, casual, mochila.
- **Composicao:** terco esquerdo, olhar fora de quadro para a direita —
  **direcao oposta a da C01**, e o que constroi o desencontro.

```
Dusk on a busy Brazilian commercial street corner. A 27-year-old Black
Brazilian man in casual after-work clothes with a backpack stands on the
sidewalk, turning ninety degrees as he scans the street, then glancing down at
a smartphone with a black powered-off screen, then looking up again. Warm
sodium streetlights mix with cool shop-window light; a passing car headlight
rims his shoulder. Very subtle handheld, 35mm anamorphic, eye level, T2.0,
pedestrians behind him dissolved into bokeh. He occupies the left third, his
gaze directed off-frame to the right. Contained impatience, the moment before
giving up.
```

- **Edicao:** o feed rolando entra em pos sobre a tela preta.
  **O post que some e a ideia da cena.**

---

### C04 · 4,0 s — O desencontro

- **Composicao:** **os dois no mesmo quadro, sem se ver.** Ele no canto inferior
  esquerdo, o trailer no superior direito. O vazio no meio e o assunto.

```
High elevated static shot looking down at a Brazilian city block at blue hour.
In the lower left, a small figure of a man with a backpack walks and turns the
corner away from camera. In the upper right of the same frame, two hundred
meters away, a lit food trailer glows warm and isolated among cool blue
streetlights. Neither is aware of the other. Empty asphalt and rooftops fill
the space between them. 24mm anamorphic, locked off, deep but still soft focus,
cool blue night grade with one warm point of light. Quiet irony, near miss.
```

- **Edicao:** manter 0,8 s do quadro **depois** que ele sai. O vazio e o ponto.

---

### C05 · 4,0 s — O silencio

```
Medium close-up of the same 38-year-old Brazilian woman in a worn apron,
standing behind the counter of her food trailer at night. She looks down the
empty street, exhales, and wipes her hand on the apron. Warm tungsten practical
light hits her face frontally; the deep blue empty street behind her falls off
into cool darkness and soft bokeh. 85mm anamorphic, completely locked-off
camera, T2.0, razor shallow focus on her eyes. She sits slightly left of
center, the empty street filling the right of the frame. Honest tiredness, no
melodrama, no tears, quiet dignity.
```

- **Transicao:** **fade rapido para preto de 300 ms.** O unico do filme.
- **Edicao:** a musica cai por completo. **Nao encurtar esta cena para ganhar
  segundos** — ela e o que faz a virada valer.

---

### C06 · 5,0 s — O pino acende

```
The same empty Brazilian street at night, now with no people in frame. A single
small point of light sits in the mid-ground, growing slightly brighter through
the shot, its glow spilling faintly onto wet asphalt. Deep blue night grade,
distant streetlights rendered as soft round bokeh. Slow push-in, 50mm
anamorphic, T2.4, twelve percent move over five seconds, everything else
perfectly still. Generous empty air in the upper third of the frame. Cinematic,
suspended, the moment something switches on.
```

- **Edicao:** o pino entra no **frame 60**, no primeiro `pin.wav` do filme.
  Esse frame e o nascimento da marca no filme — nao antecipar.

---

### C07 · 6,0 s — O mapa vivo

```
Slow aerial drone shot over a mid-sized Brazilian city at blue hour, drifting
right to left. Legible street grid, low buildings, no recognizable landmark, no
signage. City lights just coming on, warm points scattered across a cool blue
grid, last band of light on the horizon in the upper third. 24mm anamorphic
equivalent, medium altitude, steady constant drift, no rotation, no tilt. Clean
sky in the upper third of the frame with generous negative space. Expansive,
revelatory, cinematic scale.
```

- **Edicao:** pinos acendem em cascata, **um a cada 180 ms**, do centro para
  fora. A frase-conceito entra em tres tempos, uma linha por respiro da locucao.
  **Nunca as tres linhas juntas.**

---

### C08 · 6,0 s — Um toque

```
Over-the-shoulder shot inside a food trailer at night. A 38-year-old Brazilian
woman in a work apron holds a smartphone with a pure black powered-off screen;
her thumb presses the screen once, deliberately, then her hand relaxes. Warm
tungsten practical light from the left, cool soft light on her hands as if from
the screen. 50mm anamorphic, slight high angle over her shoulder, T2.2, six
percent push-in, shallow focus with the trailer interior dissolved behind. Her
face partially visible in profile, calm and focused. Small, simple, confident
gesture.
```

- **Edicao:** captura real do painel composta com corner-pin. O **pino aparece
  no mapa no mesmo frame do toque** — a simultaneidade e o argumento de "tempo
  real". Tag `TEMPO REAL` entra 400 ms depois, presa ao pino.

---

### C09 · 6,0 s — O cliente encontra

```
Macro close-up of a young Brazilian man's hands holding a smartphone vertically
on a city sidewalk at night, screen pure black and reflective. His thumb swipes
upward twice, unhurried. Cool shop-window light and street bokeh dissolved
completely behind him. 85mm macro anamorphic, near-imperceptible handheld,
T2.5, razor shallow focus on the device. The phone sits centered with generous
clean margin all around it. Calm discovery, unhurried attention.
```

- **Edicao:** captura real da **pagina publica** (`moviki.com.br/apelido`), em
  sequencia: mapa com o pino -> capa do negocio -> cardapio. 1,8 s por estado.
  **Zero zoom de UI que a interface real nao faz.**

---

### C10 · 5,0 s — Promocao e contato

```
Continuation macro close-up of the same young man's hands and smartphone on the
same sidewalk, screen pure black. His thumb taps once, then his hand lowers
slightly as if he is about to walk. Same cool shop-window bokeh behind, same
soft frontal light. 85mm macro anamorphic, T2.5, slightly tighter framing than
before, shallow focus. Decision made, about to move.
```

- **Edicao:** captura real do cupom e do botao de WhatsApp. **`SEM COMISSAO POR
  VENDA` entra em ciano, sozinha, por 1,6 s.** Unico argumento comercial duro do
  filme — nao dividir a atencao com outro texto.

---

### C11 · 6,0 s — O encontro

```
Medium frontal shot at the food trailer at night, now with a short queue. The
38-year-old Brazilian woman in the apron hands a paper-wrapped order across the
counter to the 27-year-old man with the backpack. Brief eye contact, a short
genuine smile from both, no posing. Warm tungsten practical lights dominate,
steam rising from the griddle catching the backlight, cool blue night behind.
Steadicam with a very slow push in, 40mm anamorphic, T2.0, queue behind
dissolved into warm bokeh. Human warmth, real service, unstaged.
```

- **Edicao:** `UM POST ENVELHECE. UM PONTO NO MAPA, NAO.` entra aqui, sobre o
  momento mais quente do filme. Contraste proposital entre argumento racional e
  imagem emocional — e o que fixa a frase.

---

### C12 · 7,0 s — Amplitude (5 microplanos)

| Plano | Dur | Conteudo | Camera |
| --- | --- | --- | --- |
| C12a | 1,4 s | barraca de feira livre de manha, frutas, mao entregando sacola | 35 mm, dolly curto |
| C12b | 1,4 s | carrinho de acai/sorvete na orla, fim de tarde, vento | 50 mm, lateral |
| C12c | 1,4 s | quiosque/tapioca em praca, luzes acendendo | 35 mm, push-in |
| C12d | 1,4 s | van de servico/entrega estacionando em rua residencial | 24 mm, estatico |
| C12e | 1,4 s | motoboy de entrega local saindo, visto de costas | 50 mm, panoramica curta |

```
[C12a] Early morning at a Brazilian open-air street market. A vendor's hands
pass a bag of fruit across a colorful stall. Soft warm morning light, cool
shadow, canvas awning above. 35mm anamorphic, short dolly move, T2.2, shallow
focus, background stalls dissolved into bokeh. Documentary, unposed.

[C12b] Late afternoon on a Brazilian beachfront promenade. A small acai and ice
cream cart with an open awning, sea breeze moving the fabric, a vendor serving.
Warm low sun from behind, cool blue ocean out of focus in the distance. 50mm
anamorphic, lateral move, T2.0, very shallow focus. Relaxed, sunlit, authentic.

[C12c] Dusk in a small Brazilian town square. A tapioca and snack kiosk with
its string lights just turning on, a small group waiting nearby. Warm practical
lights against deep blue evening sky. 35mm anamorphic, slow push-in, T2.2,
shallow focus, trees behind in soft bokeh. Community, warmth, evening.

[C12d] A compact white service van parking on a quiet residential Brazilian
street in late afternoon. A worker in a uniform polo steps out and slides the
side door open. Warm side light, long shadows on asphalt. 24mm anamorphic,
locked-off static shot, T2.8, moderate depth. Practical, ordinary, real.

[C12e] A local delivery rider on a small motorcycle pulling away from a curb in
a Brazilian neighborhood at dusk, seen from behind, insulated bag on the back.
Warm streetlight, cool blue sky. 50mm anamorphic, short pan following him,
T2.0, shallow focus. Movement, departure, energy.
```

- **Edicao:** **um pino ciano acende em cada plano**, sempre 300 ms antes do
  corte, com o `pin.wav`. Isso transforma cinco planos soltos em um sistema.
- **Regra de posicionamento (aprendida na producao):** **autenticidade nao
  significa precariedade.** Ver [[ARQ - Decisoes do filme institucional]].

---

### C13 · 8,0 s — A escala

```
Slow ascending aerial over the same mid-sized Brazilian city, now full night.
Starting close over one neighborhood of low buildings and gradually rising and
pulling back to reveal the whole city grid alive with thousands of warm light
points. Deep blue-black sky, no visible horizon glow blowout. 24mm anamorphic
equivalent, constant slow vertical rise with slight backward move, absolutely
no rotation. Clean dark sky area in the upper portion of frame. Vast, calm,
cinematic, breathing.
```

- **Transicao:** os pinos convergem para o centro e **se fundem no simbolo do
  logo**, que ja esta no lugar exato do card final. Nao usar fade para preto.
- **Edicao:** pinos acendem em ondas concentricas, ~40 em 3 s, tapering no fim.
  **Nao encher a tela** — mapa saturado le como poluicao, nao como escala.

---

### C14 · 8,0 s — Assinatura

**Sem geracao de IA. 100% pos-producao.**

- **Fundo:** `#0D1B2A` solido com gradiente radial sutil para `#12243A`, mais
  grao filmico igual ao do resto do filme.
- **Elementos, em ordem:**
  1. `70,0 s` — os pinos da C13 convergem e formam o simbolo oficial.
  2. `71,2 s` — o logotipo completo se desenha da esquerda para a direita.
  3. `72,5 s` — as ondas de sinal do pino pulsam **uma unica vez**.
  4. `73,0 s` — slogan entra por fade sob o logo.
  5. `74,5 s` — pilula de CTA ciano sobe 12 px com fade.
  6. `76,5 s` — `moviki.com.br` no rodape.
  7. `77,2 s` — tudo estabiliza. Ultimos 0,8 s em quadro parado.
- **Audio:** silencio de 300 ms antes do card, ultima nota de piano em 74,0 s,
  reverb longo ate o fim.
- **Regra:** o quadro final fica **parado e legivel** por 0,8 s. E o frame que
  vira thumbnail e o que o espectador fotografa.

---

## 10. Cortes derivados

| Corte | Duracao | Onde | Cenas | Observacao |
| --- | --- | --- | --- | --- |
| **Master** | 78 s | lightbox da landing, YouTube, apresentacoes | todas | com locucao e legenda ligavel |
| **Heroi** | 8 s, mudo, loop | topo de `moviki.com.br` | C06 + C07 | WebM <= 1,5 MB, sem texto |
| **Pago** | 30 s | Meta Ads, Google | C02, C03, C04, C07, C08, C09, C10, C14 | comeca na C02; legenda queimada |
| **Vertical** | 15 s, 9:16 | Reels, Stories, TikTok | C02, C04, C07, C11, C14 | texto refeito, corpo +40% |
| **Bumper** | 6 s | YouTube pre-roll | C06, C07, C14 | so a frase-conceito e o logo |

**Regra do 9:16:** nao usar reenquadre automatico. Os planos foram compostos em
16:9 com espaco grafico lateral — no vertical esse espaco some e o texto vai
para cima ou para baixo do sujeito, nunca ao lado.

---

## 11. Entrega tecnica e impacto na landing

- **Heroi:** `hero-loop.webm` (VP9) + fallback `hero-loop.mp4` (H.264).
  `<= 1,5 MB`, 8 s, sem audio, `muted playsinline loop autoplay preload="none"`
  com `poster` em WebP `<= 60 KB`. **O poster e o que entra no LCP.**
- **Master:** `institucional.mp4` (H.264, 1080p, ~8 Mbps, AAC 192 kbps) +
  `.webm`. **Nao carregar no `load` da pagina.** Injetar o `<video>` so no
  clique de "Ver como funciona".
- **Legenda:** `institucional-pt.vtt` no master. Legenda queimada nos cortes
  social e pago.
- **Hospedagem:** o MP4 do master **nao vai no repositorio**.
  **Decisao tomada: YouTube nao listado em lightbox** (banda zero).
  Consequencia obrigatoria: `frame-src https://www.youtube-nocookie.com` na CSP.
- **Verificacao obrigatoria:** rodar Lighthouse antes e depois.
  **Se o LCP mobile piorar mais que 0,2 s, o loop do heroi sai** e fica so o
  poster com o botao.
- Marca de versao: `window.MOVIKI_VERSAO` alterada no mesmo commit, e conferir
  **no dominio**, nao no GitHub.

---

## 12. Conformidade — o que o filme nao pode dizer nem mostrar

Regra de ouro do projeto: **descrever a regra, nunca o resultado.**

**Proibido no roteiro, na locucao, no texto de tela e na descricao do anuncio:**

- qualquer numero de faturamento, lucro, aumento de venda ou de clientes
- "cresca", "fature mais", "aumente suas vendas", "renda extra", "garantido",
  "sem risco", "para sempre"
- dinheiro em quadro: nota, moeda, maquininha com valor, grafico subindo
- prova social inventada: nota, contador de usuarios, numero de negocios,
  depoimento nao gravado com pessoa real e autorizacao assinada
- comparacao nominal com concorrente
- promessa de posicao, alcance ou entrega
- nenhuma mencao a valor de comissao

**Permitido, porque e fato de produto verificavel:** "sem comissao por venda",
"30 dias gratis", "sem cartao de credito", "em tempo real", "cardapio, fotos e
horario", "conversa direta no WhatsApp".

**Direito de imagem:** toda pessoa em cena gerada por IA e ficticia e nao pode
ter semelhanca com pessoa real identificavel. Se entrar filmagem real de
lojista, **termo de cessao assinado antes da publicacao**, sem excecao.

**Nome de negocio em tela:** nao usar o nome MOVIKI como nome do
estabelecimento, nao copiar marca real, nao usar dado de pessoa real, nao expor
telefone pessoal.

---

## 13. Medicao (GA4 · G-GG5CSQZVGH)

| Evento | Quando dispara | Parametros |
| --- | --- | --- |
| `video_start` | play do master no lightbox | `video_id`, `origem` |
| `video_progress` | 25% · 50% · 75% | `video_id`, `percent` |
| `video_complete` | fim do master | `video_id` |
| `video_cta_click` | clique no CTA dentro/apos o video | `video_id`, `destino` |
| `hero_loop_view` | loop do heroi visivel > 3 s | — |

**A pergunta que a medicao precisa responder:** quem assiste o video converte
mais em `cta_painel` do que quem nao assiste? Se a resposta for nao depois de
volume suficiente, o problema esta no roteiro ou no posicionamento do player —
nao em produzir mais video.

Ver [[P01 - Aquisicao - campanha de trafego pago]].

---

## 14. Plano de producao no Kairogen

**Keyframe primeiro, video depois.** Para cada bloco: gerar o still no
`nano-banana-pro`, aprovar personagem, luz e enquadramento, e so entao animar
por image-to-video.

### Ordem de execucao

1. Animatic e TTS descartavel. **Travar o tempo antes de gastar em qualidade.**
2. Keyframes stills dos blocos A, B, C, D.
3. Takes finais, comecando pelo Bloco A.
4. Montagem, camada grafica, captura de UI real, cor.
5. Locucao humana sobre o corte travado.
6. Mixagem, masterizacao a -14 LUFS, exportacoes.

---

## 15. Divergencias entre o plano e a producao real

Registrado em 2026-08-31, apos as 13 cenas geradas. **Este bloco vale mais que
o plano acima onde os dois discordarem.**

| Item | Plano (29/08) | Producao real |
| --- | --- | --- |
| Modelos | Kling O1, Kling V3 Pro, Seedance V1.5 | **`veo-3-1` em tudo** + `nano-banana-pro` nos stills |
| Custo estimado | R$ 45 a R$ 75 | **1.308 creditos** consumidos, 150 geracoes |
| Metodo | 3 variacoes por cena | **1 take por cena**, keyframe aprovado antes |
| Duracao das cenas | valores fracionados (5,0 / 6,0 / 7,0) | **Veo so aceita 4, 6 ou 8 s** — 5 s nao existe |
| C07 | cidade + comerciante | **so aereo**, sem comerciante, sem barraca, sem celular |
| C08 | geracao propria | **take reaproveitado**, sem geracao nova |
| C10 | geracao propria | **zero Kairogen**, 100% captura real em pos |
| C12 | 5 planos gerados direto | **5 keyframes aprovados** e depois animados |
| Timeline | 78 s | **74,1 s** na montagem atual |
| CDN bloqueado | armadilha permanente | contornado: `get_generation` devolve a imagem inline |

Detalhe completo em [[R - Filme institucional - inventario de takes]] e
[[ARQ - Armadilhas de geracao por IA]].

---

## Ligacoes

[[P13 - Video institucional da landing]] · [[R - Filme institucional - biblia visual e continuidade]] ·
[[R - Filme institucional - inventario de takes]] · [[R - Filme institucional - gate de assets]] ·
[[R - Filme institucional - conta demo]] · [[ARQ - Armadilhas de geracao por IA]] ·
[[ARQ - Decisoes do filme institucional]] · [[P01 - Aquisicao - campanha de trafego pago]] ·
[[R - Regras de ouro]] · [[R - Checklist conformidade Meta e Google]] ·
[[A8 - Conteudo e Social]] · [[A7 - Aquisicao e Midia Paga]] · [[A11 - Marca e Design System]]
