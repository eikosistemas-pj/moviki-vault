---
type: arquivo
status: concluido
area: A8 - Conteudo e Social
tags: [videoaula, youtube, lojista, parceiro, identificacao]
atualizado: 2026-09-11
---

# ARQ — Videoaulas no ar 11/09/2026

Retrato das videoaulas publicadas em **11/09/2026**: **16 aulas do lojista** e
**12 do parceiro**, todas **não listadas**, no canal **@app.moviki**.

## A regra: o link é o identificador

O Paulo manda **só o link do YouTube**. Os códigos `T00`, `P03` e afins existem
**só no vault e no estúdio** — no YouTube ele renomeou tudo para "aula número
tal". Então:

- **Nunca perguntar "qual T é essa?"**.
- O trecho depois de `youtu.be/` é o **id**, é único, e amarra a aula ao módulo
  do painel e à cena do estúdio.
- Link que não está em tabela nenhuma: **perguntar, não adivinhar**.

## Fluxo de refazer uma aula

1. O Paulo manda o link e diz o que mudar.
2. Acha-se o id na tabela → acha-se a cena.
3. Ajusta-se a cena, gera-se a narração (desde 10/09, voz **Malu**), grava-se e
   entrega-se `.mp4` + `.srt`.
4. Ele sobe no YouTube — **toda subida gera id NOVO**, o YouTube não troca o
   arquivo de um vídeo publicado.
5. Ele manda o link novo; troca-se o `id` no painel e **atualiza-se a tabela na
   mesma entrega**.
6. **Só então** ele apaga o vídeo antigo.

⚠️ **Nunca apagar o vídeo antigo antes de o painel apontar para o novo** — o
cliente vê quadro preto.

## Onde se troca o id

Dentro de `window.MOVIKI_TUTORIAIS`, em cada item: `id` (trecho depois de
`youtu.be/`), `d` (duração `m:ss`, medida com `ffprobe` e arredondada para
cima), `t` (só muda se o vídeo mostrar mais ou menos coisa) e o `sel` do módulo
(seção ou qualquer seletor — a P11 usa `#nvCard`). Depois: `node --check` nos
blocos de script e conferência no navegador da caixa embutida e da contagem de
publicadas.

## Arquivos e marcas de referência

| Painel | Arquivo | Marca |
| --- | --- | --- |
| Lojista | `moviki-app/index.html` | `2026-09-02-bv-completo` |
| Parceiro | `moviki-app/parceiro.html` | `2026-09-11-aula-niveis-id` |

Ordem do parceiro no `MOVIKI_TUTORIAIS`: abertura, conduta, começar, **nível**,
indicações, divulgação, crachá, comissões, pagamentos, desempenho, dados, Vik.

## Estado das travas

- **Lojista:** a tela de boas-vindas abre sozinha até ele ver as 4. **Não tranca
  nada do painel.**
- **Parceiro:** a Divulgação fica trancada até ele ver **todas as publicadas**
  (`MIN_AULAS = 8` é só o piso para a trava existir), medindo reprodução real
  pela API do YouTube. Concluiu uma vez (`aulasEm`), nunca mais tranca.
- As duas dormem sozinhas se faltar vídeo abaixo do piso.

## Conformidade das aulas do parceiro

Fala-se em **comissão**, sempre condicionada a assinatura efetivamente paga.
Nunca "renda", "garantido", "todo mês", "sem risco", e nunca número que projete
quanto a pessoa vai receber. Vídeo é anúncio aos olhos da Meta e do Google, e a
conta antiga do Moviki já foi restringida uma vez.

## Pendências

- [ ] Aula `sRdjQdyNTL0` (Fotos, cena `T16-fotos`) **desatualizada**: a tela
      virou "Fotos e vídeos" em 10/09.
- [ ] Antes de dar código de cena novo, conferir a tabela inteira — em 11/09 a
      aula de níveis nasceu "P09" e colidiu com o crachá.

## Armadilha de teste

A tela de boas-vindas do lojista abre sozinha por cima do painel e **intercepta
cliques**: toda suíte de verificação precisa fechá-la antes.

## Ligações

[[A8 - Conteudo e Social]] · [[A1 - Produto e Paineis]] ·
[[A5 - Programa de Parceiros]] · [[ARQ - Aula P11 dos niveis do parceiro]] ·
[[P28 - Videoaulas do Modo Live]] · [[R - Voz oficial das videoaulas]] ·
[[R - Marcas de versao no ar]]
