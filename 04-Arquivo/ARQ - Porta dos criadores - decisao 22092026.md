---
type: decisao
status: concluido
area: parceiros
tags: [criadores, acesso, parceiro-html, decisao]
atualizado: 2026-09-22
---

# Porta dos criadores — decisão de 22/09/2026

## Pergunta
O influenciador que não é parceiro deveria ter um link e uma conta separados?

## Decisão
- **Link separado: sim.** `https://app.moviki.com.br/criador` — tela de entrada própria ("Área do criador"), cadastro com texto de criador e, depois do login, direto nas peças.
- **Conta separada: não.** O criador continua sendo um parceiro marcado (`parceiros/{uid}.criador == true`).

## Por quê
- O cadastro de parceiro é o que dá o link `/c/apelido` (visitas no GA4), a comissão, o aceite de conduta (prova CONAR) e o @arroba do crédito.
- As regras v27 (`criadorAtivo`) exigem `parceiros/{uid}` aprovado.
- Conta só de criador duplicaria login, regras e pagamento e cortaria a medição "vale a pena" do menu Criadores.

## Fluxo do influenciador novo
1. Recebe o link `/criador` pelo WhatsApp (botão no menu Criadores).
2. Sem conta: "Faça seu cadastro" leva ao cadastro de parceiro.
3. Dono aprova o cadastro e marca como criador.
4. Entra pelo mesmo link e cai na Área do criador. Antes de ser marcado, vê "avise o Moviki".

## Arquivos
- `moviki-app/parceiro.html` `2026-09-22-criador4`
- `moviki-app/eikoadm01.html` `2026-09-22-criadores4`
- `moviki-app/vercel.json` — rewrite `/criador`

## Ligações
- [[ARQ - Area do criador no painel do parceiro]]
- [[R - Marcas de versao - area do criador 22092026]]
