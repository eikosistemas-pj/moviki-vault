---
type: projeto
status: ativo
area: Moviki
tags: [moviki, videoaulas, parceiros, narracao]
atualizado: 2026-09-03
prioridade: media
prazo: 2026-09-10
---

# P17 - Videos novos do parceiro

Duas pecas novas, pelas mudancas de 03/09 no painel do parceiro. **Roteiro pronto,
video ainda por produzir.**

| Cena | O que e | Alvo | Onde entra |
|---|---|---|---|
| `P00-abertura-parceiro` | A abertura que o parceiro nao tinha | **2:54 gravado** | Antes das 8, na tela de aulas |
| `P09-cracha-verificacao` | O cracha e a pagina que confirma ele | 1:05 | Logo depois de "Divulgacao" |

## Por que a abertura precisava existir

O lojista e recebido pela T00, com o Vik. **O parceiro era recebido por um cadeado** -
entrava e a primeira coisa que via era a faixa laranja e a Divulgacao borrada.

A trava esta certa e fica. Mas ordem importa: **cadeado sem explicacao parece
desconfianca; cadeado depois da explicacao parece cuidado.**

## A narracao da P00 ja existe

O Paulo gravou no ElevenLabs (voz `JPaHP82NTgRbDP91t8zP`) e entregou **9 blocos MP3**:
mono 44.1 kHz ~134 kbps, -16,8 LUFS, pico -0,4 dBTP, **todos entrando direto, sem
silencio na frente** (que e o que o pipeline precisa para sincronizar). Total 2:54.

### O mapa dos 9 blocos para os 17 trechos

| Bloco | Trechos | Conteudo |
|---|---:|---|
| bloco01 | 1 + 2 | Boas-vindas + o que e ser parceiro + indicacao |
| bloco02 | 3 + 4 | 15% todo mes + transparencia sobre a comissao |
| bloco03 | 5 + 6 + 7 | Quem indicar + perfil dos empreendedores + ser encontrado |
| bloco04 | 8 | Negocios moveis + fixos + prestadores de servico |
| bloco05 | 9 + 10 | "Voce ja sabe por onde comecar" + desconfianca do comerciante |
| bloco06 | 11 | Cracha + QR code + confirmacao de parceiro autorizado |
| bloco07 | 12 + 13 | Aulas + a comissao + por que o link fica travado |
| bloco08 | 14 + 15 | Liberacao do link + selo de aulas + aulas novas |
| bloco09 | 16 + 17 | Caixa de mensagens/suporte + "Vamos comecar?" |

### O AUDIO E A FONTE DE VERDADE, NAO O ROTEIRO

Durante a gravacao o Paulo alterou varios trechos - **principalmente 6, 8, 11, 12, 13,
14 e 15** - para deixar a fala mais natural e, na parte das aulas, **ATEMPORAL: a
narracao nao diz que existem exatamente oito aulas.**

**Isso corrigiu um defeito real.** O roteiro dizia "oito aulas curtas" e "assistiu as
oito", e esses dois nasceriam errados no dia em que a propria P00 e a P09 subissem e
o total virasse **dez**. Video nao se corrige com um deploy. Virou regra de ouro.

**Consequencia:** a estrutura e a ordem dos 17 trechos continuam valendo (e por elas
que a tela e sincronizada), mas o `.srt` e a legenda tem que sair do **audio**. Como o
Claude nao consegue transcrever (HuggingFace bloqueado no sandbox), **a legenda depende
do Paulo mandar o texto final** de cada bloco, ou aceitar o video sem legenda embutida.

## O efeito colateral que e o desenho funcionando

Quando as duas entrarem no `MOVIKI_TUTORIAIS`, as aulas publicadas vao de **8 para 10**:

- **O selo de todo parceiro vira laranja: "2 aulas novas".** Primeira prova real do
  mecanismo. Ninguem e retrancado, o link continua aberto, mas todos ficam sabendo.
- **A trava passa a exigir as 10 dos novatos** - o codigo compara com o que esta
  publicado, nao com o numero 8.

## Quem faz o que

**O Paulo nao grava video.** O `.mp4` e gerado no ambiente do Claude, a partir do
estudio reconstruido de `claude/moviki-estudio-codigo.md` (ele nao vive em
repositorio). O Paulo **sobe no YouTube (nao listado) e manda o link**.

## Proximos passos

1. Paulo ouve os 9 blocos e confirma a pronuncia de Moviki, Vik, Pix e WhatsApp.
2. Paulo manda o texto final de cada bloco (para o `.srt`).
3. Claude reconstroi o estudio, grava a tela no ritmo dos audios e entrega o `.mp4`.
4. Grava tambem a P09 (narracao ainda nao existe).
5. Paulo sobe as duas no YouTube e manda os links.
6. Claude poe os ids no `parceiro.html` e atualiza a tabela de identificacao.

Ver [[A12 - Atendimento e vozes do Moviki]] e [[P16 - Rodada da credibilidade]].
