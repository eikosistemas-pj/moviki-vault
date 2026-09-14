---
type: area
status: ativo
area: A14 - Material de apoio do parceiro
tags: [parceiro, material-de-apoio, conteudo, panfleto, qr, conar]
atualizado: 2026-09-14
---

# A14 — Material de apoio do parceiro

Responsabilidade contínua: manter a aba **Material de apoio** do painel do
parceiro abastecida com artes, panfletos, vídeos e textos prontos para divulgar.

> **Numeração:** esta área nasceu como "A13" no documento de 11/09/2026. Houve
> colisão: a **A13** ficou com o **Modo Live** (outra conversa) e o material de
> apoio passou a ser a **A14**. Qualquer referência a "A13 — Material de apoio"
> está errada e deve ser lida como A14.

**Dono desta área:** o chat do Claude aberto em 11/09/2026 para a aba de
material de apoio. Material novo, correção de arte e ajuste da aba vão para ele.

## Como funciona

| Peça | Onde vive |
| --- | --- |
| Aba Material de apoio | `moviki-app/parceiro.html` — destaque na Visão geral, item no menu lateral e no menu Mais |
| Catálogo | `moviki-app/material/catalogo.json`, estático. **Nada no Firestore** |
| Arquivos | `material/` com `capas/`, `feed/`, `panfletos/`, `stories/`. Vídeo fica solto em `material/`, com a capa junto |

- Panfleto com QR: **uma arte só**; o QR do parceiro
  (`/v/apelido?utm_source=panfleto&utm_medium=qr`) é desenhado por cima no
  navegador dele.
- Botões **Instagram, Facebook e WhatsApp** em cada material. Celular: lista de
  apps com o arquivo anexado e a legenda copiada. Computador: baixa, copia e
  abre a rede.
- Baixar e postar obedecem às portas do link: aprovado, aulas concluídas,
  compromisso aceito.
- Não criar subpasta nova pelo GitHub web.

## Fluxo para material novo

1. O Paulo manda a arte ou o vídeo no chat.
2. O Claude confere a conformidade (`#publi`, sem promessa de ganho, sem
   "trial"), otimiza o arquivo (JPG 88 / MP4 até 20 MB), gera a capa WebP de
   320 px e escreve a legenda.
3. Entrega um zip para a pasta que **já existe** no GitHub + `catalogo.json`
   (SUBSTITUI) com o `versao` trocado — é isso que acende o **NOVO** para os
   parceiros.
4. O `parceiro.html` não muda.

**Vídeo acima de 25 MB não passa pelo chat nem pelo GitHub web.** O caminho é o
anexo de Release — ver [[ARQ - Video do influencer pelo Release do GitHub]].

## Regras

- Toda legenda começa com `#publi` (Guia CONAR 2026).
- Descrever o que a ferramenta faz; nunca prometer ganho, venda, "garantido",
  "sem risco".
- "Teste grátis" ou "plano Básico", nunca "trial".
- Mockup de celular nas artes precisa dizer "Atualizado agora", nunca
  "há 7 dias".
- O `parceiro.html` é disputado por várias conversas: entrega que encoste nele
  se monta sobre a marca que está no GitHub **naquele momento**.

## Pendências

- [ ] Trocar "Atualizado há 7 dias" no panfleto e no vídeo 1.
- [ ] Panfleto em resolução de impressão (1748x2480 ou maior).
- [ ] Produzir mais peças tomando as 11 artes do Paulo como referência.

## Ligações

[[A5 - Programa de Parceiros]] · [[A8 - Conteudo e Social]] ·
[[A10 - Conformidade e LGPD]] · [[A13 - Modo Live]] ·
[[ARQ - Aba Material de apoio do parceiro]] ·
[[ARQ - Botoes de postar no material de apoio]] ·
[[ARQ - Incidente - aba de material apagada pela aula P11]] ·
[[ARQ - Video do influencer pelo Release do GitHub]] ·
[[R - Marcas de versao no ar]]
