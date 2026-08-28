---
type: recurso
status: referencia
area: A3 — Dados e Regras
tags: [regra-firestore, armadilha]
atualizado: 2026-08-28
---

# R — Histórico das regras do Firestore (v7 → v15)

| Versão | Data | O que mudou |
| --- | --- | --- |
| v7 | 26/08 | Coleção `newsletter` + os 4 campos da Fase 2b no `negocioValido` |
| v8 | 26/08 | Métricas por negócio + resumo de avaliações |
| v9 | 26/08 | `expiraEm` (TTL) — **exigia** o campo na criação |
| v10 | 26/08 | `expiraEm` volta a ser **opcional** na criação |
| v11 | 26/08 | Teto de campos alterados vira 3 **só** quando o documento ainda não tem `expiraEm` |
| v12 | 26/08 | `metricas/{uid}/dias` ganhou `\|\| isAdmin()` no read — sem ela o painel do dono não soma métrica de ninguém |
| v13 | 27/08 | Coleção `conversas` + subcoleção `mensagens`. Puramente aditiva |
| **v14** | 27/08 | `conversaCampos` passou a conhecer os 4 campos do robô e o valor `'bot'` em `ultimoDe`; o create do lojista passou a proibir nascer com `botLigado: true` ou carimbos forjados. **`mensagemCampos` NÃO mudou** |
| **v15** | 27/08 | Coleção `vik_memoria`: leitura e delete só admin, escrita para ninguém. **VERSÃO PUBLICADA** |

## Por que a v14 não era opcional — a armadilha mais cara do projeto
O Vik grava pelo Admin SDK, que ignora regras. **O problema é depois.** Assim que ele responde, o documento da conversa passa a ter `ultimoDe: 'bot'` e os quatro campos `bot*`.

E `conversaCampos()` é avaliada sobre o **documento INTEIRO já mesclado** em toda escrita do lojista — ela não conhecia esses campos nem o valor `'bot'`.

**Resultado com a v13 no ar: depois da PRIMEIRA resposta do robô, aquele lojista não conseguiria mais nem marcar como lido nem mandar mensagem naquela conversa. A caixa travaria, calada, sem erro visível.**

### As duas lições
1. **Em `update`, `request.resource.data` é o documento inteiro mesclado**, não só o que mudou.
2. **Campo novo gravado pelo Admin SDK exige liberar o campo no `hasOnly` que o CLIENTE atravessa.**

## As três falhas de 26/08 foram todas da mesma família
Regra que exige um campo novo **antes** de o arquivo que grava esse campo estar no ar.

## ⚠️ A divergência de 27/08
A cópia guardada no Project estava na **v12**, sem o bloco `conversas` — três versões atrás do publicado. Publicar aquele arquivo por engano teria derrubado a caixa de mensagens inteira.
**O arquivo do Project e o Console podem divergir. Na dúvida, o Console é a verdade.**

## Cópias
Corrente: `regras firebase27082026.txt` (**v15**). Backups: `...-PUBLICADAS-v9/v10/v11/v12/v13.txt`. Storage: `claude/moviki-regras-storage-v1.txt`.
