---
type: decisao
status: entregue
area: "[[A14 - Material de apoio do parceiro]]"
tags: [robo-social, feed, story, reel, criadores, material-de-apoio, padronizacao, lgpd, compliance]
atualizado: 2026-09-23
---

# Feed padronizado sobre o material de apoio

Marca do robo: **`2026-09-22-formatos`** (aparece na primeira linha do log de cada execucao do Feed, Story e Reel no Actions).

## O que mudou

- **O feed do dia a dia passou a publicar as pecas prontas do Material de apoio do parceiro.** O robo le `app.moviki.com.br/material/catalogo.json` ao vivo; peca nova que entra na aba do parceiro entra na rotacao sozinha. Nao repete ate girar o catalogo inteiro e evita dois posts seguidos do mesmo ramo.
- **A legenda e convertida para a voz da marca:** sai o `#publi` (a marca e o anunciante, nao um divulgador comissionado) e "Comece pelo meu link" vira "link da bio" no Instagram e `moviki.com.br` no Facebook. Sobrou marca de parceiro depois da troca, a peca e descartada.
- **Vitrine de lojista e card de pauta ganharam uma moldura unica** no padrao do material: marinho, mapa neon, logo do Moviki, botao verde. A cor do lojista nao entra mais. O banco `assets/fundos` foi aposentado.
- **Calendario:** sexta = card de pauta de parceiro; demais dias = peca do material. Catalogo fora do ar = card de pauta, o calendario nao fura.
- **Story novo, 2 por dia** (~9h e ~18h40), com os 33 stories do material de apoio que podem ir para a pagina oficial.
- **Reel voltou a publicar.** Com `SO_FACEBOOK` ligado o robo dizia "Reel e exclusivo do Instagram" e saia sem publicar nada — desde 24/08 nenhum reel foi ao ar. A Pagina do Facebook aceita Reel pela API; agora reel e story saem nela. Fontes do reel: o video 9:16 do material que pode ir para a pagina oficial + os 3 do banco do repo.
- **Brecha dos criadores:** peca de influenciador entra em feed, story e reel quando **ele autoriza no painel E o Moviki aprova**. Fonte desligada ate existir o secret `CRIADORES_URL`. Contrato em `moviki-assistente-social/conteudo/CRIADORES-CONTRATO.md`.
- **Previa antes de ir ao ar:** rodar o Feed com `dry_run` e baixar a arte em "Artifacts" na pagina da execucao.

## Por que

Os posts saiam cada um de um jeito: foto de vendedor de carrinho atras de loja de suplemento, etiqueta laranja num, verde no outro, texto por cima do rosto da pessoa. E a leitura do robo achou mais quatro defeitos que ja tinham ido ao ar:

| Defeito no ar | Conserto |
|---|---|
| Link `moviki.com.br/fabiofffggggmailcom` — o e-mail do lojista impresso em letra grande | slug derivado de e-mail fica fora da vitrine |
| Conta demo `hamburguermaster` e conta de teste `karina` divulgadas como negocio real | lista `VITRINE_EXCLUIR` |
| "Curitiba - PA" e "Cabedelo - PA" — Parana, Paraiba e Para viravam todos PA | UF pelo codigo ISO + tabela oficial |
| Etiqueta "TA ABERTO AGORA" sem o robo saber se estava aberto | chamadas neutras, com acento |

Todos com teste automatico.

## Decisoes tomadas

- **Vitrine de lojista DESLIGADA** (`VITRINE_POR_SEMANA` = 0) enquanto a base real for zero. De 11 a 16/09 foram 4 posts seguidos de contas de teste na pagina oficial — prova social falsa. **Ligar no primeiro lojista real:** secret `VITRINE_POR_SEMANA` = `1` no GitHub do `moviki-assistente-social`.
- **7 pecas do material nunca vao para a pagina oficial**, porque trazem "CADASTRE-SE PELO LINK DESTE PARCEIRO" impresso na arte: `feed-na-hora-foodtruck`, `feed-quem-se-move`, `feed-quem-se-move-2`, `feed-tudo-em-um-lugar`, `feed-na-hora-cidade`, `quadrado-na-hora`, `quadrado-zero-comissao`. Sobram **30 pecas publicaveis**.
- **Regra nova para quem sobe arte no material:** peca de feed com texto de parceiro impresso entra em `MATERIAL_EXCLUIR` no mesmo ciclo. Gravada na cadeira Canal e no `material/LEIA-ME.md`.
- **Peca de criador: duas chaves sempre.** O botao Autorizar sozinho nunca publica — a conta oficial e da marca, video nao passa pela trava de texto, e a decisao do funil ja era "o dono aprova, o robo nunca aprova". Revogada ou vencida (12 meses do termo) sai da rotacao; post antigo sai so a pedido, manualmente.
- **Criador fica com ate metade dos posts de cada formato** (`CRIADORES_PARTICIPACAO`, padrao 0,5), nunca o mesmo criador duas vezes seguidas, credito "Conteudo de @arroba" sempre. Legenda do criador que viola a trava vira a reserva inteira: o robo nao reescreve frase de terceiro.
- **Mais 7 pecas nunca vao para a pagina oficial**: 3 stories (`story-na-hora`, `story-tudo-em-um-lugar`, `story-quem-se-move`, com "link deste parceiro" impresso) e 4 videos (`video-cada-negocio`, `video-live-parceiro`, `video-live-parceiro-4x5` — "fale comigo pelo link"/"link deste parceiro" — e `video-parceiro-chama-parceiro`, de recrutamento e com 3:12, acima do limite de 90 s do Reel da Pagina).
- Dois falsos positivos da trava de compliance corrigidos: "Titan 160" (modelo de moto, nao o e-mail Titan) e "sem nada alem do que voce ja tem".

## O que conferir

1. Actions > Feed > Run workflow, tipo `material`, `dry_run` marcado. Log comeca com `2026-09-22-formatos`; baixar a arte em Artifacts.
2. Repetir com tipo `institucional` e ver a moldura nova.
3. Actions > Story e Actions > Reel > Run workflow **sem** `dry_run`, uma vez cada, e olhar a Pagina: **integracao nova (Reel e Story da Pagina) so se prova publicando de verdade.** Se ficar vermelho, a mensagem do erro da Meta vem no log.
4. No primeiro post real, conferir que a legenda termina em "Comece em moviki.com.br" e nao tem `#publi`.

## Pendencias

- ~~Construir a outra ponta da brecha~~ — **feito em 22/09**: endpoint `/api/criadores`, Área do criador, menu Criadores e secret `CRIADORES_URL`. Ver [[ARQ - Area do criador no painel do parceiro]] e [[ARQ - Menu Criadores no painel do dono]].
- **Integração da Página provada em produção:** reel em 22/09 às 21h58 (`video_reels`) e story em foto às 23h26 (`photo_stories`, primeira peça de criador). Falta a primeira publicação real de **story em vídeo** (`video_stories`).
- O termo do criador (v3.1) precisa dizer, com todas as letras: republicacao em feed, story e reel das redes do Moviki, com credito; revogacao a qualquer momento para frente; retirada de post antigo so a pedido; validade de 12 meses. Conferir antes do primeiro criador.

- Ligar a vitrine quando entrar o primeiro lojista real.
- As 3 contas de teste restantes (alem de `karina`, `hamburguermaster` e a do slug de e-mail) nao foram identificadas pelo slug — entram na `VITRINE_EXCLUIR` antes de ligar a vitrine, ou saem da base na limpeza da secao 3X do mapa.
- Os `.jpg` de `assets/fundos` podem ser apagados quando o Paulo quiser; nenhum codigo depende deles.

## Ligacoes

[[A14 - Material de apoio do parceiro]] · [[R - Regras de ouro]] · [[R - Marcas de versao no ar]]
