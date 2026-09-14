---
type: decisao
status: concluido
area: A13 - Modo Live
tags: [filme-hero, live, video, kairogen, elevenlabs, conformidade]
atualizado: 2026-09-13
---

# ARQ — Filme hero v6 aprovado 13/09/2026

Aprovado pelo Paulo em 13/09/2026. Fecha a produção iniciada em 12/09.
Parâmetros de montagem em [[R - Live - Folha de producao do filme hero]];
o que deu errado no caminho em [[ARQ - Incidentes de montagem do filme hero]].

## O que é

Filme institucional do Modo Live.

| Item | Valor |
| --- | --- |
| Duração | **2:38 — 158,0 s** |
| Formato | 1920x1080, 30 fps, H.264 |
| Áudio | AAC 44.1 kHz estéreo |
| Arquivo | `MOVIKI-hero-v6.mp4` — **25 MB**, crf 27 |
| Voz | Malu `fhtZMBwha5du5OxuvexO` |

Arco narrativo: **dia de chuva**. O trabalho está pronto e o dia não vem (C02);
o jeito antigo não responde (C03); a virada (C04); o que é vender ao vivo
(C05–C10); o mesmo dia com outro resultado (C11); **bloco de decisão** (D1–D3);
reposicionamento e assinatura (C12–C13).

Conceito-mãe: "E se a sua vitrine pudesse falar?". Assinatura proprietária:
**"Moviki. Do mapa para o ao vivo."**

## As três decisões que definiram o filme

**1. "Fatal" vem de remover objeção, não de explicar mais.**
O Paulo pediu um vídeo "fatal na questão de decisão do cliente". A resposta não
foi mais argumento — foi um **bloco de decisão** de 32,5 s (D1, D2, D3) colocado
depois da recompensa emocional e antes da assinatura, cada cena derrubando uma
objeção específica. Aprovado pelo ChatGPT e pelo Paulo.

**2. D1 assume, em voz alta, que a MOVIKI não entrega audiência pronta.**
Formulação aprovada: **"a MOVIKI é o palco, o megafone você já tem"**. É coerente
com a decisão de ensinar o lojista a trazer a própria audiência, e é o que impede
o filme de virar promessa de alcance automático. Não pode virar claim de
audiência garantida, alcance automático ou resultado garantido.

**3. D3 pode dizer que a live funciona no teste grátis — foi conferido no código.**
`moviki/api/live.js`, linha 226: `if (periodo === 'trial') return NIVEIS.premium;`
O teste grátis de 30 dias roda a live em nível Premium (60 min, 5 itens na
sacolinha). O Pix dentro da live segue Enterprise (`ehEnterprise` em
`moviki-robo/lib/checkout.js`). O `index.html` já diz "30 dias do plano Pró de
graça, sem cartão".

## Voz

Trocada de **Cambero** (`u4nnk7CtuMd84PLhiRN9`) para **Malu**
(`fhtZMBwha5du5OxuvexO`) — a mesma voz oficial das videoaulas. O motivo é marca:
o lojista ouve a mesma pessoa no anúncio, no painel e na Academia.

Efeito colateral que salvou a montagem: **a Malu é ~20% mais rápida que o
Cambero**, e foi isso que absorveu os +36 s do bloco de decisão sem o filme
inflar.

Grafia obrigatória para o motor: **"Mo-víki"**. Sem isso a voz lê "MÓviki". A
grafia certa fica na legenda; a fonética vale só no texto que vai para o motor.

## Escolhas visuais que ficam

- **C03 virou um post de verdade.** Cabeçalho com avatar e perfil, foto,
  curtidas e comentários, legenda e "há 2 minutos". Dentro da foto, a confeiteira
  fotografando o bolo, animada, em laço ida-e-volta. O argumento da cena ("uma
  foto não responde") fica mais forte com o post inteiro em quadro do que com a
  foto sozinha.
- **Nada de corte retrato nos clipes.** A fonte é plano fechado — cortar em
  retrato fecha ainda mais e come o produto na lateral. O quadro 16:9 inteiro
  dentro do post entrega mais personagem do que qualquer recorte.
- **A logo da maçã do celular foi removida** com `delogo`, para o filme não fazer
  propaganda de aparelho.
- **O celular parado.** Mockup frontal, sem deriva de câmera nas cenas de UI. O
  mockup 3D com movimento foi reprovado: "parece de brinquedo".

## Custos

Kairogen/Seedance: **31 créditos por 10 s a 720p** (~3,1 créditos/s). Música: 5
créditos por 42 s e 15 créditos por 130 s.
**A cena D2 foi montada com sobras dos clipes do food truck e do barbeiro — zero
crédito extra.**

O plano de 12/09 previa 136 créditos de geração sobre um saldo de 309, com voz
Cambero e 13 cenas em 2:26. A v6 saiu com 16 cenas e 2:38 sem estourar, porque a
voz nova é mais rápida e a D2 saiu de sobras.

## O que não entrou

- Nenhuma promessa de faturamento, de número de vendas ou de resultado.
- Nenhuma sugestão de que basta ligar a live para aparecer audiência.
- A enumeração de segmentos em C05 saiu: "Serve para comida, roupa, artesanato,
  beleza, serviço" virou **"Serve para quem tem algo para oferecer."**

## Ligações

- [[A13 - Modo Live]]
- [[A11 - Marca e Design System]]
- [[R - Live - Folha de producao do filme hero]]
- [[R - Regras de ouro de producao de video]]
- [[R - Voz oficial das videoaulas]]
- [[ARQ - Incidentes de montagem do filme hero]]
- [[ARQ - Filme hero no YouTube 13092026]]
- [[ARQ - Cortes do filme hero vertical e pago 13092026]]
- [[P26 - Cortes do filme hero - vertical e pago]]
- [[P27 - Publicacao do filme hero no YouTube]]
- [[P25 - Pagina de venda da live]]
