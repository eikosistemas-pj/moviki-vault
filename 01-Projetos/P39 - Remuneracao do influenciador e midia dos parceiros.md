---
type: projeto
status: ativo
prioridade: 1
prazo: 2026-10-16
area: A5 - Programa de Parceiros
tags: [influenciador, remuneracao, orcamento, margem, ugc, direito-de-imagem, custo]
atualizado: 2026-09-16
---

# P39 - Remuneracao do influenciador e midia dos parceiros

> As tres formas de remunerar um criador, com o custo de cada uma medido contra a
> margem real do produto; e o mecanismo para transformar a midia que os parceiros
> produzirem em acervo da Moviki. Decidido em 16/09/2026.

Relacionado: [[P37 - Prospeccao de parceiros e influenciadores]] ·
[[P38 - Videos de prospeccao do parceiro]] · [[R - Planos e precos]] ·
[[R - Custos e cotas]] · [[R - Teto de gasto de video no Cloudflare]] ·
[[P19 - Plano de niveis do parceiro]]

Planilha: `MOVIKI - Simulador de remuneracao de influenciador.xlsx`, com todos os
numeros abaixo em formula. Trocar um parametro recalcula tudo.

---

## 1. Quanto sobra de cada cliente - a conta que limita todo o resto

| | Pro | Premium | Enterprise |
| --- | ---: | ---: | ---: |
| Mensalidade | R$ 37,90 | R$ 49,90 | R$ 99,90 |
| Comissao do parceiro, nivel 1 | R$ 5,69 | R$ 7,49 | R$ 14,99 |
| Tarifa do Asaas (estimada) | R$ 2,00 | R$ 2,00 | R$ 2,00 |
| Video da live, cenario leve | - | R$ 6,48 | R$ 6,48 |
| **Margem por mes** | **R$ 30,21** | **R$ 33,93** | **R$ 76,43** |
| Teto de aquisicao, payback em 3 meses | R$ 90,63 | **R$ 101,79** | R$ 229,29 |

**Custo fixo + midia hoje: R$ 831/mes** (Windsor 124,20 + Kairogen 148,80 +
Vercel Pro 108,00 + outros 150,00 estimados + midia 300,00). Isso da **25
clientes Premium** so para empatar a operacao.

> **A regra que sai daqui: nao gastar mais que R$ 100 para conquistar um cliente
> Premium enquanto o caixa for o de hoje.** Com receita entrando, o teto sobe
> para R$ 200 (payback em 6 meses).

**Duas ressalvas honestas:** a tarifa do Asaas e estimativa - confirmar no
extrato; e a retencao de 12 meses e referencia de mercado, nao dado do Moviki: a
base de clientes pagantes reais e **zero** em 16/09.

---

## 2. O ACHADO QUE MUDA A CONTA: a live come a propria mensalidade

O Cloudflare cobra **por minuto entregue**, e minuto entregue e
**espectadores x duracao**. Uma live de 60 min com 30 pessoas custa 1.800
minutos, nao 60.

| Cenario por lojista/mes | Min entregues | Custo | Sobra do Premium |
| --- | ---: | ---: | ---: |
| Nenhuma live | 0 | R$ 0,00 | R$ 40,41 |
| Leve - 2 x 40 min x 15 pessoas | 1.200 | R$ 6,48 | R$ 33,93 |
| Moderado - 4 x 60 x 15 | 3.600 | R$ 19,44 | R$ 20,97 |
| **Ativo - 4 x 60 x 30** | **7.200** | **R$ 38,88** | **R$ 1,53** |
| Deu certo - 4 x 60 x 60 | 14.400 | R$ 77,76 | **-R$ 37,35** |

**Um Premium que usa bem a live da prejuizo.** O produto que mais encanta e o
que destroi a margem, e isso nao aparece em lugar nenhum do painel hoje.

### O teto global protege o caixa e pune o cliente certo

O teto de hoje e **50.000 min por ciclo**, ou seja **R$ 270/mes**. No cenario
"Ativo", ele aguenta **menos de 7 lojistas**. Quando bate, a live e barrada para
**todos** - inclusive para quem esta pagando em dia.

> **PROPOSTA:** alem do teto global, um **teto por lojista por ciclo** -
> Premium 1.500 min, Enterprise 5.000 min - com aviso na propria tela do lojista
> e a opcao de comprar minutos extras. Assim o custo por cliente tem limite, a
> margem fica previsivel, e quem consome nao derruba a live do vizinho.
>
> Sem isso, **qualquer conta de remuneracao de influenciador e chute**: nao se
> sabe quanto vale um cliente novo.

Isso vira projeto proprio. E pre-requisito para escalar aquisicao, nao para
comecar.

---

## 3. As tres opcoes, com custo

Todas somam-se a comissao normal do programa, que continua valendo em qualquer
uma.

### A - Cache fixo por peca

| | |
| --- | --- |
| Valor sugerido | R$ 150 por peca, micro-influenciador local de 5 a 30 mil |
| Escala inicial | 3 criadores, 1 peca cada = **R$ 450, uma vez** |
| Quando sai do caixa | **antes** de qualquer cliente aparecer |
| Para empatar | **12 clientes Premium** pagando um mes |

**Veredito: COMPRA DE MIDIA, nao aquisicao.** Como maquina de clientes, R$ 150
esta acima do teto de R$ 101 - nao fecha. Como **compra de acervo**, fecha bem:
o cache paga a peca **e o direito de usar a peca por 12 meses**, que e
exatamente o material que hoje nao existe. Produzir video equivalente custa mais
que R$ 150 em credito e horas.

**Condicoes obrigatorias no acordo:** cessao de uso por escrito, 12 meses, para
organico e trafego pago; **sem musica licenciada da plataforma** - trilha de
Reels usada em anuncio pago e violacao de direito autoral, e a peca cai; e a
declaracao de que ele tem direito sobre tudo que aparece no video.

### B - Bonus por ativacao

| | |
| --- | --- |
| Valor sugerido | R$ 50 por comerciante que pagar o **SEGUNDO mes** |
| Teto | 10 comerciantes por parceiro, janela de 90 dias |
| Custo maximo com 5 parceiros no teto | R$ 2.500 - **e isso significa 50 comerciantes pagando** |
| Margem ja recebida desse cliente ate o 2o mes | R$ 67,86 |
| Sobra depois de pagar o bonus | **R$ 17,86** |

**Veredito: PADRAO.** So custa quando da certo. O gatilho no **segundo** mes pago
- nao no primeiro - elimina o cadastro que assina e some, e cobre a janela de
estorno. E a unica das tres que nao aposta caixa que ainda nao existe.

**Conformidade:** e pagamento por **assinatura efetivamente paga**, nunca por
cadastro. Isso mantem a regra de ouro do programa intacta e entra no Regulamento
como bonus temporario de campanha, com data de inicio e fim.

### C - Cupom proprio do criador

| | |
| --- | --- |
| Desconto sugerido | R$ 25 no 1o mes do lojista |
| Custo com 20 usos | R$ 500 - **receita que deixa de entrar**, nao caixa que sai |

**Veredito: ADIAR.** Boa para o caixa, ruim para o calendario: **nao existe cupom
no checkout hoje**, e criar um significa mexer no `moviki-robo`, que e o
repositorio de DINHEIRO - o que muda o minimo, por regra do projeto.

**Versao sem codigo, para os primeiros casos:** o dono aplica o desconto na mao,
no Asaas. Serve para 5 ou 10 lojistas; nao serve para escala.

**Atencao que ninguem lembra:** desconto no primeiro mes **reduz a base de
comissao do parceiro** naquele mes, porque a comissao e sobre o valor
efetivamente pago. Se o cupom entrar, isso tem que estar dito ao parceiro antes,
ou vira reclamacao legitima.

---

## 4. A recomendacao

1. **B como padrao**, comecando com 5 parceiros e teto de 10 ativacoes cada.
2. **A uma unica vez, com 3 criadores**, tratado como compra de acervo - e o que
   resolve a falta de material de uma vez so.
3. **C adiado**, versao manual se fizer falta.

**Teto de aquisicao do mes 1: R$ 700** (R$ 450 de cache + R$ 250 de bonus, se os
5 parceiros ativarem um comerciante cada).

### A regra de orcamento que mantem isso auto-financiado

> **O bonus de ativacao do mes nao pode passar da margem que os parceiros geraram
> no mes ANTERIOR.** No mes 1 nao existe margem anterior, entao o teto do mes 1 e
> o valor acima - e ele e gasto de partida, nao recorrente.

E, enquanto a pagina nao converter, **nao aumentar midia paga**: sao 9 dias de
Meta com zero cadastro e o Google parado por saldo.

---

## 5. Midia dos parceiros: o botao de autorizacao

A ideia do Paulo em 16/09: depois que os primeiros criadores produzirem, um botao
no painel do parceiro autoriza a Moviki a usar a midia deles. Acervo sem custo.

**A ideia esta certa. A versao 1 dela nao precisa de upload nenhum.**

### Versao 1 - link, nao arquivo

O parceiro **cola o link do post** e marca o aceite. Nada de upload, nada de
Storage, nada de quota, nada de moderacao de arquivo. A Moviki baixa a peca
quando for usar.

Isso elimina de uma vez: custo de armazenamento, fila de aprovacao, limite de
tamanho, e o risco de receber arquivo que ninguem conferiu.

### Onde mora

- `parceiros/{uid}.midiaAceite` - `{ versao, em, escopo }`, versionado como o
  aceite do Regulamento ja e hoje.
- `parceiros/{uid}/midias/{id}` - `{ url, rede, em, status, semMusicaTerceiro }`.
- Nenhuma regra nova de leitura publica: e do dono e do proprio parceiro.

### O termo - o que ele precisa dizer, sem rodeio

1. **O que a Moviki pode fazer:** publicar e impulsionar a peca nas redes da
   Moviki e em anuncio pago, com credito ao autor, por **12 meses**.
2. **O que o parceiro declara:** que a peca e dele, que quem aparece autorizou, e
   que **nao ha musica licenciada da plataforma** na trilha.
3. **Revogacao:** ele pode retirar a autorizacao quando quiser, e a Moviki tem
   **15 dias uteis** para tirar do ar o que estiver publicado. Peca ja impressa
   nao volta atras - isso precisa estar escrito.
4. **Nao e condicao para nada.** Autorizar midia **nao** influencia aprovacao,
   comissao, nivel ou saque. Se influenciar, deixa de ser consentimento livre e
   vira permuta disfarcada - com problema de LGPD e de direito de imagem junto.

### As tres armadilhas

1. **A autorizacao do parceiro nao cobre terceiros.** Se aparece um cliente, um
   lojista ou a fachada de outra empresa no video, a autorizacao dele nao basta.
   Por isso a declaracao do item 2 existe - e por isso peca com rosto de terceiro
   nao vai para trafego pago sem autorizacao separada.
2. **Musica e o erro mais comum e o mais caro.** O Instagram licencia a trilha
   para post organico de pessoa fisica; **anuncio pago nao esta coberto**. Peca
   com musica so vale para republicacao organica.
3. **`#publi` continua obrigatorio** na publicacao original dele. Republicar uma
   peca sem a marcacao nao conserta a origem.

### Ordem

Nao construir agora. **Primeiro os tres criadores da Opcao A** - o cache ja
compra o direito de uso por contrato, sem codigo nenhum. O botao vira necessario
quando houver dez parceiros publicando, nao tres.

---

## 6. Pendencias

- [ ] Confirmar a tarifa real do Asaas no extrato - hoje e estimativa de R$ 2,00
- [ ] Preencher o custo real de dominio, PABX e Resend na planilha
- [ ] Decidir A, B, C - a recomendacao e B + A uma vez
- [ ] Se B entrar: clausula de bonus temporario de campanha no Regulamento, com
      data de inicio e fim
- [ ] **Teto de minutos por lojista** - pre-requisito para escalar aquisicao
- [ ] Modelo de acordo do criador, com a cessao de uso de 12 meses
