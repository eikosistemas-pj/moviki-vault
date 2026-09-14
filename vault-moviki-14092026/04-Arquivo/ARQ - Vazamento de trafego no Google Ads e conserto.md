---
type: incidente
status: concluido
area: A7 - Aquisicao e Midia Paga
tags: [moviki, google-ads, aquisicao, armadilha, palavras-chave]
atualizado: 2026-09-11
---

# ARQ - Vazamento de tráfego no Google Ads e conserto

> A campanha de Pesquisa queimou **R$ 38,78 em 21 cliques com zero conversão** porque
> cinco palavras estavam em **correspondência AMPLA** — incluindo literalmente
> "localização em tempo real" e "mapa em tempo real". Consertado em 11/09/2026.
> Conta **718-683-2490** (Eiko Sistemas).

---

## 1. O sintoma

Leitura dos termos de pesquisa de 09 a 10/09 (52 termos registrados):

| Termo | Cliques | Gasto |
| --- | --- | --- |
| localização em tempo real | 1 | R$ 2,00 |
| quero ver minha localização | 1 | R$ 1,99 |
| mapa em tempo real | 1 | R$ 1,99 |
| minha localização atual agora maps | 1 | R$ 1,98 |
| acessar minha localização | 1 | R$ 1,98 |
| ver rua em tempo real via satélite grátis | 1 | R$ 1,96 |
| satélite ao vivo do brasil em tempo real | 1 | R$ 1,72 |
| imagens via satélite em tempo real | 1 | R$ 1,63 |
| mapa meteorológico em tempo real | 1 | R$ 1,57 |
| mapa do mundo em tempo real | 1 | R$ 1,47 |

**Nenhum termo de food truck apareceu.** Todo o gasto foi de pessoa física procurando
GPS, Google Maps ou imagem de satélite. CPC médio de R$ 1,85 contra teto de R$ 2,00 —
a campanha pagava quase o teto por clique inútil.

## 2. A causa real

O diagnóstico inicial foi errado: culpou-se a expansão automática do Google por falta
de inventário (7 das 10 palavras em "baixo volume"). A leitura da estrutura pela ponte
do Windsor mostrou outra coisa — **cinco palavras em correspondência AMPLA no Grupo 1**,
que o documento de 09/09 não registrava:

- `mapa em tempo real` (ampla)
- `mapa tempo real` (ampla)
- `localização em tempo real` (ampla)
- `sistema para food truck` (ampla)
- `app para food truck` (ampla)

As três primeiras descrevem o **produto**, não o **cliente**. Em correspondência ampla
o Google entende "usuário que quer ver um mapa em tempo real" — que é o consumidor
final, não o lojista. As duas últimas já existiam em frase e exata; a versão ampla só
somava porta aberta.

**Lição:** descrever a própria funcionalidade como palavra-chave atrai quem quer usar
a funcionalidade de graça, não quem quer vendê-la. A palavra tem que descrever o
problema do lojista, nunca o recurso do produto.

## 3. O conserto — 11/09/2026

Tudo executado pela ponte do Windsor, sem tocar no painel.

- **Removidas as 5 palavras em correspondência ampla** do Grupo 1 — ver a ressalva na seção 6
- **+27 negativas** no nível campanha: onde estou · onde eu estou · minha localizacao ·
  localizacao atual · google maps · maps · satelite · imagem de satelite · gps ·
  rastrear · rastreador · coordenadas · latitude · longitude · bussola · altitude ·
  meteorologico · street view · qual rua · que lugar · cidade que estou ·
  mapa do mundo · mundo em tempo real · terra em tempo real · planeta · ao vivo · celular
  (negativas da campanha: 34 → **61**)
- **Grupo 2 — Cardápio digital** (`197850432137`) criado ativo, 9 palavras em frase e exata
- **Grupo 3 — Ser encontrado** (`200983560958`) criado ativo, 9 palavras em frase
- **2 anúncios responsivos** novos, 15 títulos e 4 descrições cada, destino
  `comerciantes.html`, caminhos `/cardapio/qr-code` e `/divulgar/meu-negocio`
- **3 sitelinks** recriados (Ver os planos · Conheça o Moviki · Criar conta grátis)
- **6 frases de destaque** e o **telefone (41) 2018-6848** recriados no nível campanha

Conferido lendo de volta: as 34 negativas antigas **estavam salvas** — aquele item do
checklist de 09/09 era falso alarme.

## 4. Achado sobre a ponte do Windsor

O documento de 10/09 dizia que o conector do Google Ads estava quebrado por limite do
plano gratuito. **Não está.** Em 11/09 a ponte entrega a conta certa
(**718-683-2490 · Eiko Sistemas**) e aceita **leitura e escrita**: negativas, grupos,
palavras, anúncios responsivos, sitelinks, destaques, telefone, orçamento, estratégia
de lance, teto de CPC, idioma, agenda e segmentação geográfica.

Os três "Caminhos" daquele documento ficam descartados. Nada a assinar por causa disso.

**O que a ponte NÃO faz:** remover o recurso de Local (o endereço de Curitiba que vem
do Perfil da Empresa). Não é critério de campanha, é asset de nível conta — só pelo
painel. **Saldo também não passa pela ponte:** ela entrega gasto, não saldo, e a
reposição é feita pelo próprio Paulo.

## 5. Regra de ouro que nasce daqui

> **Correspondência AMPLA é proibida no Google Ads do Moviki.** Só frase e exata.
> E palavra-chave nunca descreve a funcionalidade do produto ("mapa em tempo real",
> "localização em tempo real") — descreve o problema de quem vende.

## 6. Ressalva importante — o conserto foi parcial

Na leitura de **13/09** pela ponte, **3 das 5 palavras continuavam ativas em BROAD**
(`mapa em tempo real`, `mapa tempo real`, `localizacao em tempo real`). Só as duas de
food truck realmente saíram da ampla. O que segurou o vazamento entre 11 e 13/09 foram
as **negativas**, não a remoção. Detalhe em [[ARQ - Pulso das campanhas 12 e 13092026]].

> **Conserto se confere lendo o objeto alterado, nunca o relatório de gasto.**
> Gasto zero pode ser sintoma suprimido, não causa removida.

## 7. O que fica

- [x] Reler os termos de pesquisa em 13/09 — feito, o vazamento de GPS/satélite parou
- [x] Confirmação de identidade do Google — resolvida em 11/09
- [ ] Remover o recurso de Local (Curitiba) — manual, no painel; considerado irrelevante por ora
- [ ] Deixar só **Inscrição** como conversão principal
- [ ] Repor saldo do Google — feito pelo próprio Paulo

## Ligações

[[A7 - Aquisicao e Midia Paga]] · [[P21 - Google Ads campanha de pesquisa]] ·
[[P23 - Acesso do Claude ao Google Ads]] ·
[[ARQ - Reposicao das palavras positivas do Google Ads]] ·
[[ARQ - Pulso das campanhas 12 e 13092026]] ·
[[ARQ - O funil real do trafego pago]] ·
[[R - Rotina de checagem das campanhas]] · [[R - Armadilhas do Google Ads]] ·
[[R - Checklist conformidade Meta e Google]] · [[R - Regras de ouro]] ·
[[R - Links e identificadores]]
