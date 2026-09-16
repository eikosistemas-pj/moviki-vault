---
type: incidente
status: resolvido
area: A13 - Modo Live
tags: [live, regressao, b5b, incidente, armadilha]
atualizado: 2026-09-16
---

# ARQ - Regressoes da migracao b5b 16092026

Quatro funcionalidades da live estavam quebradas desde 15/09 pela **mesma
causa**, nenhuma delas com erro na tela ou no console. Todas foram encontradas
no teste de fumaça de 16/09 — ver [[ARQ - Teste de fumaca da live executado 16092026]].

## A causa

O b5b de 15/09 (achado A2 da auditoria) separou **conteúdo** de **autoridade**:

- `negocios/{uid}/estado/live` — escrito pelo lojista: título, sacola, oferta,
  cupom, brinde. **Conteúdo.**
- `live_sessoes/{uid}` — escrito só pelo Admin SDK: `ativa`, `whep`, `pulsoEm`,
  `inicioEm`, `sessaoId`, `encerradaPor`. **Autoridade.**

O estúdio passou a gravar, de propósito, `ativa:false`, `whep:''` e `pulso:null`
no documento antigo. Quem continuou lendo esses campos para **decidir** alguma
coisa passou a receber sempre "não". Sem erro, sem log: a funcionalidade
simplesmente não acontecia.

## Os quatro

| Onde | O que quebrou | Conserto |
| --- | --- | --- |
| `moviki-robo/lib/checkout.js` | **100% das compras na live** recusadas com `live_fora` — oferta e sacolinha | autoridade passa a vir de `live_sessoes` |
| `checkout.js` → `marcarPago` | `liveId` virou `''` dos dois lados; `'' === ''` dava baixa de estoque em **qualquer** live do lojista | compara `sessaoId` |
| `moviki/live.html` | chat da live anterior aparecia na live nova: `ms(est.inicio)` sumiu e caía no fallback de **1 hora** | janela começa em `ses.inicioEm` |
| `moviki/404.html` | selo **AO VIVO** nunca aparecia na página do negócio, em live nenhuma | lê `live_sessoes` |

## Varredura de fechamento

Cinco repositórios varridos em 16/09 atrás de qualquer leitura de `ativa`,
`whep`, `pulso` ou `inicio` de `estado/live`. **Não há quinto caso.**

Lê `estado/live` e está **certo** — só usa conteúdo:
`api/og.js` (título do card), `api/live.js` (varredura de termos),
`eikoadm01.html` (moderação lê, e derruba via `live_adm_fechar`),
`moviki-app/live.html` (o estúdio).

O marcador "sem registro do estúdio" do painel usa `ativa` da coleção `lives/`,
que é outro documento e continua sendo escrito.

## Ausencias encontradas na varredura

Não são defeito, são funcionalidade que nunca existiu:

- O **mapa da home** não marca quem está transmitindo.
- O **painel do lojista** não mostra nada quando a live dele está no ar.

## Ligacoes

[[A13 - Modo Live]] · [[R - Regras de ouro]] ·
[[ARQ - Teste de fumaca da live executado 16092026]] ·
[[R - Marcas de versao no ar]]
