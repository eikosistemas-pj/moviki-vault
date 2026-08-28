---
type: moc
tags: [moviki, home]
atualizado: 2026-08-28
---

# MOVIKI — Home

> SaaS de localização em tempo real para negócios itinerantes. Single-vendor, assinatura recorrente, programa de parceiros até o 3º nível.
> Empresa: EIKO SISTEMAS DESENVOLVIMENTO DE SOFTWARE LTDA · CNPJ 68.289.841/0001-02 · Curitiba/PR.

## Estado em uma linha
Produto pronto, medido de ponta a ponta e **em conformidade**. **O gargalo é aquisição — e agora é o único.** → [[P01 - Aquisicao - campanha de trafego pago]]

## Bloqueio crítico
- 🔴 [[P01 - Aquisicao - campanha de trafego pago]] — prazo **2026-09-04**. Nada de produto bloqueia; falta trazer gente.

## Fechado em 28/08
- ✅ **LGPD do Vik** — `privacidade.html` declara a `vik_memoria` (seção 5). → [[ARQ - LGPD do Vik na politica de privacidade]]

## O que ainda segura o Vik em escala
Não é mais conformidade, é **calibragem**. O padrão global está DESLIGADO de propósito: ele multiplica qualquer erro de extração de memória por todas as conversas de uma vez. → [[P05 - Calibrar o Vik]]

## PARA
- 🎯 [[_Indice de Projetos]] — esforço com fim e data.
- 🔁 [[_Indice de Areas]] — responsabilidade contínua, sem data de fim.
- 📚 [[_Indice de Recursos]] — referência reutilizável (não exige ação).
- 📦 [[_Indice do Arquivo]] — concluído ou inativo.

## Áreas
[[A1 - Produto e Paineis]] · [[A2 - Infraestrutura e Deploy]] · [[A3 - Dados e Regras]] · [[A4 - Financeiro]] · [[A5 - Programa de Parceiros]] · [[A6 - Medicao e Analytics]] · [[A7 - Aquisicao e Midia Paga]] · [[A8 - Conteudo e Social]] · [[A9 - IA e Atendimento Vik]] · [[A10 - Conformidade e LGPD]] · [[A11 - Marca e Design System]]

## Referência de uso diário
[[R - Regras de ouro]] · [[R - Stack e repositorios]] · [[R - Colecoes do Firestore]] · [[R - Marcas de versao no ar]] · [[R - Links e identificadores]] · [[R - Checklist conformidade Meta e Google]] · [[R - Checklist de deploy]]

## Projetos ativos (dataview)
```dataview
TABLE status, prioridade, area, prazo
FROM "01-Projetos"
WHERE status != "concluido"
SORT prioridade ASC
```

## Sem plugin Dataview
A lista manual está em [[_Indice de Projetos]].
