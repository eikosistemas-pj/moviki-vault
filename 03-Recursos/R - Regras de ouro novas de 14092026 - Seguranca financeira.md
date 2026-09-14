---
type: recurso
status: ativo
area: "[[A13 - Modo Live]]"
tags: [regra-de-ouro, seguranca, dinheiro]
atualizado: 2026-09-14
---

# Regras de ouro novas de 14/09/2026 — seguranca financeira

Apendice de [[R - Regras de ouro]]. O texto completo e o raciocinio de cada uma
estao em [[R - Doutrina de seguranca financeira]], que passa a valer para toda
entrega que toque dinheiro.

- O Moviki nunca custodia dinheiro de venda. Nenhuma tela, texto ou anuncio
  pode sugerir que recebe ou repassa.
- Preco e quantidade sao recalculados no servidor. Valor que chega do navegador
  e descartado, nunca conferido.
- QR e copia-e-cola do Pix sao gerados no servidor. O navegador nunca monta
  payload, nunca concatena chave, nunca calcula CRC.
- A tela de pagamento nao carrega script de terceiro e mostra sempre o nome e o
  documento mascarado de quem vai receber, para o comprador conferir no banco.
- Toda gravacao de dinheiro usa id deterministico e `create()`, nunca `set()`
  cego — o Asaas entrega o mesmo evento mais de uma vez, por projeto.
- Webhook responde HTTP 200 depois de persistir o evento e antes de processar a
  regra de negocio. Apos 15 falhas seguidas a fila do Asaas pausa calada.
- Variavel de ambiente que falta derruba o modulo. Nunca rebaixa para sandbox,
  texto puro ou modo permissivo.
- Segredo de terceiro fica cifrado, em colecao sem match nas regras, e nunca
  volta para a tela — nem mascarado com digitos reais.
- Todo endpoint de dinheiro tem dono, origem conferida, autenticacao e freio.
  Freio por IP e o piso, nao o teto.
- Toda mudanca de dinheiro ou de status grava trilha com quem, quando, de onde
  e valor antes e depois.
- Existe interruptor de emergencia por negocio e global, valido no servidor, e
  ele e testado antes de precisar.
- Troca de chave de recebimento exige reautenticacao, avisa por e-mail e fica
  na trilha.
