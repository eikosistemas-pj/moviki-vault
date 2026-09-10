---
type: recurso
status: referencia
area: A11 - Marca e Design System
tags: [copy, marca, linguagem, vik, produto]
atualizado: 2026-09-10
---

# R - Terminologia visivel ao cliente

Regra permanente de vocabulario do Moviki, e o registro da varredura que tirou a
palavra "trial" do sistema em 10/09/2026.

## A decisao

**Ninguem entende "trial".** O publico e dono de food truck, feirante, carrinho de
lanche. Palavra em ingles no meio da tela e atrito de conversao: a pessoa nao
sabe se vai pagar, se ja pagou, ou se aquilo e o plano dela.

| Nunca escrever | Escrever sempre |
| --- | --- |
| trial, plano trial, periodo trial | **teste gratis** / **periodo de teste** |
| free, plano free | **plano Basico** / **conta gratuita** |
| upgrade / downgrade | subir de plano / descer de plano *(pendente)* |

Vale para site, painel do lojista, painel do parceiro, e-mails automaticos,
regulamento, videoaulas, anuncios e as respostas do Vik.

## O que foi corrigido em 10/09

Seis arquivos, tres repositorios, todos SUBSTITUEM:

| Repo | Caminho | O que mudou |
| --- | --- | --- |
| moviki | `regulamento.html` | clausula 4.5: "teste gratuito (trial)" vira "teste gratis" |
| moviki-app | `regulamento.html` | mesma clausula |
| moviki-ai | `lib/promptPainel.js` | tirou "trial" do catalogo e das regras do Vik |
| moviki-ai | `lib/promptAtendimento.js` | idem, inclusive no FAQ |
| moviki-ai | `lib/contextoUsuario.js` | o bloco de dados da conta nao entrega mais "trial" cru |
| moviki-ai | `lib/segurancaVik.test.js` | frases de teste alinhadas |

## O achado que importava

`contextoUsuario.js` montava a linha **`Periodicidade: trial`** e injetava no
contexto que o Vik le antes de cada resposta. Era dai que o robo repetia a palavra
ao lojista, com a tela inteira dizendo "teste gratis". Agora a linha e traduzida
antes de ser injetada.

> **Licao geral: texto que so a IA le tambem e texto que o cliente le.** Todo dado
> cru injetado em prompt precisa passar pelo mesmo filtro de vocabulario que a
> interface.

## O que NAO foi tocado, de proposito

Sao nomes internos, invisiveis na tela — mexer destrava plano de todo mundo:

- **Valor no Firestore:** `periodo: 'trial'` em `assinaturas/{uid}`. Todas as
  travas de plano comparam com essa string, em `moviki-app/index.html`,
  `moviki/404.html`, `moviki/api/og.js` e `moviki-robo/api/webhook.js`
- **Nomes de arquivo e rota:** `api/ativar-trial.js`, `api/lembrete-trial.js` e a
  linha do cron no `vercel.json`
- **Classes e funcoes:** `.bannerTrial`, `.selo-trial`, `garantirTrial()`,
  `mostrarBannerTrial()`

Renomear isso um dia exige migracao de dados, nunca find-and-replace.

## O que ja estava certo antes

Selo do painel, banner de fim de teste, e-mails de lembrete, painel do parceiro e
landing ja falavam "teste gratis". O problema era pontual.

## Pendencia

"upgrade" e "downgrade" ainda aparecem ao lojista na secao Meu Plano e nos prompts
do Vik. Trocar por "subir de plano" e "descer de plano".

## Ligacoes

[[A11 - Marca e Design System]] · [[A9 - IA e Atendimento Vik]] ·
[[R - Regras de ouro]] · [[P05 - Calibrar o Vik]]
