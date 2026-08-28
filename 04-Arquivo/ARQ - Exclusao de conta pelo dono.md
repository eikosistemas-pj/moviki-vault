---
type: arquivo
status: concluido
data: 2026-08-27
area: A1 — Produto e Paineis
tags: [produto, lgpd]
atualizado: 2026-08-28
---

# ARQ — Exclusão de conta pelo dono — NO AR 27/08/2026

**O painel prometia e não entregava.** A seção "Exclusões de conta" só listava pedidos feitos pelo próprio lojista. Cadastro de teste, duplicata e conta abandonada **não tinham como ser apagados** — e a lista de negócios já estava com mais teste do que cliente.

**O robô nunca foi o problema:** `api/exclusoes` com `action: 'excluir'` sempre aceitou qualquer uid. Faltava lugar no painel.

## No painel
Cartão "Excluir uma conta agora". Busca por **nome, apelido, e-mail e segmento** (mesma lição do seletor de mensagens), a partir de 2 letras, teto de 20.

**A confirmação é DIGITADA — a pessoa escreve `EXCLUIR`.** Um `confirm()` está a um Enter distraído de distância, e isto não tem volta.

## O que a exclusão passou a limpar de verdade
A versão anterior deixava rastro: **o apelido continuava reservado para sempre**.

| Também apaga | Por quê |
| --- | --- |
| `slugs/{slug}` | sem isso o apelido fica travado. **Lido do documento ANTES de apagá-lo** |
| `pontos` + `ponto_slugs` | unidades Enterprise ficavam órfãs no mapa |
| `metricas/{uid}/dias` | contador de desempenho |
| `conversas/{uid}/mensagens` | **subcoleção não some com o pai** |
| `faturamento/{uid}/ga` | trava de dedup do purchase |
| `negocios/{uid}/resumo` · `avisos_cliente/{uid}` | restos |
| **Storage:** `logos/{uid}`, `produtos/{uid}/`, `documentos/{uid}/` | contra a promessa do painel e contra a LGPD |

## Duas travas novas no servidor
O dono não consegue excluir **a própria conta**, nem a de **outro admin**.

→ [[A3 - Dados e Regras]] · [[A10 - Conformidade e LGPD]]
