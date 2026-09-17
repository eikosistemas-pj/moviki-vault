---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [backup, firestore, incidente, recuperacao, lgpd]
atualizado: 2026-09-16
---

# R - Plano de recuperacao do banco

**Escrito em 16/09/2026, com o banco saudavel.** E para isso que serve: plano de
recuperacao que nasce durante o incidente ja nasceu tarde.

## O que esta ligado hoje

| | |
| --- | --- |
| Backups programados | **diario, retencao 7 dias** |
| Recuperacao pontual (PITR) | **desativada** (custa 5x o backup; adiar) |
| Politicas de TTL | 5, todas **Veiculando** (`checkout_freio`, `dias`, `livechat`, `livepresenca`, `pedidos`) |

O primeiro backup aparece na lista **em ate 24 h**. Lista vazia logo depois de
ligar e normal, nao e falha.

## ⚠️ A verdade desconfortavel: restaurar NAO desfaz

Restaurar **grava os dados num banco NOVO, com outro ID**. O `(default)`
estragado continua exatamente como esta. E o banco restaurado nasce **sem as
regras de seguranca e sem as politicas de TTL** — nada disso viaja com o
backup.

Ou seja, a recuperacao nao e "clicar em restaurar". E uma migracao.

## O roteiro, na ordem

1. **PARAR a escrita.** Chave-mestra das lives ligada (`liveDesligada`) e, se o
   estrago for no dinheiro, tirar as variaveis do Asaas do projeto do robo na
   Vercel. Restaurar por cima de um sistema que continua escrevendo produz um
   terceiro estado, pior que os dois.
2. **Restaurar** o backup para um banco novo — `moviki-restore` serve. Console do
   Firestore > Recuperacao de desastres > menu do backup > "Restaurar com o
   Cloud Shell". A cobranca e por GiB do backup.
3. **Republicar as regras** (v25 ou a vigente) **nesse banco novo**. Ele nasce
   sem nenhuma.
4. **Recriar as 5 politicas de TTL**, campo `expiraEm`, adiamento 0. Ver
   [[R - TTL de retencao no Firestore]].
5. **Apontar a aplicacao para o banco novo.** Sao **15 pontos**, todos com o
   banco implicito hoje:

| Onde | O que muda |
| --- | --- |
| 10 paginas com `getFirestore(app)` — `moviki-app`: `index.html`, `eikoadm01.html`, `live.html`, `parceiro.html`, `seja-parceiro.html`; `moviki`: `index.html`, `404.html`, `live.html`, `v.html`, `descadastro.html` | passa a `getFirestore(app, 'moviki-restore')` |
| `moviki-robo/lib/firebase.js` (`admin.firestore()`) | passa a `admin.firestore(app, 'moviki-restore')` — **um arquivo so serve todo o robo**, que e a razao de ele existir |
| 4 endpoints REST do site: `api/live.js`, `api/og.js`, `api/sitemap.js`, `api/vitrine.js` | `/databases/(default)/` vira `/databases/moviki-restore/` |

6. **Conferir antes de anunciar:** entrar no painel do dono, ver os negocios, as
   comissoes e os pedidos. Backup restaurado que ninguem olhou nao e backup.

## O que este plano nao cobre

- **Dado escrito depois do ultimo backup diario some.** A janela e de ate 24 h.
  Fechar essa janela e o PITR, que e a decisao a revisitar quando houver
  faturamento — nao antes.
- O **Asaas nao restaura junto**: assinaturas, subcontas e transferencias sao
  de la. Banco restaurado com assinatura cancelada no Asaas continua cancelada.
- **Storage (fotos, logos, comprovantes) nao entra no backup do Firestore.**

## Melhoria mapeada

O nome do banco ficar implicito em 15 lugares e o que transforma uma restauracao
em uma tarde de trabalho. Concentra-lo numa constante por repositorio
(`MV_DB`) faria a migracao virar tres edicoes. **Nao e urgente e nao deve ser
feito no meio de um incidente** — mas e o conserto certo quando sobrar folga.

## Regras de ouro

1. **Backup que ninguem sabe restaurar e um custo mensal, nao uma protecao.**
2. **Restaurar cria banco novo:** regras e TTL nao viajam com os dados.
3. **Parar a escrita vem antes de restaurar.**
4. **O que mora fora do Firestore nao volta** — Asaas, Storage, Cloudflare.

## Ligacoes

[[A2 - Infraestrutura e Deploy]] · [[R - TTL de retencao no Firestore]] ·
[[R - Marcas de versao no ar]]
