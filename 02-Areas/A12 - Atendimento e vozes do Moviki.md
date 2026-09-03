---
type: area
status: ativo
area: Moviki
tags: [moviki, atendimento, vozes, narracao, elevenlabs, kairogen]
atualizado: 2026-09-03
---

# A12 - Atendimento e vozes do Moviki

Responsabilidade continua: **quem fala pelo Moviki, e com que voz** - no atendimento
escrito e na narracao dos videos.

## Os cinco atendentes da caixa de mensagens

No ar desde 03/09/2026, nos tres paineis (`index.html`, `parceiro.html`,
`eikoadm01.html` do moviki-app). A resposta do dono deixou de chegar como um "Moviki"
sem rosto: **Pamella, Mateus, Miguel, Karina e Junior**.

**A regra, nas palavras do Paulo:** mesmo dia e mesmo turno = mesmo atendente; virou
a noite = outro; virou o dia = outro; de vez em quando repete.

**Determinístico, nunca sorteado.** O nome sai de `(data da mensagem + uid da
conversa)`. Turno de dia 06h-17h59, de noite 18h-05h59, em horario de Brasilia fixo
(UTC-3), nunca no relogio do aparelho. O turno anda de 1 em 1 e sao 5 nomes: turnos
seguidos nunca repetem, e a volta acontece a cada 5 turnos.

**Por que nao sorteio:** o nome mudaria a cada F5 e - pior - o lojista veria "Karina"
enquanto o dono veria "Miguel" na MESMA mensagem. No painel do dono a mensagem dele
aparece como "voce - Karina", pra ele saber com que nome o cliente recebeu.

**A trava que nao se negocia:** os nomes valem so para `de:'admin'`. O robo continua
assinando "Vik - assistente". Dar nome de gente a resposta automatica e a pessoa achar
que falou com alguem quando nao falou - destroi autoridade em vez de construir.

## A narracao dos videos: o Kairogen E o ElevenLabs

**Descoberto em 03/09/2026, e muda a producao.** O `get_voices_data` do Kairogen
devolve vozes cujos enderecos de preview sao literalmente `api.us.elevenlabs.io` e
`eleven-public-prod`. Os `voice_settings` aceitos sao os parametros do ElevenLabs,
nome por nome.

**Consequencia:** a assinatura Kairogen que ja e paga (PRO, 930 creditos/mes) da
acesso a biblioteca profissional inteira do ElevenLabs em pt-BR. **Nao precisa mais
gerar narracao na mao no site** - da pra chamar direto pelo MCP e regravar um bloco
isolado quando a pronuncia sair errada.

**Voz escolhida pelo Paulo: `JPaHP82NTgRbDP91t8zP`.**

**Nao clonar a voz a partir dos MP3.** Nao e preciso - esta disponivel licenciada -
e nao seria certo: as vozes profissionais sao de dubladores reais que licenciaram o
trabalho atraves da plataforma.

**O Kokoro (`pf_dora`) continua sendo o motor das 24 aulas ja no ar.** Elas nao serao
regravadas por causa de voz; a troca vale do que for produzido daqui em diante.

**Dicionario de pronuncia e por motor.** O `PRONUNCIA` do `narrar.py` foi feito para
o Kokoro. Trocando a voz, ele nao vale mais - cada motor erra palavras diferentes.

## Limitacao do ambiente, registrada

**O Claude nao consegue ouvir audio entregue.** O HuggingFace esta bloqueado no
sandbox, entao nao da para baixar modelo de transcricao. Audio do Paulo so pode ser
conferido por **medicao** (duracao, loudness, silencio, formato) - o conteudo e a
pronuncia dependem dele ouvir e confirmar.

Ver [[P17 - Videos novos do parceiro]].
