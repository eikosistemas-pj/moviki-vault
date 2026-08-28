---
type: guia
tags: [meta, para]
atualizado: 2026-08-28
---

# Como usar este vault

## O teste PARA (aplique a cada nota nova)
1. Tem data de fim e um resultado definido? → **01-Projetos**
2. É um padrão que preciso manter para sempre? → **02-Areas**
3. É referência que consulto, sem exigir ação? → **03-Recursos**
4. Acabou ou parou? → **04-Arquivo**
5. Não sei? → **00-Inbox** (esvaziar 1x por semana)

## Regra de fluxo
- Projeto concluído **não é apagado**: move para `04-Arquivo` e vira registro de decisão.
- Toda nota de Arquivo mantém o link para a Área que a originou.
- Área nunca tem checkbox de conclusão. Se tiver, é projeto disfarçado.

## Convenções deste vault
- Frontmatter obrigatório: `type`, `status`, `area`, `tags`, `atualizado`.
- `type`: `projeto | area | recurso | arquivo | decisao | incidente | moc | guia`.
- `status`: `ativo | pausado | bloqueado | concluido | referencia`.
- `prioridade`: `1` (crítico) · `2` (alto) · `3` (normal).
- Datas em `AAAA-MM-DD`.
- **Nome de arquivo só com ASCII** — sem travessão, acento ou til. O conteúdo pode ter acento; o nome, não. Ver [[R - Regras de ouro]].

## Tags de corte transversal
`#dinheiro` `#regra-firestore` `#deploy` `#conformidade` `#medicao` `#ia` `#aquisicao` `#lgpd` `#armadilha`

`#armadilha` marca tudo que já custou tempo e vai voltar a acontecer. Busque por ela antes de caçar bug.

## Sync
O vault é um repositório git. Ver [[R - Sync do vault Obsidian Git]].

## Plugins recomendados
- **Dataview** — as tabelas automáticas deste vault dependem dele.
- **Templater** — usa `_Templates/`.
- **Periodic Notes** — diário de rodadas.
- **Git** — versionar o vault (**obrigatório neste setup**).

## Relação com o Mapa Mestre
`MAPA-MESTRE.md` continua sendo o documento canônico de retomada de chat.
Este vault é a **navegação humana** do mesmo conteúdo, fatiado por ação.
Quando os dois divergirem, **o Mapa Mestre é a verdade** — e o Console do Firebase é a verdade acima dele para regras.
