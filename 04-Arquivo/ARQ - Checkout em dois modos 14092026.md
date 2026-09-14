---
type: arquivo
status: concluido
area: "[[A13 - Modo Live]]"
tags: [financeiro, checkout, pix, cardapio, asaas, seguranca]
atualizado: 2026-09-14
---

# Checkout em dois modos — motor pronto, 14/09/2026

Primeira entrega de codigo da [[P31 - Financeiro e cardapio compravel]]. Reescreve
o coracao do checkout para os tres modos de recebimento, sob a
[[R - Doutrina de seguranca financeira]].

**Nada muda na tela ainda.** Esta rodada e so servidor: as paginas continuam
chamando o que sempre chamaram e o caminho antigo (subconta) segue funcionando
sem reconfiguracao. O painel e o cardapio compravel vem nas proximas.

## Arquivos

| Repositorio | Arquivo | Marca | Tipo |
|---|---|---|---|
| moviki-robo | `lib/pix.js` | 2026-09-14-pixdireto | NOVO |
| moviki-robo | `lib/checkout.js` | 2026-09-14-doismodos | SUBSTITUI |

## Os tres modos

- **`pix` — Pix direto (PADRAO).** Chave Pix do proprio lojista. O servidor
  monta o copia-e-cola; o dinheiro vai direto para a conta dele. Sem gateway,
  sem tarifa, sem teto de subconta. Piso do pedido: R$ 5.
- **`asaas` — conta do lojista conectada (upgrade).** Chave de API dele,
  cifrada. Confirmacao automatica por webhook. Nao cria subconta e nao consome
  o teto de 10. Piso: R$ 20 (a tarifa fixa de R$ 1,99 pesa demais abaixo disso).
- **`subconta` — legado.** Continua funcionando para quem ja tinha; deixou de
  ser o caminho oferecido.

Um modo ativo por vez. Quem ja tinha subconta ligada e aprovada antes desta
rodada cai automaticamente no modo `subconta` sem tocar em nada.

## lib/pix.js — o gerador de BR Code

Escrito do zero, sem dependencia. Monta o payload EMV (campos 00 a 62), calcula
o CRC-16/CCITT-FALSE e devolve o copia-e-cola pronto.

Validado fora do ar contra dois vetores independentes:

- CRC de `"123456789"` = `29B1` (vetor canonico do algoritmo);
- o payload de exemplo do BACEN fecha em `1D3D`.

O `6304` entra no calculo do CRC — e o erro mais comum em gerador de Pix na
internet, e produz QR que as vezes le e as vezes nao.

Reconhece as cinco formas de chave (aleatoria, e-mail, telefone, CPF, CNPJ) e
desempata os 11 digitos que servem para CPF e para celular pelo digito
verificador.

## O que este arquivo defende

- **QR montado no servidor, sempre.** O navegador recebe a string pronta.
  Montar payload de Pix no cliente e entregar o ataque de QR trocado de bandeja.
- **Nome e documento mascarado do recebedor voltam junto do payload.** A tela
  tem que mostrar os dois, com a instrucao de conferir no aplicativo do banco.
  E a unica defesa que sobrevive a um front-end comprometido.
- **A chave Pix aparece no copia-e-cola porque tem que aparecer** — ela e o
  endereco de recebimento. O que nunca sai cifrado ou cru para a tela e a chave
  de API do Asaas, e em nenhum campo de exibicao aparece a chave inteira, so a
  mascara.
- **Preco sai do cardapio do lojista, nunca do navegador.** Testado: pedido com
  `preco: 0.01` no corpo da requisicao cobra os R$ 24,90 do cardapio.

## Centavos identificadores

O Pix direto nao avisa o Moviki quando o dinheiro cai. Cada pedido recebe
centavos unicos derivados do proprio id (R$ 49,80 vira R$ 50,03), para o
lojista achar o pagamento no extrato sem caçar nome. Deterministico: a mesma
funcao chamada duas vezes para o mesmo pedido devolve o mesmo valor.

## Maquina de estados

```
aguardando ──30 min sem pagar──> expirado
    │                                │
    ├─ comprador avisa ─> conferindo │
    │         lojista confirma ──────┴──> pago ──> entregue
    │         lojista recusa ───────────> recusado
    └─ cancelado
```

Pedido **expirado ainda pode ser confirmado** pelo lojista: a janela de 30
minutos e da tela do comprador, nao do dinheiro. Pix que caiu atrasado continua
sendo Pix que caiu.

## Comprovante

Sobe em base64 pelo POST e quem grava no Storage e o Admin SDK — o comprador
nunca escreve la. O tipo e conferido pelos BYTES do arquivo, nao pelo que o
cliente declara. Nome com 16 bytes aleatorios e leitura por link assinado de 20
minutos, so para o lojista dono do pedido.

## Trilha e freios

- `financeiro_trilha` registra pedido criado, confirmado, recusado, chave Pix
  cadastrada ou trocada, modo ligado ou desligado.
- **Troca de chave Pix dispara aviso no Telegram na hora.** Chave trocada em
  silencio e o jeito mais barato de desviar o dinheiro de um lojista invadido.
- Freio por IP (ja existia) **mais freio por negocio** — 40 pedidos por hora.
  IP sozinho nao segura ataque distribuido.

## Colecoes novas

| Colecao | Conteudo |
|---|---|
| `recebimento/{uid}` | modo, chave Pix cifrada, chave Asaas cifrada. Sem match nas regras |
| `financeiro_trilha/{id}` | rastro do dinheiro, so escrita |
| `checkout_publico/{uid}` | ganhou `modo`, `minimo` e `entrega` |

Nenhuma exige regra nova do Firestore: sao todas escritas e lidas so pelo
Admin SDK.

## Testado fora do ar

43 verificacoes num Firestore de mentira, em tres roteiros: funcoes puras,
fluxo de compra ponta a ponta e ciclo do painel. Cobrem preco forjado pelo
cliente, quantidade absurda, segredo do pedido errado, pedido de outro negocio,
consentimento ausente, valor abaixo do minimo, live barrada no Premium,
recebimento desligado, interruptor do dono, expiracao e recusa.

## Falta para a Fase 1 fechar

- `api/pedido.js` e `api/recebimento.js` (agora cabem: o Pro tirou o teto de 12).
- Regras do Firestore v24 — `vendaAtiva` e `sku` no cardapio.
- Aba Financeiro no painel do lojista.
- Cardapio compravel nas paginas publicas, com o QR desenhado pelo `mvqr.js` a
  partir do copia-e-cola que o servidor mandar.
- Aulas 07R, 08R e 14, que so podem ser gravadas quando essas telas existirem.
