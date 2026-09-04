---
type: projeto
status: ativo
area: A2 - Infraestrutura e Deploy
tags: [deploy, regra-firestore, armadilha, seguranca]
prioridade: 1
prazo: 2026-09-11
atualizado: 2026-09-04
---

# P14 - App Check enforcement

Ligar a chave do App Check no Console do Firebase. O App Check esta instalado
nas 8 paginas desde 03/09/2026, mas **sem imposicao**: enquanto a chave nao
vira, a escrita anonima (avaliacoes, resumo, metricas, newsletter) segue sem
limite de velocidade, protegida so pelas regras — que dizem O QUE pode ser
gravado, nao QUEM pode gravar.

## O que travava

Requisicao de servidor nao carrega token de App Check. Enforcar com um
consumidor de servidor de fora derruba aquele consumidor, **calado**.

Eram **dois**, nao um:

| Quem | O que fazia | Sintoma se o enforcement subisse antes |
| --- | --- | --- |
| `moviki/api/og.js` | lia o Firestore por REST com a chave publica | todo link de lojista compartilhado viraria **cartao cinza** — o canal de distribuicao do produto |
| `moviki-assistente-social` | lia `/negocios` por REST com a chave publica, do GitHub Actions | o robo **pararia de postar**, e o erro so apareceria dentro de um workflow que ninguem le todo dia |

O segundo nao estava registrado em lugar nenhum. Foi achado varrendo os 6
repositorios atras de **tudo** que fala com o Firebase fora de um navegador.

O `moviki-robo` e o `moviki-ai` ja usam Admin SDK e sao imunes por definicao.

## O que foi feito em 04/09/2026

**Conta de servico SOMENTE LEITURA, so no projeto Vercel do site.**
Chamada de conta de servico passa por IAM, nao pela chave publica do app: o
App Check nao se aplica a ela. Nao e gambiarra, e a via oficial.

- `moviki/lib/gauth.js` (NOVO) — assina o JWT e troca por token OAuth usando
  so o `crypto` do Node. **Sem `firebase-admin`**: o repo do site nao tem
  `package.json`, e puxar o Admin SDK so para ler 4 documentos criaria passo de
  instalacao no deploy e engordaria o cold start da unica funcao que serve
  TODA rota `/apelido`. Token guardado em memoria por ~55 min.
- `moviki/api/og.js` (SUBSTITUI) — le autenticado. **Sem a env, volta sozinho
  ao modo antigo**: da para subir o arquivo antes de a conta existir.
- `moviki/api/vitrine.js` (NOVO) — devolve em JSON os negocios que marcaram
  `autorizaDivulgacao`, com campos fechados. O robo social passa a consumir
  isto e **nunca mais fala com o Firestore**.
- `moviki-assistente-social/src/config.py` e `src/firestore.py` (SUBSTITUEM) —
  leem a vitrine.

**Por que o robo social nao ganhou a chave:** aquele repo e PUBLICO. Chave de
banco num GitHub Secret so para ler dado que ja e publico troca um problema
por outro maior. O segredo fica onde ja tem que ficar — nas variaveis da
Vercel.

**Tres ganhos de brinde:** o filtro de opt-in virou server-side (quem nao
autorizou divulgacao nao sai mais do banco), o robo deixou de paginar a base
inteira a cada rodada, e o teto de funcoes nao foi tocado (o projeto Vercel do
site foi de 1 para 2 de 12 — a regra dos 12 e do `moviki-robo`).

## Ordem de operacao — nao pular etapa

1. Subir os 5 arquivos. Nada muda no ar ainda.
2. Google Cloud > projeto `moviki-app` > Contas de servico > criar
   `moviki-site-leitura` com papel **Visualizador do Cloud Datastore**. Nunca a
   conta do `moviki-robo`, que tem escrita total.
3. Chave JSON > Vercel do SITE > env `FIREBASE_SA_LEITURA` > redeploy.
   Apagar o JSON do computador depois.
4. Abrir `moviki.com.br/api/vitrine`: o campo `via` tem que dizer **`sa`**.
   Enquanto disser `key`, **nao ligar o enforcement**.
5. Rodar o workflow `manutencao` do robo social na mao e ver a base contada.
6. Firebase Console > App Check > **Cloud Firestore** > aplicar.
   Depois **Storage**. **Authentication por ultimo**, em dia separado.

## Riscos aceitos

- **Nao existe papel do IAM por colecao.** A conta le todo o Firestore,
  inclusive colecao de dinheiro. Por isso ela e SO LEITURA e vive isolada da
  conta do robo. Quem usar `gauth.js` so pode ler o que a pagina ja mostra.
- **reCAPTCHA v3 barrado por bloqueador** vira trafego nao verificado. Olhar as
  metricas do App Check por alguns dias antes de virar a chave.
- **Pagina velha no cache do navegador** de quem visitou antes de 03/09 nao tem
  App Check. Some sozinho com o tempo.

## Depois de ligar

- Apagar os secrets `FIREBASE_API_KEY` do `moviki-assistente-social`.
- Mover esta nota para `04-Arquivo` e registrar em
  [[R - Marcas de versao no ar]].

Ver [[R - Regras de ouro]] · [[A2 - Infraestrutura e Deploy]]
