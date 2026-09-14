---
type: incidente
status: concluido
area: A13 - Modo Live
tags: [filme-hero, ffmpeg, kairogen, playwright, incidente]
atualizado: 2026-09-13
---

# ARQ — Incidentes de montagem do filme hero

Tudo o que quebrou entre 12 e 13/09/2026 e como foi consertado. Cada um custou
pelo menos uma rodada de refação — estão aqui para não custarem a segunda.
Ver [[R - Live - Folha de producao do filme hero]] e
[[R - Regras de ouro de producao de video]].

## Áudio

**1. O slogan foi cortado no fim.** A narração tinha sido dividida por corte de
silêncio, e a fronteira de um bloco caiu **dentro** da frase final, depois de
"Mo-víki." — roubando a primeira palavra do slogan.
**Conserto:** abandonar a divisão por silêncio. **Um arquivo de áudio por cena**,
sempre.

**2. "Bugou tudo — som, sincronização, narração sumiu."** Na v3 o filme inteiro
saiu fora de sincronia. Causa: C02 e C11 ficaram **estéreo** (por causa da
mixagem da chuva) e as outras 14 cenas continuaram **mono**. O demuxer `concat`
com `-c copy` **não junta faixas com layouts de canal diferentes** — e falha de um
jeito que parece problema de sincronia.
**Conserto:** forçar `aac, 44100, 2 canais` em **todas** as cenas antes do
concat, e conferir que as 16 respondem `{aac,44100,2}`.

**3. C07 saiu "embolada".** Uma frase longa com vírgulas, lida a 1,03 de
velocidade. **Conserto:** frases curtas, ponto no lugar da vírgula, velocidade
0,93.

**4. "MÓviki".** A voz lia o nome como paroxítona. **Conserto:** escrever
**"Mo-víki"** no texto que vai para o motor, em todos os blocos.

**5. O "xiou" da C09.** A palavra inglesa "Enterprise" entrava sem embalo e a voz
engasgava. Tentativas com "No plano Enterprise" e com mais estabilidade não
resolveram no Cambero. **Com a Malu a palavra sai limpa.**

## Imagem

**6. Mockup 3D do celular reprovado.** "Movimento do celular totalmente amador."
**Conserto:** mockup frontal, sem deriva de câmera nas cenas de UI.

**7. "O celular parece de brinquedo."** Nas cenas do food truck e do barbeiro o
aparelho no tripé não pertencia à cena. **Conserto:** briefing exigindo **tela
preta/apagada**, aparelho maior, tripé com **sombra de contato** e o personagem
**olhando para a tela**. Aprovado.

**8. A panela que chegava do nada em C02.** O clipe materializava um recipiente
com bolo no meio da cena. **Conserto:** regerar com a instrução **"REGRA
ABSOLUTA: nada aparece nem desaparece"**.

**9. Língua para fora no C02 novo.** Varredura de quadros achou o defeito entre
0,8 e 3,8 s. **Conserto:** usar o clipe a partir de 4,5 s.

**10. C02 parecia congelada.** Estava a 0,45x para caber nos 16,6 s.
**Conserto:** três enquadramentos do mesmo clipe, em **velocidade natural**.

**11. C03 estática.** Os três primeiros segundos eram uma imagem parada.
**Conserto:** o post animado cobre os 8,1 s inteiros; depois, o clipe da
personagem fotografando dentro do cartão, em laço ida-e-volta.

**12. Mapa tremido.** `zoompan` sobre fonte de baixa resolução produz tremor.
**Conserto:** pré-escalar a textura para **6688x3764** antes do `zoompan` (regra
geral: pré-escalar ~4x).

**13. A entrada da C13 pela lateral foi reprovada.** **Conserto:** revelação pelo
centro — 36 quadros escalando de 0,90 a 1,00 com suavização cúbica e fade.

## Ambiente e entrega

**14. `aspect_ratio` ignorado.** O argumento genérico não tem efeito; o aspecto
vai em `extra_params.aspectRatio`. O endpoint de status sempre ecoa "16:9", então
**não dá para conferir pelo status** — só medindo o arquivo.

**15. 429 do Kairogen e limite de 4 vídeos simultâneos.** Espaçar ~50 s entre
lotes.

**16. `cdn.kairogen.ai` bloqueado.** Todo asset gerado passa pelo Paulo: ele baixa
e anexa. Imagem de referência sobe pelo widget.

**17. Entrega acima de 30 MiB recusada.** Recomprimir com `crf` 25 a 27. A v6
saiu com **crf 27 = 25 MB**; `crf 25` dava 33 MB e era recusado.

**18. O deslocamento da captura do Playwright.** A sacolinha nunca aparecia em
C07 porque a gravação começa **antes** do `t0` do roteiro — 3,8 s, depois 4,6 s.
**Conserto:** varredura de quadros procurando a faixa laranja da oferta, a cada
vez que a captura muda.

**19. Chromium do Playwright não toca H.264.** A fonte de câmera tem que ser
VP9/WebM.

## Ligações

- [[A13 - Modo Live]]
- [[A2 - Infraestrutura e Deploy]]
- [[R - Live - Folha de producao do filme hero]]
- [[R - Regras de ouro de producao de video]]
- [[R - Regras de ouro de producao de cortes]]
- [[ARQ - Filme hero v6 aprovado 13092026]]
- [[R - Retomada live parte 02]]
