---
type: area
status: ativo
area: A13 - Material de apoio do parceiro
tags: [parceiro, material-de-apoio, conteudo, panfleto, qr, conar]
atualizado: 2026-09-11
---

# A13 — Material de apoio do parceiro

Responsabilidade contínua: manter a aba **Material de apoio** do painel do parceiro
abastecida com artes, panfletos, vídeos e textos prontos para divulgar.

**Dono desta área:** o chat do Claude aberto em 11/09/2026 para a aba de material
de apoio. Material novo, correção de arte e ajuste da aba vão para ele.

## Como funciona
- Aba no `moviki-app/parceiro.html` (no ar: **2026-09-11-postar**). Destaque na Visão geral, item no menu lateral e no menu Mais.
- Catálogo estático `moviki-app/material/catalogo.json`. Nada no Firestore.
- Panfleto com QR: uma arte só; o QR do parceiro (`/v/apelido?utm_source=panfleto&utm_medium=qr`) é desenhado por cima no navegador dele.
- Botões **Instagram, Facebook e WhatsApp** em cada material. Celular: lista de apps com o arquivo anexado e a legenda copiada. Computador: baixa, copia e abre a rede.
- Baixar e postar obedecem às portas do link: aprovado, aulas concluídas, compromisso aceito.

## Fluxo para material novo
1. O Paulo manda a arte ou o vídeo no chat.
2. O Claude confere a conformidade (#publi, sem promessa de ganho, sem "trial"), otimiza o arquivo (JPG 88 / MP4 até 20 MB), gera a capa WebP de 320 px e escreve a legenda.
3. Entrega um zip para a pasta que JÁ existe no GitHub + `catalogo.json` (SUBSTITUI) com o `versao` trocado — é isso que acende o NOVO para os parceiros.
4. O `parceiro.html` não muda.

## Pastas no ar
`material/` com `capas/`, `feed/`, `panfletos/`, `stories/`. Vídeo fica solto em `material/`, com a capa junto. Não criar subpasta nova pelo GitHub web.

## Regras
- Toda legenda começa com `#publi` (Guia CONAR 2026).
- Descrever o que a ferramenta faz; nunca prometer ganho, venda, "garantido", "sem risco".
- "Teste grátis" ou "plano Básico", nunca "trial".
- Mockup de celular nas artes precisa dizer "Atualizado agora", nunca "há 7 dias".

## Pendências
- Trocar "Atualizado há 7 dias" no panfleto e no vídeo 1.
- Panfleto em resolução de impressão (1748x2480 ou maior).
- Produzir mais peças tomando as 11 artes do Paulo como referência.

## Ligações
[[A5 - Programa de Parceiros]] · [[A8 - Conteudo e Social]] · [[A10 - Conformidade e LGPD]] · [[ARQ - Aba Material de apoio do parceiro]] · [[R - Marcas de versao no ar]]
