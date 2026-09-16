---
type: decisao
status: no ar
area: Painel do lojista
tags: [video, capa, tiktok, oembed, storage]
atualizado: 2026-09-16
---

# Capa do TikTok automática — 16/09/2026

## O problema
Cartão de vídeo do Instagram e do TikTok nascia sem imagem na página pública.
Nenhuma das duas redes entrega miniatura para fora do aplicativo delas.

## A diferença entre as duas
- **TikTok**: mantém um endereço público que devolve a miniatura **sem pedir
  chave nenhuma**. Dá para automatizar.
- **Instagram**: fechou a saída pública. Não existe caminho, e prometer que
  existe só geraria tentativa que sempre falha. Fica na mão, de propósito.

## Como ficou
`moviki-robo/api/upload-imagem.js` ganhou um modo novo: `tipo:'tiktok'`. O
painel manda o link do TikTok, o robô busca a miniatura e **re-hospeda no
nosso Storage**.

### Quase virou arquivo novo — e não podia
A primeira versão nasceu como `api/video-capa.js`, arquivo novo. Errado: o
`moviki-robo` já está com **15 funções em `api/`** e a regra do projeto é
explícita — *função nova entra como etapa de uma existente, nunca como arquivo
novo*. Foi dobrado dentro do `upload-imagem.js`, que já verifica o token, já
fala com o bucket e já devolve URL pública. A etapa final é literalmente a
mesma. Contagem de funções: **continua em 15**.

A regra existia, estava no vault, e ainda assim o arquivo novo foi escrito
primeiro. Conferir o teto de funções faz parte de escrever qualquer coisa que
toque o `moviki-robo`.

### Por que re-hospedar em vez de guardar o endereço do TikTok
1. O endereço que eles devolvem é **assinado e temporário**. Guardado como
   está, funcionaria hoje e sumiria em algumas semanas — e o lojista nunca
   saberia por que a capa dele evaporou.
2. A CSP das páginas públicas não precisa abrir para mais um domínio.
3. A validação `fotoOk()` das duas pontas continua como está: só
   firebasestorage e ibb.co.

### Travas
- Só link do TikTok entra. O Instagram nem tenta.
- A miniatura tem que vir de um domínio do próprio TikTok. Sem essa trava, um
  endereço adulterado mandaria o robô baixar qualquer coisa da internet com a
  credencial dele.
- Tipo da imagem conferido **pelos bytes**, não pelo que o servidor diz.
- Tempo limite de 6 s.
- **Falha fechada**: qualquer tropeço responde `ok:false` e o painel
  simplesmente não põe capa. Capa é conforto, não tarefa — erro vermelho na
  tela por causa de uma capa automática seria pior que a ausência dela.

## No painel
- Colou link do TikTok: a busca dispara **sozinha**, em segundo plano. Se vier,
  o cartão já nasce com imagem.
- Dentro da folha de capa: botão **"Buscar a capa no TikTok"** para tentar de
  novo. Aqui o lojista pediu — então o silêncio seria grosseria: se não vier,
  ele é avisado.
- O vídeo é achado **pela URL, não pelo índice**: entre o pedido e a resposta a
  lista pode ter sido reordenada.
- Nunca passa por cima de capa que o lojista escolheu.
- Depois, **Salvar tudo** — como qualquer campo.

## Ordem de subida
`upload-imagem.js` primeiro, `index.html` depois. Ao contrário, o botão
aparece antes de o servidor saber responder.

## Pendência
O teste do endereço público do TikTok só pode ser feito no ar — o domínio deles
é bloqueado no ambiente onde o código foi escrito. Todo o resto foi testado com
respostas simuladas: capa boa, sem capa e endereço fora da peneira.

[[ARQ - Capa do video escolhida pelo lojista 16092026]]
[[ARQ - Tela escura na escolha da cena 16092026]]
[[R - Marcas de versao no ar]]
