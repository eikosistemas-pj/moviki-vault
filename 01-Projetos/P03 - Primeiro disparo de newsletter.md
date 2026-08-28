---
type: projeto
status: ativo
prioridade: 2
area: A7 — Aquisicao e Midia Paga
tags: [aquisicao, lgpd, email]
atualizado: 2026-08-28
---

# P03 — Primeiro disparo de newsletter

## Resultado esperado
Primeiro e-mail da lista enviado, só para quem está `ativo`, com link de descadastro individual.

## O que já existe
- `descadastro.html` no ar (repo `moviki`), com confirmação em uma etapa. Ver [[ARQ - Caixa de mensagens e newsletter|ARQ — Descadastro e LGPD]].
- CSV da Newsletter no painel do dono já traz a coluna **"Link de descadastro"**, montada por pessoa.
- `privacidade.html` com a seção 10 · Comunicações por e-mail.
- **Resend já configurado com o domínio verificado** (suporte@moviki.com.br).

## Definição de pronto
- [ ] Ferramenta de disparo escolhida (Resend é o caminho pronto)
- [ ] Texto do primeiro e-mail escrito
- [ ] Link individual de descadastro em **todo** envio
- [ ] Disparo só para `ativo: true`

## Armadilha
O link é `moviki.com.br/descadastro.html?id=<docId>&e=<email>`. O `id` é quem manda; o `e` é só exibição — a página **nunca** consulta o e-mail no banco, porque a lista só pode ser lida pelo dono.

## Ligações
[[A10 - Conformidade e LGPD]] · [[R - Colecoes do Firestore]]
