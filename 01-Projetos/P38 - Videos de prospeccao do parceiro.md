---
type: projeto
status: ativo
prioridade: 1
prazo: 2026-10-05
area: A5 - Programa de Parceiros
tags: [video, roteiro, prospeccao, parceiro, influenciador, conar, malu]
atualizado: 2026-09-16
---

# P38 - Videos de prospeccao do parceiro

> Os quatro roteiros que faltavam para a prospecao de parceiro e de
> influenciador, mais o plano de captacao da live real. Escritos em 16/09/2026,
> depois da reescrita das tres paginas do funil - ver
> [[R - Marcas de versao - Landing do parceiro 16092026]].

Relacionado: [[P37 - Prospeccao de parceiros e influenciadores]] ·
[[R - Regras de ouro de producao de video]] ·
[[R - Checklist conformidade Meta e Google]] ·
[[P16 - Perfil do criador de conteudo no quiz]]

---

## Parametros de producao - valem para os quatro

- Voz **Malu** `fhtZMBwha5du5OxuvexO`, Kairogen, `language_code: pt`
- `stability 0.5 - similarity_boost 0.8 - use_speaker_boost true` - **sem `speed`**
- Grafia para o motor: **Mo-viki**, com hifen e acento agudo no primeiro i. A
  legenda e o `.srt` mantem **Moviki**
- Blocos concatenados com pausa de **0,35 s**, nunca depois do ultimo
- `loudnorm I=-16 TP=-1.5 LRA=11` + `aresample=44100`
- **Um arquivo de audio por cena.** Cortar narracao por silencio corta frase no meio
- **Uma geracao por vez, com ~60 s entre elas** - o Kairogen devolve 429 sob
  concorrencia
- Duracoes abaixo calculadas pela medicao de 14/09: a Malu le **~2,7 palavras por
  segundo**. Mas **a locucao e a regua**: gravar primeiro, cronometrar, ajustar o
  texto no papel se passar, e so entao montar

### A UI aparece de tres formas, nunca de outra

1. Tela cheia, captura real
2. Celular parado em plano fixo
3. Celular desfocado ou de costas

**Proibido** compor interface legivel dentro de celular gerado por IA em
movimento - a geometria escorrega entre quadros e o defeito le como "isso e
falso". E **nada de interface, icone ou cenario gerado por IA na hora**: o banco
de imagens e o do proprio Moviki.

### Conformidade - vale para os quatro, sem excecao

- Descrever a **REGRA**, nunca o **RESULTADO**
- Proibido: "renda", "garantido", "sem risco", "para sempre", numero que projete
  quanto alguem vai receber, prazo de retorno
- Obrigatorio dizer, em algum ponto: a comissao so existe sobre assinatura
  efetivamente paga, e pode ser zero
- Nenhum dado real em quadro: chave Pix, e-mail, telefone, nome de cliente, valor
- O `vik-neutro.webp` e bracos cruzados com cara fechada - **nao usar em
  abertura**, apesar do nome

---

## V1 - Video de venda do programa

**Onde entra:** `parceiros-ganhos.html` e `parceiros.html`, na constante
`MOVIKI_VIDEO_PARCEIRO`. **Nos dois arquivos, na mesma rodada.**
**Publico:** quem chega frio na pagina.
**Duracao estimada: 1:23.**

| # | Fala (texto que vai ao motor) | Tela | Dur. |
| ---: | --- | --- | ---: |
| 1 | Todo bairro tem aquele negócio bom que quase ninguém acha. | Rua de bairro ao entardecer. Sem interface. | 4s |
| 2 | O Mo-víki põe esse negócio no mapa. Em tempo real. E deixa ele vender ao vivo. Em vídeo. Para quem está por perto. | Tela cheia: mapa com o pino. Corte para a tela da live com a sacolinha. | 9s |
| 3 | O Programa de Parceiros existe para quem faz essa apresentação. | Cartão com a marca do programa. Fundo escuro. | 4s |
| 4 | Funciona assim. Você recebe um link com o seu apelido. Todo comerciante que assinar por ele fica vinculado a você. | Tela cheia do painel do parceiro no card do link. Sem dado real. | 7s |
| 5 | A cada mensalidade que ele pagar. Quinze por cento dessa mensalidade entra como comissão para você. | Tela cheia do extrato, com nomes de exemplo. Nenhum valor real. | 6s |
| 6 | Só sobre assinatura efetivamente paga. Plano grátis não gera comissão. E se ninguém assinar. Não entra nada. Isso também faz parte da regra. | Texto sobre fundo escuro. Sem mascote. Sem ícone comemorando. | 9s |
| 7 | Não tem cota para comprar. Não tem taxa para entrar. Não tem meta. Você não ganha por cadastrar gente. Você ganha quando um comércio de verdade usa e paga um serviço de verdade. | Comparação lado a lado da seção Isso não é pirâmide, tirada da própria página. | 12s |
| 8 | E você não começa do zero. Artes prontas separadas por ramo de comércio. Crachá com QR Code. Extrato com o nome de quem gerou cada comissão. Saque no Pix a partir de vinte reais. | Tela cheia da aba Material de apoio. Depois o crachá. | 13s |
| 9 | Antes do link nascer. Tem aulas curtas dentro do painel. Elas explicam o que pode e o que não pode ser dito ao divulgar. É o que protege você. | Tela cheia da biblioteca de aulas do parceiro. | 11s |
| 10 | O cadastro leva um minuto e não custa nada. Depois da aprovação. O seu link está lá. | Formulário de cadastro, plano fixo. Encerra na marca. | 6s |

**A ordem dos blocos e o argumento.** O bloco 6 vem logo depois do 5 de
proposito: a frase que assume que pode nao entrar nada e o que da autoridade a
tudo que veio antes. Tirar esse bloco para "nao assustar" transforma a peca em
promessa de ganho - e ai ela vira anuncio reprovavel.

---

## V2 - Corte vertical para conversa e story

**Onde entra:** DM, status de WhatsApp, story.
**NAO usar como anuncio pago na Meta** - anuncio de comissao por indicacao para
publico frio e o padrao classico de restricao de conta, e a conta antiga do
Moviki ja foi restringida uma vez.
**Formato:** 9x16, legenda queimada. Montado das fontes do V1, **nunca recortado
do master**.
**Duracao estimada: 0:33.** Para fechar em 30 s exatos, o bloco 5 e o primeiro a
sair.

| # | Fala (texto que vai ao motor) | Tela | Dur. |
| ---: | --- | --- | ---: |
| 1 | Você conhece algum comerciante que quase ninguém acha? | Vertical. Rosto ou rua. Sem interface. | 3s |
| 2 | O Mo-víki põe o negócio dele no mapa. E deixa ele vender ao vivo. Em vídeo. | Tela cheia vertical: mapa, depois a live. | 6s |
| 3 | Quem apresenta o Mo-víki a um comerciante pode entrar no Programa de Parceiros. | Cartão do programa. | 5s |
| 4 | Assinou pelo seu link. Você recebe quinze por cento da mensalidade que ele pagar. Enquanto ele pagar. | Card do link no painel. Sem valor real. | 6s |
| 5 | Entrar é de graça. Não tem cota e não tem meta. | Texto sobre fundo escuro. | 4s |
| 6 | Se ninguém assinar. Não entra nada. Essa é a regra inteira. | Mesmo fundo. Sem mascote. | 4s |
| 7 | O link do programa está aqui embaixo. | Cartão final com o endereço da página. | 3s |

---

## V3 - Midia kit em video para o influenciador

**Onde entra:** mandado direto na conversa com o criador, antes de qualquer
proposta. Nao vai para pagina publica.
**Duracao estimada: 2:07.**

| # | Fala (texto que vai ao motor) | Tela | Dur. |
| ---: | --- | --- | ---: |
| 1 | O Mo-víki é uma plataforma para negócio que se move. Feira. Food truck. Loja de bairro. Serviço que vai até o cliente. | Tela cheia do mapa com vários pinos. | 8s |
| 2 | Ele põe o negócio no mapa em tempo real. Dá a ele uma página própria com cardápio. E deixa ele transmitir ao vivo. Com a lista de produtos do lado. | Tela cheia: página pública. Depois o estúdio da live. | 11s |
| 3 | Antes de qualquer coisa. Uma frase honesta. A Mo-víki é o palco. O megafone é seu. | Texto sobre fundo escuro. Sem imagem. | 6s |
| 4 | A gente não entrega audiência pronta. Quem tem audiência é você. O que a gente entrega é um produto que funciona e uma regra clara de comissão. | Mesmo fundo. | 10s |
| 5 | O rastreio é simples. Você escolhe um apelido. Ele vira o seu link e o seu QR Code. Quem se cadastrar por ele fica vinculado a você. | Tela cheia do card do link e do crachá. | 10s |
| 6 | A regra de pagamento. Nível um. Quinze por cento da mensalidade do comerciante que você indicou. A cada mês em que ele pagar. | Cartão dos três níveis, tirado da página do programa. | 9s |
| 7 | Nível dois e nível três. Sete e meio e cinco por cento. Bônus de uma vez só. Pagos apenas no primeiro mês pago. | Mesmo cartão. | 9s |
| 8 | Em todos os níveis. A comissão só existe sobre assinatura efetivamente paga. Recebimento no Pix. A partir de vinte reais. | Aviso de conformidade da página, tela cheia. | 7s |
| 9 | Agora a parte que mais importa para quem publica. O que você pode dizer. | Texto sobre fundo escuro. | 5s |
| 10 | Pode dizer o que o produto faz. Pode dizer a regra da comissão. Pode dizer que entrar é de graça. | Lista em texto, uma linha por vez. | 7s |
| 11 | Não pode dizer quanto alguém vai receber. Não pode falar em renda. Em ganho garantido. Nem em prazo de retorno. Não pode mostrar número de faturamento de ninguém. | Lista em texto, em vermelho suave. | 10s |
| 12 | E toda publicação sua leva a marcação de publicidade. Visível antes do ver mais. | Exemplo de legenda com a marcação no começo. | 5s |
| 13 | Isso não é burocracia. Conteúdo comissionado é publicidade. E o que você publica responde junto com a gente. | Texto sobre fundo escuro. | 7s |
| 14 | O que você recebe pronto. Artes e legendas por ramo de comércio. Crachá com QR. E uma página pública onde qualquer comerciante confere que você é parceiro de verdade. | Aba Material de apoio. Depois a página de verificação. | 11s |
| 15 | Se você topa falar de uma coisa que existe. Do jeito que ela é. Esse programa é para você. | Encerra na marca. | 7s |

**Por que este video existe:** o criador medio recusa o programa no preco, nao no
produto. Este video nao tenta resolver o preco - resolve a **confianca**: mostra
que o rastreio funciona, que a regra e escrita, e que a empresa ja sabe o que nao
pode ser dito. Os blocos 3 e 4 - "a Moviki e o palco, o megafone e seu" - evitam
a conversa em que ele acha que a gente vai trazer audiencia para ele.

**Falta uma decisao antes de mandar este video a alguem:** a condicao do criador.
Quinze por cento vale igual para o feirante e para quem tem audiencia. Sem uma
segunda moeda - cache fixo por peca, bonus por ativacao nos primeiros
comerciantes, ou cupom proprio - a conversa termina no preco.

---

## V4 - Abertura do criador

**Onde entra:** `parceiro.html`, como abertura alternativa para quem marcou
`instagram` em `parceiros/{uid}.canais`. Desenho aprovado em 06/09 e nunca
produzido.
**Duracao estimada: 0:54** - contra 2:54 da abertura de campo, que fala de
feira, carrinho e barraca, e faz o criador concluir na primeira tela que o
programa nao e para ele.

| # | Fala (texto que vai ao motor) | Tela | Dur. |
| ---: | --- | --- | ---: |
| 1 | Oi. Bem-vindo ao Programa de Parceiros da Mo-víki. | Abertura com a marca. Vik acenando. | 3s |
| 2 | Você marcou que vai divulgar nas suas redes. Então essa abertura é a sua. | Texto sobre fundo escuro. | 5s |
| 3 | O que você vai apresentar não é mais um aplicativo. É o jeito de um comércio pequeno ser achado. E de vender ao vivo. Em vídeo. | Tela cheia: mapa e depois a live. | 10s |
| 4 | Seu trabalho aqui não é vender. É apresentar. Quem decide assinar é o comerciante. E ele testa antes. | Texto sobre fundo escuro. | 7s |
| 5 | Você tem um apelido só seu. Ele vira o seu link e o seu QR Code. Quem se cadastrar por ele fica vinculado a você. | Card do link no painel, plano fixo. | 9s |
| 6 | As próximas aulas são as mesmas para todo mundo. Inclusive a de conduta. | Biblioteca de aulas. | 5s |
| 7 | E a de conduta importa mais para quem publica do que para quem conversa na rua. Porque conteúdo que gera comissão é publicidade. E o que você publica responde junto com a gente. | Texto sobre fundo escuro. | 12s |
| 8 | Vamos começar. | Encerra na marca. | 1s |

### A armadilha que o desenho ja resolve

Os modulos extras do criador entram marcados como **`extra: true`**, e
`chavesPublicadas()` **ignora extras**. Assim o total obrigatorio continua o
mesmo para todo mundo e a trava segue valida.

**Sem isso, filtrar aula por perfil derruba a contagem abaixo de `MIN_AULAS = 8`
e a trava DESLIGA INTEIRA** - o link abriria para qualquer um sem assistir nada.
Quem mexer no filtro refaz a conta da trava na mesma rodada.

A abertura **conta para a trava**: ela e justamente a parte que explica por que a
trava existe.

---

## V5 - Demonstracao da ferramenta, SEM gente real

**Decisao de 16/09:** a live com lojista de verdade sai do caminho critico. A
prospecao dos primeiros influenciadores nao pode ficar esperando terceiro
aparecer. O que vai ao ar agora e gravado pelo proprio Paulo, na propria conta.

### A linha que nao se cruza

> **Demonstracao rotulada e legitima. Prova social fabricada, nao.**

Pode: gravar as telas reais com produtos de exemplo e a palavra **DEMONSTRACAO**
visivel no quadro. Pode: dizer em voz alta "e assim que funciona".

Nao pode: chat com mensagens escritas por nos parecendo cliente de verdade,
contador de espectadores inflado, depoimento encenado, "veja o que nossos
lojistas dizem" sem lojista. Isso e fabricar prova, e a peca circula por anos.

### O que substitui a prova social enquanto ela nao existe

Nao e pedir confianca - e **mostrar mecanismo**:

1. **A pagina de verificacao `/v/apelido`**, funcionando na tela: o comerciante
   confere quem e o parceiro.
2. **O extrato por comerciante**, com o nome de quem gerou cada comissao.
3. **O Regulamento**, com a escada de niveis escrita e as clausulas de estorno.
4. **O teste gratis de 30 dias**, que tira o risco do lado do comerciante.

E o angulo honesto com o criador: **"o programa esta comecando, voce chega
antes"**. E verdade, e verificavel, e para quem tem audiencia e um argumento
melhor do que numero de cliente que a gente ainda nao tem.

### O que gravar - tudo na conta do Paulo

| Cena | O que mostra | Como |
| ---: | --- | --- |
| 1 | Mapa com pinos e a pagina publica de um negocio | captura real, tela cheia |
| 2 | Painel: por o titulo e tocar em Entrar ao vivo | captura real |
| 3 | A tela de quem assiste, com o selo AO VIVO | segunda aba, gravada junto |
| 4 | Sacolinha, produto em destaque, preco da live | captura real |
| 5 | Tocar em Quero este e o WhatsApp abrir com a mensagem | numero de exemplo |
| 6 | Encerrar e o resumo da live | captura real |
| 7 | Painel do parceiro: link, cracha, material, extrato | captura real |

**Selo `DEMONSTRACAO` no canto, em todas as cenas de live.** Sai do quadro so
quando existir gravacao de uso real.

**Dado de exemplo, nunca real:** nada de Pix, telefone pessoal, e-mail ou nome de
cliente. O estudio Playwright das videoaulas ja grava painel real contra Firebase
de mentira - e o caminho mais barato para as cenas 1, 2, 4, 6 e 7.

### O ativo que ja existe e nao esta sendo usado

O **filme hero do Modo Live** esta pronto: `n2nmTfGY_mo`, 2:38, no canal
@app.moviki, mais os cortes de 60 s e de 27 s em 9x16 e 4x5. Foi feito para o
lojista, mas serve ao criador **como demonstracao do produto** — e ja passou por
revisao de conformidade.

**Antes de gravar qualquer coisa nova:** publicar o filme hero e usar o corte de
27 s como anexo da primeira mensagem ao influenciador. Custo zero, hoje.

---

## V6 - A live real, quando houver o primeiro lojista

Nao morre: fica para a fase 2, quando o primeiro comerciante pagante existir.
O plano completo continua valendo.

**Antes de gravar, na ordem:**

1. **Por o uid dele em `configuracoes/liveTermos.liveBeta`**, ou esvaziar a lista.
   Com a lista preenchida e sem o uid dele, ele nao enxerga a live e a gravacao
   nao acontece.
2. **Autorizacao de imagem por escrito** - mensagem de WhatsApp serve, desde que
   diga onde o video vai ser usado.
3. Combinar produto e horario. Live vazia nao prova nada.

**O que NAO pode entrar, nem na fase 2:** depoimento dizendo quanto vendeu.
"Vendi trezentos reais na primeira live" e projecao de resultado aos olhos da
Meta e do Google, mesmo sendo verdade e mesmo sendo ele falando. O que entra e
ele falando da **ferramenta**: que foi facil, que a pessoa pediu ali mesmo, que
nao precisou de loja nem de estudio.

**Entrega:** master de 2 a 3 min em 16x9, corte de 45 s em 9x16, H.264 8 bits
(HEVC 10 bits nao toca em celular antigo), legenda queimada nos dois.

---

## Ordem de producao

1. **Publicar o filme hero** e usar o corte de 27 s ja hoje. Custo zero.
2. **V5, a demonstracao sem gente real** - nao depende de ninguem.
3. **V1**, que e o que destrava as duas landings ja no ar esperando o id.
4. **V2**, montado das mesmas fontes do V1.
5. **V3**, quando a condicao do criador estiver decidida - ver [[P39 - Remuneracao do influenciador e midia dos parceiros]].
6. **V4**, junto com a entrega dos modulos extras do P16.
7. **V6, a live real**, quando o primeiro lojista pagante existir.

## Pendencias que este documento deixa

- [ ] Decidir a condicao do influenciador antes de mandar o V3 a alguem
- [ ] Gravar as narracoes no Kairogen e **cronometrar** - os alvos acima sao
      calculados, nao medidos
- [ ] Publicar no YouTube, nao listados, e mandar os links
- [ ] Trocar `MOVIKI_VIDEO_PARCEIRO` nos DOIS arquivos das landings
- [ ] Atualizar `claude/moviki-videoaulas-no-ar.md` com os ids novos - o link e o
      identificador
