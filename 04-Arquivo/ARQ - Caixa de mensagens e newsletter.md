---
type: arquivo
status: concluido
data: 2026-08-27
area: A1 — Produto e Paineis
tags: [produto, lgpd]
atualizado: 2026-08-28
---

# ARQ — Caixa de mensagens + descadastro da newsletter — NO AR 27/08/2026

## Caixa de mensagens
**Uma conversa por lojista, e o id do documento É o uid dele** (`conversas/{uid}`). Não existe conversa entre lojistas.
**Nenhuma função nova no Vercel** — o navegador fala direto com Firestore e Storage.

- **Painel do lojista:** balão no topo (ponto vermelho), item no menu, cartão na grade.
- **Painel do dono:** seção Mensagens + botão em cada linha de Negócios.
- **Painel do parceiro:** 8ª seção, mesmo motor, **nenhuma regra nova** (a v13 é por `uid` da conta). Quem é lojista **e** parceiro vê a **mesma conversa** nos dois painéis — proposital.

**Bloco "Mensagens do admin"** (anexo de documento) é **por lojista**, nasce desligado. PDF, imagem, Word, Excel, texto e CSV, **até 10 MB**.

**A trava:** `docsLiberado` **fica fora da lista de campos que o lojista pode alterar**. Está no Firestore **e** no Storage — só no Firestore, o arquivo subiria e a mensagem seria recusada depois, deixando arquivo órfão.

**Não existe contador de não lidas** — é comparação de `ultimaEm` com `vistoLojistaEm`/`vistoDonoEm`. Contador exigiria que cada lado escrevesse no campo do outro.

**Mensagem não pode ser editada** (`allow update: if false`).

### O que o primeiro uso real quebrou (rodada 2)
Quatro problemas que 300 verificações automáticas não pegaram, todos ao anexar do celular:

| O que aconteceu | Conserto |
| --- | --- |
| Sem barra de progresso, o Paulo achou que não funcionou e **tocou 4 vezes** | `uploadBytesResumable` com barra e porcentagem; o clipe **trava** enquanto sobe |
| O iPhone mandou **`.heif`**, que sobe e **não abre** | HEIC/HEIF recusado na entrada, com a instrução |
| Foto e PDF com o mesmo cartão cinza | Imagem vira **miniatura** clicável |
| Nada podia ser apagado | **"apagar este anexo"** (só o dono), apaga a mensagem **e** o arquivo |

Mais dois: **o interruptor mentia** (ligava e o texto continuava "Desligado") e **a busca só achava pelo NOME** — procurar "karina", que é o apelido, não achava nada. O `prompt()` virou seletor de verdade, com busca por nome, apelido, e-mail, arroba, segmento e endereço.

### O aviso central para o dono
Título da aba vira `(2) Moviki — Painel do Dono` · entra em "Precisa de você" e no sino · aviso flutuante clicável · **bipe curto (WebAudio, sem arquivo externo)**. A primeira leitura do dia não avisa, e conversa aberta na tela também não grita.

## Descadastro da newsletter (LGPD)
`descadastro.html` no ar. Link individual: `moviki.com.br/descadastro.html?id=<docId>&e=<email>`. O **`id`** é quem manda; o **`e`** é só exibição — a página **nunca consulta o e-mail no banco**.

**Pede UMA confirmação, não sai em um clique** — alguns aplicativos de e-mail abrem links sozinhos para pré-carregar. Cinco estados tratados. 30 verificações no Playwright, 0 falhas.

O CSV da Newsletter ganhou a coluna **"Link de descadastro"** por pessoa. `privacidade.html` ganhou a seção 10.

## Regras do Storage — primeira vez do projeto
Até aqui o Storage só era escrito pelo Admin SDK, que ignora regras. O arquivo publicado tem, **de propósito**, `logos/{uid}` e `produtos/{uid}` com `read: if true` — sem essas duas linhas, publicar regras **apagaria da tela todas as logos de pino e fotos de produto**.

→ [[A1 - Produto e Paineis]] · [[P03 - Primeiro disparo de newsletter]] · [[R - Historico de regras v7 a v15]]
