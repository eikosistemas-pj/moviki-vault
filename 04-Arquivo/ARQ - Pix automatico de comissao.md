---
type: arquivo
status: concluido
data: 2026-08-27
area: A4 — Financeiro
tags: [dinheiro]
atualizado: 2026-08-28
---

# ARQ — Pagamento de comissão por Pix automático — NO AR 26–27/08/2026

**Testado ao vivo:** dois Pix reais (R$ 5,00 e R$ 1,00) saíram da conta Asaas e caíram na chave do parceiro, com baixa automática das comissões.

## Decisões
| Assunto | Decisão |
| --- | --- |
| Prazo mostrado ao parceiro | **Até 1 dia útil (24h)** (antes prometia 5 dias úteis) |
| Como o dono paga | 1 clique **com confirmação**: o robô consulta o titular da chave, mostra na tela, e só aí o dinheiro sai |
| Onde | Nos pedidos de saque **e** direto na linha de cada parceiro |
| Trava | **Teto de R$ 500 por pagamento** (`TETO_SAQUE_AUTOMATICO`) |
| Relatório | Tabela e CSV de comissões trazem a **chave Pix** |

O mínimo de R$ 20 vale **só** para o parceiro pedir saque.

## Infra Asaas
`POST /v3/transfers` (value, operationType PIX, pixAddressKey, pixAddressKeyType, description, **externalReference = id do saque**) · `GET /v3/pix/addressKeys/external` (5/min) · header `access_token` · **100 transferências grátis/mês**.

## Tipo da chave Pix — heurística
O parceiro digita livre e o robô descobre: `@` = e-mail · formato UUID = aleatória · 14 dígitos = CNPJ · 10 = telefone · 11 = testa CPF (validando o dígito verificador) e celular, com a consulta no Asaas desempatando. Não identificou, recusa.
*(Pendência: campo "tipo da chave" no cadastro, para dispensar a heurística.)*

## Confirmação automática (webhook de transferência)
- `TRANSFER_DONE` → quita as comissões, marca o saque como pago, guarda o comprovante, **sem ninguém clicar**.
- `TRANSFER_FAILED` / `CANCELLED` / `BLOCKED` → desfaz a baixa e marca **"Pix não saiu"**, com o motivo à vista.

Webhook separado no Asaas: **Transferências** · URL `.../api/webhook` · v3 · fila ligada · **Sequencial** · token próprio em `ASAAS_WEBHOOK_TOKEN_TRANSFER`. O `webhook.js` aceita **dois** tokens porque a Vercel não deixa mais reler env salva.

## A lição dos 10 segundos
Num teste, o Pix foi criado no Asaas mas a resposta não voltou a tempo e o painel não deu baixa. No segundo clique o Asaas recusou com *"Saque X já solicitado"* — **o `externalReference` funcionou como trava anti-duplicidade e o dinheiro não saiu duas vezes.**

Duas correções vieram daí: o `pagar-saque.js`, ao ver "já solicitado", **busca a transferência existente e segue com ela**; e o webhook fecha o saque sozinho.

## Ensaio de pagamento
Bloco no painel do dono cria uma comissão de mentira (até R$ 10, `teste: true`, já liberada) para ensaiar o Pix de ponta a ponta. Roda como `etapa: 'teste'` **dentro do próprio `pagar-saque.js`** — nenhuma função nova.

→ [[A4 - Financeiro]] · [[P04 - Decisao fiscal do Programa de Parceiros]]
