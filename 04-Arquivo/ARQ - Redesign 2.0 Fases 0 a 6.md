---
type: arquivo
status: concluido
data: 2026-08-27
area: A1 — Produto e Paineis
tags: [produto]
atualizado: 2026-08-28
---

# ARQ — Redesign Visual 2.0 (Fases 0 a 6) — CONCLUÍDO

**Regra que governou a reescrita:** a **ARTE manda no visual**; os **SPECS mandam na copy**, na estrutura e nas regras. Nunca inventar métrica, link, depoimento ou campo que não existe no banco.

| Fase | Tela | Estado |
| --- | --- | --- |
| 0 | Design system (`movikiui.css`) | ✅ |
| 1 | Landing (`index.html`) | ✅ |
| 2a | Página pública (`404.html`) | ✅ 26/08 |
| 2b | Campos novos + regras v7 | ✅ 26/08 |
| 3 | Painel do lojista | ✅ 26/08 |
| 4 | Painel do parceiro | ✅ 26/08 |
| 5 | Painel do dono | ✅ 26/08 |
| 6 | Métricas ✅ + caixa de mensagens ✅ | ✅ COMPLETA 27/08 |

## Página pública
Deixou de ser telinha de app (largura fixa 480px, zero media queries) e virou página que rola, de largura total. Herói (capa + logo + status + nota + distância + 2 CTAs + cards de info) · faixa EMPRESA/unidades com carrossel · promoção em destaque · destaques do cardápio · mapa Leaflet · abas · barra inferior.
Sem backend: favorito por localStorage, geolocalização só se já liberada, pinos numerados, busca de unidade a partir de 6, badge "mais perto", modo `?demo=1`.

## Painel do lojista
Casca de aplicativo. Desktop ≥1120px: lateral fixa + centro + coluna de apoio, ambas sticky. Celular: cabeçalho grudado + barra inferior de 5 lugares com o (+) no meio. **Próximas ações recomendadas** calculadas do próprio documento do negócio.

## Painel do parceiro
7 seções. Gráfico de 8 meses com dado real (campo `competencia`). Enriquecer indicação custa 2 leituras → teto de 40 mais recentes. **148 verificações no Playwright, 0 falhas.**

## Painel do dono
13 seções. Métricas só leem sob comando, **com o custo escrito ao lado do botão**. Newsletter exporta CSV com BOM UTF-8 e separador `;`. Abre por e-mail na lista OU documento em `admins`, e Configurações mostra qual das duas vale. **297 verificações no Playwright, 0 falhas.**

## O que a arte pedia e NÃO entrou
"Alcance", "Como encontraram você", rosca "+18% vs semana anterior", atividades recentes, modo escuro, "Nível do parceiro/Diamante". **Número inventado é propaganda enganosa.**

→ [[A1 - Produto e Paineis]]
