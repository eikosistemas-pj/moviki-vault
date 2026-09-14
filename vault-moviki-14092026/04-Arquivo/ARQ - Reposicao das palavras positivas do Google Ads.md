---
type: decisao
status: concluido
area: A7 - Aquisicao e Midia Paga
tags: [moviki, google-ads, aquisicao, autonomia, palavras-chave]
atualizado: 2026-09-11
---

# ARQ - Reposição das palavras positivas do Google Ads

> Depois do conserto de 11/09 a campanha de Pesquisa ficou tecnicamente limpa mas
> **sem alcance**: 4 impressões e zero clique no dia. As 10 palavras que sobraram no
> Grupo 1 são todas de nicho itinerante e não têm volume de busca. Paulo transferiu a
> palavra positiva para a rotina e mandou repor. Feito no mesmo dia: **+25 palavras**
> em frase e **+32 negativas** novas. Conta **718-683-2490**.

---

## 1. O que o pulso de 11/09 encontrou

Dado de 10/09:

| Lado | Gasto | Cliques | Conversão |
| --- | --- | --- | --- |
| Google | R$ 20,33 | 12 | 0 |
| Meta (campanha antiga) | R$ 9,44 | 34 | 0 |

Nove dos doze cliques do Google foram em termo de GPS e satélite — o vazamento já
diagnosticado, no último dia antes do conserto.

O achado do dia foi o oposto do esperado: em 11/09 **nenhuma palavra em ampla
registrou impressão** — o conserto pegou. Mas a campanha inteira entregou **4
impressões** até as 07h, contra 57 por dia antes.

## 2. Falso alarme do primeiro relatório — lição de leitura

O primeiro relatório da manhã disse que o **Grupo 1 tinha ficado vazio** de palavra
positiva. Errado.

A leitura com `include_inactive: true` devolve palavras **removidas** junto com as
ativas, porque elas ainda carregam dado histórico da janela consultada. As três amplas
apareceram na lista com `criterion_id` e gasto acumulado, e isso foi lido como "ainda
estão lá". A prova veio pela escrita: um `remove_keywords` contra os três ids devolveu
**"Resource was not found"** nos três.

> **Lição:** no Google Ads, presença de uma palavra numa leitura com `include_inactive`
> NÃO significa que ela está ativa. Para saber o estado real, tentar a escrita — a
> recusa é a resposta. O mesmo vale ao contrário: ausência numa leitura sem
> `include_inactive` só quer dizer que ela não serviu naquela janela.

O Grupo 1 nunca ficou vazio: tinha 10 palavras em frase e exata (`sistema para food
truck`, `app para feirante`, `divulgar carrinho de lanche`…), todas com **zero
impressão em 7 dias**. O problema não era estrutura, era **volume de busca**.

## 3. A mudança de autonomia

Regra anterior (manhã de 11/09): palavra positiva era recomendação, nunca ação.
Paulo revogou no mesmo dia:

> "Eu quero que você tome conta das campanhas, e não deixe ela cair. Faça as palavras
> positivas, coloque lá. Eu não vou colocar não, quem vai colocar é você."

**A partir de 11/09, palavra positiva é ação do assistente**, não recomendação. A
proibição de correspondência **AMPLA** continua intacta, e a regra de que a palavra
descreve o problema de quem vende — nunca a funcionalidade do produto — continua sendo
o filtro de toda palavra nova.

## 4. O que entrou — 11/09/2026

### Grupo 2 — Cardápio digital (`197850432137`) · +8 em frase
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

**Total após a reposição: 53 palavras, todas PHRASE ou EXACT. Zero BROAD.**

## 5. Blindagem que entrou junto

Palavra mais genérica atrai lixo mais genérico. Antes de as novas começarem a servir,
**+32 negativas de frase** no nível campanha:

| Bloco | Qtd | Exemplos |
| --- | --- | --- |
| Sobra do vazamento de mapa | 7 | mapa virtual · mapa real · navegador mapa · mapa 3d · mapa do satelite |
| Infoproduto e serviço | 11 | curso · consultoria · mentoria · agencia de marketing · ebook · franquia · emprego · vaga · salario |
| Quem quer o ARQUIVO, não o sistema | 8 | template · para imprimir · canva · pdf · editavel · word · excel · grafica |
| Compra e montagem de food truck | 5 | montar food truck · comprar food truck · food truck a venda · food truck preco · como montar |
| Consumidor final | 1 | receita |

Negativas da campanha: 61 → **93**.

`gratis` ficou de fora de propósito — `cardapio digital gratis` é palavra positiva.

## 6. Conferido no mesmo dia

- Os 3 grupos: `ad_group_status` ENABLED
- Os 3 anúncios responsivos: `ad_group_ad_status` ENABLED e
  `policy_summary_approval_status` **APPROVED** — nenhum ficou pausado na criação, que
  era a suspeita (a ação `create_responsive_search_ad` entrega pausado por padrão)
- As 53 palavras lidas de volta: nenhuma BROAD

## 7. Volume de busca — o que o Keyword Planner mostrou

Levantamento no mesmo dia pela ponte, 3.070 ideias a partir de 10 sementes, 73 com
1.000+ buscas/mês. O bloco aderente ao Moviki gira em torno de catálogo e WhatsApp:

| Termo | Buscas/mês | Concorrência |
| --- | --- | --- |
| catálogo online | 2900 | MEDIUM |
| catalogo digital | 1600 | MEDIUM |
| catálogo online grátis | 1300 | HIGH |
| criar catalogo online | 1000 | HIGH |
| catálogos digitais | 880 | MEDIUM |
| catálogo digital como fazer | 720 | HIGH |
| vender pelo whatsapp | 480 | MEDIUM |
| vendas pelo whatsapp | 480 | MEDIUM |
| vendas whatsapp | 320 | LOW |

**Descartados de propósito:** o bloco de e-commerce clássico (`loja virtual` 9.900,
`como criar um site de vendas` 4.400) — não é o Moviki — e o bloco de `link de
pagamento` (8.100), que é busca por adquirente, não por plataforma.

## 8. O que fica em aberto

- [ ] **Teto de CPC de R$ 2,00 contra palavra competitiva.** `cardapio digital` disputa com Goomer, Anota AI e Cardápio Web, onde o CPC de mercado passa de R$ 3. Com teto de R$ 2 essas palavras podem simplesmente não entregar, e o sintoma será impressão perto de zero. **Lance continua sendo recomendação, não ação** — decisão do Paulo
- [ ] Avaliar entrar no cluster de catálogo/WhatsApp levantado na seção 7
- [ ] Reposição de saldo — ele mesmo faz

## Ligações

[[A7 - Aquisicao e Midia Paga]] · [[P21 - Google Ads campanha de pesquisa]] ·
[[ARQ - Vazamento de trafego no Google Ads e conserto]] ·
[[ARQ - Pulso das campanhas 12 e 13092026]] ·
[[R - Rotina de checagem das campanhas]] · [[R - Armadilhas do Google Ads]] ·
[[R - Regras de ouro]] · [[R - Links e identificadores]]
