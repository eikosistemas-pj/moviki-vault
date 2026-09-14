---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [filme-hero, producao, ffmpeg, kairogen, elevenlabs, playwright]
atualizado: 2026-09-13
---

# R — Live: folha de produção do filme hero

Folha da **v6 aprovada** em 13/09/2026. Substitui a versão escrita em 12/09
(13 cenas, 2:26, voz Cambero, 136 créditos). Decisões editoriais em
[[ARQ - Filme hero v6 aprovado 13092026]]; erros e consertos em
[[ARQ - Incidentes de montagem do filme hero]]; regras em
[[R - Regras de ouro de producao de video]].

## Entrega final

| Item | Valor |
| --- | --- |
| Duração | **2:38 — 158,0 s** |
| Formato | 1920x1080, 30 fps, H.264 |
| Áudio | AAC 44.1 kHz **estéreo** em todas as cenas |
| Arquivo | `MOVIKI-hero-v6.mp4` — 25 MB, crf 27 |
| Voz | **Malu** `fhtZMBwha5du5OxuvexO` |
| Grafia para o motor | **"Mo-víki"** |

## As 16 cenas, na ordem, com duração congelada

| Cena | Duração | Origem |
| --- | ---: | --- |
| C01 Você já tem o que vender | 6,5 s | clipe IA |
| C02 O dia que não veio | 16,6 s | clipe IA em 3 enquadramentos + chuva sintetizada |
| C03 Uma foto não responde | 8,1 s | post animado + clipe IA dentro do cartão |
| C04 E se a sua vitrine pudesse falar? | 4,2 s | tipografia |
| C05 Você mostra, a pessoa pergunta | 12,7 s | 2 clipes IA |
| C06 Começa no painel que você já usa | 11,0 s | UI real |
| C07 O preço fica na tela | 12,8 s | UI real |
| C08 Agora a vitrine responde | 9,4 s | UI real |
| C09 Pix dentro da live (Enterprise) | 13,7 s | UI real |
| C10 Estou aqui agora | 6,7 s | mapa + UI real |
| C11 Mesmo dia, outro resultado | 7,3 s | clipe IA + chuva |
| **D1** O palco e o megafone | 12,8 s | imagem do ChatGPT animada |
| **D2** Serve para o seu caso | 9,9 s | sobras de C05 |
| **D3** Já está no seu teste grátis | 9,8 s | UI real |
| C12 Do mapa para o ao vivo | 8,0 s | UI real |
| C13 Assinatura | 8,5 s | pós |

**Ordem de montagem** (`lfinal.txt`): I01 · I02 · I03 · I04 · I05 · I06 · I07 ·
I08 · I09 · I10 · I11 · **ID1 · ID2 · ID3** · I12 · I13.

## Pipeline

Uma pasta por etapa, em `hero/`:

- `clipes/` — clipes do Kairogen, `k_*.mp4`
- `voz/` — um MP3 por cena, `m_c01`..`m_c13`, `m_d1`..`m_d3`, mais `trilha_a` e `trilha_b`
- `ui/` — capturas do produto: `publico.webm` (58,08 s) e `estudio.webm` (22,88 s)
- `mapa/aprovado/textura-tratada.png` — o mapa desenhado, porque os tiles não
  sobem no sandbox
- `cenas/` — placas, montagem e master

Nomenclatura dentro de `cenas/`: `c<nn>_mudo.mp4` (vídeo sem som) →
`H<nn>.m4a` (áudio da cena, já estéreo) → `I<nn>.mp4` (cena com som, pronta para
concatenar).

## Parâmetros que não se mudam sem refazer tudo

**Grade dos clipes de IA**

```
eq=contrast=1.07:saturation=1.06,
curves=r='0/0.015 0.5/0.5 1/0.985':b='0/0.03 0.5/0.5 1/0.975',
vignette=PI/5.2,noise=alls=5:allf=t+u
```

**Grade das cenas de UI e tipografia** — `noise=alls=4:allf=t+u,vignette=PI/6`.
Serve para amarrar o grão com o resto; sem isso a UI parece colada por cima.

**Composição do celular** (todas as cenas de UI)

```
[1:v]scale=440:953,setsar=1,pad=1920:1080:1120:64:color=black@0[w];
[2:v]format=gray[mk];[w][mk]alphamerge[scr];
[0:v][4:v]overlay=0:0[b1];[b1][scr]overlay=0:0[b2];[b2][3:v]overlay=0:0,format=yuv420p[v]
```

Mockup gerado por `fone2.py`: tela 440x953 em (1120,64), corpo 476x989 em
(1102,46), raios 54/36, 3x de supersampling. Saídas `mask.png`, `moldura.png` e
`sombra.png`.

**Mixagem da trilha**

```
[0:a]aformat=fltp:44100:stereo,asplit=2[nar][key];
[1:a]...atrim=0:37.5,afade=t=out:st=34.5:d=3,volume=0.62[a1];
[2:a]...volume=0.55,adelay=35400|35400:all=1,afade=t=in:st=35.4:d=2.5[a2];
[a1][a2]amix=inputs=2:duration=longest:normalize=0[mus];
[mus][key]sidechaincompress=threshold=0.03:ratio=9:attack=15:release=350:makeup=1[musd];
[nar][musd]amix=inputs=2:duration=first:normalize=0,alimiter=limit=0.95[out]
```

A virada de trilha cai em **0:35**, na cena C04 — pedido do Paulo, e é o ponto em
que o filme deixa a dor e começa a empolgar. O `sidechaincompress` usa a narração
como chave e abaixa a música sozinho quando ela fala.

**Chuva sintetizada** (C02 em 0,16 e C11 em 0,10)

```
anoisesrc=c=pink:r=44100:a=0.9 → highpass=f=700,lowpass=f=8500,tremolo=f=0.4:d=0.15,volume=V
```

Nada de banco de sons: licença para cumprir, atribuição para dar e risco de
Content ID derrubar o vídeo.

**C02 — três enquadramentos do mesmo clipe, em velocidade natural**

| Trecho | Recorte |
| --- | --- |
| A | `trim=start=4.6:duration=6.56`, quadro cheio |
| B | `trim=start=6.0:duration=5.0`, `crop=iw*0.52:ih*0.52:0:ih*0.12` (janela e chuva) |
| C | `trim=start=7.0:duration=5.04`, `crop=iw*0.56:ih*0.56:iw*0.40:ih*0.06` (rosto) |

**C03 — o post**

- Cartão **670x670** em (196,206) sobre a placa de fundo; a moldura antiga do
  cartão quadrado fica exatamente coberta.
- Área da foto **670x378** em (196,288), 16:9 inteiro, sem recorte lateral.
- Clipe `k_c03.mp4` (seedance-v1-pro, 5,04 s, geração `6aa64b4f043d2bf3c7581bd5`)
  em laço **ida-e-volta** para cobrir os 8,1 s sem esticar e sem congelar.
- `delogo=x=478:y=250:w=50:h=66` remove a logo da maçã do aparelho.
- Balões de pergunta em 1,3 / 2,8 / 4,3 / 5,8 s; título a partir de 5,6 s.

## Kairogen — o que vale saber antes de gerar

- Modelo `seedance-v1-pro`, imagem-para-vídeo. Referência em
  `extra_params.referenceImages`. `cameraFixed: true`.
- **O aspecto vai em `extra_params.aspectRatio`** — o argumento genérico
  `aspect_ratio` é ignorado e o endpoint de status sempre devolve "16:9".
- **31 créditos por 10 s a 720p** (~3,1 créditos/s). Música: 5 créditos por 42 s
  e 15 créditos por 130 s.
- **Limite de 4 vídeos simultâneos** e 429 quando as chamadas vêm coladas.
  Espaçar ~50 s entre lotes.
- **`cdn.kairogen.ai` é bloqueado pelo proxy do ambiente.** Todo asset gerado
  precisa ser baixado pelo Paulo e anexado de volta; imagem de referência sobe
  pelo widget `open_upload_reference_widget`.

## Captura de UI — o deslocamento do Playwright

A gravação do Playwright **começa antes** do `t0` do roteiro de teste. Medido
3,8 s, e depois **4,6 s** quando o arquivo da câmera cresceu. Toda janela de
corte sobre a captura precisa ser deslocada por esse valor.

**Como medir:** varrer os quadros procurando a faixa laranja da oferta e usar o
quadro em que ela aparece como marco. Refazer a medição sempre que a captura
mudar.

O Chromium do Playwright **não decodifica H.264** — a fonte de câmera tem que ser
**VP9/WebM**.

## Fontes que precisam estar anexadas para refazer qualquer corte

| Pacote | Conteúdo |
| --- | --- |
| `hero-fontes-1-voz-e-trilha.zip` | 16 MP3 da Malu (`m_c01`..`m_c13`, `m_d1`..`m_d3`) + `trilha_a.mp3` + `trilha_b.mp3` |
| `hero-fontes-2-ui-e-mapa.zip` | `publico.webm`, `estudio.webm`, `textura-tratada.png` |
| `hero-fontes-3-clipes-a.zip` | `k_c01`, `k_c02b`, `k_c03` |
| `hero-fontes-4-clipes-b.zip` | `k_c05a`, `k_c05b` |
| `hero-fontes-5-clipes-c.zip` | `k_c11`, `k_d1` |
| `MOVIKI-hero-v6.mp4` | o master aprovado |

## Ligações

- [[A13 - Modo Live]]
- [[A11 - Marca e Design System]]
- [[ARQ - Filme hero v6 aprovado 13092026]]
- [[ARQ - Incidentes de montagem do filme hero]]
- [[R - Regras de ouro de producao de video]]
- [[R - Regras de ouro de producao de cortes]]
- [[R - Voz oficial das videoaulas]]
- [[R - Retomada live parte 02]]
- [[P26 - Cortes do filme hero - vertical e pago]]
- [[P27 - Publicacao do filme hero no YouTube]]
