---
type: arquivo
status: concluido
data: 2026-08-27
area: A1 — Produto e Paineis
tags: [produto]
atualizado: 2026-08-28
---

# ARQ — WhatsApp por unidade (Enterprise) — NO AR 27/08/2026

O Enterprise deixa o negócio ter até 3 pontos, mas existia **um único número** — toda unidade mandava o cliente pro mesmo telefone. Agora cada ponto tem o próprio, no campo `whatsapp` de `pontos/{pid}`.

## A regra de queda
Unidade com número próprio usa o dela → sem número, cai no WhatsApp do negócio principal → sem nenhum dos dois, **o botão some**.
Deixar o campo em branco **apaga** o número da unidade, de propósito.

## Onde muda
Botão do topo da página pública (segue a unidade selecionada) · cada linha da gaveta de unidades · a página própria do ponto (`moviki.com.br/apelido-do-ponto`).

## A armadilha
**`atualizarBtnWpp()` roda em 4 lugares.** Na página do ponto os dois `onSnapshot` (negócio e ponto) chegam em **qualquer ordem** — uma chamada só não bastava.

O servidor guarda só os dígitos, **sem o 55**; aceita 10 ou 11. Validação nos dois lados. **Nenhuma regra do Firestore mudou.**

→ [[A1 - Produto e Paineis]]
