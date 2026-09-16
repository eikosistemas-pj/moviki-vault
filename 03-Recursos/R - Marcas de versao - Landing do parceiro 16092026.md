---
type: recurso
status: referencia
area: "[[A5 - Programa de Parceiros]]"
tags: [marcas-de-versao, upload, parceiro, landing, live-commerce]
atualizado: 2026-09-16
---

# R - Marcas de versao - Landing do parceiro 16092026

Pacote `MOVIKI-SUBIR-landing-parceiro-16092026.zip`. **Dois repositorios.**
Reescrita das duas paginas de entrada do Programa de Parceiros no eixo de live
commerce, com o fluxo real de cadastro declarado antes do formulario.

| Repo | Pasta | Arquivo | Acao | Marca | Montado sobre |
|---|---|---|---|---|---|
| `moviki` | raiz | `parceiros.html` | SUBSTITUI | `2026-09-16-parceirolive` | `2026-08-28-vikparceiros` |
| `moviki-app` | raiz | `seja-parceiro.html` | SUBSTITUI | `2026-09-16-parceirolive` | `2026-09-04-conta-existente` |

## Ordem

Nao ha dependencia entre os dois. Podem subir em qualquer ordem, em qualquer dia.
Nenhum arquivo novo, nenhuma pasta nova, nenhuma regra do Firestore, nenhuma
funcao da Vercel, nenhuma env.

## O que mudou

1. **O passo 1 do "Como comecar" era falso.** Dizia "Fale com a gente, chame no
   WhatsApp" e **nao existia botao de WhatsApp na pagina** — os dois CTAs sempre
   levaram ao formulario, com a classe `.cta wpp` pintando o botao de verde de
   WhatsApp. Quem lia os passos esperava conversa e caia num cadastro. Os quatro
   passos agora sao o fluxo real: cadastro, analise, aulas, divulgacao.
2. **A aprovacao manual e as aulas obrigatorias passaram a ser ditas ANTES do
   cadastro**, nas duas paginas, com o motivo — conteudo comissionado e
   publicidade e o anunciante responde junto. Deixa de ser surpresa pos-cadastro
   e vira filtro de qualidade.
3. **Live commerce entrou no eixo das duas paginas.** Ate 16/09 so `index.html` e
   `comerciantes.html` tinham sido reposicionadas; as paginas do parceiro
   seguiam vendendo so mapa.
4. Bloco novo **"O que voce recebe ao entrar"**: link pessoal, artes e legendas
   prontas, cracha com QR, extrato e saque por Pix.
5. Bloco novo da **verificacao `/v/apelido`** como argumento anti-golpe.
6. `seja-parceiro.html` ganhou contexto do produto e link para
   `parceiros-ganhos.html`: quem chega pelo `/pp/<apelido>` caia num formulario
   pedindo chave Pix sem uma linha dizendo o que e o Moviki.
7. Tela de sucesso encaminha para as aulas, em vez de so dizer "em analise".
8. O card "Produto que se paga" descrevia **resultado para o lojista**
   ("ajuda o comerciante a vender mais"); virou descricao da ferramenta.

## O video de venda ja esta montado, e nasce invisivel

`parceiros.html` carrega a constante:

```
window.MOVIKI_VIDEO_PARCEIRO = '';
```

Vazia, o bloco inteiro do video fica escondido — nenhuma tela quebrada, nenhum
player preto. **Trocar esse valor pelo trecho depois de `youtu.be/` e a UNICA
coisa necessaria para publicar o video.** Mesmo padrao das videoaulas.

A capa e uma imagem do proprio YouTube; o `iframe` do `youtube-nocookie` so e
criado **depois do clique**. A pagina nao chama o YouTube a toa e abre sem
depender dele.

## ATENCAO - a `parceiros.html` e a pagina SECUNDARIA

Ela carrega, desde 16/09, `canonical` para `parceiros-ganhos.html` e saiu do
sitemap. A canonica e a `parceiros-ganhos.html`, que e mais completa e e a que a
home e o regulamento linkam.

> **O destino de trafego pago e de link mandado a influenciador tem que ser a
> `parceiros-ganhos.html`.** Apontar campanha para a `parceiros.html` e pagar
> clique numa pagina que diz ao Google que a boa e a outra.

A `parceiros-ganhos.html` **ainda nao recebeu** estas mudancas. Entrega separada.

## Conferir depois de subir

1. `www.moviki.com.br/parceiros.html` — o "Como comecar" mostra **quatro** passos
   e o terceiro fala das aulas. O rodape da secao explica o motivo legal.
2. Duas secoes novas depois dele: "O que voce recebe ao entrar" e "Qualquer
   comerciante pode conferir quem voce e".
3. Nenhum bloco de video visivel enquanto `MOVIKI_VIDEO_PARCEIRO` estiver vazia.
4. `app.moviki.com.br/seja-parceiro.html` — caixa azul "O que voce vai indicar"
   no topo e a lista "Depois de enviar" logo acima do botao.
5. Abrir `app.moviki.com.br/seja-parceiro.html?ref=paulopj` e conferir no console
   que o evento `chegou_por_indicacao` sai com o `ref` — a captura do upline dos
   niveis 2 e 3 nao foi tocada, mas e o que mais dói se quebrar.
6. `Ctrl+Shift+R` nas duas antes de julgar qualquer coisa. Cache foi o suspeito
   numero um de dois "bugs" em 16/09.

## Conferido antes da entrega

- `node --check` limpo nos 7 blocos de script inline dos dois arquivos
- Chromium a 390px nas duas paginas: **zero erro de JavaScript**
- Video: escondido com a constante vazia; visivel com id; `iframe` montado no
  clique, uma vez so
- Medicao preservada: `mvmetrica`/`mvEv` em 5 ocorrencias na `parceiros.html` e 9
  na `seja-parceiro.html`; todos os `data-ev` antigos mantidos
- App Check, captura do `ref`, fluxo de conta existente de 04/09 e a reserva do
  apelido: intactos
- UTF-8 sem BOM, LF, zero byte de controle nos dois
- Varredura de conformidade nos dois arquivos: nenhum "para sempre", "renda",
  "sem risco" ou numero que projete ganho. A unica ocorrencia de "garantido" e a
  frase original **"nao existe valor minimo garantido"**, que e negativa e deve
  continuar la

## Ligacoes

[[A5 - Programa de Parceiros]] · [[P37 - Prospeccao de parceiros e influenciadores]] ·
[[R - Checklist conformidade Meta e Google]] ·
[[R - Marcas de versao - SEO lote 2 16092026]]
