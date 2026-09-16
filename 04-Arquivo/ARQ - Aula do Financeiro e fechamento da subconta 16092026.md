---
type: arquivo
status: concluido
area: A4 - Financeiro
tags: [financeiro, asaas, subconta, videoaulas, vik, pix]
atualizado: 2026-09-16
---

# ARQ - Aula do Financeiro e fechamento da subconta 16092026

Rodada aberta por uma pergunta do Paulo: *"a gente tem um bloco onde o cliente
sincroniza com o Asaas e não fez nada em relação a isso, né?"*

## Arquivos entregues

| Repo | Pasta | Arquivo | Ação | Marca nova | Montado sobre |
| --- | --- | --- | --- | --- | --- |
| moviki-robo | `lib/` | `checkout.js` | SUBSTITUI | `2026-09-16-subfechada` | `2026-09-15-whtoken` |
| moviki-app | `/` | `live.html` | SUBSTITUI | `2026-09-16-pixfinanceiro` | `2026-09-15-liveaulas` |
| moviki-app | `/` | `liveaulas.js` | SUBSTITUI | `2026-09-16-pixnovo` | `2026-09-15-liveaulas2` |
| moviki-app | `/` | `index.html` | SUBSTITUI | `2026-09-16-aulafinanceiro` | `2026-09-16-quizlive1` |
| moviki-ai | `lib/` | `catalogoPainel.js` | SUBSTITUI | `2026-09-16-4` | `2026-09-16-3` |

**Ordem:** robô → app → `catalogoPainel.js` por último, depois do
`parceiro.html` `2026-09-16-liveparc2`. O catálogo do Vik aponta para as marcas
novas dos dois painéis; subindo antes deles, o modo cauteloso liga.

## O que foi achado

1. **A aba Financeiro estava no ar desde 14/09 sem nenhuma aula.**
2. **A aula 07 do Modo Live ensinava o caminho errado.** Narrada com o roteiro
   de 13/09, ela mandava abrir subconta pelo estúdio — caminho adiado pela P31
   em 14/09 — e falava em piso de R$ 20, que é o do Asaas, não o do Pix direto.
3. **O catálogo do Vik também não conhecia a aba** — buraco de dois dias,
   fechado na revisão de 16/09 por outra rodada.

## Decisões

- **Aula nova do Financeiro**, `mod-financeiro`, 3:27, id `c0tHy37jv7o`,
  embutida na própria aba. O painel do lojista passa de 16 para **17 aulas**.
- **Aula 07 regravada**, id `xxulNw7JRhQ`, 1:14. O id antigo `hhTBM163vK0` sai
  do catálogo agora e **não pode voltar a catálogo nenhum**.
  O campo `em` continua `2026-09-15` de propósito: **regravação não é aula
  nova** e não pode virar alerta para quem já concluiu.
- **Subconta fechada para conta nova.** Constante `SUBCONTA_NOVA_ABERTA = false`
  no `checkout.js`, barreira no topo do `lojaCriar`, antes de qualquer
  validação e de qualquer chamada ao Asaas. Quem já tem conta continua:
  `loja_estado` e `loja_ligar` não mudaram.
- **O formulário de abertura saiu do estúdio.** A aba "Receber no Pix" passou a
  explicar que o recebimento se configura no Financeiro, com botão para lá.
  Os listeners do formulário saíram junto — não ficou campo órfão no DOM.

## A regra que fica

> **Recurso que mexe com dinheiro não sobe sem a aula dele.** A aba Financeiro
> ficou dois dias no ar sem aula e com uma videoaula ativa ensinando o caminho
> antigo. Aula errada é pior que aula faltando: a faltando gera dúvida, a
> errada gera lojista fazendo a coisa errada com confiança.

E a segunda, do mesmo dia:

> **Trava de terceiro que cancela assinatura não é risco de recurso, é risco de
> empresa.** O teto de 10 subcontas do Asaas, ao estourar, cancela as
> assinaturas existentes. Por isso a porta fechou antes de o produto abrir.

## Prova de não-regressão

`index.html` — contagens idênticas ao arquivo recebido:
`MvLiveAulas=7 · liveaulas.js=2(+1 comentário) · faixaLive=3 · liveLiberada=2 ·
mvAvisoLiveOk=3 · MOVIKI_TUTORIAIS=3 · BOASVINDAS=8`. O diff tem só a marca e o
módulo novo. BOM e CRLF preservados.

`live.html` — zero referência órfã: `pxCriar`, `pxNome`, `pxErro`, `pxEmail` e
os outros campos do formulário foram a zero junto com o HTML. `MvLiveAulas`
segue com 13 ocorrências. Carregado em Chromium: **zero erro de página**.

`node --check` limpo em `checkout.js`, `liveaulas.js`, `catalogoPainel.js` e nos
9 blocos de script do `index.html`. `avisoVersao` testado nos dois sentidos.

## Pendências que ficam

- [ ] Teste real da aba Financeiro ponta a ponta (chave Pix, ligar a venda,
      pedido, confirmar) — nunca foi feito com conta de verdade.
- [ ] A aula 08 antiga (`WmpIQr36b2o`) segue publicada e fora de catálogo.
- [ ] Apagar `hhTBM163vK0` no YouTube **só depois** de o `liveaulas.js` novo
      estar no ar.

## Ligações

[[P31 - Financeiro e cardapio compravel]] · [[P29 - Teto de 10 subcontas no Asaas]] ·
[[R - Live - Checkout Pix e subcontas Asaas]] · [[R - Live - Videoaulas do modulo]] ·
[[R - Dicionario de pronuncia da voz Malu]] · [[R - Regras de ouro]]
