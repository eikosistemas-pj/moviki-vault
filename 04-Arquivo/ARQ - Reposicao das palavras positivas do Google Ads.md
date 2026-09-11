---
type: decisao
status: concluido
area: trafego-pago
tags: [moviki, google-ads, aquisicao, autonomia, palavras-chave]
atualizado: 2026-09-11
---

# ARQ - Reposicao das palavras positivas do Google Ads

> Depois do conserto de 11/09, a campanha de Pesquisa ficou tecnicamente limpa mas
> **sem alcance**: 4 impressoes e zero clique no dia. As 10 palavras que sobraram no
> Grupo 1 sao todas de nicho itinerante e nao tem volume de busca. Paulo transferiu a
> palavra positiva para a rotina e mandou repor. Feito no mesmo dia: **+25 palavras**
> em frase, **+32 negativas** novas.

Relacionado: [[ARQ - Vazamento de trafego no Google Ads e conserto]] · [[R - Regras de ouro]] · [[R - Rotina de checagem das campanhas]]

---

## 1. O que o pulso de 11/09 encontrou

Dado de 10/09, conta 718-683-2490:

| Lado | Gasto | Cliques | Conversao |
| --- | --- | --- | --- |
| Google | R$ 20,33 | 12 | 0 |
| Meta (campanha antiga) | R$ 9,44 | 34 | 0 |

Nove dos doze cliques do Google foram em termo de GPS e satelite — o vazamento ja
diagnosticado, no ultimo dia antes do conserto. Nada novo.

O achado do dia foi o oposto do esperado: em 11/09, **nenhuma palavra em
correspondencia ampla registrou impressao**. O conserto pegou. Mas a campanha inteira
entregou 4 impressoes ate as 07h, contra 57 por dia antes.

## 2. Falso alarme do primeiro relatorio — licao de leitura

O primeiro relatorio da manha disse que o **Grupo 1 tinha ficado vazio** de palavra
positiva. Errado.

A leitura com `include_inactive: true` devolve palavras **removidas** junto com as
ativas, porque elas ainda carregam dado historico da janela consultada. As tres amplas
apareceram na lista com `criterion_id` e gasto acumulado, e isso foi lido como "ainda
estao la".

A prova veio pela escrita: um `remove_keywords` contra os tres ids devolveu
**"Resource was not found"** nos tres. Ja estavam removidas.

> **Licao:** no Google Ads, presenca de uma palavra numa leitura com `include_inactive`
> NAO significa que ela esta ativa. Para saber o estado real, tentar a escrita — a
> recusa e a resposta. O mesmo vale ao contrario: ausencia numa leitura sem
> `include_inactive` so quer dizer que ela nao serviu naquela janela.

O Grupo 1 nunca ficou vazio: tinha 10 palavras em frase e exata (`sistema para food
truck`, `app para feirante`, `divulgar carrinho de lanche`...). Todas com **zero
impressao em 7 dias**. O problema nao era estrutura, era **volume de busca**.

## 3. A mudanca de autonomia

Regra anterior (manha de 11/09): palavra positiva era recomendacao, nunca acao.

Paulo revogou no mesmo dia:

> "Eu quero que voce tome conta das campanhas, e nao deixe ela cair. Faca as palavras
> positivas, coloque la. Eu nao vou colocar nao, quem vai colocar e voce."

**Palavra positiva passou a ser acao da rotina.** A proibicao de correspondencia AMPLA
continua intacta, e a regra de que a palavra descreve o problema de quem vende — nunca
a funcionalidade do produto — continua sendo o filtro de toda palavra nova.

## 4. O que entrou (11/09/2026)

### Grupo 2 — Cardapio digital (`197850432137`) · +8 em frase
`cardapio digital` · `cardapio digital gratis` · `fazer cardapio digital` ·
`menu digital qr code` · `cardapio digital para restaurante` ·
`cardapio digital para delivery` · `criar cardapio online` · `cardapio por qr code`

### Grupo 3 — Ser encontrado (`200983560958`) · +9 em frase
`como atrair mais clientes` · `como conseguir mais clientes` · `como divulgar minha loja` ·
`como divulgar meu comercio` · `cadastrar meu negocio no google` ·
`como divulgar meu negocio no google` · `divulgar meu negocio local` ·
`link na bio para negocio` · `como aumentar as vendas do meu negocio`

### Grupo 1 (`206808639824`) · +8 em frase
`divulgar food truck` · `como atrair clientes para food truck` ·
`aplicativo para vendedor ambulante` · `sistema para trailer de lanche` ·
`divulgar barraca de feira` · `como divulgar carrinho de cachorro quente` ·
`divulgar quiosque` · `como atrair clientes para lanchonete`

**Total apos a reposicao: 53 palavras, todas PHRASE ou EXACT. Zero BROAD.**

## 5. Blindagem que entrou junto

Palavra mais generica atrai lixo mais generico. Antes de as novas comecarem a servir,
**+32 negativas de frase** no nivel campanha:

- **Sobra do vazamento de mapa (7):** mapa virtual · mapa real · navegador mapa ·
  mundo para ver · local que estou · mapa 3d · mapa do satelite
- **Infoproduto e servico (11):** curso · cursos · consultoria · mentoria ·
  agencia de marketing · ebook · franquia · emprego · vaga · salario · quanto ganha
- **Quem quer o ARQUIVO, nao o sistema (8):** template · para imprimir · canva · pdf ·
  editavel · word · excel · grafica
- **Compra e montagem de food truck (5):** montar food truck · comprar food truck ·
  food truck a venda · food truck preco · como montar
- **Consumidor final (1):** receita

Negativas da campanha passaram de 61 para **93**.

`gratis` ficou de fora de proposito — `cardapio digital gratis` e palavra positiva.

## 6. Conferido no mesmo dia

- Os 3 grupos: `ad_group_status` ENABLED
- Os 3 anuncios responsivos: `ad_group_ad_status` ENABLED e
  `policy_summary_approval_status` **APPROVED** — nenhum ficou pausado na criacao,
  que era a suspeita (a acao `create_responsive_search_ad` entrega pausado por padrao)
- As 53 palavras lidas de volta: nenhuma BROAD

## 7. Pendencias que sairam da lista

- ~~Confirmacao de identidade do Google~~ — **resolvida**, declarada por ele em 11/09
- ~~Remover o recurso de Local (Curitiba)~~ — ele considera irrelevante por ora
- Reposicao de saldo — ele mesmo faz

## 8. O que fica em aberto

- [ ] **Teto de CPC de R$ 2,00 contra palavra competitiva.** `cardapio digital` disputa
      com Goomer, Anota AI e Cardapio Web, onde o CPC de mercado passa de R$ 3. Com teto
      de R$ 2 essas palavras podem simplesmente nao entregar, e o sintoma sera
      identico ao de hoje: impressao perto de zero. Lance continua sendo recomendacao,
      nao acao — decisao do Paulo.
- [ ] **Ler os termos de pesquisa em 13/09.** E a primeira leitura com as palavras novas
      ja rodando; e onde se ve se a blindagem de 32 negativas foi suficiente ou se as
      genericas do Grupo 3 abriram porta nova.
- [ ] Zero conversao continua. Meta queimou R$ 103,67 em 348 cliques e zero lead em 14
      dias antes de ser pausada. O gargalo medido segue sendo a comerciantes.html
      (215 visitantes -> 5 cliques no CTA), nao a campanha.

---

**PENDENTE DE SYNC**
