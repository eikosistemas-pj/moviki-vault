---
type: projeto
status: concluido
area: Moviki
tags: [moviki, parceiros, credibilidade, instagram, qrcode, verificacao]
atualizado: 2026-09-03
prioridade: alta
prazo: 2026-09-03
---

# P16 - Rodada da credibilidade

Rodada da noite de 03/09/2026. O produto estava pronto e medido, mas **nao passava
autoridade**. Quatro buracos, todos conferidos no codigo antes de mexer.

## O diagnostico

| # | O que faltava |
|---|---|
| 1 | **Zero** mencoes ao CNPJ ou razao social nos dois paineis. O `parceiro.html` nao tinha nenhuma. |
| 2 | **Nenhuma** tela onde o lojista ve o que ja pagou. "Meu Plano" so vende. |
| 3 | **Nenhuma** forma de conferir se um parceiro e parceiro. O `/p/` era redirecionador de 20 linhas. |
| 4 | Prova de treinamento (`aulasEm`) gravada desde 02/09 e **nunca mostrada**. |

O terceiro e o maior: num programa de indicacao, que ja carrega o cheiro de piramide,
o feirante ouvir "sou do Moviki" e nao ter como checar e o que mais custa venda.

## O que entrou no ar

**1. Busca do @ do Instagram no quiz** - `moviki-robo/lib/instagram.js` + branch
`?instagram=` no `novo-parceiro.js`. API oficial da Meta (`business_discovery`),
nunca o endpoint interno que os sites de venda de seguidores usam. Freios: 700ms de
espera, 25 buscas por IP a cada 10 min, teto de 3.000/dia, cache de 7 dias. A foto
vem como `data:` URI porque a CSP nao libera o CDN da Meta e a URL assinada expira.

**2. Selo do certificado** no painel do parceiro. Ideia do Paulo, e a boa: **a
destrava e permanente, o selo e vivo**. Aula nova nao retranca o link, mas o selo
compara o que ele viu com o que esta publicado agora e vira pendencia na hora.

**3. Cracha com QR code** dentro da Divulgacao, atras da mesma trava das 8 aulas -
nao por simetria: o cracha afirma "treinamento concluido", e mostra-lo antes seria
imprimir uma mentira. Gerador de QR escrito a mao (a CSP nao deixa carregar
biblioteca de fora).

**4. Pagina publica de verificacao** `moviki.com.br/v/{apelido}` - o comerciante
abre no celular dele, na frente do parceiro.

**5. Colecao `parceiros_publicos`** e **regras v20**.

**6. Rodape institucional** nos dois paineis e **selo "atualizado hoje"** na pagina
publica do negocio.

**7. Os cinco atendentes** na caixa de mensagens (ver [[A12 - Atendimento e vozes do Moviki]]).

## As decisoes que valem mais que o codigo

**O espelho existe porque regra do Firestore libera o documento INTEIRO ou nada.**
A chave Pix mora em `parceiros/{uid}`. Abrir aquela colecao para leitura publica
entregaria a chave Pix de todo parceiro. Entao o robo copia so o que pode ser visto
para uma colecao separada. Virou regra de ouro.

**A pagina protege antes de vender.** O bloco "O que isso quer dizer" - com a frase
*"Voce nao paga nada a ele"* - vem **antes** de qualquer botao. Pagina de verificacao
que vende antes de proteger deixa de ser verificacao e vira propaganda.

**O botao principal fecha, nao apresenta.** Ideia do Paulo: quem chega pelo cracha ja
ouviu o parceiro ao vivo, minutos atras. Mandar para a landing e faze-lo repetir uma
etapa ja cumprida. Vai direto ao cadastro, levando o `?ref=`.

**Quando nao encontra, a pagina nao acusa ninguem.** E se a rede cair, diz que o
problema e nosso - jamais "nao e parceiro", que seria acusar alguem por falha nossa.

## O que NAO foi feito, e por que

- Selo "Verificado" que nao verifica nada - selo so vale quando existe quem nao tem.
- Nivel/medalha/ranking de parceiro - e a estetica exata do multinivel.
- Numero que ninguem contou - quando o lojista percebe que um numero nao bate, ele
  deixa de acreditar em todo o resto do painel.

## Ficou em aberto

- **A2** - "Meu Plano" virar extrato (esforco medio).
- **C2** - o dono responder as avaliacoes (esforco alto).

Ver [[ARQ - Erros de implementacao 03092026]] para os dois defeitos que custaram a
subida, e [[R - Regras de ouro]] para as regras novas que nasceram daqui.
