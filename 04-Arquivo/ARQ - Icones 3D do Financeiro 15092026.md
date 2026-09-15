---
type: arquivo
status: concluido
area: "[[A1 - Produto e Paineis]]"
tags: [icones, kairogen, painel-lojista, financeiro, entrega]
atualizado: 2026-09-15
---

# ARQ - Icones 3D do Financeiro 15092026

Fecha o terceiro item pendente de [[ARQ - Cardapio compravel na pagina publica 14092026]].
Mesma familia de [[Moviki - Icones 3D 10092026]].

## Arquivos

| Repositorio | Pasta | Arquivo | Tipo |
|---|---|---|---|
| moviki-app | `icones/` | `financeiro.png` | NOVO |
| moviki-app | `icones/` | `vender.png` | NOVO |
| moviki-app | `icones/` | `vendas.png` | NOVO |

256x256, PNG com transparencia. 83, 42 e 58 KB.

## O que cada um e

| Arquivo | Objeto | Por que |
|---|---|---|
| `financeiro.png` | cofre azul-royal, roda ciano, moeda dourada encostada | a aba e onde o lojista guarda a forma de receber |
| `vender.png` | etiqueta de preco verde, ilhos branco, cordao azul e um interruptor ciano na face | "Ligar a venda" — etiqueta e o simbolo universal de vender, e o interruptor conta o resto |
| `vendas.png` | sacola azul com alcas cianas e um cupom branco saindo | pedidos que entraram |

## Producao

Kairogen, `seedream-v4`, 2048x2048, 2 creditos cada. Saldo: 394 antes, **382
depois** (6 geracoes; as 3 primeiras foram descartadas).

**As 3 primeiras sairam com chao reflexivo.** O reflexo do objeto tem a cor do
objeto, nao do fundo — o chroma key nao o remove, e ele virava um degrau
esbranquicado colado na base do icone, visivel em qualquer fundo claro. Nao se
conserta no tratamento: o conserto foi no prompt, com "FLOATING in empty space,
no ground plane, no reflection, no cast shadow" e magenta nos quatro lados.

Fundo chroma **magenta**, seguindo a regra de 10/09: verde so quando o objeto
nao tem verde, ciano nem vidro — e os tres tem.

## Tratamento

Script proprio em Pillow/numpy: chroma key por diferenca de canal
`(R+B)/2 - G`, mediana para tirar pontinhos, **despill** mais forte na borda
(sem ele o icone fica com contorno rosa no fundo escuro do painel), recorte pelo
objeto solido e reencaixe em 256x256 ocupando 90% do quadrado — e assim os tres
tem o mesmo peso visual lado a lado.

Duas decisoes contra o que a rodada de 10/09 fazia:

- **Sem sombra reconstruida.** Reconstruir a sombra a partir do escurecimento do
  fundo pintava um borrao cinza atras do objeto: visivel no painel escuro e pior
  em fundo claro. Icone recortado limpo e o que a familia ja usa.
- **Sem quantizar a paleta.** A reducao para 200 cores levava de 85 KB para
  37 KB, mas abria faixas de banding nos degrades do cofre e da sacola. PNG
  completo com `optimize` fica em 42-83 KB, que esta longe do problema do
  favicon de 949 KB.

A sombra de contato quase preta que o chroma nao pega (magenta escurecido ate o
preto perde a diferenca de canal) sai por um filtro proprio: pixel com
luminancia abaixo de 75 e saturacao abaixo de 0,38. Nenhum dos tres objetos tem
parte quase preta — azul royal, verde e dourado ficam bem acima disso.

## Conferido

Folha de contato sobre o azul do painel (#0e1c30) E sobre fundo claro, com cada
icone tambem reduzido a 44 px — que e o tamanho real no menu lateral. Sem franja
rosa, sem plataforma cinza, sem banding.

## Ainda nao aparecem na tela

O `index.html` do painel desenha esses tres em **SVG**, escrito assim de
proposito em 14/09 para nao depender de PNG que nao existia. Trocar o SVG pelo
`<img>` com `onerror` (a degradacao limpa que o resto do painel usa) entra na
proxima edicao do `moviki-app/index.html`, junto com o `sku` e o aviso sonoro de
pedido novo.
