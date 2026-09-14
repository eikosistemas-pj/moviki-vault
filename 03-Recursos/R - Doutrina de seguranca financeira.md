---
type: recurso
status: ativo
area: "[[A13 - Modo Live]]"
tags: [seguranca, dinheiro, checkout, pix, regra-de-ouro]
atualizado: 2026-09-14
---

# Doutrina de Seguranca Financeira do Moviki

Regra permanente declarada por Paulo em 14/09/2026, quando o produto passou a
mexer com dinheiro de terceiro. Vale para TODA entrega daqui em diante — live,
cardapio, painel, robo, regra do Firestore e pagina publica. Entrega que
contraria um artigo desta doutrina nao sobe.

Relacionado: [[R - Regras de ouro]] · [[R - Live - Relatorio de seguranca]] ·
[[P31 - Financeiro e cardapio compravel]] · [[ARQ - Auditoria de seguranca do dinheiro 14092026]]

---

## Artigo 1 — O Moviki nunca custodia dinheiro de venda

O dinheiro da venda vai do comprador para o lojista. Nunca passa por conta da
EIKO, nunca fica retido, nunca e repassado por nos.

Consequencia juridica: o Moviki nao e instituicao de pagamento e nao pode
parecer uma. Nenhuma tela, texto, anuncio ou videoaula pode dizer "o Moviki
recebe", "o Moviki repassa", "seu dinheiro fica no Moviki" ou equivalente.

A unica excecao futura e a tarifa por pedido, que so pode existir como split
declarado, com aviso de 30 dias, e ainda assim sem retencao.

## Artigo 2 — Barreira que nao roda no servidor nao e barreira

Tela, botao escondido, campo desabilitado e validacao em JavaScript sao
conforto visual. A decisao que envolve dinheiro, acesso ou status e tomada no
robo ou na regra do Firestore, e nunca em outro lugar.

Teste para cada limite novo: se a pessoa abrir o F12 e chamar o endpoint na
mao, o limite continua valendo? Se a resposta for nao, o limite nao existe.

## Artigo 3 — Preco e quantidade sao recalculados no servidor, sempre

O navegador informa QUAIS itens e QUANTOS. Nunca quanto custa.

O servidor le o preco no catalogo do proprio lojista, recalcula o total,
aplica o piso do pedido e so entao emite a cobranca. Valor que chega do
cliente e descartado sem excecao — inclusive no "confere se bate", que e
convite a divergencia.

## Artigo 4 — Integridade do que o comprador ve na hora de pagar

Este artigo nasceu do golpe documentado em setembro de 2026: codigo malicioso
injetado em lojas virtuais trocava o QR Code do Pix (e o copia-e-cola) por um
do criminoso, sem o comprador perceber. A loja continuava funcionando.

Regras que impedem esse ataque no Moviki:

1. O QR e o copia-e-cola sao gerados NO SERVIDOR e entregues prontos. O
   navegador nunca monta payload de Pix, nunca concatena chave, nunca calcula
   CRC.
2. A tela de pagamento tem CSP propria e fechada: sem script de terceiro, sem
   CDN, sem tag de analytics injetada depois. Todo script e do proprio dominio.
3. Nenhuma extensao de catalogo, tema ou plugin de terceiro roda na tela de
   pagamento. Ponto.
4. A tela mostra SEMPRE, em texto legivel, o nome e o CPF/CNPJ mascarado de
   quem vai receber, com a instrucao de conferir no aplicativo do banco antes
   de confirmar. Essa e a unica defesa que sobrevive a um comprometimento de
   front-end.
5. A chave Pix do lojista, depois de cadastrada, so muda com reautenticacao e
   gera aviso por e-mail e no painel. Troca silenciosa de chave e o vetor mais
   barato de desvio.
6. O hash da tela de pagamento entra na marca de versao. Mudanca nao anunciada
   nesse arquivo e incidente ate prova em contrario.

## Artigo 5 — Segredo de terceiro e material radioativo

Chave de API do Asaas do lojista, token e credencial de qualquer terceiro:

- Cifrados em repouso (AES-256-GCM), com a frase em variavel de ambiente.
- Falha fechada: sem a variavel, o modulo nao funciona — nunca degrada para
  texto puro.
- Guardados em colecao SEM match nas regras do Firestore. Nem o dono da conta
  le pelo app; so o Admin SDK.
- Nunca voltam para a tela, nem mascarados com os ultimos digitos reais.
- Tela mostra apenas "conectada" ou "nao conectada", com data e teste de
  validade.
- O aceite do lojista diz, em portugues simples, o que o Moviki pode fazer com
  aquela chave.

## Artigo 6 — Idempotencia e a entrega "pelo menos uma vez"

O Asaas entrega webhook em modelo at-least-once: o mesmo evento chega de novo,
e isso e normal, nao e ataque. Toda gravacao de dinheiro usa chave
deterministica e criacao que falha se ja existe — nunca gravacao cega.

Padrao adotado: id do documento derivado do id do pagamento (`{payId}_nN`,
`pedido:{id}`), gravado com create, nao com set.

Duas obrigacoes que vem junto:

- O endpoint responde HTTP 200 depois de PERSISTIR o evento, e so entao
  processa a regra de negocio. Qualquer status diferente de 200 conta como
  falha para o Asaas.
- Apos 15 falhas consecutivas a fila do Asaas PAUSA e para de entregar. Eventos
  ficam guardados 14 dias e depois somem. Uma fila pausada silenciosa significa
  plano nao ligado, comissao nao creditada e pedido nao confirmado. Por isso a
  fila entra no monitoramento diario, nao na esperanca.

## Artigo 7 — Toda porta tem dono, origem, autenticacao e freio

Para cada endpoint que toca dinheiro:

- **Dono**: quem pode chamar (visitante anonimo, lojista logado, dono).
- **Origem**: CORS restrito a lista fechada de dominios. Nunca `*`.
- **Autenticacao**: idToken verificado no servidor para acao de lojista; token
  em tempo constante para webhook; nada disso para leitura publica.
- **Freio**: limite por IP, por conta e por negocio, com resposta 429. Freio
  por IP sozinho nao segura ataque distribuido — e o piso, nao o teto.

## Artigo 8 — O comprador anonimo escreve o minimo possivel

Pedido nasce por escrita de visitante nao autenticado. Isso e superficie nova
no Firestore e exige:

- `hasOnly` fechado na criacao, com todos os campos de dinheiro e status
  proibidos na entrada.
- Status do pedido so muda pelo Admin SDK ou pelo lojista dono, nunca pelo
  comprador.
- Teto de pedidos abertos por sessao e por negocio.
- Dado pessoal do comprador reduzido ao necessario para a entrega, com
  consentimento versionado e expurgo automatico do pedido abandonado.

## Artigo 9 — Nenhuma mudanca de dinheiro sem rastro

Toda alteracao de saldo, status de pedido, comissao, saque ou chave de
recebimento grava registro com quem, quando, de onde (IP e user agent) e o
valor antes e depois. O registro e somente-escrita para o app: ninguem edita
nem apaga pela interface.

Sem trilha, a apuracao de fraude vira a palavra de um contra a do outro.

## Artigo 10 — Interruptor de emergencia

Existe, e testado, um jeito de desligar em segundos, sem deploy:

- o checkout de UM negocio (lojista suspeito ou invadido);
- o checkout INTEIRO da plataforma;
- a live inteira.

Os interruptores moram em `configuracoes/` e valem no servidor, nao so na
tela. Deploy no meio de um incidente e o pior momento para descobrir um erro
de sintaxe.

## Artigo 11 — A conta do dono e o alvo mais valioso

O painel do dono aprova parceiro, paga saque e ve tudo. Comprometer essa conta
e pior do que comprometer qualquer lojista. Exigencias: segundo fator na conta
do dono, sessao curta, reautenticacao antes de pagar saque e alerta por e-mail
em login de dispositivo novo.

## Artigo 12 — Defesa em profundidade, nao muralha unica

Nenhuma camada e tratada como suficiente:

WAF e limite de taxa na borda · App Check · regra do Firestore · verificacao no
endpoint · idempotencia na gravacao · trilha de auditoria · monitoramento ·
interruptor.

Cada uma supoe que a anterior falhou.

## Artigo 13 — O que nunca pode existir

- Chave de API, token ou segredo em arquivo de front-end, mesmo ofuscado.
- `Access-Control-Allow-Origin: *` em endpoint que aceita POST.
- Confirmacao de pagamento originada de clique do comprador.
- Preco vindo do navegador.
- Regra do Firestore que expoe colecao de dinheiro para leitura ampla.
- Endpoint de dinheiro sem freio.
- Segredo em log, inclusive em log de erro.
- Dependencia de CDN de terceiro na tela de pagamento.
- Gate que existe so na tela.

---

## Checklist obrigatorio antes de subir qualquer arquivo que toque dinheiro

1. O valor e recalculado no servidor?
2. A gravacao e idempotente por chave deterministica?
3. O endpoint responde 200 ao webhook antes de processar?
4. CORS restrito e origem conferida?
5. Freio por IP e por conta ativo?
6. Regra do Firestore acompanha o campo novo, com hasOnly?
7. Segredo cifrado, falha fechada, invisivel ao app?
8. Trilha de auditoria gravada?
9. O interruptor de emergencia cobre esse caminho?
10. A tela de pagamento continua sem script de terceiro?
11. A marca de versao mudou?
12. O texto novo respeita Meta, Google, CONAR e CDC?
