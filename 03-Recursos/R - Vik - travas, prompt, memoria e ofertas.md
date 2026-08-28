---
type: recurso
status: referencia
area: A9 — IA e Atendimento (Vik)
tags: [ia]
atualizado: 2026-08-28
---

# R — Vik: travas, contexto, prompt, memória e ofertas

`moviki-ai/api/chat.js`. **Nunca no `moviki-robo`.**

## O fluxo
1. Confere o `idToken` (o `uid` vem **sempre** do token verificado, nunca do corpo)
2. Lê `conversas/{uid}` e exige `botLigado === true`
3. Lê as últimas 16 mensagens (`orderBy desc` + `limit`, **depois inverte** — com `asc` pegaria as PRIMEIRAS e responderia o passado)
4. Aplica as travas
5. Monta o contexto real da conta
6. Chama o Claude e grava a resposta como **`de: 'bot'`**
7. Atualiza os carimbos, **tudo em UM lote** (sem lote, uma falha no meio deixaria a mensagem sem `botRespondeuAte` e a próxima chamada responderia de novo)

## As cinco travas
| Trava | O que faz |
| --- | --- |
| `botLigado` | por conversa, **nasce desligada**; quem liga é o dono |
| Handoff | admin falou nos últimos **30 min** → o robô cala |
| Idempotência | `botRespondeuAte` guarda o id da última mensagem respondida |
| Teto de uso | `botDia` + `botUsos`, padrão **40 respostas/conta/dia** (`CHAT_LIMITE_DIA`) |
| CORS | lista fixa de origens (`CHAT_ORIGENS`), **nunca `*`** |

## O que o Vik sabe (`lib/contextoUsuario.js`)
Só leitura, nunca escreve em coleção financeira.
`negocios/{uid}` (nome, slug, status, segmento + **estado do cadastro**: localização definida? WhatsApp? horário? endereço? quantos itens de cardápio, promoções, eventos, fotos) · `assinaturas/{uid}` · `parceiros/{uid}` · `comissoes` **sempre agregada em quatro números** (disponível, retido, recebido, próxima liberação) · último `saques` · `metricas/{uid}/dias` em **UMA** consulta ordenada pelo id · `resumo/avaliacoes` · `pontos`.

**A trava de plano do painel foi COPIADA para dentro do robô.** Básico recebe só as visitas de 7 dias.

## O prompt (`lib/promptPainel.js`)
- Trava principal: **só afirma número, data, valor ou status que esteja no bloco de dados.**
- Corrigido na rodada 8: **encaminhar uma dúvida que ele sabia responder é tão ruim quanto inventar resposta.** Dado parcial se entrega como parcial.
- Vão para o time sem tentativa de resolver: cobrança, reembolso, cancelamento, saque que não caiu, comissão contestada, desconto, fraude, documento, questão fiscal, bug de sistema, pedido explícito de humano.
- Carrega o **painel inteiro descrito seção por seção**. Inclui os erros clássicos: *"sumi do mapa"* = localização não definida; *"cliente não me chama"* = WhatsApp em branco.
- **O bloco de dados entra DEPOIS das instruções**, marcado como dado e não comando.

## Memória (`vik_memoria/{uid}`)
Extraída na **mesma** chamada em que responde: bloco marcado `<<<VIK ... VIK>>>` que o servidor arranca antes de gravar. *(Uma segunda chamada de IA dobraria custo e latência.)*

`limparResposta()` corta a partir do marcador de abertura **mesmo com o bloco malformado**. Na dúvida, corta: perder um aprendizado é barato, mostrar tripa de prompt não é.

**Duas barreiras de privacidade:** o prompt proíbe CPF, CNPJ, chave Pix, dado bancário, telefone, endereço e conteúdo de anexo — e o `memoria.js` **filtra de novo por regex** (termos proibidos e qualquer sequência de 8+ dígitos).

Guarda: `fatos[]` (teto 10) · `temas[]` (12) · `objecoes[]` (6) · `recusadas[]` · `aceitas[]` · `conversas`. Item novo entra no fim; ao estourar sai o mais antigo.

**O lojista NÃO lê a própria memória** — leria junto as objeções comerciais anotadas sobre ele. É nota interna de atendimento.

## Ofertas (`lib/oportunidade.js`)
Função **pura**, sem banco e sem IA. Devolve **no máximo uma** oportunidade, ou nenhuma.

| # | Gatilho | Proposta |
| --- | --- | --- |
| 1 | sem lat/lng | definir localização — sem ela o negócio **não existe** no mapa |
| 2 | sem WhatsApp | cadastrar o número |
| 3 | plano pago + cardápio vazio | montar o primeiro item |
| 4 | parceiro aprovado, 0 comissões | o link está parado |
| 5 | parceiro sem chave Pix | sem ela o pagamento não sai |
| 6 | Básico com **20+** visitas em 7 dias | Pró |
| 7 | Pró com **60+** visitas em 14 dias | Premium |
| 8 | Premium com **150+** visitas em 14 dias | Enterprise (**perguntando** se atende em mais de um ponto) |
| 9 | sem horário | preencher em Informações |
| 10 | plano pago sem foto | galeria vazia |

**Os três números (20 / 60 / 150) são constantes no topo do arquivo. Mexer neles muda a agressividade comercial do Vik inteiro.**

**O que barra a oferta:** oferta recusada nunca volta · uma por conversa e só depois de resolver o que foi perguntado · nenhuma em conversa sobre cobrança, saque, comissão contestada, documento, erro de sistema ou com a pessoa irritada · nenhuma em conversa de duas linhas · sempre com o número real como motivo, nunca com promessa de ganho · se a pessoa disser não, aceita na hora.

## O que ficou de fora, de propósito
- **Não lê documento anexado** — responde que vai passar para o time.
- **Sem streaming** — "Vik está escrevendo…" é barra fixa de 1,5 s; streaming exigiria manter a função aberta.
- **Camada 3** → [[P06 - Camada 3 do Vik]]
