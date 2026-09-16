---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [regras, armadilha]
atualizado: 2026-09-16
---

# R - Regras de ouro novas de 16092026

Apêndice de [[R - Regras de ouro]]. Nasceram do teste de fumaça da live.

## Migracao e leitura de estado

- **Migrar a fonte da verdade sem varrer quem lê a fonte velha deixa
  funcionalidade morta e silenciosa.** O b5b trocou a autoridade da live de
  `estado/live` para `live_sessoes` e deixou **quatro** leitores para trás: o
  Pix da live, a baixa de estoque, a janela do chat e o selo AO VIVO. Nenhum deu
  erro. Depois de migrar, varrer TODO leitor do campo antigo, no mesmo dia.
- **Campo zerado de propósito é pior que campo apagado.** `ativa:false` e
  `pulso:null` continuam existindo e passam por qualquer teste de existência: o
  código lê, acredita e responde "não" para sempre.
- **Dois lados que decidem a mesma coisa lendo documentos diferentes nunca vão
  concordar.** A página mostrava a live no ar e o checkout dizia que tinha
  acabado.
- **Comparação de igualdade entre dois campos mortos passa.** `'' === ''` é
  verdadeiro: a baixa de estoque valia para qualquer live, e ninguém veria
  enquanto nenhuma compra fechasse.

## Teste

- **Teste de fumaça só vale percorrendo o fluxo até o fim.** O Pix quebrado só
  apareceu porque se chegou à tela de gerar o QR — todas as etapas anteriores
  passaram.
- **Teste em condição ruim dá falso negativo.** 4G fraco derruba o vídeo por
  sinal, não por defeito; adiar o teste é a decisão técnica correta.
- **Roteiro de teste que pede o que a tela não mostra naquele momento gera caça
  a bug inexistente.** O limite da live só aparece depois de transmitir.

## Moderacao e conformidade

- **Filtro do que não pode ser VENDIDO e filtro do que não pode ser DITO são
  listas separadas.** O primeiro roda no nome de produto; palavrão ali dentro
  impede o lojista de cadastrar "galinha caipira".
- **Lista de palavrão pronta é matéria-prima, não produto.** Contra o público do
  Moviki, a lista pública bloqueava *delícia*, *gostoso*, *galinha*, *pinto*,
  *banca* (onde o feirante trabalha), *sob* e *paraiba*.
- **Filtro por substring precisa de piso de tamanho.** Sem isso "disputa" vira
  "puta" e "cuscuz" vira "cu". Busca de termo sem espaço só em texto
  reconhecidamente ofuscado.
- **Bloqueio de conteúdo vale no envio E na leitura**, senão o que já está
  gravado continua na tela.
- **Link de espectador no chat de live de venda é vetor de golpe**, não
  comodidade. Nenhuma plataforma de live commerce permite. Só o dono da live.

## Pagamento

- **Não prometa confirmação automática onde não existe gateway.** No modo chave
  Pix própria, "esta tela confirma sozinha" deixa o comprador esperando até o
  Pix vencer — depois de já ter pago.
- **Comprovante de Pix não é prova; dinheiro na conta é.** Os centavos
  identificadores são a prova, e são conferidos no extrato, não num print.
- **Anexo sensível nunca vai pelo chat público** — vai como anexo privado do
  pedido.
- **Confirmação que depende de clique humano contamina a métrica.** "Vendido
  pelo Pix" passa a medir a diligência do lojista, não a venda.

## Interface

- **Reforma visual só é segura quando não toca handler.** Envolver o que existe
  num contêiner `display:contents` e acionar os botões originais mantém intacto
  o que já foi testado.
- **No celular, a tela é do produto.** Ferramenta que rouba metade do visor
  durante a transmissão atrapalha a única coisa que a live precisa fazer.

## Ligacoes

[[R - Regras de ouro]] · [[A13 - Modo Live]] ·
[[ARQ - Regressoes da migracao b5b 16092026]]
