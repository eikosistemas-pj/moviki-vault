---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [retomada, live, filme-hero, handoff, aovivo]
atualizado: 2026-09-14
---

# R — Retomada live parte 02

**Documento de partida para chat novo.** Anexe este arquivo primeiro. Ele fecha a
parte 01 (Modo Live no ar + filme hero) e diz exatamente de onde continuar.
Estado conferido em 13/09/2026 de madrugada, com atualização de 13/09 à tarde e
de 14/09 marcada no fim de cada seção.

Hierarquia de verdade continua valendo:
**Console do Firebase > MAPA-MESTRE.md > vault.**

## 1. Onde o produto está

### Modo Live — no ar, em beta fechado

- 15 arquivos nos três repositórios, regras do Firestore **v23** publicadas.
- Beta fechado: **só o negócio do Paulo** vê a live.
- Asaas conferido no painel do dono: **Liberado, 0 de 10 subcontas** — a conta da
  Eiko pode criar subconta por API.
- `moviki/api/live.js` — marca `2026-09-12-beta1`.
- **Linha 226:** `if (periodo === 'trial') return NIVEIS.premium;` — a live
  funciona no teste grátis de 30 dias, em nível Premium (60 min, 5 itens na
  sacolinha). **O Pix dentro da live continua Enterprise** (`ehEnterprise` em
  `moviki-robo/lib/checkout.js`).
- Vídeo demo da tela de venda: `demo-live-moviki.mp4`, 58 s, 4:5, voz da Malu. O
  id do YouTube mora em `configuracoes/liveTermos.demoYoutube`, editável no
  painel do dono > Lives.

### Página pública de negócio

É o **`moviki/404.html`**, servido para todo caminho desconhecido. Usa Leaflet.
Contém o `#mvAoVivo` (pílula vermelha fixa AO VIVO que leva a `/live/{slug}`) e
um **cartão de mapa de 540x228 px CSS**, não um mapa de tela cheia. Isso já
confundiu uma rodada inteira — está aqui para não confundir a próxima.

### Filme hero do Modo Live — v6 aprovada em 13/09

2:38, 1920x1080, 30 fps, `MOVIKI-hero-v6.mp4` (25 MB), voz Malu
`fhtZMBwha5du5OxuvexO`, grafia **"Mo-víki"** para o motor.
Detalhe editorial em [[ARQ - Filme hero v6 aprovado 13092026]], parâmetros em
[[R - Live - Folha de producao do filme hero]], armadilhas em
[[ARQ - Incidentes de montagem do filme hero]].

### Página /aovivo — V2 no ar

Marca `2026-09-13-aovivo4`, rota `/aovivo` no `vercel.json`, player em fachada
`youtube-nocookie`, CSP por arquivo via `<meta http-equiv>`, preço fora da
página. Está com **noindex** enquanto o beta estiver fechado — ver
[[ARQ - Live escondida durante o beta 14092026]] e
[[P25 - Pagina de venda da live]].

## 2. O que fazer primeiro no chat novo

1. **[[P27 - Publicacao do filme hero no YouTube]]** — subir **não listado**,
   título recomendado `Vender ao vivo pelo celular, sem loja e sem estúdio | MOVIKI`.
   Público só quando a página de venda estiver no ar.
2. **[[P26 - Cortes do filme hero - vertical e pago]]** — vertical de 45–60 s
   remontado **das fontes** (não recortado do master) e corte pago de 15–30 s.
3. **[[P25 - Pagina de venda da live]]** — continua aberta e é ela que destrava o
   "público" do YouTube.
4. **Beta com 3 a 5 lojistas** — nenhuma live real rodou ainda fora da conta do
   Paulo.

**Atualização de 13/09 à tarde:** os itens 1 e 2 foram executados. O filme subiu
como `n2nmTfGY_mo` e os três cortes ficaram prontos. O item 3 entregou V1 e V2 da
`/aovivo`. **O item 4 segue intocado e é hoje o primeiro da fila**, junto do
checklist de YouTube Studio de P27.

## 3. Fontes do filme — o que precisa estar anexado no chat novo

O ambiente é descartado quando a sessão acaba. Sem estes arquivos, refazer
qualquer corte custa crédito do Kairogen.

| Pacote | Conteúdo |
| --- | --- |
| `hero-fontes-1-voz-e-trilha.zip` | 16 MP3 da Malu (`m_c01`..`m_c13`, `m_d1`..`m_d3`) + `trilha_a.mp3` + `trilha_b.mp3` |
| `hero-fontes-2-ui-e-mapa.zip` | `publico.webm` (58,08 s), `estudio.webm` (22,88 s), `textura-tratada.png` |
| `hero-fontes-3-clipes-a.zip` | `k_c01`, `k_c02b`, `k_c03` |
| `hero-fontes-4-clipes-b.zip` | `k_c05a`, `k_c05b` |
| `hero-fontes-5-clipes-c.zip` | `k_c11`, `k_d1` |
| `MOVIKI-hero-v6.mp4` | o master aprovado |

Para mexer nos cortes, anexar também `logo.png` da raiz de `moviki` ou
`moviki-app` — o proxy nega `moviki.com.br` e `i.ytimg.com` com 403 no CONNECT.

## 4. Pendências herdadas, ainda abertas

### Mídia paga (desde 11/09)

- [ ] Repor saldo do Google Ads
- [ ] Confirmação de identidade do Google — **obrigatória a partir de 23/09**
- [ ] Remover o recurso de Local (endereço de Curitiba) — manual
- [ ] Deixar só **Inscrição** como conversão principal no Google Ads
- [ ] Reler o funil: `cta_click / page_view` estava em **2,3%** e o favicon de
      949 KB foi corrigido — se não subir, o problema é a copy

### Produto e medição

- [ ] Registrar o parâmetro `etapa` como dimensão personalizada no GA4
- [ ] Apagar a conta de teste "Eiko Jato", que contamina o `sign_up`
- [ ] **Decidir o domínio: apex x www.** Os 16 links do site, os QR dos crachás e
      os links dos parceiros apontam para o apex e pegam um salto de
      redirecionamento a cada visita — foi isso que quebrou o CORS do estúdio.
      Ver [[P30 - Decisao de dominio apex ou www]]
- [ ] Teto de 10 subcontas no Asaas — ver [[P29 - Teto de 10 subcontas no Asaas]]

### Documentação

- [ ] **MAPA-MESTRE continua parado em 04/09.** Precisa de recompilação inteira:
      de 05 a 13/09 entraram App Check enforçado, Modo Live, regras v22 e v23, as
      campanhas novas, o vídeo demo e o filme hero.
- [x] **A fila de notas do vault de 04–06/09 subiu** no pacote
      `vault-moviki-10092026.zip`. **Correção:** a versão anterior deste
      documento dizia que a fila seguia sem subir — está errado. O que ficou
      pendente é outra coisa: **apagar 3 notas órfãs da renumeração** — ver
      [[ARQ - Faxina de notas orfas do vault]].

## 5. Como o trabalho é feito (não repetir os erros)

- **O Paulo não é de programação e trabalha só pela interface web do GitHub.**
  Arquivo completo, com repositório, pasta e NOVO/SUBSTITUI. Nunca trecho para
  colar. Nunca código na resposta.
- **`.js` vai dentro de `.zip`** — o navegador dele bloqueia o download solto.
- **Nome de arquivo entregue no chat não pode depender de hífen** — o navegador
  dele remove hífen no download. Dentro de `.zip` não tem esse problema.
- **Nunca criar arquivo novo em `moviki-robo/api`** — o plano Hobby aceita 12
  funções e o repo está no teto.
- **Antes de entregar regra do Firestore, perguntar qual versão está publicada.**
- **`CHECKOUT_CHAVE` nunca muda depois de criadas as subcontas.**
- **Segredo nunca entra em chat, código ou GitHub.** Env com chave de
  administrador só em Production.
- **Não fazer commit nem push nos repositórios dele.** Os clones locais são
  espelho de trabalho.
- **URL bloqueada pelo WebFetch não se busca por curl, wget ou script.**
- O MAPA MESTRE é responsabilidade do assistente — ele nunca copia e cola seção.

## 6. Numeração de projetos

**P26 e P27 foram os números tomados na rodada de 13/09 de madrugada; P25 já
existia.** Conferir a fila de notas represadas antes de criar um `P` novo — o
índice de projetos do vault não reflete o que ainda não subiu.

## Ligações

- [[A13 - Modo Live]]
- [[A1 - Produto e Paineis]]
- [[A2 - Infraestrutura e Deploy]]
- [[A6 - Medicao e Analytics]]
- [[A7 - Aquisicao e Midia Paga]]
- [[P24 - Modo Live - lancamento]]
- [[P25 - Pagina de venda da live]]
- [[P26 - Cortes do filme hero - vertical e pago]]
- [[P27 - Publicacao do filme hero no YouTube]]
- [[P28 - Videoaulas do Modo Live]]
- [[P29 - Teto de 10 subcontas no Asaas]]
- [[P30 - Decisao de dominio apex ou www]]
- [[R - Live - Folha de producao do filme hero]]
- [[R - Live - Exposicao e interruptores do beta]]
- [[R - Live - Relatorio de seguranca]]
- [[R - Regras de ouro de producao de video]]
- [[R - Regras de ouro de producao de cortes]]
- [[R - Protocolo Claude e vault]]
- [[ARQ - Modo Live no ar em beta fechado 12092026]]
- [[ARQ - Live escondida durante o beta 14092026]]
- [[ARQ - Filme hero v6 aprovado 13092026]]
- [[ARQ - Incidentes de montagem do filme hero]]
- [[ARQ - Faxina de notas orfas do vault]]
