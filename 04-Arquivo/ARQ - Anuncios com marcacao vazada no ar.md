---
type: incidente
status: concluido
data: 2026-09-04
area: A7 — Midia paga
tags: [meta-ads, criativo, incidente, medicao]
atualizado: 2026-09-04
---

# ARQ — Anuncios da campanha de Joao Pessoa com marcacao vazada no ar

## O que aconteceu

Os dois anuncios da campanha `Moviki | Cadastro de lojista | Joao Pessoa | set-2026`
subiram com **marcacao de prompt vazada dentro do texto principal**, visivel para
o publico:

```
...30 dias gratis do plano Pro, sem cartao de credito.</message>
<parameter name="headline">Um link so seu, no mapa
```

O headline pretendido de cada anuncio caiu **dentro** do corpo. Resultado: os dois
subiram com o mesmo titulo generico `Moviki · Coloque seu negocio no mapa`, e o
publico via uma tag de codigo no fim do anuncio.

## Causa

Texto gerado por IA copiado para o Gerenciador de Anuncios sem conferencia do
delimitador final. O campo `headline` foi colado junto com o corpo.

## Impacto medido

Periodo 02/09 a 04/09, campanha de Joao Pessoa:

| Metrica | Valor |
| --- | --- |
| Gasto | R$ 33,06 |
| Impressoes | 5.880 |
| Cliques | 105 |
| CTR | 1,79% |
| CPC | R$ 0,31 |
| Visualizacoes de pagina de destino | 75 |
| Cadastros | 0 |

Anuncio que exibe tag de codigo le como golpe. CTR de 1,79% em publico local frio
e conversao zero sao consistentes com isso.

## Conserto — aplicado em 04/09/2026 pela API

- Texto dos dois anuncios reescrito, marcacao removida.
- Titulos separados: `Coloque seu negocio no mapa` (A) e `Um link so seu, no mapa` (B).
  Antes os dois tinham o mesmo titulo — o A/B nao testava nada.
- Descricao preenchida nos dois, que estava vazia. Entrou o diferencial de
  **sem comissao por venda**.
- `conversion_domain = moviki.com.br` definido nos dois anuncios. Faltava, e sem ele
  a Meta nao atribui conversao de site.
- Campanha `Post do Instagram: Seu negocio vive em movimento` pausada — impulsionamento
  disputando o mesmo publico da campanha estruturada e inflando o CPM dela.

A Meta trata criativo como imutavel: a edicao gerou criativos novos
(`1619212483148311` para o A, `1578263884078928` para o B) e reapontou os anuncios.
Os `ad_id` nao mudaram.

## Regra que nasce daqui

**Nenhum criativo sobe sem leitura do texto final no preview do anuncio.**
Texto vindo de IA passa por conferencia de delimitador antes do Gerenciador.

## Pendencia aberta que este incidente expos

A cadeia de atribuicao esta quebrada mesmo com a CAPI no ar desde 27/08:

- `lib/meta.js` monta `user_data` sem `fbc` e sem `fbp` — sem o parametro do clique,
  a Meta nao liga o `Lead` ao anuncio.
- `api/novo-cliente.js` nao recebe nem repassa esses campos, e nao manda o
  `client_ip_address`, que e uma das chaves de correspondencia mais fortes.
- `comerciantes.html` manda para `https://app.moviki.com.br` **sem repassar** o
  `fbclid` nem as UTMs — a origem se perde no salto de dominio.
- `event_source_url` do `Lead` esta fixo em `https://app.moviki.com.br/`.

Enquanto isso nao for corrigido, a campanha otimiza no escuro.

→ [[ARQ - Meta CAPI]] · [[A6 - Medicao e Analytics]] · [[A7 - Midia paga]]
