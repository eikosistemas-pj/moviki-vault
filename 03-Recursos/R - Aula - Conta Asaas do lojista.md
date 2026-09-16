---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [aula, financeiro, asaas, roteiro, voz-malu]
atualizado: 2026-09-16
---

# R - Aula - Conta Asaas do lojista

Roteiro pronto para gravar. Nasceu da pergunta do Paulo em 16/09: a tela do
Asaas estava "em aberto" para o lojista. Par de
[[ARQ - Conta Asaas na tela do lojista 16092026]] e de
[[P36 - Videoaula da conta Asaas]].

## Ficha

| Item | Valor |
| --- | --- |
| Chave no painel | `mod-asaas` |
| Cena do estudio | `T27-conta-asaas` |
| Onde embute | bloco "Pix automatico (Asaas)" da aba Financeiro |
| Voz | Malu (Kairogen) |
| Duracao alvo | 2:10 a 2:30 |
| Formato | cartelas e mockup em HTML/CSS, 1280x720, 25 fps |

⚠️ **Conferir `claude/moviki-videoaulas-no-ar.md` antes de fixar `T27` e
`mod-asaas`.** A aula `mod-financeiro` saiu de outra frente em 16/09 e ainda
esta sem id do YouTube; duas frentes dando codigo de cena no mesmo dia foi
exatamente o que gerou a colisao da P09 em 11/09.

## Pronuncia

**Escrever `Ásaas` no texto que vai para o motor de voz** — sem o acento a
Malu le *asáas*. Na legenda e no titulo, `Asaas`. Ver
`R - Dicionario de pronuncia da voz Malu`.

## Conformidade

- Nunca dizer quanto o lojista vai vender ou ganhar. So custo e funcionamento.
- Nunca dizer que a conta "sai na hora": a aprovacao e do Asaas, nao do Moviki.
- Nunca sugerir que o Moviki guarda, ve ou movimenta o dinheiro do lojista.
- O video e anuncio aos olhos da Meta e do Google. Vale a secao 3H do mapa.

## Narracao, bloco a bloco

**B1 — Abertura (0:00, ~12 s)**
Cartela: titulo "Como o dinheiro da sua venda chega ate voce".
> No Moviki voce tem dois jeitos de receber pelo cardapio. Os dois poem o
> dinheiro na sua conta, direto. A diferenca esta em quem confere se o
> pagamento caiu.

**B2 — Pix direto (~16 s)**
Mockup do cartao "Pix direto — gratis".
> No Pix direto, o cliente paga no seu Pix e o dinheiro cai na sua conta na
> hora, sem taxa nenhuma. Cada pedido vem com centavos diferentes, entao voce
> acha ele no extrato num piscar. Voce confere e confirma aqui no painel.

**B3 — Pix automatico (~16 s)**
Mockup do cartao "Pix automatico (Asaas)".
> No Pix automatico, quem confere e o sistema. O pagamento cai na sua conta do
> Ásaas e o pedido muda de estado sozinho, sem voce abrir o banco. Para isso o
> Ásaas cobra um real e noventa e nove por Pix recebido, descontado da sua
> conta, e o pedido minimo passa a ser vinte reais.

**B4 — Qual escolher (~18 s)**
Cartela com os dois lado a lado.
> Nao existe o melhor dos dois: existe o melhor para o seu dia. Se voce recebe
> poucos pedidos por dia, conferir no extrato leva segundos e o Pix direto sai
> de graca. Se os pedidos chegam todos ao mesmo tempo, e o tempo de conferir
> que comeca a custar caro — ai o automatico se paga.
> E voce pode comecar no Pix direto hoje e mudar depois. A troca leva um toque.

**B5 — Abrir a conta (~20 s)**
Mockup: botao "Abrir minha conta no Asaas".
> Para usar o automatico, voce precisa de uma conta no Ásaas. A conta e sua,
> nao do Moviki. Toque em "Abrir minha conta no Ásaas": abre o site deles, o
> cadastro e gratuito e leva uns cinco minutos.
> Depois voce envia seus documentos e espera o Ásaas aprovar. Costuma sair no
> mesmo dia, mas pode levar ate dois dias uteis.

**B6 — A espera (~14 s)**
Mockup do aviso "Sua conta no Asaas ainda nao foi aprovada".
> Enquanto o Ásaas nao aprovar, a chave nao funciona aqui — e o painel te
> avisa dizendo exatamente o que esta faltando. Nao e erro do Moviki: e a sua
> conta que ainda esta em analise.
> E ninguem fica parado esperando: no Pix direto voce ja pode vender hoje.

**B7 — A chave (~16 s)**
Mockup: Integracoes > chave de API.
> Conta aprovada, entre no Ásaas, va em Integracoes e gere a sua chave de
> API. Use a chave de producao, nunca a de teste — a de teste emite um Pix que
> nao cai na conta de ninguem. Se voce colar a de teste, o painel recusa e te
> avisa.

**B8 — Seguranca (~22 s)**
Cartela de atencao, fundo ambar.
> Agora a parte mais importante deste video. Essa chave vale para a sua conta
> inteira no Ásaas. Cole ela so aqui, no seu painel, e nao mande para mais
> ninguem: nem para amigo, nem para quem oferecer ajuda, nem para o suporte do
> Moviki — o suporte do Moviki nunca vai te pedir essa chave. Se alguem pedir,
> desconfie na hora.
> Aqui ela fica guardada criptografada, nunca aparece de novo nesta tela, e o
> Moviki usa ela para uma coisa so: criar e conferir os Pix dos seus pedidos.
> O seu saldo, o Moviki nao ve e nao mexe.

**B9 — Conectar e conferir (~18 s)**
Mockup do cartao verde "Conta conectada".
> Colou a chave, toque em "Conectar minha conta". O painel mostra o nome do
> titular da conta que voce acabou de ligar. Olhe esse nome: ele tem que ser o
> seu. Se aparecer outro nome, desconecte na hora.
> E voce pode desconectar quando quiser. Se a sua venda estiver ligada no Pix
> automatico, ela desliga junto — o painel avisa antes de voce confirmar.

**B10 — Fecho (~14 s)**
Cartela com o resumo dos dois modos.
> Resumindo: Pix direto, de graca, voce confere. Pix automatico, um real e
> noventa e nove por Pix, o sistema confere. Os dois poem o dinheiro na sua
> conta.
> Escolha o que combina com o seu movimento de hoje. Amanha voce troca, se
> quiser.

## Cenas do estudio

| Bloco | Cena | Elemento |
| --- | --- | --- |
| B1, B4, B10 | cartela | texto grande, fundo do painel |
| B2, B3 | mockup | os dois cartoes de modo, um destacado por vez |
| B5, B7, B9 | mockup | botao, passo a passo e cartao verde da aba |
| B6 | mockup | aviso de conta pendente com a lista do que falta |
| B8 | cartela ambar | mesmo tom do alerta da tela (`#251d10` / `#e8c98a`) |

Reaproveitar os tokens de cor da aba: fundo `#111a24`, borda `#1e2c3a`, verde
`#3ddc97`, azul do botao `#00b4ff` a `#0066ff`.

## Ligacoes

[[ARQ - Conta Asaas na tela do lojista 16092026]] ·
[[P36 - Videoaula da conta Asaas]] · [[P31 - Financeiro e cardapio compravel]] ·
[[R - Dicionario de pronuncia da voz Malu]]
