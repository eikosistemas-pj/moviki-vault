---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [regra, armadilha, live, video, aquisicao]
atualizado: 2026-09-14
---

# R - Regras de ouro novas de 11 a 14092026

Regras que nasceram entre 11 e 14/09/2026 e ainda **não** estão em
[[R - Regras de ouro]]. Esta nota é o apêndice; a nota mestre continua sendo a
que se lê antes de mexer em qualquer coisa.

> **Por que apêndice e não substituição:** a nota mestre tem conteúdo acumulado
> desde agosto e não foi possível reler o arquivo inteiro publicado. Fundir sem
> o texto integral apagaria regra antiga. A fusão é uma rodada própria, com o
> arquivo em mãos.

## Dinheiro e checkout

- **Dinheiro de venda nunca passa pela conta da Eiko.** A cobrança é emitida pela
  subconta do lojista; taxa do Moviki, quando houver, só por split.
- **Preço de compra nunca vem do navegador.** O servidor recalcula pelo estado da
  live: oferta ativa > preço da live > preço do cardápio.
- **Todo `externalReference` novo tem prefixo e é desviado ANTES do fluxo das
  assinaturas no webhook.** Sem o desvio, `pedido:...` viraria uma assinatura
  falsa em `assinaturas/{pedido:...}`.
- **Chave de API de subconta só cifrada, e a env de cifra não se troca.** Trocar
  `CHECKOUT_CHAVE` depois de criar subconta deixa as chaves guardadas ilegíveis.
- **Tarifa fixa por transação define o pedido mínimo.** R$ 1,99 de Pix numa venda
  de R$ 5 é 40% do valor — por isso o mínimo do checkout passou a R$ 20.
- **Todo pagamento tem três caminhos para virar pago:** webhook, tela do comprador
  e botão do lojista. Nenhum depende do outro.
- **Todo webhook do Asaas tem cadastro separado por ambiente.** Virar para
  produção exige sincronizar o token no cadastro de produção no mesmo dia; um
  lado sozinho penaliza a fila.

## Deploy, módulos e interruptores

- **Módulo novo sobe ANTES do arquivo que o importa.** `require` de arquivo que
  não existe derruba a função inteira — e o webhook é a função do dinheiro.
- **Escrita em documento de configuração compartilhado é sempre com `merge`.**
  `setDoc` sem merge em `configuracoes/liveTermos` apagaria os outros
  interruptores.
- **Todo módulo novo sobe com chave-mestra.** `liveDesligada` derruba tudo na
  hora, sem deploy.
- **Interruptor de produto mora em `configuracoes`, editável no painel do dono** —
  nunca num arquivo que exige subida para mudar de ideia.
- **Rota bonita citada no `canonical` precisa existir no `vercel.json`, antes do
  curinga de apelido.** Senão o endereço cai no `api/og` e responde "Negócio não
  encontrado", sem erro visível.
- **Domínio que redireciona quebra CORS.** Redirecionamento entre origens troca a
  origem por `null` e o navegador bloqueia a chamada.
- **No repo `moviki` a CSP é `<meta http-equiv>` por arquivo**, não header de
  servidor. Página nova leva a própria meta ou o recurso é bloqueado calado.
- **Entrega de arquivo compartilhado se monta sobre a marca que está no GitHub na
  hora**, nunca sobre a cópia que a conversa tem em mãos — e a marca se reconfere
  no momento de subir.

## Live e conteúdo

- **Número na tela é número contado.** Assistindo, "Restam N", pico e toques em
  Quero são reais. Escassez de teatro é propaganda enganosa (CDC art. 37).
- **Nunca sorteio.** Brinde por ordem de chegada. Sorteio com fim comercial exige
  autorização prévia (Lei 5.768/71).
- **Estado que o dono escreve não prova plano.** A página pública confere
  `assinaturas/{uid}` antes de pintar qualquer ferramenta paga, e o endereço de
  transmissão só sai do servidor.
- **Presença ao vivo precisa de pulso.** Aba fechada sem "Encerrar" deixa
  `ativa:true` para trás; só o carimbo `pulso` com prazo de 3 min diz a verdade.
- **WebRTC não grava no servidor.** O que precisar virar vídeo guardado grava no
  aparelho de quem transmite.
- **Filtro de conteúdo que só roda na tela não é trava.** A barreira real é a
  cópia que roda no servidor.
- **Aceite de regra é versionado.** Mudou o texto, sobe a versão e todo mundo
  aceita de novo.
- **Freio por IP no Brasil precisa de folga:** o 4G põe centenas de pessoas atrás
  do mesmo IP (CGNAT).
- **`Disallow` no `robots.txt` não tira da busca** — página não rastreada nunca
  chega a ler o `noindex`. Para esconder, `noindex`; nunca bloquear.

## Produção de vídeo

- **A locução é a régua.** Escolher a voz, gravar, cronometrar e só então montar.
- **Voz oficial em toda peça: Malu `fhtZMBwha5du5OxuvexO`.** Grafia para o motor:
  **"Mo-víki"** — sem isso a voz lê "MÓviki".
- **UI em vídeo aparece de três formas, nunca de outra:** tela cheia, celular
  parado em plano fixo, ou celular desfocado. Proibido compor UI legível dentro
  de celular gerado por IA em movimento.
- **O corte se monta das fontes, nunca recortado do master.**
- **Legenda queimada em todo corte**, com tempos medidos por `silencedetect`.
- **Nunca desacelerar clipe para caber na duração.**
- **Nada de banco de sons** — ambiência se sintetiza.
- **Nenhuma peça exibe número que sugira alcance automático.** O Moviki é o palco;
  o megafone o lojista já tem.
- **Vídeo entregue ao cliente sai em H.264 8 bits** — HEVC 10 bits não toca em
  celular antigo, e o Chromium do Playwright não lê H.264 na entrada.
- **Vídeo acima de 25 MB entra só pelo anexo de Release do GitHub** (release
  `Material_bruto`, repo `moviki-app`, até 2 GB).
- **Nunca apagar vídeo antigo do YouTube antes de o painel apontar para o id
  novo** — enquanto isso o cliente vê quadro preto.
- **Verificação de vídeo no YouTube só é confiável por oembed.**

## Aquisição e medição

- **Antes de consertar uma etapa do funil, meça quantas pessoas chegaram nela.**
  Etapa que quase ninguém alcança não explica resultado nenhum.
- **Antes de reescrever uma página que não converte, pese a página.** Copy só
  importa para quem esperou o carregamento terminar.
- **Favicon não é arte — é ícone de aba.** Nunca acima de 512x512.
- **Objetivo de campanha é o que você está comprando.** Otimizar por visita compra
  visita; na Meta o objetivo não é editável, e errar custa campanha nova.
- **Objetivo de conversão exige conversão existente.** Consertar a página vem
  antes de trocar o objetivo.
- **Correspondência AMPLA é proibida no Google Ads do Moviki.** Só frase e exata.
- **Palavra-chave descreve o problema de quem vende, nunca a funcionalidade do
  produto.**
- **Negativa só contra termo de consumidor final.**
- **Conserto se confere lendo o objeto alterado, nunca o relatório de gasto.**
  Gasto zero pode ser sintoma suprimido, não causa removida.
- **Campanha que gasta pouco pode estar asfixiada, não econômica** — o que separa
  saúde de falta de inventário é impressão, nunca custo.
- **Diagnóstico se confirma na fonte, não na anotação anterior.**
- **Estimativa interna de conversão nunca vira texto de anúncio ou de página.**
- **Autonomia da rotina de campanhas: ação direta só no reversível.** Negativa,
  pausar anúncio reprovado e criar palavra positiva são ação; orçamento, lance,
  pausar campanha, remover palavra e segmentação são recomendação.

## Ligações

[[R - Regras de ouro]] · [[R - Marcas de versao no ar]] · [[A13 - Modo Live]] ·
[[A14 - Material de apoio do parceiro]] · [[R - Rotina de checagem das campanhas]] ·
[[R - Regras de ouro de producao de video]] · [[R - Regras de ouro de producao de cortes]]
