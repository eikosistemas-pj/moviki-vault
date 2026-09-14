---
type: arquivo
status: concluido
area: A5 - Programa de Parceiros
tags: [videoaula, parceiro, niveis, comissao, conformidade]
atualizado: 2026-09-11
---

# ARQ — Aula P11 dos níveis do parceiro

Aula **"Seu nível e as barras da comissão"**, no ar em **11/09/2026**.

## Ficha

| Campo | Valor |
| --- | --- |
| Código de cena | **P11** (`P11-parceiro-niveis`) |
| ID do YouTube | `6E3z6cbOXJ4`, não listado |
| Duração (`d`) | `2:34` |
| Chave | `mod-parc-niveis`, módulo "Seu nível" |
| Onde embute | `#nvCard` — fim do card Seu nível, na Visão geral |
| Voz | **Malu** (Kairogen, `fhtZMBwha5du5OxuvexO`) — primeira aula do parceiro com ela |
| Entregáveis | `P11-parceiro-niveis.mp4` (1080p, legenda queimada) + `.srt` |
| Custo | 23 créditos Kairogen (1 por fala); saldo após ~326 |

## Marcas do `parceiro.html`

| Marca | O que era |
| --- | --- |
| `2026-09-11-aula-niveis` | Slot com `id:''` — aula invisível até o id do YouTube chegar |
| `2026-09-11-aula-niveis-id` | Id e duração preenchidos; aula visível |

Conferido na entrega: box embutida no `#nvCard`, **12 aulas publicadas**, zero
erro de JS.

## Decisões

- **Aula NOVA, não substituição** da aula de comissões (decisão do Paulo).
- Ao subir com id, o selo de todo parceiro vira laranja "1 aula nova" e o card
  mostra "11 de 12" — **ninguém é retrancado**, porque `aulasEm` permanece.
- O código nasceu como "P09" e **colidiu com o crachá**; virou P11. Antes de dar
  código de cena novo, conferir a tabela inteira das videoaulas.
- Narração **sem valores em R$**: preço muda e vídeo não se corrige com deploy.

## O que mudou no painel na mesma entrega

- **Barra 1 da calculadora passou a aplicar o % do nível** (`NIVEIS_CV`, igual ao
  `NIVEIS_PARCEIRO` do webhook): 26+ → 16%, 51+ → 17%, 101+ → 18%. Antes ficava
  presa em 15% e contradizia o Regulamento 1.1. Rótulos dinâmicos `#cvN1Sub` e
  `#cvSomaRecRot`.
- **Linguagem corrigida** (autorização permanente Meta/Google):
  "Indique e ganhe mais" → "Convide outros parceiros"; "ganhe bônus" → "recebe um
  bônus único"; 5 ocorrências de "todo mês" em texto de comissão → "cada
  mensalidade paga"; "Como você ganha" → "Como a comissão funciona"; texto de
  compartilhamento do link sem "ganhe comissão"; olhinho "Ocultar sua equipe" →
  "Ocultar suas indicações".
- Textos de 15% atualizados com a faixa 16–18% dos níveis Ouro a Esmeralda.

## Estúdio do parceiro (bastidor, não vai para repositório)

- Rodar: clonar `moviki-app`, `python3 -m http.server 8899 --bind 127.0.0.1` na
  raiz, `NODE_PATH=$(npm root -g) node rodar-p.js`.
- **`npm install` bloqueado (403 da política)** — usar o Playwright global e a
  Poppins do sistema (sem SemiBold: 600 → Bold).
- Áudio: `generate_audio` por fala; o CDN do Kairogen é bloqueado no curl, baixar
  com `download_audio_from_url`. **429 a cada ~10 chamadas** — esperar ~60 s.
- Pós-áudio: `silenceremove` nas pontas + `loudnorm -16 LUFS` + `aresample=44100`.
- Seed: `demo-parceiro` "João da Feira", 14 comissões nível 1 no mês, olhinhos de
  dinheiro e gráfico **ligados** — nenhum valor de saldo aparece no vídeo.
- Armadilha: `.mkSimGrupo:nth-of-type(n)` não funciona (o 1º div é o título) —
  usar `>> nth=`.
- Armadilha: cortar o fim pelo último áudio; a gravação sobra ~8 s mudos.

## Efeito colateral

A entrega desta aula foi montada sobre marca velha e apagou a aba de material de
apoio — ver [[ARQ - Incidente - aba de material apagada pela aula P11]].

## Ligações

[[A5 - Programa de Parceiros]] · [[A8 - Conteudo e Social]] ·
[[P19 - Plano de niveis do parceiro]] ·
[[ARQ - Videoaulas no ar 11092026]] ·
[[ARQ - Incidente - aba de material apagada pela aula P11]] ·
[[R - Voz oficial das videoaulas]] ·
[[R - Checklist conformidade Meta e Google]]
