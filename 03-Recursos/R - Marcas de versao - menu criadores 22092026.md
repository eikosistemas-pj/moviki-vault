---
type: recurso
status: referencia
area: "[[A5 - Programa de Parceiros]]"
tags: [marcas-de-versao, upload, criadores]
atualizado: 2026-09-23
---

# R - Marcas de versao - menu criadores 22092026

Apêndice de [[R - Marcas de versao no ar]]. Entregue em 22/09/2026 — **subiu** (conferido no GitHub em 22 e 23/09). As marcas atuais estão em [[R - Marcas de versao - area do criador 22092026]].

| Repo | Arquivo | Ação | Marca |
|---|---|---|---|
| moviki-app | `eikoadm01.html` | SUBSTITUI | `2026-09-22-criadores` (era `2026-09-19-cotalive`) |
| moviki-app | `firebase/firestore.rules` | SUBSTITUI | **v27** (publicar no console) |
| moviki-app | `firebase/storage.rules` | SUBSTITUI | + `criadores/{uid}/` (publicar no console) |
| moviki-app | `firebase/testes/regras.test.js` | SUBSTITUI | + 13 casos de `criador_pecas` |
| moviki | `api/criadores.js` | NOVO | `2026-09-22-criadores1` |
| moviki | `lib/gauth.js` | SUBSTITUI | `2026-09-22-gauth2` (era `2026-09-04-gauth1`) |
| moviki-assistente-social | `src/estado.py` | SUBSTITUI | histórico de 2.000 posts |
| moviki-assistente-social | `conteudo/CRIADORES-CONTRATO.md` | SUBSTITUI | modelo definido |
| os seis | `CLAUDE.md` | SUBSTITUI | cópia idêntica |

## Ordem de subida

1. Regras v27 e Storage no console.
2. `moviki` (endpoint + gauth).
3. `moviki-app` (painel).
4. `moviki-assistente-social`.

Qualquer ordem funciona sem quebrar o que está no ar. Mas o painel só lê a fila depois da regra v27, e só mostra as visitas depois do endpoint.

## Ligações

[[ARQ - Menu Criadores no painel do dono]] · [[R - Marcas de versao no ar]]
