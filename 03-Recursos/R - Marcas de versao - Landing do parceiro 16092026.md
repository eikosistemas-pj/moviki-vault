---
type: recurso
status: referencia
area: "[[A5 - Programa de Parceiros]]"
tags: [marcas-de-versao, upload, parceiro, landing, live-commerce, comissao]
atualizado: 2026-09-16
---

# R - Marcas de versao - Landing do parceiro 16092026

Pacote `MOVIKI-SUBIR-landing-parceiro-16092026-v2.zip`. **Dois repositorios, tres
arquivos.**

> **Este pacote SUBSTITUI o primeiro** (`MOVIKI-SUBIR-landing-parceiro-16092026.zip`,
> com dois arquivos). Se o primeiro ja tiver subido, suba este por cima: a
> `parceiros.html` muda de `2026-09-16-parceirolive` para
> `2026-09-16-parceirolive2` e ganha o repasse do `?ref=`. Se o primeiro nao
> subiu, **descarte-o** e use so este.

| Repo | Pasta | Arquivo | Acao | Marca | Montado sobre |
|---|---|---|---|---|---|
| `moviki` | raiz | `parceiros-ganhos.html` | SUBSTITUI | `2026-09-16-parceirolive` | `2026-08-27-conformidade` |
| `moviki` | raiz | `parceiros.html` | SUBSTITUI | `2026-09-16-parceirolive2` | `2026-08-28-vikparceiros` |
| `moviki-app` | raiz | `seja-parceiro.html` | SUBSTITUI | `2026-09-16-parceirolive` | `2026-09-04-conta-existente` |

## Ordem

Nao ha dependencia entre os tres. Qualquer ordem, qualquer dia. Nenhum arquivo
novo, nenhuma pasta nova, nenhuma regra do Firestore, nenhuma funcao da Vercel,
nenhuma env.

## O ACHADO DESTA RODADA - buraco de dinheiro, nao de medicao

As duas landings mandavam para um endereco **FIXO** do cadastro:
`https://app.moviki.com.br/seja-parceiro.html`, sem parametro nenhum.

Consequencia: a pagina aberta com `?ref=<apelido>` — que e exatamente o link que
um parceiro manda para convidar outro — **perdia o apelido no clique**. O
`seja-parceiro.html` sempre soube ler o `ref` da URL; nunca teve quem lhe
entregasse o valor vindo da landing. O `indicadoPor` nao era gravado e o **upline
dos niveis 2 e 3 nunca nascia**. Quem indicou perdia o bonus sem nunca saber por
que.

As tres paginas agora repassam `ref` e `utm_source/medium/campaign/content/term`
para o cadastro, higienizados. Sem `ref` e sem UTM na URL, o endereco continua
identico ao de hoje.

> **Regra de ouro:** carimbar UTM so vale se o destino medir — e **link de
> indicacao so vale se o clique CARREGAR o apelido adiante**. Pagina que le o
> `ref` e o joga fora no botao e pior que pagina sem `ref`: parece instrumentada.

## O que mudou no conteudo

1. **O passo 1 do "Como comecar" da `parceiros.html` era falso.** Dizia "Fale com
   a gente, chame no WhatsApp" e **nao existia botao de WhatsApp na pagina** —
   os dois CTAs sempre levaram ao formulario, com a classe `.cta wpp` pintando o
   botao de verde de WhatsApp. Agora sao quatro passos reais.
2. **A `parceiros-ganhos.html` comecava no passo 4 da vida real.** O primeiro
   passo era "Pegue seu link"; antes dele existem cadastro, analise e aulas, e
   nenhuma das duas paginas avisava. Entrou a secao **"Como voce entra no
   programa"**, com os tres passos e o motivo legal das aulas.
3. **Live commerce entrou nas tres paginas.** Ate 16/09 so `index.html` e
   `comerciantes.html` tinham sido reposicionadas.
4. Secao nova **"O que ja vem pronto no seu painel"**: artes e legendas por ramo,
   cracha com QR, extrato por comerciante, saque por Pix.
5. Secao nova da **verificacao `/v/apelido`** como argumento anti-golpe.
6. `seja-parceiro.html` ganhou contexto do produto e link para
   `parceiros-ganhos.html`: quem chega pelo `/pp/<apelido>` caia num formulario
   pedindo chave Pix sem uma linha dizendo o que e o Moviki.
7. Tela de sucesso encaminha para as aulas, em vez de so dizer "em analise".
8. O card "Produto que se paga" descrevia **resultado para o lojista**; virou
   descricao da ferramenta. No card "Pra quem voce indica" entrou a venda ao
   vivo.

## O video de venda ja esta montado, e nasce invisivel

As duas landings carregam:

```
window.MOVIKI_VIDEO_PARCEIRO = '';
```

Vazia, o bloco do video fica escondido — nenhuma tela quebrada, nenhum player
preto. **Trocar esse valor pelo trecho depois de `youtu.be/` e a UNICA coisa
necessaria para publicar o video.** Mesmo padrao das videoaulas. A capa e uma
imagem; o `iframe` do `youtube-nocookie` so e criado **depois do clique**.

Sao dois arquivos: trocar nos dois, na mesma rodada.

## Qual das duas paginas recebe trafego

A `parceiros.html` carrega `canonical` para a `parceiros-ganhos.html` e saiu do
sitemap em 16/09.

> **O destino de trafego pago e de link mandado a influenciador e a
> `parceiros-ganhos.html`.** A `parceiros.html` fica de pe para quem chega por
> link antigo.

## Conferir depois de subir

1. `parceiros-ganhos.html` — secao "Como voce entra no programa" com tres passos,
   e "O que ja vem pronto no seu painel" antes do CTA final.
2. Abrir `www.moviki.com.br/parceiros-ganhos.html?ref=paulopj` e **passar o mouse
   no botao "Quero ser parceiro Moviki"**: o endereco tem que terminar em
   `seja-parceiro.html?ref=paulopj`. Sem o `ref` na URL, o endereco fica limpo.
3. Mesmo teste na `parceiros.html`.
4. Fazer um cadastro de teste por esse caminho e conferir no Firestore que
   `parceiros/{uid}.indicadoPor` gravou o apelido. **E o unico jeito de provar
   que o bonus de nivel 2 voltou a existir.**
5. `parceiros.html` — "Como comecar" com quatro passos, o terceiro falando das
   aulas.
6. `seja-parceiro.html` — caixa "O que voce vai indicar" no topo e a lista
   "Depois de enviar" acima do botao.
7. Nenhum bloco de video visivel enquanto `MOVIKI_VIDEO_PARCEIRO` estiver vazia.
8. `Ctrl+Shift+R` nas tres antes de julgar qualquer coisa.

## Conferido antes da entrega

- `node --check` limpo nos 9 blocos de script inline dos tres arquivos
- Chromium a 390px nas tres paginas: **zero erro de JavaScript**
- Repasse do `ref`: com `?ref=paulopj&utm_source=instagram&utm_medium=bio` o CTA
  vira `seja-parceiro.html?ref=paulopj&utm_source=instagram&utm_medium=bio`; sem
  parametro, fica identico ao de hoje; `ref` com caractere estranho e higienizado
  antes de entrar no endereco
- Video: escondido com a constante vazia; visivel com id; `iframe` montado no
  clique, uma vez so
- Medicao preservada: todos os `data-ev` antigos mantidos nas tres
- App Check, captura do `ref`, fluxo de conta existente de 04/09 e reserva do
  apelido: intactos no `seja-parceiro.html`
- UTF-8 sem BOM, LF, zero byte de controle nos tres
- Conformidade: nenhum "para sempre", "renda", "sem risco", "lucro" ou numero que
  projete ganho. A unica ocorrencia de "garantido" e a frase original **"nao
  existe valor minimo garantido"**, que e negativa e deve continuar la

## Ligacoes

[[A5 - Programa de Parceiros]] · [[P37 - Prospeccao de parceiros e influenciadores]] ·
[[R - Checklist conformidade Meta e Google]] ·
[[R - Marcas de versao - SEO lote 2 16092026]]
