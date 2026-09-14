---
type: incidente
status: ativo
area: A4 - Financeiro
tags: [asaas, webhook, moviki-robo, vercel, 401, producao, incidente]
atualizado: 2026-09-14
---

# ARQ - Incidente - webhook do Asaas 401 em produção

## Sintoma

11/09/2026, painel de **produção** do Asaas (asaas.com). O webhook "Moviki Robo"
-> `https://moviki-robo.vercel.app/api/webhook` devolveu **401 Unauthorized**
desde 10:48, com retentativas até 13:48 e **Penalização aplicada**. Evento visto:
`PAYMENT_DELETED` do pagamento `pay_ilwt3fvueu98ydri`, assinatura
`sub_exw3bw1ega1kmkx7`, criada em 07/09. A fila pausa sozinha na 15ª tentativa.

## Causa

Configuração, não código. Conferido no repositório: o trecho do token no
`api/webhook.js` era o mesmo desde antes de 10/09 (o upload de 10/09 01:53 só
mexeu nos níveis do parceiro). O token do cadastro de produção no Asaas não batia
com `ASAAS_WEBHOOK_TOKEN` da Vercel.

Origem provável: a pendência "Para ir a produção" do incidente de 04/09 (Sandbox)
— o cadastro de produção nunca recebeu o token sincronizado, e este foi o
primeiro evento de cobrança de produção a chegar. O `PAYMENT_DELETED` das 10:48
bate com exclusão de conta pelo painel do dono (o `exclusoes.js` cancela a
assinatura no Asaas, que dispara o evento).

## Gravidade

Crítica. Com a fila pausada, `PAYMENT_RECEIVED` não chega: lojista que pagar fica
em Básico e a comissão do parceiro não é creditada. O webhook "Transferências"
usa token próprio (`ASAAS_WEBHOOK_TOKEN_TRANSFER`) e não é afetado.

## Conserto

1. Gerar token novo: 48 caracteres, só letras e números.
2. Vercel `moviki-robo` -> Settings -> Environment Variables ->
   `ASAAS_WEBHOOK_TOKEN` -> Edit -> colar, sem espaço nem Enter no fim -> Save.
3. Deployments -> último -> Redeploy, sem cache de build. Esperar Ready.
4. Asaas produção -> Integrações -> Webhooks -> "Moviki Robo" -> Editar ->
   mesmo valor em "Token de autenticação" -> fila de sincronização ATIVA -> Salvar.
5. Logs de Webhooks, eventos em 401:
   - cliente `cus_000149223165` é a conta de teste excluída no dia -> **Remover da
     fila** (reenviar recriaria `assinaturas/{uid}` órfão de conta apagada);
   - cliente real -> **Reenviar**, esperar 200.
6. Prova: criar cobrança avulsa qualquer e excluí-la -> o log novo tem que
   mostrar **200**.

Não mexer no webhook "Transferências". O cadastro do Sandbox passa a dar 401 —
irrelevante com o robô em produção.

## O precedente de 04/09 (Sandbox, resolvido)

Mesmo sintoma, mesmo motivo: `PAYMENT_OVERDUE` em 401 nas 5 tentativas, fila
penalizada. O `api/webhook.js` compara o header `asaas-access-token` com a env
por `timingSafeEqual`; espaço ou quebra de linha invisível já reprova pelo
comprimento. Consertado com token novo de 48 caracteres nos 3 ambientes,
Redeploy sem cache, mesmo valor no painel do Asaas, fila reativada e os 5 eventos
reenviados até 200.

## Em aberto

- [ ] Confirmar no log de produção do Asaas que o evento de prova voltou 200
- [ ] Conferir no ar as melhorias que viajaram no `api/webhook.js` do pacote Modo
      Live (subiu em 12/09): alerta no Telegram antes de devolver 401 com trava de
      1 aviso por hora, `trim()` no token e na env, e `PAYMENT_DELETED` ignorado
      quando `assinaturas/{uid}` não existe

## Regras de ouro que nasceram aqui

- Todo webhook do Asaas tem cadastro separado por ambiente. Virar para produção
  exige sincronizar o token no cadastro de produção no mesmo dia.
- Segredo só nas Environment Variables da Vercel e no campo do painel do Asaas;
  nunca no código ou no GitHub.
- Alterar env na Vercel exige Redeploy.
- Trocar token é operação de dois lados na mesma janela (Vercel + Asaas); um lado
  sozinho penaliza a fila.

## Ligações

[[A4 - Financeiro]] · [[R - Regras de ouro]] · [[R - Variaveis de ambiente]] ·
[[R - Live - Checkout Pix e subcontas Asaas]] · [[A2 - Infraestrutura e Deploy]]
