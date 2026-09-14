---
type: recurso
status: referencia
area: A13 - Modo Live
tags: [live, cdc, lgpd, conar, sorteio, termos]
atualizado: 2026-09-14
---

# R - Live - Regras legais e conformidade

Não é parecer jurídico — é o mapa do que pesa na live. Validar os textos com
advogado antes de divulgar a live em anúncio.

Em 12/09/2026 subiram `termos.html` e `privacidade.html` com as cláusulas da live
e do checkout, mais a página nova `regras-da-live.html`. Os textos abaixo são a
base do que está no ar.

## Código de Defesa do Consumidor

- **Oferta vincula** (arts. 30 e 35): preço dito ou mostrado na live obriga o
  lojista. Por isso o estúdio lembra: "anuncie só o que vai cumprir".
- **Informação clara** (art. 31) e **Decreto 7.962/2013** (comércio eletrônico):
  preço, condições e quem vende. A página da live mostra o nome do negócio e o
  aviso da sacolinha.
- **Propaganda enganosa** (art. 37): escassez falsa, "de/por" com preço "de"
  inventado. "Restam N" só existe com estoque informado e baixado pelo lojista.
- **Arrependimento de 7 dias** (art. 49) vale para compra fora do
  estabelecimento — responsabilidade do lojista.

## Sorteio

Distribuição gratuita de prêmio por sorteio, vale-brinde ou concurso com fim
comercial exige **autorização prévia do Ministério da Fazenda (Lei 5.768/71)**.
O Moviki não oferece sorteio. Oferece **brinde garantido por ordem de chegada**,
que é condição de compra, não sorte.

## LGPD

- Chat: nome digitado e mensagem, públicos para quem assiste, **30 dias** (TTL).
  O aviso aparece antes do primeiro comentário e pede para não escrever
  telefone, endereço ou documento.
- Presença: sem nome, sem IP guardado — só a hora, por 2 dias.
- Nenhum vídeo é guardado pelo Moviki.
- **Checkout:** o comprador informa nome, WhatsApp e CPF. O CPF vai ao Asaas
  (exigido para gerar o Pix) e **no Moviki fica só o final**. Nome e WhatsApp
  ficam no pedido para o lojista entregar. "Fulano comprou" no chat só com a
  caixa marcada pelo comprador, e só o primeiro nome.
- **Pendente:** TTL configurado no Google Cloud para `livechat`, `livepresenca`,
  `checkout_freio` e `pedidos` — o campo `expiraEm` já é gravado, a regra de
  expiração ainda não.

## CONAR e plataformas

- Se o lojista trouxer influenciador pago para a live, é publicidade: `#publi`
  falado e escrito no título.
- Anúncio da Meta/Google falando da live: descrever a ferramenta, nunca venda ou
  resultado ("mostre seus produtos ao vivo", nunca "venda 3x mais").

## Imagem e menores

- Quem aparece ao fundo na feira tem direito de imagem — orientar o lojista a
  filmar o produto e a si mesmo.
- Menor de idade apresentando a live: proibido nos termos.

## Cláusula dos Termos de Uso (base do que subiu em 12/09; validar com advogado)

> **Transmissões ao vivo.** O Assinante é o único responsável pelo conteúdo que
> transmite, pelos produtos, preços, estoques, cupons e brindes que anuncia e
> pelo cumprimento das ofertas feitas durante a transmissão, nos termos do
> Código de Defesa do Consumidor. É proibido transmitir produtos ou serviços
> ilegais ou de venda restrita, realizar sorteios sem a autorização exigida em
> lei, anunciar escassez ou preços que não correspondam à realidade, exibir
> terceiros sem autorização e usar menores de idade como apresentadores. O
> Moviki pode interromper transmissões que violem estes Termos.
>
> **Pagamento pela live (Enterprise).** Quando o Assinante ativa o recebimento
> por Pix, o Moviki abre, em nome dele, uma conta de pagamento na instituição
> parceira (Asaas), sujeita aos termos dela. O valor pago pelo cliente cai
> diretamente nessa conta; o Moviki não recebe, não guarda e não repassa valores
> de venda. O Assinante é o vendedor: responde pela entrega, pela troca, pelo
> arrependimento em 7 dias (art. 49 do CDC), pelo reembolso e pela nota fiscal
> da venda. A entrega ou retirada é combinada entre o Assinante e o cliente.

## Em aberto

- [ ] Validação dos textos com advogado antes de anunciar a live
- [ ] TTL no Google Cloud
- [ ] Revisar as páginas de plano para descrever a ferramenta, nunca a venda

## Ligações

[[A13 - Modo Live]] · [[A10 - Conformidade e LGPD]] ·
[[R - Checklist conformidade Meta e Google]] · [[R - Regras de conteudo e tom]] ·
[[R - Live - Moderacao e regras de conteudo]] · [[P24 - Modo Live - lancamento]]
