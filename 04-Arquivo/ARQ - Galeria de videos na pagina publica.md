---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [pagina-publica, painel-lojista, regra-firestore, premium, entrega]
atualizado: 2026-09-10
---

# ARQ - Galeria de videos na pagina publica

**No ar em 10/09/2026.** Regras **v22** publicadas, `moviki-app/index.html` e
`moviki/404.html` na marca `2026-09-10-videos` — conferido no repositorio.

Pedido do Paulo: *"preciso que a pagina final do cliente seja muito mais
atrativa"*, com galeria de videos alem da de fotos.

## A decisao que mudou o desenho: nao hospedar video

| | Peso |
| --- | --- |
| Uma foto | ~200 KB |
| 30 s de video | 15 a 20 MB |

Hospedar significaria pagar banda do Storage **a cada visita** e derrubar a
pagina no 4G — o contrario do objetivo. O lojista **cola o link** de um video que
ele ja postou. Custo de infraestrutura zero, trabalho menor que subir arquivo, e
ainda leva trafego para o Instagram dele.

Fontes aceitas: **YouTube/Shorts, Instagram Reels e TikTok**. Posicao: acima da
galeria de fotos.

**Decisao de marca:** nenhuma logo de rede social na tela. O nome vai escrito no
selo e o desenho e um play generico do Moviki. Marca de terceiro na pagina do
cliente e risco juridico a troco de nada.

## Como funciona

- Campo `videos` em `negocios/{uid}`: lista de `{ url, titulo }`, no maximo 6
- Direito de uso: **Premium / Enterprise e no teste gratis** — o mesmo gate das
  fotos, reaproveitado de proposito (dois gates para a mesma "galeria" viram
  duas explicacoes diferentes no painel)
- Secao `secVideos` no `404.html`, entre "Destaques do cardapio" e "Onde
  estamos": faixa horizontal de cartoes em pe que desliza com o dedo
- **YouTube toca dentro da pagina**, em visor proprio com `youtube-nocookie`.
  Moldura em pe para Shorts, deitada para video normal — uma so nao serve: Short
  em caixa 16:9 vira tira preta
- **Instagram e TikTok abrem no aplicativo**: essas redes nao permitem tocar
  embutido sem login e nao entregam a capa por link
- O cartao e **capa, nao player** — nada carrega antes do clique; seis iframes
  abertos juntos passariam de 3 MB
- Miniatura real so no YouTube (`i.ytimg.com/vi/<id>/hqdefault.jpg`), com a arte
  em degrade sempre atras, para video apagado degradar bonito
- No painel: bloco "Videos do negocio" acima das fotos, contador `n / 6`, aviso
  em vermelho no link nao reconhecido **sem limpar o campo**, e o rotulo "Fotos"
  virou "Fotos e videos"

## O ponto de seguranca

`url` e texto que o lojista digita e que a pagina publica joga dentro de um
`href`. Sem lista fechada de dominios, um `javascript:...` colado no campo
**executaria na pagina do cliente dele**.

Expressao ancorada em `^https://` + dominio, conferida **nos dois lados**: no
painel ao colar e de novo no `404.html` ao publicar. Link que nao casa nao
aparece. A query string cai fora (`?igsh=`, `?is_from_webapp=`). Titulo passa por
`esc()` nos dois lados. Recusados e testados: `javascript:`, `data:`, `http://`
sem s, dominio de fora, `youtube.com.malvado.com`.

**A regra do Firestore nao valida item de lista** — regra nao entra em mapa
dentro de lista. La so se trava `is list && size() <= 6`. Por isso o filtro de
dominio e responsabilidade do HTML, e por isso ele e duplicado.

## A licao que ficou

> O `.txt` de regras que estava no Project era a **v19 — defasado**. No ar ja
> havia v20 e v21. A primeira versao da entrega foi montada sobre a v19 e
> **teria apagado as duas**.
>
> **Regra nova: antes de entregar qualquer regra do Firestore, pedir a atual ao
> Paulo. O arquivo do Project nao e prova do que esta publicado.**

## Validacao

159 verificacoes na pagina publica e 84 no painel, zero falhas: filtro de link
com 17 casos, gate por plano nos 5 estados, XSS no titulo, visor abrindo,
fechando e **matando o iframe**, campo ausente ou com lixo, modo demonstracao,
layout em 8 larguras de 360 a 1920.

## Ficou de fora

- [ ] Capa escolhida pelo lojista para Instagram/TikTok
- [ ] Video em destaque no topo tocando sem som em laco
- [ ] Contar cliques em video na metrica por negocio — o evento GA4 `video_abriu`
      ja dispara, mas o contador do painel nao tem essa faixa

## Ligacoes

[[A1 - Produto e Paineis]] · [[A3 - Dados e Regras]] ·
[[R - Historico de regras do Firestore]] · [[R - Marcas de versao no ar]]
