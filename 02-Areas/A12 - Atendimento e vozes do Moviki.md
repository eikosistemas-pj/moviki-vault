---
type: area
status: ativo
area: Moviki
tags: [moviki, atendimento, vozes, narracao, elevenlabs, kairogen]
atualizado: 2026-09-04
---

# A12 - Atendimento e vozes do Moviki

Responsabilidade contínua: **quem fala pelo Moviki, e com que voz** — no
atendimento escrito e na narração dos vídeos.

## Os cinco atendentes da caixa de mensagens

No ar desde 03/09/2026, **nos três painéis** — `index.html`, `parceiro.html` e
`eikoadm01.html` do moviki-app. O do lojista foi o último a entrar, em 04/09: até
então o dono assinava "você — Karina" e **o cliente recebia sem nome nenhum**,
que é o oposto do que a mudança existe para fazer.

Os cinco: **Pamella, Mateus, Miguel, Karina e Júnior**.

**A regra, nas palavras do Paulo:** mesmo dia e mesmo turno = mesmo atendente;
virou a noite = outro; virou o dia = outro; de vez em quando repete.

**Determinístico, nunca sorteado.** O nome sai de `(data da mensagem + uid da
conversa)`. Turno de dia 06h–17h59, de noite 18h–05h59, em horário de Brasília
fixo (UTC−3), nunca no relógio do aparelho. O turno anda de 1 em 1 e são 5 nomes:
turnos seguidos nunca repetem, e a volta acontece a cada 5 turnos.

**Por que não sorteio:** o nome mudaria a cada F5 e — pior — o lojista veria
"Karina" enquanto o dono veria "Miguel" na MESMA mensagem. No painel do dono a
mensagem dele aparece como "você — Karina", para ele saber com que nome o cliente
recebeu.

**A trava que não se negocia:** os nomes valem só para `de:'admin'`. O robô
continua assinando "Vik — assistente". Dar nome de gente à resposta automática é
a pessoa achar que falou com alguém quando não falou — destrói autoridade em vez
de construir.

## A narração: o Kairogen É o ElevenLabs

**Descoberto em 03/09.** O `get_voices_data` do Kairogen devolve vozes cujos
endereços de preview são literalmente `api.us.elevenlabs.io` e
`eleven-public-prod`. Os `voice_settings` aceitos são os parâmetros do
ElevenLabs, nome por nome.

**Consequência:** a assinatura Kairogen que já é paga (PRO, 930 créditos/mês) dá
acesso à biblioteca profissional em pt-BR. **Não precisa mais gerar narração na
mão no site.**

**Voz escolhida pelo Paulo: `JPaHP82NTgRbDP91t8zP`.**

**Não clonar a voz a partir dos MP3.** Não é preciso — está disponível
licenciada — e não seria certo: as vozes profissionais são de dubladores reais
que licenciaram o trabalho através da plataforma.

## O caminho funciona ponta a ponta — conferido em 04/09

O MCP gera e o arquivo chega ao ambiente do Claude por `download_audio_from_url`.
O CDN é bloqueado no `curl`, mas a própria ferramenta entrega o binário — **sem
isso o áudio seria gerado e não daria para montar vídeo nenhum.**

**Custo medido:** 1 a 2 créditos por bloco de fala. A P09 inteira (10 blocos,
1:18) saiu por menos de 20.

⚠️ **Limite de taxa:** a API recusa com 429 quando as chamadas vêm coladas.
Espaçar cerca de 30 segundos entre gerações.

⚠️ **A voz não aparece no catálogo do Kairogen.** Foram listadas as 60 vozes da
conta e ela não está lá — mas o id passa direto para o ElevenLabs e gera normal.
**O id é a única coisa que amarra essa voz.** Se um dia parar de funcionar, não
existe "procurar pelo nome na lista".

## O dicionário de pronúncia DESTA voz

**Dicionário de pronúncia é por MOTOR.** O `PRONUNCIA` do `narrar.py` foi feito
para o Kokoro e **não vale aqui**. O desta voz nasceu com a P09:

| Escrever no áudio | Por quê |
| --- | --- |
| **`Movíqui`** | sem isso ela às vezes lê "moviCÍ", oxítona |

**O erro é intermitente** — a mesma palavra sai certa num bloco e errada no
seguinte, porque o motor é neural, não é um leitor. Por isso a correção fonética
entra em **todos** os blocos que citam a palavra, não só onde o defeito apareceu.

**Frase começando com "E" sai lida como a letra.** Reescrever sem o "E" inicial;
vale também para `, e ` no meio de frase longa.

**A legenda e o `.srt` mantêm a grafia certa** — a troca é só no texto que vai
para o motor.

## Armadilha de prosódia, e não é do motor

A frase *"…que ele não paga nada a você"* tem dois pronomes disputando o mesmo
lugar e um "a você" solto no fim. Qualquer pausa ali **inverte o sentido**: vira
"ele não paga nada… só você".

**O conserto é estrutural, não de entonação:** nomear o sujeito ("o comerciante
não te paga nada") ou quebrar em duas afirmações curtas ("ele não precisa te
pagar nada. Quem paga a sua comissão é o Moviki").

## O plano de futuro declarado

O Paulo acha a voz Kokoro das 24 aulas no ar **"muito sintetizada, quadrada"**
perto desta, e quer **regravar todas com o ElevenLabs, aos poucos**. Não bloqueia
nada: cada aula tem o roteiro guardado, e o vídeo se refaz no ritmo da fala nova.
Por enquanto fica como está, para pôr o produto no ar.

## Limitação do ambiente, registrada

**O Claude não consegue ouvir áudio.** O HuggingFace está bloqueado no sandbox,
então não há modelo de transcrição. Áudio só se confere por **medição** —
duração, loudness, silêncio, formato. **Conteúdo e pronúncia dependem do Paulo
ouvir e confirmar**, e foi assim que os dois defeitos da P09 apareceram.

## Ligações

[[P17 - Videos novos do parceiro]] · [[P16 - Rodada da credibilidade]] · [[R - Regras de ouro]]
