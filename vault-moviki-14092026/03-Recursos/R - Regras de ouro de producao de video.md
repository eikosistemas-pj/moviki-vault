---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [video, producao, regras, ffmpeg, kairogen, conformidade]
atualizado: 2026-09-13
---

# R — Regras de ouro de produção de vídeo

Regras tiradas da produção do filme hero (12–13/09/2026). Valem para toda peça de
vídeo da Moviki. Cada uma custou pelo menos uma refação — ver
[[ARQ - Incidentes de montagem do filme hero]].

## Como a UI aparece em vídeo

A interface do Moviki aparece de **três formas, nunca de outra**:

1. Tela cheia — captura real ocupando o quadro inteiro.
2. Celular parado em plano fixo — câmera imóvel, máscara estática.
3. Celular desfocado ou de costas — quando o conteúdo não precisa ser lido.

**Proibido** compor UI legível dentro de celular gerado por IA em movimento na
mão: o vídeo de IA não mantém a geometria do aparelho entre quadros, o
rastreamento perde o alvo e a tela escorrega. O defeito lê como "isso é falso" —
o oposto do que a cena precisa provar.

Corolários aprovados na v6:

- Mockup **frontal**, sem deriva de câmera nas cenas de UI. O mockup 3D com
  movimento foi reprovado: "parece de brinquedo".
- Aparelho em cena de personagem: tela **preta/apagada**, aparelho maior, tripé
  com **sombra de contato**, personagem **olhando para a tela**.
- Remover a logo do fabricante com `delogo` — o filme não faz propaganda de
  aparelho.

## Áudio

- **Um arquivo de áudio por cena.** Divisão de narração por corte de silêncio
  corta frase no meio — foi assim que o slogan perdeu a primeira palavra.
- **Forçar `aac, 44100, 2 canais` em todas as cenas antes do concat.** O demuxer
  `concat` com `-c copy` não junta faixas com layouts de canal diferentes, e
  falha de um jeito que parece problema de sincronia.
- Locução: frases curtas, **ponto no lugar da vírgula**, velocidade ~0,93. Frase
  longa com vírgulas em velocidade acima de 1,0 sai embolada.
- **Grafia para o motor: "Mo-víki".** Sem o hífen e o acento a voz lê "MÓviki".
  A grafia certa fica na legenda; a fonética vale só no texto que vai ao motor.
- Voz oficial: **Malu** `fhtZMBwha5du5OxuvexO`, a mesma das videoaulas — o
  lojista ouve a mesma pessoa no anúncio, no painel e na Academia. A Malu é ~20%
  mais rápida que o Cambero, e é ela que resolve palavras em inglês como
  "Enterprise".
- **Nada de banco de sons.** Ambiência se sintetiza (`anoisesrc` + filtros):
  evita licença, atribuição e risco de Content ID derrubar o vídeo.
- Música com `sidechaincompress` tendo a narração como chave — a trilha abaixa
  sozinha quando a voz entra.

## A locução é a régua

Duração de filme narrado é ditada pela locução, não pela montagem. Imagem se
estica e se encolhe; texto falado, não.

Ordem obrigatória: escolher a voz → gravar as locuções → cronometrar → ajustar o
texto no papel se passar do alvo → congelar duração por cena → montar a folha de
produção → começar a gerar.

## Geração de imagem e vídeo

- **"REGRA ABSOLUTA: nada aparece nem desaparece"** no prompt — sem isso a IA
  materializa objetos no meio da cena.
- Varrer os quadros do clipe procurando defeito antes de montar (língua para
  fora, dedo a mais, deformação de rosto) e cortar a partir de um ponto limpo.
- Rosto em close por 5 s é o caso de maior risco: gerar 2 variações.
- **Nunca desacelerar um clipe para caber na duração** — a 0,45x a cena parece
  congelada. Usar **três enquadramentos do mesmo clipe em velocidade natural**.
- Imagem parada não cobre cena longa: animar o elemento inteiro, ou usar laço
  **ida-e-volta** para cobrir a duração sem esticar e sem congelar.
- **Pré-escalar ~4x antes de `zoompan`** (o mapa foi para 6688x3764). `zoompan`
  sobre fonte de baixa resolução produz tremor.
- Revelação de cena: pelo **centro**, não pela lateral — 36 quadros escalando de
  0,90 a 1,00 com suavização cúbica e fade.
- Amarrar o grão: grade e `noise` também nas cenas de UI e tipografia, senão a UI
  parece colada por cima.

## Economia

- Vídeo de IA só onde o movimento humano ou físico é indispensável. Cena
  emocional resolve com **imagem estática + movimento de câmera na pós**
  (~1 crédito contra 16 a 31).
- Captura real de UI custa zero e é repetível — usar sempre que a cena for de
  produto.
- **Sobras de clipes já gerados montam cena nova** — a D2 saiu de sobras de C05,
  zero crédito extra.
- Clipe reaproveitado entre cenas (a chuva de C02 volta em C11): gerar uma vez,
  usar duas.

## Entrega

- Limite prático de anexo no chat: **30 MiB**. Recomprimir com `crf` entre 25 e
  27. A v6 saiu com **crf 27 = 25 MB**; `crf 25` dava 33 MB e era recusado.
- O master do hero não tem legenda queimada — legenda entra por `.srt` no
  YouTube.

## O que o vídeo nunca diz

- Nenhuma promessa de faturamento, de número de vendas ou de resultado.
- Nenhuma sugestão de que basta ligar a live para aparecer audiência.
  Formulação aprovada: **"a MOVIKI é o palco, o megafone você já tem"**.
- Os cortes **não saem automaticamente**: o lojista grava um corte de até 60 s e
  o arquivo fica no celular dele.
- **Pix dentro da live é recurso Enterprise** e precisa estar identificado na
  cena em que aparece.
- A live funciona no **teste grátis** de 30 dias em nível Premium — nunca usar a
  palavra "trial" em texto voltado ao cliente.
- Enumerar segmentos exclui quem não está na lista: "Serve para quem tem algo
  para oferecer."

## Ligações

- [[A13 - Modo Live]]
- [[A11 - Marca e Design System]]
- [[A10 - Conformidade e LGPD]]
- [[R - Live - Folha de producao do filme hero]]
- [[R - Regras de ouro de producao de cortes]]
- [[R - Regras de conteudo e tom]]
- [[R - Voz oficial das videoaulas]]
- [[R - Checklist conformidade Meta e Google]]
- [[ARQ - Incidentes de montagem do filme hero]]
- [[ARQ - Filme hero v6 aprovado 13092026]]
