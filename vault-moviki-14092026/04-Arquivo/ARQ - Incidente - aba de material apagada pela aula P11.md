---
type: incidente
status: concluido
area: A14 - Material de apoio do parceiro
tags: [incidente, parceiro, material-de-apoio, deploy, marca-de-versao]
atualizado: 2026-09-11
---

# ARQ — Incidente: aba de material apagada pela aula P11

## O que aconteceu

Em **11/09/2026, às 14h14**, a entrega da **aula P11** foi montada sobre a marca
**`2026-09-10-icones-nivel`** do `parceiro.html` — uma marca **anterior** à do
material de apoio. Ao subir, o arquivo levou embora:

- a **aba Material de apoio** inteira;
- os **botões de postar** (Instagram, Facebook e WhatsApp).

## O que NÃO foi perdido

A pasta **`material/` nunca foi tocada** — arquivos, capas e `catalogo.json`
continuaram no lugar. O que sumiu foi **só o HTML que lê essa pasta**. Nenhum
material precisou ser regerado.

## Causa

O `parceiro.html` é **disputado por várias conversas ao mesmo tempo** (aulas,
níveis, material de apoio, ícones). Cada conversa entrega o arquivo inteiro. Uma
entrega montada sobre uma cópia velha apaga, sem erro nenhum, tudo que entrou
depois daquela cópia.

## Conserto

Merge de **três pontas** em um só arquivo — a base dos ícones/níveis, a aba de
material com os botões de postar e a aula P11 — entregue com a marca
**`2026-09-11-material-aulaniveis`**.

| Marca | Papel |
| --- | --- |
| `2026-09-10-icones-nivel` | Base sobre a qual a P11 foi montada por engano |
| `2026-09-11-postar` | Aba de material + botões de postar (apagados no incidente) |
| `2026-09-11-material-aulaniveis` | Merge das três pontas — versão correta |

## Lição

- **Entrega se monta sobre a marca que está no GitHub**, não sobre a última cópia
  que a conversa tem em mãos.
- **Reconferir a marca na hora de subir.** Entre montar e subir, outra conversa
  pode ter entregue.
- Arquivo compartilhado por várias frentes precisa de marca de versão visível —
  é ela que denuncia a divergência antes do estrago.

## Em aberto

- [ ] Conferir, a cada entrega que encoste no `parceiro.html`, se a aba de
      material e os botões de postar continuam presentes.

## Ligações

[[A14 - Material de apoio do parceiro]] ·
[[ARQ - Aba Material de apoio do parceiro]] ·
[[ARQ - Botoes de postar no material de apoio]] ·
[[ARQ - Aula P11 dos niveis do parceiro]] ·
[[A2 - Infraestrutura e Deploy]] · [[R - Marcas de versao no ar]] ·
[[R - Checklist de deploy]]
