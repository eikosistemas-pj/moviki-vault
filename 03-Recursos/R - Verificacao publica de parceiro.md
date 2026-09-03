---
type: recurso
status: referencia
area: Moviki
tags: [moviki, parceiros, verificacao, firestore, qrcode]
atualizado: 2026-09-03
---

# R - Verificacao publica de parceiro

Referencia de como funciona a confirmacao publica de um parceiro do Moviki. No ar
desde 03/09/2026.

## Os tres enderecos, e que cada um faz

| Endereco | O que e | Redireciona? |
|---|---|---|
| `/p/{apelido}` | **Link de indicacao.** Carimba UTM e `ref` e joga em `comerciantes.html`. | Sim, na hora |
| `/pp/{apelido}` | **Upline.** Convida outro parceiro. | Sim, na hora |
| `/v/{apelido}` | **Verificacao.** Pagina de verdade, que o comerciante le. | **Nao** |

**O `/p/` nao foi tocado quando a `/v/` nasceu.** Ele e o link de rastreio e carimba o
UTM que alimenta o GA4. Dois links, dois trabalhos.

Rota no `vercel.json` do repo `moviki`: `{ "source": "/v/:slug", "destination": "/v.html" }`,
**antes** do curinga de slug.

## Por que existe uma colecao espelho

**A decisao de arquitetura da rodada.** A `v.html` **nao le** `parceiros/{uid}`, e
nunca vai ler: **a chave Pix mora naquele documento**, e regra do Firestore libera o
documento **inteiro ou nada** - nao existe "libera so estes campos". Abrir aquela
colecao entregaria a chave Pix de todo parceiro a qualquer visitante.

Entao o robo copia, para `parceiros_publicos/{slug}`, so o que pode ser visto por
estranho:

```
slug · nome · arroba · desde (mes/ano) · treinado · ativo · espelhoEm
```

**Dinheiro, e-mail e uid nao atravessam. O numero de seguidores tambem nao** - e dado
do parceiro, nao credencial dele, e viraria vitrine de tamanho.

Regras v20: `read: true, write: false`. So o Admin SDK grava.

## Quem escreve o espelho, e quando

`moviki-robo/lib/espelhoParceiro.js`, chamado de tres lugares:

1. **Aprovacao automatica** - dentro da varredura do cron (`?processarPendentes=1`).
2. **Aprovacao manual** - no `parceiro-aprovado.js`, **antes** do e-mail de boas-vindas
   (o e-mail ja aponta o parceiro pro proprio link; chegar nele com a pagina vazia
   seria a pior primeira impressao).
3. **`?espelho=1`** - o proprio parceiro pede, autenticado pelo idToken dele.

**Como os parceiros antigos ganham espelho, sem migracao:** o painel chama `?espelho=1`
uma vez por sessao quando um parceiro aprovado abre, e de novo quando ele conclui as
aulas (que e quando `treinado` muda). Custo exato: uma leitura e uma escrita, so
quando muda de verdade.

**Parceiro que sai vira `ativo:false`, nao e apagado.** Documento apagado daria "nao
encontrado", que o comerciante leria como erro de digitacao em vez de alerta.

## O que a pagina mostra, e a ordem

1. Foto e @ do Instagram, nome, selo verde **"Parceiro autorizado do Moviki"**
2. "Autorizado desde <mes/ano>" · "Treinamento oficial concluido" · o apelido `/p/`
3. **Bloco "O que isso quer dizer"** - aparece nos DOIS casos, inclusive quando nao
   confere. A frase que mais importa: *"Voce nao paga nada a ele. A comissao dele sai
   do Moviki, e so existe se voce assinar um plano pago - nunca do seu bolso, nunca em
   dinheiro na mao."*
4. **So entao** os botoes.

**A ordem e a regra:** pagina de verificacao que vende antes de proteger deixa de ser
verificacao e vira propaganda - e ai nao serve nem pra vender.

## Os botoes

- **"Quero me cadastrar agora"** (principal) - vai direto ao cadastro com `?ref=`.
  Quem chega pelo cracha **ja ouviu o parceiro** ao vivo; mandar para a landing e
  faze-lo repetir uma etapa cumprida.
- **"Prefiro entender melhor antes"** - `comerciantes.html`.
- **O `ref` viaja nos dois** - nao se perde comissao por nenhum lado.

## Quando nao confirma

A pagina **nao acusa ninguem**: diz que nao confirmou, lembra que pode ser apelido
digitado errado, e avisa para nao contar como confirmacao. **Se a rede cair, diz que o
problema e nosso** - jamais "nao e parceiro", que seria acusar alguem por falha nossa.

## O cracha e o QR

Cartao na secao **Divulgacao** do painel do parceiro, **atras da mesma trava das 8
aulas** - nao por simetria: o cracha afirma "treinamento concluido", e mostra-lo antes
seria imprimir uma mentira.

Gerador de QR **escrito a mao** (`mvQR()`, embutido no `parceiro.html`) porque a CSP
nao deixa carregar biblioteca de fora. Modo byte, correcao **M**, versoes 1 a 6.
Baixa como imagem 1080x1350 (formato que Instagram e WhatsApp nao cortam).

**O QR e so um endereco escrito em quadradinhos.** Nao guarda informacao. Por isso o
destino pode mudar depois sem reimprimir nada, e por isso o endereco tem que ser um
que nunca seja aposentado - `/v/` e `/p/` sao exatamente isso.

Ver [[P16 - Rodada da credibilidade]] e [[ARQ - Erros de implementacao 03092026]].
