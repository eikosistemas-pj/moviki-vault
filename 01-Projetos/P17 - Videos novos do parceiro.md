---
type: projeto
status: ativo
prioridade: 2
area: A12 — Atendimento e vozes do Moviki
prazo: 2026-09-10
tags: [moviki, videoaulas, parceiros, narracao]
atualizado: 2026-09-03
---

# P17 — Vídeos novos do parceiro

Duas peças novas, pelas mudanças de 03/09 no painel do parceiro.

| Cena | O que é | Duração | Estado |
| --- | --- | --- | --- |
| `P00-abertura-parceiro` | A abertura que o parceiro não tinha | 2:54 | ✅ **NO AR** — `fQqR9ae5vnI` |
| `P09-cracha-verificacao` | O crachá e a página que confirma ele | ~1:05 | roteiro pronto, sem narração |

## A P00 está no ar (03/09/2026)

Subida no YouTube como não listada, id **`fQqR9ae5vnI`**, e já apontada no
`parceiro.html` (marca `2026-09-03-abertura`).

**Entrou como módulo próprio, sem `sel`.** A abertura não pertence a nenhuma
seção do painel — se tivesse `sel`, ela substituiria a aula daquela seção no
bloco embutido, porque o `embutir()` pega só a primeira aula de cada módulo.
Sem `sel`, ela aparece na tela de aulas e conta para a trava, e nenhuma seção
perde a sua própria aula.

**Conferido no Chromium antes de entregar:** 9 aulas publicadas, a abertura em
primeiro, 8 caixas embutidas nas 8 seções de sempre, nenhum erro de página, e o
aviso da trava já lendo *"Assista as 9 aulas para liberar o seu link"* — o texto
é montado do total publicado, não de um número escrito à mão.

## Por que a abertura precisava existir

O lojista é recebido pela T00, com o Vik. **O parceiro era recebido por um
cadeado** — entrava e a primeira coisa que via era a faixa laranja e a
Divulgação borrada.

A trava está certa e fica. Mas ordem importa: **cadeado sem explicação parece
desconfiança; cadeado depois da explicação parece cuidado.**

## O efeito colateral, que é o desenho funcionando

Com 9 publicadas em vez de 8:

- **O selo de todo parceiro vira laranja: "1 aula nova".** Primeira prova real
  do mecanismo. Ninguém é retrancado, o link continua aberto, mas todos ficam
  sabendo.
- **A trava passa a exigir as 9 dos novatos** — o código compara com o que está
  publicado, não com o número 8.

Quando a P09 subir, vira 10, e o mesmo acontece de novo.

## Como a P00 foi feita

Narração gravada pelo Paulo no **ElevenLabs**, voz `JPaHP82NTgRbDP91t8zP`, 9
blocos MP3 — mono 44,1 kHz, −16,8 LUFS, pico −0,4 dBTP, todos entrando direto
sem silêncio na frente. Total 2:54.

Vídeo montado **quadro a quadro**, não gravado: 26 quadros repartidos entre os 9
blocos por peso, com a duração exata de cada MP3. O `recordVideo` do Playwright
entrega webm de taxa variável e obriga a adivinhar onde cortar — quadro a quadro
o vídeo bate com o áudio no milésimo. Detalhe em
`claude/moviki-estudio-p00-abertura.md`.

**O áudio é a fonte de verdade, não o roteiro.** Durante a gravação o Paulo
alterou vários trechos — principalmente 6, 8, 11, 12, 13, 14 e 15 — para deixar
a fala natural e, na parte das aulas, **atemporal: a narração não diz que
existem exatamente oito aulas**. Isso corrigiu um defeito real, porque o roteiro
escrito nasceria errado no dia em que a própria P00 subisse. Virou regra de
ouro: *texto de vídeo nunca cita a quantidade de itens de uma lista que pode
crescer.*

**A P00 não tem `.srt`.** O sandbox não alcança o HuggingFace, então não há
modelo de transcrição, e a redação final está no áudio. Ou o Paulo manda o texto
final de cada bloco, ou o vídeo fica sem legenda embutida.

## O que falta para a P09

1. Gravar a narração (roteiro pronto em `claude/moviki-roteiros-parceiro-cracha.md`).
2. **O crachá precisa estar no `parceiro.html`** — a P09 mostra o crachá e o QR
   sendo lido, e o `mvQR` ainda não subiu ao repositório. Ver
   [[ARQ - Entregue e nao subiu 03092026]].
3. Montar a cena e entregar o `.mp4`.
4. Paulo sobe no YouTube e manda o link; o id entra no painel e na tabela.

## Ligações

[[A12 - Atendimento e vozes do Moviki]] · [[P16 - Rodada da credibilidade]] · [[ARQ - Entregue e nao subiu 03092026]] · [[R - Marcas de versao no ar]]
