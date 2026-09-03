---
type: projeto
status: ativo
prioridade: 1
area: A5 — Programa de Parceiros
prazo: 2026-09-05
tags: [conformidade, produto, medicao, armadilha]
atualizado: 2026-09-03
---

# P14 — Verificação de parceiro (moviki.com.br/v/apelido)

A página que o **comerciante** abre no celular dele, na frente do parceiro, para responder uma pergunta só: essa pessoa é mesmo do Moviki?

Existe para desmontar o golpe de quem cobra taxa de cadastro em nome da marca. Por isso o bloco "O que isso quer dizer" vem **antes** de qualquer botão: página de verificação que vende antes de proteger deixa de ser verificação.

## O desenho

| Peça | Onde | O que faz |
| --- | --- | --- |
| `v.html` | repo `moviki`, raiz | lê `parceiros_publicos/{slug}` e pinta o crachá |
| rota `/v/:slug` | `moviki/vercel.json` | rewrite para `v.html` |
| `parceiros_publicos/{slug}` | Firestore | espelho público: slug, nome, arroba, desde, ativo, treinado |
| `lib/espelhoParceiro.js` | repo `moviki-robo` | escreve o espelho pelo Admin SDK |
| regras **v20** | Console do Firebase | libera a leitura pública da coleção nova |

**Por que espelho e não ler `parceiros/{uid}` direto:** aquele documento guarda a **chave Pix**. Regra do Firestore libera o documento inteiro ou nada — não existe "libera só estes campos". Abrir a coleção entregaria a chave Pix de todo parceiro a qualquer visitante. Dinheiro, e-mail e uid não atravessam para o espelho.

**Como os parceiros antigos ganham espelho:** sem migração e sem varredura paga. O `parceiro.html` chama `api/novo-parceiro?espelho=1` ao abrir o painel, se o parceiro estiver aprovado, e de novo quando ele conclui as 8 aulas (que é quando `treinado` muda). Um por um, conforme entram.

## Estado em 03/09/2026

- ✅ `v.html`, `vercel.json`, `espelhoParceiro.js` e a chamada no `parceiro.html` estão nos repositórios.
- ✅ Regras **v20 publicadas** — confirmado pelo Paulo.
- ✅ `v.html` corrigido entregue em 03/09: **App Check**, **CSP** e **medição dos CTAs**. Marca `2026-09-03-verificacao-appcheck`.

## O que ainda falta

- [ ] **Nenhuma porta de entrada para o `/v/`.** Só o `parceiro.html` referencia a página. Nem a página pública `/apelido`, nem `comerciantes.html`, nem `parceiros.html`. Verificação que o comerciante desconfiado não encontra sozinho não protege contra o golpe que ela existe para impedir — o falso parceiro simplesmente não mostra o crachá. Decidir onde entra o link.
- [ ] Material de divulgação do parceiro com o link `/v/apelido` (crachá, assinatura de WhatsApp, cartão).
- [ ] Conferir no GA4, depois de alguns dias, se `cta_click` com `pagina: verificacao` está chegando.

## Armadilhas registradas

- **A ordem de publicação é regra, não recomendação.** As regras v20 vêm ANTES do `v.html` no ar. Invertido, a página diz "não existe parceiro com este apelido" para todo mundo — a mentira exata que ela existe para evitar, dita na frente do comerciante.
- **Página nova que fala com o Firebase nasce fora do App Check.** O `v.html` foi criado depois da rodada que instalou o App Check nas sete páginas e ficou de fora. Toda página nova leva o bloco no mesmo dia.
- **`data-ev` sem ouvinte não mede nada.** O `mvmetrica.js` não faz delegação; cada página traz o ouvinte inline. Copiar o atributo sem copiar o ouvinte deixa o CTA mudo no GA4.

## Ligações

[[A5 - Programa de Parceiros]] · [[P15 - Enforcement do App Check]] · [[R - Colecoes do Firestore]] · [[R - Marcas de versao no ar]] · [[R - Historico de regras do Firestore]]
