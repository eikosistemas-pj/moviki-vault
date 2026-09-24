---
data: 2026-09-17
projeto: Moviki
repos: [moviki-app, moviki-ai]
pr: não registrado
tags: [moviki, alteracao, seguranca, regras]
---

# Regras v26 sem curinga e teto do atendente do WhatsApp

## O que mudou

- **Regras do Firestore v26:** saiu o curinga que liberava tudo dentro de `negocios/{uid}`. Cada subcoleção do negócio passou a ter regra própria. Subcoleção nova agora nasce **fechada**, não pública.
- O **e-mail do lojista**, que ficava em `estado/liveAceite`, deixou de ser público. Só `estado/live` e `estado/liveSessao` continuam abertos.
- A validação do cadastro do negócio (`hasOnly`) **voltou a valer**. Antes, dava para gravar campo inventado, nome vazio e cor inválida.
- As regras do Firestore e do Storage passaram a morar no repositório (`moviki-app/firebase/`), com **teste automático** contra o emulador oficial.
- O atendente do WhatsApp ganhou **teto de uso**: 30 mensagens por telefone por dia (`ATENDIMENTO_LIMITE_DIA`), com teste automático.
- O `.bat` do vault passou a trazer do GitHub antes de enviar e a subir também o que é escrito direto no Obsidian.

## Por quê

- O curinga anulava em silêncio a validação do cadastro e faria qualquer subcoleção futura nascer pública. Regra do Firestore **não tem "deny"**: basta um match permitir.
- Regra que só existia no Console não tinha revisão, histórico nem como voltar.
- O atendente falava com desconhecido sem limite, e cada mensagem é uma chamada paga à Anthropic. A assinatura da Meta barra chamada forjada, não pessoa real insistindo.

## Decisões tomadas

- Subcoleção nova em `negocios/{uid}` **exige regra escrita** no mesmo ciclo.
- Mapa mestre mantido em **cópia completa nos seis repositórios**, com regra de sincronização no topo.

## O que conferir

- Painel do lojista: salvar cadastro, cardápio e fotos continua funcionando.
- Página pública `moviki.com.br/<apelido>` abre normal.

## Pendências

- Confirmar no Console se a v25 e a v26 estão publicadas — o Console é a verdade.

Ver também: [[MOVIKI 2026-09-17 - equipe de especialistas]] · [[R - Regras de ouro]]

*Reconstruída em 23/09/2026 a partir do histórico de decisões do CLAUDE.md.*
