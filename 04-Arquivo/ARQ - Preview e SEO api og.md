---
type: arquivo
status: concluido
data: 2026-08-27
area: A7 — Aquisicao e Midia Paga
tags: [seo, aquisicao]
atualizado: 2026-08-28
---

# ARQ — Preview do link e SEO da página pública — NO AR 27/08/2026

## Os dois problemas
1. **O ativo mais compartilhado do produto abria sem preview.** A página é montada 100% no navegador, e o robô do WhatsApp, Facebook, Instagram e Google **não roda JavaScript**: liam `<title>Moviki</title>` e mais nada. **No modelo single-vendor, esse compartilhamento É o canal de distribuição.**
2. **E ninguém tinha visto:** como o `404.html` era servido como *página de erro*, **cada página de negócio respondia HTTP 404**. Nenhum buscador indexa um 404. **O produto era invisível para o Google desde o primeiro dia.**

## A solução: `api/og.js` no repo `moviki`
Lê o negócio pela **API REST pública do Firestore** (a mesma leitura que o navegador já faz, com a mesma chave pública — sem service account, sem dependência, sem `package.json`), injeta `<title>`, description, Open Graph, Twitter Card, canonical e **JSON-LD `LocalBusiness`** dentro do próprio `404.html`, e devolve **HTTP 200**.

- **O HTML entregue é o mesmo para robô e para gente** — servir diferente é *cloaking* e o Google pune.
- **Respeita a trava de plano:** foto no preview só de Premium/Enterprise (ou trial); logo do pino idem. **Preview nunca mostra o que a página esconde.** Sem direito, cai em `ogmoviki.jpg` (1200×630).
- **Funciona para unidade Enterprise** (`ponto_slugs`): *"Unidade Centro · Nome do Negócio — Moviki"*.
- **Estrelas no Google:** `aggregateRating` sai de `resumo/avaliacoes` — o mesmo `{n, soma}` do conserto de custo.
- **Custo:** 4 leituras por **miss** de cache; `s-maxage=300` + `stale-while-revalidate=86400`.
- **Não encostou no `moviki-robo`** — o teto de 12 é por projeto, e o do site usava **zero**.

Entraram junto `robots.txt` (com `Disallow` em `/p/`, `/pp/`, descadastro e exclusão de conta) e `sitemap.xml` das institucionais. Sitemap dinâmico dos negócios fica para depois.

## Os dois consertos ao vivo (`og2`, `og3`)
- **A canonical vinha com `www`.** O site responde no apex **e** no `www`, e a função montava a canonical a partir do host da requisição — **dois hosts com canonical diferente é exatamente o conteúdo duplicado que a canonical existe para evitar.** Agora é sempre o domínio do CNAME.
- **O portão de qualidade reprovou o cliente ideal.** A primeira versão exigia segmento **ou** endereço, e reprovou o CALDEIRÃO NORDESTINO — 12 fotos, cardápio, promoções e eventos, **sem endereço**. **Exigir endereço é o oposto do produto: ele existe justamente para quem NÃO tem endereço fixo.** Corrigido em `og3`: o `index` exige nome + ponto no mapa + **algum** conteúdo real (segmento, endereço, foto, cardápio ou promoção).

## A distinção que virou regra
**Preview e indexação são decisões separadas.** O preview **sempre** funciona (é o que o lojista compartilha). O `index` é seletivo — **página magra em quantidade derruba a reputação do domínio inteiro, e o domínio é um só para todos os lojistas.** Cadastros de teste (`email`, `paulo`, `mapamoviki`, `ricopj`…) saem como `noindex,follow`.

→ [[A7 - Aquisicao e Midia Paga]]
