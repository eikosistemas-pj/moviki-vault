---
type: area
status: ativo
tags: [regra-firestore, dados, armadilha]
atualizado: 2026-08-28
---

# A3 — Dados e Regras (Firestore / Storage)

## Padrão a manter
**O Console é a verdade.** A cópia das regras no Project pode estar atrás do que está publicado — já aconteceu (cópia na v12 com a v13 no ar). Antes de publicar qualquer versão nova, comparar.

## Regras de ouro desta área
- Regras Firestore usam `hasOnly`. **Campo novo entra como opcional:** `!('x' in d) || …`.
- Regra com campo novo tem que ser pensada nos **três estados**: documento antigo sem o campo · documento em transição ganhando o campo · documento novo já com o campo. **O estado do meio é onde tudo quebrou em 26/08.**
- **Nunca publicar regra que EXIGE campo novo antes de o arquivo que grava esse campo estar no ar.**
- **Em `update`, `request.resource.data` é o documento INTEIRO já mesclado**, não só o que mudou. Checar um campo direto ali nega escritas legítimas que nem tocaram nele.
- **Campo novo gravado pelo Admin SDK precisa entrar no `hasOnly` que o CLIENTE atravessa.** O servidor não precisa de permissão; quem escreve depois dele, precisa. *(Foi isso que tornou a v14 obrigatória — sem ela, a caixa de mensagens travaria calada depois da primeira resposta do Vik.)*
- Quando o código escreve num documento com `hasOnly` apertado, **`setDoc` com `merge` é armadilha**. Padrão certo: `setDoc` completo na criação, `updateDoc` só com os campos permitidos depois.
- **Trocar as regras do Storage pode apagar imagem da tela.** Qualquer conjunto novo precisa manter `logos/{uid}` e `produtos/{uid}` com `read: if true`.
- **Apagar o documento não apaga a subcoleção, nem o apelido, nem o arquivo.** Exclusão que promete "os dados somem" tem que ir atrás dos quatro.
- **Ler o documento ANTES de apagá-lo** quando algo depende do que está dentro dele.
- **Nunca travar a coleta de dado — travar só a exibição.** Dado guardado hoje é argumento de venda amanhã.
- **TTL do Firestore só existe no Console do Google Cloud**, nunca no Console do Firebase.
- **O emulador de regras não roda na sandbox do Claude.** Regra se confere à mão e se valida pelo que o código MANDA (campos enviados × `hasOnly`).

## Recursos
[[R - Colecoes do Firestore]] · [[R - Historico de regras v7 a v15]] · [[ARQ - Incidentes e cacadas de bug]]
