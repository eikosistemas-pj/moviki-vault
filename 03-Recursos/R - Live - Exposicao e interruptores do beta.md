---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, beta, exposicao, seo, interruptor, teto]
atualizado: 2026-09-16
---

# R - Live - Exposicao e interruptores do beta

Onde ficam os interruptores do Modo Live e o que reverter no dia do lancamento
aberto. O registro datado da auditoria de exposicao esta em
[[ARQ - Live escondida durante o beta 14092026]].

## O documento unico

Tudo vive em `configuracoes/liveTermos`, editado no painel do dono, **sem
deploy**.

| Chave | O que faz | Hoje |
| --- | --- | --- |
| `liveBeta` | **lista de uid** que enxerga a live. Vazia = live aberta a todos | com o negocio do Paulo |
| `liveDesligada` | chave mestra: derruba a live para todo mundo, inclusive quem esta na lista | falso |
| `extras` | termos proibidos extras do filtro | — |
| `demoYoutube` | id do video demo na tela de venda. Sem id, a caixa nao aparece | — |
| `tetoMinutosMes` | **teto de minutos entregues no ciclo do Cloudflare** (16/09) | **50000** |
| `cicloDia` | **dia da virada do ciclo de faturamento do Cloudflare** (16/09) | **12** |

⚠️ **Escrita neste documento e sempre `merge`.** `setDoc` sem merge apaga os
outros campos — e desde 16/09 isso **desliga o teto de video** junto.

Regra do Firestore: leitura publica (os filtros precisam ler), escrita so do
admin, delete proibido.

## Superficies controladas pelo interruptor

- Botao **Fazer live** no painel do lojista.
- **Estudio** `app.moviki.com.br/live.html`, inclusive por URL direta.
- Botao **Aulas** dentro do estudio.
- **Aulas do Modo Live** na biblioteca Tutoriais do painel.

## Superficies que nao dependem do interruptor

- `/live/{apelido}` — so existe com live no ar, e e `noindex`.
- Selo **AO VIVO** na pagina do negocio — so com live ativa.
- `regras-da-live.html` — publica, `noindex,follow` durante o beta.
- **`aovivo.html` JA NAO tem `noindex`** — foi removido em 16/09, junto com o
  conserto do JSON-LD. Ver
  [[ARQ - Violacao de FAQPage na pagina aovivo 16092026]].
- Termos e Privacidade (itens 6-A e 5-A) — publicos: e obrigacao legal.

## No dia do lancamento aberto

1. Painel do dono > Lives > **esvaziar a lista do beta**. Botao, estudio e
   aulas aparecem para todos os Premium e Enterprise no mesmo instante.
2. Tirar `noindex,follow` do `regras-da-live.html`. **(O `aovivo.html` ja
   esta feito.)**
3. Acrescentar `https://www.moviki.com.br/aovivo` ao `sitemap.xml`.
4. Tornar o filme hero **publico** no YouTube.
5. Citar a live no `premium.html`, no `enterprise.html` e no comparativo de
   planos — descrevendo a ferramenta, nunca prometendo resultado.
   **Conferido em 16/09: zero mencao a live nas duas.**

**Nada disso depende de codigo novo. O passo 1 sozinho ja abre o produto.**

## Em aberto

- [ ] Definir a URL do passo 3 depois da decisao de dominio
      ([[P30 - Decisao de dominio apex ou www]]).
- [ ] Passo 5: `premium.html` e `enterprise.html` sem uma linha sobre a live.

## Ligacoes

[[A13 - Modo Live]] · [[A2 - Infraestrutura e Deploy]] ·
[[ARQ - Live escondida durante o beta 14092026]] ·
[[P24 - Modo Live - lancamento]] · [[P25 - Pagina de venda da live]] ·
[[P29 - Teto de 10 subcontas no Asaas]] ·
[[P30 - Decisao de dominio apex ou www]] ·
[[R - Teto de gasto de video no Cloudflare]] ·
[[R - Live - Videoaulas do modulo]] ·
[[R - Live - Arquitetura e arquivos]] · [[R - Links e identificadores]]
