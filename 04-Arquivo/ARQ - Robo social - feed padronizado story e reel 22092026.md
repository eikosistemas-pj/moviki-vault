---
type: arquivo
status: concluido
area: A8 - Conteudo e Social
tags: [robo-social, feed, story, reel, material-de-apoio, criador, conformidade, armadilha]
atualizado: 2026-09-22
---

# ARQ - Robo social - feed padronizado story e reel 22092026

Três rodadas no `moviki-assistente-social` em 22/09/2026. Marca em
`src/config.py` (`VERSAO`, impressa na 1ª linha do log):
`2026-09-22-feedpadrao` → `2026-09-22-formatos` → **`2026-09-22-criador`**.

## 1. Feed padronizado sobre o Material de apoio

- **Seg a Qui = peça pronta do Material de apoio do parceiro**, lida ao vivo de `app.moviki.com.br/material/catalogo.json` (`src/material.py`). Só `tipo: feed`, proporção 4:5 a 1,91:1, sem `recrutar`. Não repete até girar o catálogo; evita dois posts seguidos do mesmo ramo. **30 peças publicáveis** em 22/09.
- **A arte vai como está; a legenda é convertida:** sai `#publi` (a marca é o anunciante), `Comece pelo meu link: {link}` vira "link da bio" (Instagram) ou `moviki.com.br` (Facebook). Sobrou marca de parceiro → peça descartada.
- **7 peças nunca vão para a página oficial** (`MATERIAL_EXCLUIR`): trazem "CADASTRE-SE PELO LINK DESTE PARCEIRO" impresso.
- **Sexta = card de pauta de parceiro.** Catálogo fora do ar → card de pauta; o calendário não fura.
- **Moldura única** (`src/arte.py`): marinho, mapa neon, logo, botão verde. Cor do lojista não entra; `assets/fundos` aposentado.

## 2. Vitrine de lojista DESLIGADA

`VITRINE_POR_SEMANA` = 0. De 11 a 16/09 foram **4 posts seguidos de contas de
teste** na página oficial. Barrados com teste: slug derivado de e-mail (foi ao ar
`fabiofffggggmailcom`), conta demo/teste (`hamburguermaster`, `karina` em
`VITRINE_EXCLUIR`), UF errada ("Curitiba - PA"), "TÁ ABERTO AGORA" sem saber se
está aberto. **Ligar no 1º lojista real** com o secret `VITRINE_POR_SEMANA=1`.

## 3. Story e reel

- `story.yml` novo: **2 stories por dia** (~9h e ~18h40), com os 33 stories do material.
- Reel ter e sáb com o vídeo 9:16 do material + os 3 do banco do repo.
- ⚠️ **O reel não publicava NADA desde 24/08.** Com `SO_FACEBOOK` ligado o robô dizia "Reel é exclusivo do Instagram" — falso, a Página aceita Reel pela API.
- **Reel na Página confirmado:** 22/09, 21h58 (`video_reels`, media `1435287178666529`).
- **Story em foto confirmado:** 22/09, 23h26 — ver [[ARQ - Primeiro story de criador no ar 22092026]].

## 4. Brecha dos criadores

Peça de influenciador entra em feed, story e reel com **duas chaves**. Fonte
ligada pelo secret `CRIADORES_URL`. Reel 3 a 90 s, story 3 a 60 s. **Até metade
dos posts de cada formato**; crédito "Conteúdo de @arroba"; legenda suja do
criador vira reserva inteira; peça revogada ou vencida (12 meses) sai da
rotação. Contrato: `moviki-assistente-social/conteudo/CRIADORES-CONTRATO.md`.

## Trava de conteúdo

`src/compliance.py`. Dois falsos positivos corrigidos em 22/09: "Titan 160" e
"sem nada além".

## Prévia antes de ir ao ar

Actions > Feed > Run workflow com `dry_run` → a arte fica em "Artifacts".

> **Dry-run valida conteúdo; só a publicação real valida integração.**

## Ligações

[[A8 - Conteudo e Social]] · [[A14 - Material de apoio do parceiro]] ·
[[ARQ - Area do criador no painel do parceiro]]

*Reconstruída em 23/09/2026 a partir do MAPA-MESTRE de 23/09.*
