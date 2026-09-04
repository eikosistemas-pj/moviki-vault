---
type: projeto
status: concluido
prioridade: 2
area: A12 — Atendimento e vozes do Moviki
prazo: 2026-09-04
tags: [moviki, videoaulas, parceiros, narracao]
atualizado: 2026-09-04
---

# P17 — Vídeos novos do parceiro

**As duas peças estão prontas.**

| Cena | Duração | Estado |
| --- | --- | --- |
| `P00-abertura-parceiro` | 2:54 | ✅ **no ar** — `fQqR9ae5vnI` |
| `P09-cracha-verificacao` | 1:18 | ✅ **produzida e aprovada** — aguarda subir |

## A P09 foi feita inteira aqui dentro

Primeira peça do projeto em que **narração e vídeo saíram do mesmo lugar**. O
Paulo não gravou nada.

**Narração:** MCP do Kairogen com a voz `JPaHP82NTgRbDP91t8zP`, 10 blocos, menos
de 20 créditos. Cada bloco foi aparado nas pontas e normalizado em **−16 LUFS**,
o padrão do YouTube — saíam em −22, e o pipeline precisa deles justos.

**Vídeo:** 22 quadros montados quadro a quadro no ritmo medido de cada MP3, o
mesmo método da P00. Sai idêntico toda vez e casa com a fala no milésimo.

**Tem `.srt`**, ao contrário da P00 — o texto saiu daqui, então a legenda é o
que foi falado. Na P00 o Paulo alterou a fala durante a gravação e o sandbox não
alcança modelo de transcrição.

## O que aparece na tela é real

- O **painel** é o `parceiro.html` publicado, rodando contra um Firebase de mentira
- O **crachá** é o render de verdade, com o QR desenhado pelo `mvQR`
- A **imagem 1080×1350** foi baixada pelo botão — o clique foi dado e o arquivo capturado
- A **página `/v/`** é o `v.html` do repositório, com o espelho semeado

Nome, arroba e data são inventados: **Carlos Mendes · @carlosmendes**.

## Duas correções que vieram do Paulo, e ficam registradas

**1. "João da Feira" estava errado.** Não pelo som: o crachá é do **parceiro**,
que apresenta o Moviki — ele não é o dono da barraca. Apelido de negócio numa
credencial diz a coisa errada sobre quem está ali. **Nome de exemplo em
credencial é nome de pessoa.**

**2. A mira da câmera não caía sobre o QR** — defeito visto na P00. Aqui, em vez
de jogar o crachá inteiro na tela do celular e torcer para a mira acertar, entra
**só o recorte do QR**, centralizado: mira e código ocupam o mesmo lugar por
construção, não por ajuste de olho. **A P00 não será regravada por causa disso**
— decisão do Paulo.

## Pronúncia: o dicionário desta voz nasceu aqui

Ver [[A12 - Atendimento e vozes do Moviki]]. Em resumo: escrever **`Movíqui`** no
áudio, em **todos** os blocos que citam a marca; e nada de frase começando com
"E". A legenda mantém a grafia certa.

E uma armadilha que não é do motor: *"que ele não paga nada a você"* inverte de
sentido quando falado — vira "ele não paga nada… só você". Numa frase que existe
para dizer que o comerciante não desembolsa nada, é o pior erro possível. O
conserto é estrutural, não de entonação.

## O que acontece quando a P09 subir

As aulas do parceiro vão de **9 para 10**:

- **O selo de todo parceiro vira laranja: "1 aula nova".** Ninguém é retrancado,
  o link continua aberto, mas todos ficam sabendo.
- **Parceiro novo passa a precisar das 10** — o código compara com o que está
  publicado, não com um número escrito à mão.

**Nada é apagado do YouTube:** a P09 é aula nova, não substitui nenhuma.

## Ligações

[[A12 - Atendimento e vozes do Moviki]] · [[P16 - Rodada da credibilidade]] · [[R - Verificacao publica de parceiro]] · [[R - Marcas de versao no ar]]
