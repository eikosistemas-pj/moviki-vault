---
type: arquivo
status: concluido
area: A14 - Material de apoio
tags: [anuncio, video, trafego-pago, comerciante, live-commerce, avatar, conformidade]
atualizado: 2026-09-17
---

# ARQ - Anuncio do comerciante live commerce 17092026

Primeira peca de video pronta para trafego pago. Entregue em 17/09/2026,
`moviki-anuncio-live-commerce-v4.mp4`, **23,7 s**, 1080x1920, H.264 8 bits,
audio normalizado em -16 LUFS, legenda queimada.

Substitui o rascunho do eixo "mapa" e o do eixo "dia de chuva", os dois
descartados pelo Paulo.

## Corte final

| # | Fala | Imagem | Dur. |
| ---: | --- | --- | ---: |
| 1 | Artesanato, roupa, eletrônico, comida. Se você tem o que mostrar, você tem o que vender ao vivo. | 4 cortes: croche, loja de roupa, eletronicos, confeiteira com o bolo | 6,4s |
| 2 | Vender ao vivo mudou isso. Você abre a câmera do celular, mostra o que tem, e quem está perto vê na hora. | Dona Cleide transmitindo da cozinha | 7,3s |
| 3 | A pessoa toca no produto e fala com você. Sem sair de casa. Sem loja, sem estúdio. | Confeiteira do video institucional mostrando o bolo | 6,4s |
| 4 | Trinta dias grátis. Sem cartão. | Cartao da marca | 3,5s |

Voz Malu `fhtZMBwha5du5OxuvexO`, pt, stability 0.5, similarity_boost 0.8,
use_speaker_boost true, sem speed.

## Conformidade

- Avatar demonstra, nunca testemunha. Nenhuma fala em primeira pessoa.
- Nenhuma promessa de resultado, faturamento ou prazo de retorno.
- Celular dos avatares sempre de costas, tela nunca visivel.
- "Trinta dias gratis, sem cartao" bate com a copy no ar em `comerciantes.html`.
- Peca da oferta do COMERCIANTE. Nada do Programa de Parceiros entra como
  anuncio pago.

## Custo

181 creditos Kairogen no total, **267 restantes**. 4 clipes novos de 9x16, 6
imagens base e 9 narracoes, contando as refeitas.

## Defeitos que a conferencia pegou antes de virar peca no ar

1. Celular encostado no ouvido na cena da live - lia como ligacao, nao como
   transmissao. Refeita.
2. Maca da Apple visivel em duas geracoes diferentes. Refeitas as duas.
3. Texto embaralhado na caixa do fone e embalagem de terceiro na prateleira da
   loja de eletronicos. Refeita.
4. Segundo celular inventado na mao da lojista de roupas - dois aparelhos na
   mesma cena. Refeita.
5. Legenda longa vazando pelas laterais: `WrapStyle 2` desliga a quebra
   automatica. Corrigido para `WrapStyle 0`, corpo 58.
6. Bloco montado com `-c:v copy` saiu com 6,47 s em vez de 6,40 s e empurrava
   os blocos seguintes. So reencodando o corte fecha no frame exato.
7. Tres legendas entrando 0,3 s antes da fala. Reancoradas nos silencios
   medidos no proprio audio.

## Regras de ouro que esta rodada deixou

1. **O que entra em trafego pago e a oferta do comerciante.** O Programa de
   Parceiros circula em conversa e em DM, nunca em anuncio para publico frio -
   a conta antiga ja foi restringida uma vez por isso.
2. **Banco de clipe nao e material.** 59 clipes gerados e zero peca montada
   custam o mesmo que nenhum clipe.
3. **Corte de video se alinha a palavra, nao ao bloco.** Mostrar roupa enquanto
   a voz diz "eletronico" desmonta a peca inteira.
4. **Marca de terceiro e texto embaralhado sao o mesmo defeito:** os dois fazem
   a peca ler como falsa. Conferir quadro a quadro antes de montar.
5. **Ambiente sem saida de rede nao monta video.** `cdn.kairogen.ai` e
   `moviki.com.br` nao respondem do ambiente do Claude: o que e gerado la e
   baixado pelo Paulo e sobe pelo chat.
6. **Ilustracao aprovada no site vale como imagem de produto.** A `livehero.png`
   resolveu a tela do Moviki sem gravacao - mas a captura real continua sendo
   melhor.
7. **Quem nao escuta o audio confere pelo desenho das pausas** - e diz que
   conferiu assim. Nome de arquivo baixado nao e prova de ordem: dois dos quatro
   vieram trocados.

> As regras 1 a 7 precisam ser fundidas em
> [[R - Regras de ouro]] - nao consegui editar o arquivo porque o
> `moviki-vault` e privado e nao clona sem credencial.

## Onde a peca vai

- `moviki-app/material/` + entrada nova no `catalogo.json`, tipo `video`
- Meta: conjunto proprio, publico frio de Joao Pessoa, objetivo conversao no
  `CompleteRegistration`, R$ 20/dia. **Nao ligar antes do teste do navegador
  embutido** - ver [[ARQ - Medicao do funil 17092026]]

## Ligacoes

[[P - Anuncio do comerciante 9x16]] · [[R - Elenco de avatares do material]] ·
[[ARQ - Medicao do funil 17092026]] · [[R - Marcas de versao no ar]]
