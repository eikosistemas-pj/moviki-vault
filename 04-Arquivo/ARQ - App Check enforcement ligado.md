---
type: decisao
status: concluido
area: A2 - Infraestrutura e Deploy
tags: [appcheck, seguranca, firestore, armadilha]
atualizado: 2026-09-10
---

# ARQ - App Check enforcement ligado

**Era `P14 - App Check enforcement`.** Deixou de ser projeto quando o enforcement
foi ligado em 05/09/2026 — e por isso nao disputa numero com
[[P14 - Verificacao de parceiro]].

**Estado: Cloud Firestore = Aplicada desde 05/09.** Metrica na virada: 82%
verificadas, 16% cliente desatualizado, 1% origem desconhecida (janela de 7 dias,
ainda suja).

## O que travava — eram DOIS, nao um

App Check protege o Firestore contra quem nao e navegador. Requisicao de servidor
nao carrega token e vira "nao verificada".

| Quem | O que fazia | Sintoma se o enforcement subisse antes |
| --- | --- | --- |
| `moviki/api/og.js` | lia Firestore por REST com a chave publica | todo link de lojista compartilhado viraria **cartao cinza** |
| `moviki-assistente-social` | lia `/negocios` por REST com a chave publica, do GitHub Actions | o robo **pararia de postar**, com erro so dentro de um workflow que ninguem le |

**O segundo nao estava registrado em lugar nenhum.** Apareceu varrendo os 6
repositorios atras de tudo que fala com o Firebase fora de um navegador.
`moviki-robo` e `moviki-ai` usam Admin SDK — imunes.

## A solucao

**Conta de servico SOMENTE LEITURA, so no projeto Vercel do site.** Chamada de
conta de servico passa por IAM, nao pela chave publica: o App Check nao se aplica
a ela.

**Sem `firebase-admin`.** O repo do site nao tem `package.json`. Puxar o Admin SDK
para ler 4 documentos criaria passo de instalacao no deploy e engordaria o cold
start da unica funcao que serve TODA rota `/apelido`. O que o Admin SDK faria ali
e assinar um JWT e trocar por token OAuth — o `crypto` do Node faz sozinho.

**O robo social NAO ganhou a chave.** Aquele repositorio e publico; credencial de
banco em GitHub Secret so para ler dado que ja e publico troca um problema por
outro maior. Ele passou a consumir `moviki.com.br/api/vitrine`.

## Arquivos no ar (04/09)

| Repo | Caminho | Acao | Marca |
| --- | --- | --- | --- |
| moviki | `lib/gauth.js` | NOVO | `2026-09-04-gauth1` |
| moviki | `api/og.js` | SUBSTITUI | `2026-09-04-og-sa` |
| moviki | `api/vitrine.js` | NOVO | `2026-09-04-vitrine1` |
| moviki-assistente-social | `src/config.py`, `src/firestore.py` | SUBSTITUI | 2026-09-04 |

**Degradacao segura:** sem a env `FIREBASE_SA_LEITURA`, `og.js` e `vitrine.js`
voltam sozinhos ao modo antigo. Teto de funcoes intacto: o projeto Vercel do site
foi de 1 para 2 de 12 — a regra dos 12 e do `moviki-robo`.

## Credencial

- `moviki-site-leitura@moviki-app.iam.gserviceaccount.com`
- Papel unico: **Leitor do Cloud Datastore** (`roles/datastore.viewer`)
- Env `FIREBASE_SA_LEITURA` no projeto Vercel do **site**, Production + Preview
- O projeto `moviki-app` pertence a **eikosistemas@gmail.com**

Conferido no ar: `moviki.com.br/api/vitrine?x=1` responde `"via":"sa"`.

## A regra critica que nasceu daqui

> **NUNCA enforcar o App Check no Storage.** As fotos e logos sao servidas por URL
> direta do `firebasestorage.googleapis.com` com `?alt=media` — nao passam pelo
> SDK e nunca carregam token. O painel mostra 0% verificadas por motivo
> estrutural. Ligar apagaria a imagem de todas as paginas publicas de negocio,
> com sintoma de foto quebrada e nenhum erro. **Deixar em Monitoramento,
> permanentemente.**

## Ganhos de brinde

1. O filtro de opt-in (`autorizaDivulgacao`) virou server-side: quem nao autorizou
   divulgacao nao sai mais do banco
2. O robo social deixou de paginar a base inteira (ate 20x300 leituras por rodada)
3. `api/vitrine` serve qualquer consumidor futuro sem ninguem mais falar com o
   Firestore por fora

## Riscos aceitos

- Nao existe papel do IAM por colecao: a conta le todo o Firestore, inclusive
  colecao de dinheiro. Por isso e so-leitura e isolada da do robo
- reCAPTCHA v3 barrado por bloqueador vira trafego nao verificado
- Pagina velha no cache de quem visitou antes de 03/09 nao tem App Check

## Em aberto

- [ ] Conferir a metrica com **filtro de 1 dia**, nao 7 — a janela de 7 dias ainda
      carrega as leituras antigas pela chave publica
- [ ] **Authentication** so num dia separado, e so com a metrica do Firestore limpa
- [ ] Apagar os secrets `FIREBASE_API_KEY` do `moviki-assistente-social`
- [ ] `run_verificar.py` mostra dois numeros iguais porque a lista ja chega
      filtrada — ajuste cosmetico

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[A3 - Dados e Regras]] ·
[[P15 - Enforcement do App Check]] · [[R - Regras de ouro]] ·
[[R - Marcas de versao no ar]]
