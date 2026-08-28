---
type: area
status: ativo
tags: [parceiros, conformidade, dinheiro]
atualizado: 2026-08-28
---

# A5 — Programa de Parceiros

## Padrão a manter
**Nunca prometer ganho, renda ou retorno.** Fala-se em **comissão**, sempre condicionada a assinatura efetivamente paga.
**Descreva a REGRA, nunca o RESULTADO.**

## Estado das fases
| Fase | O que é | Estado |
| --- | --- | --- |
| F0 | Migração | ✅ |
| F1 | Rastreio (`/p/` grava `indicacoes/{lojistaUid}`, imutável) | ✅ |
| F2 | Cadastro + aprovação automática (Actions a cada 5 min) | ✅ |
| F3 | Painel do parceiro | ✅ |
| F4 | Motor de comissão | ✅ |
| F5/F6 | Virou o atendente de dentro do sistema | → [[A9 - IA e Atendimento Vik]] |

## Rastreio
- `/p/{apelido}` → `comerciantes.html` com UTM
- `/pp/{apelido}` → `app.moviki.com.br/seja-parceiro.html` com UTM
- **Os redirecionadores não carregam GA de propósito** (o `location.replace()` sai antes do gtag assíncrono). Eles **carimbam UTM no destino**, e o destino mede.
- Limitação honesta do `pp.html`: manda para outro domínio sem o `_gl` do linker → a sessão recomeça lá; a atribuição vem pelo UTM.

## Regra de acúmulo
**Só pagante opera como parceiro-lojista** — em camadas no `index.html` + `webhook.js`. Não se aplica a parceiro puro.

## Projetos vinculados
[[P04 - Decisao fiscal do Programa de Parceiros]]

## Recursos
[[R - Checklist conformidade Meta e Google]] · [[ARQ - Conformidade Meta e Google nas landings]]
