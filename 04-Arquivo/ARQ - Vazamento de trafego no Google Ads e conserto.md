---
type: incidente
status: concluido
area: trafego-pago
tags: [moviki, google-ads, aquisicao, armadilha, medicao]
atualizado: 2026-09-11
---

# ARQ - Vazamento de trafego no Google Ads e conserto

> A campanha de Pesquisa queimou **R$ 38,78 em 21 cliques com zero conversão** porque cinco
> palavras estavam em **correspondência ampla** — incluindo literalmente
> "localização em tempo real" e "mapa em tempo real". Consertado em 11/09/2026.

Relacionado: [[Moviki — Google Ads]] · [[R - Regras de ouro]] · [[R - Checklist conformidade Meta e Google]]

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
GPS, Google Maps ou imagem de satélite. CPC médio de R$ 1,85, teto de R$ 2,00 —
ou seja, a campanha pagava quase o teto por clique inútil.

## 2. A causa real

O diagnóstico inicial foi errado: culpei a expansão automática do Google por falta de
inventário (7 das 10 palavras em "baixo volume"). A leitura da estrutura pela ponte
mostrou outra coisa — **cinco palavras em correspondência AMPLA no Grupo 1**, que o
documento de 09/09 não registrava:

- `mapa em tempo real` (ampla)
- `mapa tempo real` (ampla)
- `localização em tempo real` (ampla)
- `sistema para food truck` (ampla)
- `app para food truck` (ampla)

As três primeiras descrevem o **produto**, não o **cliente**. Em correspondência ampla,
o Google entende "usuário que quer ver um mapa em tempo real" — que é o consumidor
final, não o lojista. As duas últimas já existiam em frase e exata; a versão ampla
só somava porta aberta.

**Lição:** descrever a própria funcionalidade como palavra-chave atrai quem quer usar
a funcionalidade de graça, não quem quer vendê-la. A palavra tem que descrever o
problema do lojista, nunca o recurso do produto.

## 3. O conserto (11/09/2026)

Tudo executado pela ponte do Windsor, sem tocar no painel.

- **Removidas as 5 palavras em correspondência ampla** do Grupo 1
- **+27 negativas** no nível campanha: onde estou · onde eu estou · minha localizacao ·
  localizacao atual · google maps · maps · satelite · imagem de satelite · gps ·
  rastrear · rastreador · coordenadas · latitude · longitude · bussola · altitude ·
  meteorologico · street view · qual rua · que lugar · cidade que estou ·
  mapa do mundo · mundo em tempo real · terra em tempo real · planeta · ao vivo · celular
  (total de negativas na campanha passou de 34 para **61**)
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
(718-683-2490 · Eiko Sistemas) e aceita **leitura e escrita**: negativas, grupos,
palavras, anúncios responsivos, sitelinks, destaques, telefone, orçamento, estratégia
de lance, teto de CPC, idioma, agenda e segmentação geográfica.

Os Caminhos 1, 2 e 3 daquele documento ficam descartados. Nada a assinar.

**O que a ponte NÃO faz:** remover o recurso de Local (o endereço de Curitiba que vem
do Perfil da Empresa). Não é critério de campanha, é asset de nível conta — só pelo
painel.

## 5. Regra de ouro que nasce daqui

> **Correspondência ampla é proibida no Google Ads do Moviki.** Só frase e exata.
> E palavra-chave nunca descreve a funcionalidade do produto ("mapa em tempo real",
> "localização em tempo real") — descreve o problema de quem vende.

Entra em [[R - Regras de ouro]].

## 6. O que fica pendente

- [ ] Remover o recurso de Local (Curitiba) — manual, no painel
- [ ] Repor saldo até ~14/09
- [ ] Confirmação de identidade do Google — obrigatória a partir de 23/09
- [ ] Deixar só **Inscrição** como conversão principal
- [ ] Reler os termos de pesquisa em 13/09 para conferir se o vazamento parou
