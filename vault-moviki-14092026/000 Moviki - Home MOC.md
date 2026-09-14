---
type: moc
tags: [moviki, home]
atualizado: 2026-09-14
---

# MOVIKI — Home

> SaaS de localização em tempo real para negócios itinerantes. Single-vendor, assinatura recorrente, programa de parceiros até o 3º nível.
> Empresa: EIKO SISTEMAS DESENVOLVIMENTO DE SOFTWARE LTDA · CNPJ 68.289.841/0001-02 · Curitiba/PR.

## Estado em uma linha
O produto virou para o **live commerce**. O Modo Live está no ar em **beta fechado** desde 12/09 e o gargalo continua sendo **aquisição**. → [[A13 - Modo Live]] · [[P01 - Aquisicao - campanha de trafego pago]]

## Bloqueios críticos
- 🔴 [[P29 - Teto de 10 subcontas no Asaas]] — segura o lançamento aberto do Modo Live. Enquanto não cair, o módulo inteiro fica escondido pelo interruptor do beta.
- 🔴 [[P25 - Pagina de venda da live]] — é ela que destrava tornar o filme hero público.
- 🔴 [[P01 - Aquisicao - campanha de trafego pago]] — cadastro real vindo de anúncio ainda é **zero**. Ver [[ARQ - O funil real do trafego pago]].
- 🔴 [[ARQ - Furos nas regras v16]] — o `create` anônimo de `resumo/avaliacoes` deixa qualquer pessoa criar nota 5,0 com 100 mil avaliações em qualquer negócio que ainda não tenha resumo. Brecha **aberta**.
- 🟡 [[ARQ - Faxina de notas orfas do vault]] — 3 arquivos antigos a apagar à mão no repositório do vault.

## PARA
- 🎯 [[_Indice de Projetos]] — esforço com fim e data.
- 🔁 [[_Indice de Areas]] — responsabilidade contínua, sem data de fim.
- 📚 [[_Indice de Recursos]] — referência reutilizável (não exige ação).
- 📦 [[_Indice do Arquivo]] — concluído ou inativo.

## Áreas
[[A1 - Produto e Paineis]] · [[A2 - Infraestrutura e Deploy]] · [[A3 - Dados e Regras]] · [[A4 - Financeiro]] · [[A5 - Programa de Parceiros]] · [[A6 - Medicao e Analytics]] · [[A7 - Aquisicao e Midia Paga]] · [[A8 - Conteudo e Social]] · [[A9 - IA e Atendimento Vik]] · [[A10 - Conformidade e LGPD]] · [[A11 - Marca e Design System]] · [[A13 - Modo Live]] · [[A14 - Material de apoio do parceiro]]

## Referência de uso diário
[[R - Regras de ouro]] · [[R - Regras de ouro novas de 11 a 14092026]] · [[R - Stack e repositorios]] · [[R - Colecoes do Firestore]] · [[R - Marcas de versao no ar]] · [[R - Links e identificadores]] · [[R - Checklist conformidade Meta e Google]] · [[R - Checklist de deploy]] · [[R - Retomada live parte 02]]

## Projetos ativos (dataview)
```dataview
TABLE status, prioridade, area, prazo
FROM "01-Projetos"
WHERE status != "concluido"
SORT prioridade ASC
```

## Sem plugin Dataview
A lista manual está em [[_Indice de Projetos]].
