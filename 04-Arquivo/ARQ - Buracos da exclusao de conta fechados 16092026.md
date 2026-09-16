---
type: arquivo
status: concluido
area: A2 - Infraestrutura e Deploy
tags: [exclusao, lgpd, comissao, asaas, saque, seguranca]
atualizado: 2026-09-16
---

# ARQ - Buracos da exclusao de conta fechados 16092026

Fecha a pendencia 3 de [[P - Abertura da live para lojista pagante]]. No ar em
16/09/2026: `moviki-robo/api/exclusoes.js` e `moviki-app/eikoadm01.html`, ambos
marcados **`2026-09-16-exclusao2`**.

Era o que travava a limpeza das 6 contas de teste — e a limpeza e o que trava a
abertura para lojista pagante.

## Os dois buracos mapeados

| Buraco | O que acontecia | O que passou a valer |
| --- | --- | --- |
| **Assinatura viva e sem rastro** | o cancelamento no Asaas falhava, o robo anotava `assinaturaErro` e **seguia apagando** — inclusive `faturamento/{uid}`, unico lugar onde mora o `asaasSubscriptionId`. Cobranca mensal viva, conta apagada, id perdido | **falha fechada**: sem confirmacao, NADA e apagado e o endpoint devolve 409 com o id da assinatura |
| **Comissao orfa por `lojistaUid`** | a limpeza so removia comissoes por `parceiroUid`. As que o excluido GEROU ficavam na carteira do parceiro que o indicou — **sacaveis por Pix** | comissao nao paga vira `estornada: true` com `estornoMotivo: 'lojista_excluido'`; comissao **ja paga** e so marcada `lojistaExcluido: true` |

## Os tres que a varredura achou por cima

- **O Modo Live e o checkout nasceram depois do `exclusoes.js`.** Sobreviviam a
  exclusao: `live_sessoes`, `live_cota`, `live_throttle`, `live_bloqueios`,
  `checkout_publico`, **`checkout_contas`**, `recebimento`, `vik_memoria`, e os
  `pedidos`, `lives`, `denuncias` e `moderacao` daquele lojista.
  `checkout_contas` sozinho ja e incidente de LGPD.
- **Subcolecao orfa.** Apagar `negocios/{uid}` nao apaga subcolecao. O robo
  listava `avaliacoes` e `resumo` na mao — `estado` (com `estado/live`),
  `livechat` e `livepresenca` ficavam no banco para sempre. Agora usa
  `listCollections()`: apaga o que existe hoje e o que nascer amanha.
- **`parceiros_publicos/{slug}`** e `read: true` e continuava no ar com o nome
  de um parceiro que nao existe mais.

E mais um menor: se `deleteUser` falha, a conta de acesso fica de pe num app
sem dados. Agora ha plano B — `disabled: true`.

## Por que estorno e nao delete

Apagar comissao **ja paga** quebraria a conferencia com o extrato do Asaas: o
dinheiro saiu de verdade e o historico do parceiro tem que bater. Estorno tira
do sacavel e deixa rastro; delete some com a prova. O `pagar-saque.js` e o
`parceiro.html` ja ignoram `estornada`, entao nenhuma tela precisou mudar para
o saldo cair.

## A ordem que deixou de ser necessaria

O roteiro antigo de limpeza das contas de teste era: conferir comissoes por
`lojistaUid` -> zerar na mao -> cancelar no Asaas -> so entao excluir. **O robo
faz isso sozinho agora**, e na ordem certa: assinatura primeiro (e aborta se
falhar), comissoes geradas depois, deletes so no fim. Sobra conferir o resumo
que a tela devolve.

## Regras de ouro que esta rodada deixou

1. **Cancelamento externo que falha e segue em frente e falha aberta.** Dinheiro
   so se apaga depois que a cobranca comprovadamente morreu.
2. **Erro de rede no DELETE nao e prova de que nao cancelou.** Falha fechada sem
   conferencia por GET trava exclusao legitima — 404 e `deleted:true` contam
   como cancelada.
3. **Rotina de limpeza envelhece sozinha.** Colecao nova nao entra na faxina de
   quem foi escrita antes dela. Onde der, varrer por `listCollections()` em vez
   de lista na mao.
4. **Quem apaga por `parceiroUid` esquece `lojistaUid`.** A mesma linha de
   dinheiro tem dois donos.
5. **A tela mostrava o codigo do erro, nao a frase.** Falha fechada so vira
   ferramenta quando a mensagem diz o que fazer a seguir.

## Ligacoes

[[P - Abertura da live para lojista pagante]] ·
[[R - Marcas de versao no ar]] · [[R - Regras de ouro]]
