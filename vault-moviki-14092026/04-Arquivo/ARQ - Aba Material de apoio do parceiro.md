---
type: arquivo
status: concluido
area: A14 - Material de apoio do parceiro
tags: [parceiro, material-de-apoio, entrega, catalogo, qr]
atualizado: 2026-09-11
---

# ARQ — Aba Material de apoio do parceiro

Entrega da aba que dá ao parceiro artes, panfletos, vídeos e textos prontos para
divulgar, sem depender de pedir peça no chat.

## O que foi entregue

| Item | Onde | Observação |
| --- | --- | --- |
| Aba **Material de apoio** | `moviki-app/parceiro.html` | Destaque na Visão geral, item no menu lateral e item no menu Mais |
| Catálogo `catalogo.json` | `moviki-app/material/` | Estático, sem Firestore. O campo `versao` é o que acende o selo **NOVO** |
| Pastas de arquivo | `material/capas/`, `feed/`, `panfletos/`, `stories/` | Vídeo fica solto em `material/`, com a capa junto |

## Decisões

- **Catálogo estático, não Firestore.** Material é conteúdo do produto, não dado
  do parceiro: não precisa de regra, de leitura autenticada nem de cota. Trocar
  material é trocar dois arquivos no repositório.
- **Panfleto com QR é uma arte só.** O QR do parceiro
  (`/v/apelido?utm_source=panfleto&utm_medium=qr`) é desenhado por cima no
  navegador dele. Nenhuma arte por parceiro, nenhum processamento no servidor.
- **NOVO por versão do catálogo**, não por data de arquivo: material corrigido
  sem querer chamar atenção não acende o selo.
- **Não criar subpasta nova pelo GitHub web** — o upload por arrastar não
  garante a estrutura.

## Portas

Baixar e postar respeitam as mesmas portas do link do parceiro: **aprovado**,
**aulas concluídas** e **compromisso aceito**.

## Em aberto

- [ ] Panfleto em resolução de impressão (1748x2480 ou maior).
- [ ] Trocar "Atualizado há 7 dias" no panfleto e no vídeo 1.

## Ligações

[[A14 - Material de apoio do parceiro]] · [[A5 - Programa de Parceiros]] ·
[[ARQ - Botoes de postar no material de apoio]] ·
[[ARQ - Incidente - aba de material apagada pela aula P11]] ·
[[R - Marcas de versao no ar]]
