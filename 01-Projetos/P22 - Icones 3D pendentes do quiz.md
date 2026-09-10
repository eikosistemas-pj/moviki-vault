---
type: projeto
status: ativo
prioridade: 3
prazo: 2026-09-30
area: A11 - Marca e Design System
tags: [icones, quiz, kairogen, pendencia]
atualizado: 2026-09-10
---

# P22 - Icones 3D pendentes do quiz

Os quatro itens novos do quiz funcionam, mas **sem icone proprio**: aparecem com
o emoji no lugar do desenho 3D que os outros 34 itens tem. Conferido no
repositorio em 10/09 — a pasta `moviki-app/quiz/icones/` tem 34 arquivos e
nenhum dos quatro.

| Arquivo que falta | Item do quiz | Hoje aparece |
| --- | --- | --- |
| `sushi.png` | Sushi / Comida Japonesa | emoji |
| `suplementos.png` | Aba Suplementos + Nutricao Esportiva | emoji |
| `naturais.png` | Produtos Naturais / Vitaminas | emoji |
| `otica.png` | Otica / Oculos, em Servicos | emoji |

Pasta: `moviki-app/quiz/icones/`. **Nao trava nada** — o quiz troca sozinho pelo
emoji quando o `.png` nao existe. Subindo os quatro com exatamente esses nomes,
os icones aparecem sem mexer em mais nada.

## Por que ainda nao foi feito

O download do Kairogen esta bloqueado na sessao em nuvem: da para gerar a imagem,
nao para baixar e tirar o fundo. **Precisa ser feito numa conversa ligada ao
computador**, ou ele baixa da galeria do Kairogen e manda no chat para tratar.

## Padrao visual — o mesmo dos 34 existentes

Objeto 3D brilhante flutuando, fundo transparente, 256x256, sombra neutra
embaixo, sem texto e sem marca. Pipeline: Kairogen `flux-2-klein-9b` gerando com
fundo verde chapado + remocao do verde (chroma key e despill) em Python.

Prompt que funciona, trocando so o objeto:

```
3D glossy app icon: <OBJETO>, floating slightly above a soft neutral gray
shadow, playful stylized 3D render, smooth plastic-like glossy surfaces with
bright specular highlights, centered composition, isolated object, flat solid
pure chroma green background (#00FF00), no text, no letters, no labels, no
logos, no background scenery
```

- sushi: `two pieces of salmon nigiri sushi and one maki roll with nori`
- suplementos: `a black protein powder tub with a closed lid and a plastic scoop, unbranded and completely blank surface`
- naturais: `an amber supplement bottle with a few capsules beside it and a small green leaf`
- otica: `a pair of eyeglasses with thin metal frame and clear lenses, three-quarter view`

## Pendencia irma, no robo social

Falta o fundo `suplementos-01.jpg` em
`moviki-assistente-social/assets/fundos/`. Sem ele o post desse segmento usa o
fundo generico — funciona, so fica menos especifico. Cena: banca de suplementos
em corredor de academia ou feira, potes alinhados, luz de fim de tarde, **sem
rotulo de marca legivel**. Otica nao precisa: usa o de Servicos.

## Ligacoes

[[A11 - Marca e Design System]] · [[A8 - Conteudo e Social]] ·
[[ARQ - Suplementos sushi e otica no quiz]]
