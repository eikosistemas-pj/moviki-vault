---
type: decisao
status: concluido
area: A12 — Atendimento e vozes do Moviki
tags: [moviki, videoaulas, narracao, kairogen, decisao]
atualizado: 2026-09-04
---

# ARQ — A P09 produzida ponta a ponta, 04/09/2026

**Primeira peça de vídeo do projeto em que narração e imagem saíram do mesmo
lugar.** O Paulo não gravou nada: só ouviu, reprovou o que estava errado e
aprovou.

Isso muda o custo de produzir aula nova. Antes: escrever o roteiro aqui, o Paulo
gravar a narração no site do ElevenLabs, mandar os MP3, e só então montar. Agora
o ciclo inteiro cabe numa rodada.

## Como foi

**Narração** — MCP do Kairogen, voz `JPaHP82NTgRbDP91t8zP`, 10 blocos, menos de
20 créditos. Aparados nas pontas e normalizados em **−16 LUFS**: saíam em −22, e
o vídeo precisa deles justos para colar na fala.

**Vídeo** — 22 quadros montados quadro a quadro no ritmo medido de cada MP3.
Nada depende do relógio: `__montar(n)` arma o quadro e devolve quanto dura a
entrada, `__pintar(t)` põe tudo no instante `t`. A mesma chamada dá sempre a
mesma imagem, e o `concat` do ffmpeg recebe a duração exata de cada foto.

**Legenda** — a P09 **tem `.srt`**, ao contrário da P00: o texto saiu daqui,
então a legenda é o que foi falado.

## As duas reprovações do Paulo, e o que cada uma ensinou

**1. "moviCÍ" no bloco 6.** A voz leu a marca como oxítona. Resolvido escrevendo
**`Movíqui`** no áudio — e em **todos** os blocos que citam a marca, não só onde
o defeito apareceu: motor neural erra de forma intermitente, e corrigir só onde
apareceu é esperar o erro voltar no próximo.

**2. O bloco 5 embrulhou o sentido.** *"…que ele não paga nada a você"* soou como
"ele não paga nada… só você" — **invertendo** a frase mais importante da peça.

O problema não era a voz: eram dois pronomes disputando o mesmo lugar e um "a
você" solto no fim. **O conserto foi estrutural**, não de entonação — quebrar em
duas afirmações curtas, cada uma com um sujeito só: *"ele não precisa te pagar
nada. Quem paga a sua comissão é o Moviki."*

## E uma reprovação de conteúdo

**"João da Feira" no crachá do exemplo.** Não era só o som: o crachá é do
**parceiro**, que apresenta o Moviki — ele não é o dono da barraca. Apelido de
negócio numa credencial diz a coisa errada sobre quem está ali.

Virou **Carlos Mendes · @carlosmendes**. Regra: **nome de exemplo em credencial
é nome de pessoa.**

## O defeito da P00 consertado aqui

Na P00, a mira da câmera não caía em cima do QR — o crachá inteiro entrava na
tela do celular e o quadrado ciano pegava o canto.

Aqui entra **só o recorte do QR**, centralizado: mira e código ocupam o mesmo
lugar **por construção**, não por ajuste de olho.

Na primeira montagem o crachá, que é quase 2:1, estourou a largura e empurrou o
celular para fora do quadro. **Foi medindo a geometria que apareceu** — não no
olho. Mesma lição das suítes de janela.

**A P00 não será regravada por causa disso.** Decisão do Paulo: refazer geraria
id novo no YouTube por um detalhe de um quadro.

## O que aparece na tela é real

Painel, crachá, imagem 1080×1350 e página `/v/` são capturas do que está no ar —
o `parceiro.html` e o `v.html` publicados, rodando contra um Firebase de mentira.
A imagem do crachá foi **baixada pelo botão**, não recriada.

Nome, arroba e data são inventados, como manda a regra: nada de dado real em
gravação.

## Ligações

[[P17 - Videos novos do parceiro]] · [[A12 - Atendimento e vozes do Moviki]] · [[R - Regras de ouro]] · [[R - Verificacao publica de parceiro]]
