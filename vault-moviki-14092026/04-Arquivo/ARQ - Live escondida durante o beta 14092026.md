---
type: decisao
status: concluido
area: A13 - Modo Live
tags: [live, beta, exposicao, seo, robots]
atualizado: 2026-09-14
---

# ARQ - Live escondida durante o beta 14092026

Auditoria de exposição do Modo Live, feita **clonando os cinco repositórios**,
não de memória. Motivo: enquanto o teto de dez subcontas no Asaas não estiver
resolvido ([[P29 - Teto de 10 subcontas no Asaas]]), **nenhum lojista fora da
lista, nenhum parceiro e nenhum cliente pode topar com a live**.

## O interruptor único

`configuracoes/liveTermos.liveBeta` — **lista de uid**. Vazia significa live
aberta a todos. Editável no **painel do dono > Lives**, sem deploy.

`configuracoes/liveTermos.liveDesligada: true` — **chave mestra**: derruba a live
para todo mundo, inclusive quem está na lista.

A partir desta rodada **as videoaulas do Modo Live obedecem ao mesmo
interruptor**. Um lugar só decide botão, estúdio e aulas.

## Mapa de exposição

| Superfície | Quem vê | Estado em 14/09/2026 |
| --- | --- | --- |
| Botão **Fazer live** no painel | só uid na `liveBeta` | já estava certo |
| **Estúdio** `app.moviki.com.br/live.html` por URL direta | qualquer lojista logado abria e via mensagem de erro técnica (`beta`) | **corrigido**: tela própria, "A live ainda está em preparação" |
| **Aulas do Modo Live** na biblioteca Tutoriais | apareceriam para **todo lojista** assim que os vídeos entrassem | **corrigido**: entram só para quem está na `liveBeta` |
| Botão **Aulas** dentro do estúdio | apareceria mesmo para quem não passou da porta | **corrigido**: só com o estúdio liberado |
| Página `/live/{apelido}` | só com live no ar; `noindex` | já estava certo |
| Selo **AO VIVO** na página do negócio | só com live ativa | já estava certo |
| **`moviki.com.br/aovivo.html`** — página de venda da live | **pública e indexável pelo Google** | **corrigido**: `noindex,follow` |
| **`regras-da-live.html`** | indexável | **corrigido**: `noindex,follow` |
| Termos e Privacidade (itens 6-A e 5-A) | público | **fica** — é obrigação legal, e texto de contrato não é divulgação |
| **Vik** no painel | já sabia do beta: não afirma, não manda procurar o botão | já estava certo |
| Painel do **parceiro** e material de apoio | nenhuma menção à live | conferido, zero ocorrências |
| **Robô social** | nunca publicou sobre live | conferido, zero ocorrências |
| Filme hero no YouTube | ainda não publicado | subir **não listado** |

## O defeito achado de quebra: a rota /aovivo não existia

O `canonical` da página aponta para `https://www.moviki.com.br/aovivo`, mas o
`vercel.json` **não tinha essa rota**. O endereço caía no curinga de apelido, ia
para o `api/og` e respondia **"Negócio não encontrado"**.

O link bonito — que é o destino do filme hero e dos convites do beta — estava
quebrado desde que a página subiu. Corrigido no `vercel.json`, **antes** do
curinga de slug.

## Por que NÃO entrou Disallow no robots.txt

Página bloqueada no `robots.txt` **não é rastreada** — e, não sendo rastreada, o
Google **nunca lê a linha `noindex`**. O resultado seria o oposto do pedido: a
URL pode ser indexada seca, só com o endereço, a partir de qualquer link
externo.

Para tirar da busca, o certo é **deixar rastrear e marcar `noindex`**. O
`robots.txt` fica como está.

## No dia do lançamento

1. Painel do dono > Lives > **esvaziar a lista do beta**. Botão, estúdio e aulas
   aparecem para todos os Premium e Enterprise no mesmo instante.
2. Tirar `<meta name="robots" content="noindex,follow">` do `aovivo.html` e do
   `regras-da-live.html`.
3. Acrescentar `https://moviki.com.br/aovivo` ao `sitemap.xml`.
4. Tornar o filme hero **público** no YouTube.
5. Citar a live no `premium.html`, no `enterprise.html` e no comparativo de
   planos — descrevendo a ferramenta, nunca prometendo resultado.

Nada disso depende de código novo. O passo 1 sozinho já abre o produto.

## Arquivos desta rodada

| Repo | Arquivo | Ação | Marca |
| --- | --- | --- | --- |
| moviki-app | `liveaulas.js` | NOVO | 2026-09-13-liveaulas1 |
| moviki-app | `live.html` | SUBSTITUI | 2026-09-14-aulas-beta |
| moviki-app | `index.html` | SUBSTITUI | 2026-09-14-liveoculta |
| moviki | `aovivo.html` | SUBSTITUI | 2026-09-14-aovivo-beta |
| moviki | `regras-da-live.html` | SUBSTITUI | 2026-09-14-regras-beta |
| moviki | `vercel.json` | SUBSTITUI | sem marca |

Conferido no Chromium: o painel abre com **16 aulas** e nenhuma da live; com o
interruptor ligado vai a **29**; desligado volta a 16. No estúdio, o botão Aulas
só existe depois que a porta do servidor liberou a conta.

## Em aberto

- [ ] Reverter os cinco passos no dia do lançamento, em uma entrega só.
- [ ] Definir a URL do `sitemap.xml` depois da decisão de domínio
      ([[P30 - Decisao de dominio apex ou www]]).

## Ligações

[[A13 - Modo Live]] · [[A2 - Infraestrutura e Deploy]] ·
[[A6 - Medicao e Analytics]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[R - Live - Videoaulas do modulo]] ·
[[R - Live - Arquitetura e arquivos]] ·
[[P24 - Modo Live - lancamento]] · [[P25 - Pagina de venda da live]] ·
[[P28 - Videoaulas do Modo Live]] · [[P29 - Teto de 10 subcontas no Asaas]] ·
[[P30 - Decisao de dominio apex ou www]] ·
[[ARQ - Modo Live no ar em beta fechado 12092026]] ·
[[R - Retomada live parte 02]]
