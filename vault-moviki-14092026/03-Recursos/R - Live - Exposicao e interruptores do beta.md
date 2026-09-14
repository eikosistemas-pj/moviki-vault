---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, beta, exposicao, seo, interruptor]
atualizado: 2026-09-14
---

# R - Live - Exposicao e interruptores do beta

Onde ficam os interruptores do Modo Live e o que reverter no dia do lançamento
aberto. O registro datado da auditoria de exposição está em
[[ARQ - Live escondida durante o beta 14092026]].

## O interruptor único

| Chave | O que faz | Onde se edita |
| --- | --- | --- |
| `configuracoes/liveTermos.liveBeta` | **lista de uid** que enxerga a live. Vazia = live aberta a todos | painel do dono > Lives, sem deploy |
| `configuracoes/liveTermos.liveDesligada: true` | chave mestra: derruba a live para todo mundo, inclusive quem está na lista | painel do dono > Lives, sem deploy |
| `configuracoes/liveTermos.extras` | termos proibidos extras do filtro | painel do dono > Lives, sem deploy |
| `configuracoes/liveTermos.demoYoutube` | id do vídeo demo na tela de venda. Sem id, a caixa não aparece | painel do dono > Lives, sem deploy |

Um lugar só decide **botão, estúdio e videoaulas**. Desde 14/09/2026 as aulas do
Modo Live obedecem ao mesmo interruptor.

Regra do Firestore: `configuracoes/liveTermos` tem leitura pública (os filtros
precisam ler), escrita só do admin, delete proibido.

## Superfícies controladas pelo interruptor

- Botão **Fazer live** no painel do lojista.
- **Estúdio** `app.moviki.com.br/live.html`, inclusive por URL direta.
- Botão **Aulas** dentro do estúdio.
- **Aulas do Modo Live** na biblioteca Tutoriais do painel.

Conferência no Chromium: painel abre com **16 aulas** e nenhuma da live; com o
interruptor ligado vai a **29**; desligado volta a 16.

## Superfícies que não dependem do interruptor

- `/live/{apelido}` — só existe com live no ar, e é `noindex`.
- Selo **AO VIVO** na página do negócio — só com live ativa.
- `aovivo.html` e `regras-da-live.html` — páginas públicas, marcadas
  `noindex,follow` durante o beta.
- Termos e Privacidade (itens 6-A e 5-A) — ficam públicos: é obrigação legal, e
  texto de contrato não é divulgação.

## No dia do lançamento aberto

1. Painel do dono > Lives > **esvaziar a lista do beta**. Botão, estúdio e aulas
   aparecem para todos os Premium e Enterprise no mesmo instante.
2. Tirar `<meta name="robots" content="noindex,follow">` do `aovivo.html` e do
   `regras-da-live.html`.
3. Acrescentar `https://moviki.com.br/aovivo` ao `sitemap.xml`.
4. Tornar o filme hero **público** no YouTube.
5. Citar a live no `premium.html`, no `enterprise.html` e no comparativo de
   planos — descrevendo a ferramenta, nunca prometendo resultado.

**Nada disso depende de código novo. O passo 1 sozinho já abre o produto.**

O que segura o lançamento não é técnico: é o teto de subcontas do Asaas
([[P29 - Teto de 10 subcontas no Asaas]]).

## Em aberto

- [ ] Definir a URL do passo 3 depois da decisão de domínio
      ([[P30 - Decisao de dominio apex ou www]]).

## Ligações

[[A13 - Modo Live]] · [[A2 - Infraestrutura e Deploy]] ·
[[ARQ - Live escondida durante o beta 14092026]] ·
[[P24 - Modo Live - lancamento]] · [[P25 - Pagina de venda da live]] ·
[[P29 - Teto de 10 subcontas no Asaas]] ·
[[P30 - Decisao de dominio apex ou www]] ·
[[R - Live - Videoaulas do modulo]] ·
[[R - Live - Arquitetura e arquivos]] · [[R - Links e identificadores]]
