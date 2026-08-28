---
type: incidente
status: concluido
area: A2 — Infraestrutura e Deploy
tags: [armadilha]
atualizado: 2026-08-28
---

# ARQ — Incidentes e caçadas de bug

> **Ler antes de caçar bug.** Cada um destes vai voltar a acontecer.

## 27/08 — as quatro portas fechadas em sequência (o Vik mudo)
1. **Os arquivos não tinham subido.** O `MOVIKI_VERSAO` no console dizia a verdade e o GitHub confirmava. → **Sempre conferir a marca de versão antes de caçar bug.**
2. **`ANTHROPIC_API_KEY` não existia** no projeto `moviki-ai` da Vercel. *(E env criada depois do deploy não vale para o deploy existente — isso custou meia hora.)*
3. **Modelo aposentado.** O padrão do `lib/anthropic.js` era `claude-3-5-sonnet-20241022`, de 2024, fora do catálogo. A API recusa, `perguntarClaude` devolve `null` e o atendente fica **mudo, sem erro nenhum na tela**.
4. **A CSP bloqueava o domínio do robô.** O `connect-src` do `index.html` liberava `moviki-robo.vercel.app` mas **não** `moviki-ai.vercel.app`. **Fetch bloqueado por CSP não aparece no Network** — a requisição nem chega a existir. E o `catch(e){}` era mudo e engolia tudo.

**Corrigido nos dois sentidos:** a CSP liberou o domínio, e o catch passou a escrever `[vik] não consegui chamar o assistente` no console.

## 27/08 — o `404.html` do `moviki-app` era código público velho
Era uma cópia de 26/08 da página pública do repo `moviki` — **140 KB**, com Leaflet, cardápio, avaliações e o roteador de slug. Como o `moviki-app` **não tem `vercel.json`**, a Vercel servia esse arquivo em **QUALQUER URL inválida** de `app.moviki.com.br`: código velho num endereço público, e `pagina_negocio` disparando no GA4 **pelo host errado**. Substituído por um 404 real de 4,6 KB.
→ **404 é rota de produção.**

## 27/08 — a cópia das regras estava 3 versões atrás
O arquivo guardado no Project estava na **v12**, sem o bloco `conversas`, com a **v13** publicada. **Publicar aquele arquivo por engano teria derrubado a caixa de mensagens inteira.**
→ **O Console é a verdade.** Foi o Paulo anexar as regras reais que salvou a rodada.

## 27/08 — a v14 e a caixa que teria travado calada
Depois da **primeira** resposta do Vik, o lojista não conseguiria mais nem marcar como lido nem mandar mensagem — porque `conversaCampos()` é avaliada sobre o **documento inteiro mesclado** e não conhecia os campos `bot*`. Detalhe em [[R - Historico de regras v7 a v15]].

## 27/08 — o portão de SEO reprovou o cliente ideal
A primeira versão do `api/og.js` exigia segmento **ou** endereço e reprovou o CALDEIRÃO NORDESTINO: 12 fotos, cardápio, promoções e eventos, **sem endereço**.
→ **Nunca usar endereço como sinal de negócio completo. O Moviki existe para quem NÃO tem endereço fixo.**

## 27/08 — a canonical com `www`
Dois hosts respondendo, duas canonicals diferentes para a mesma página — **o duplicado que a canonical existe para evitar.**
→ **Canonical nunca sai do host da requisição.** Fixar no domínio do CNAME.

## 27/08 — o anexo que subiu 4 vezes
Sem barra de progresso, o Paulo achou que não tinha funcionado e tocou de novo.
→ **Upload sem barra de progresso vira arquivo duplicado.** Barra **e** trava no botão.

## 27/08 — o interruptor que mentia
Ligava o envio de documentos e o texto ao lado continuava "Desligado: o lojista não vê o bloco".
→ **Botão que muda estado muda o rótulo junto.**

## 27/08 — a busca que só achava pelo nome
Procurar "karina" — o **apelido do link** — não achava nada.
→ **Na cabeça de quem usa, o negócio "é" o apelido.**

## 26–27/08 — os 10 segundos do Pix
O Pix foi criado no Asaas mas a resposta não voltou a tempo. **O `externalReference` funcionou como trava anti-duplicidade e o dinheiro não saiu duas vezes.** Detalhe em [[ARQ - Pix automatico de comissao]].

## 26/08 — as três falhas da mesma família
Regra que exige um campo novo **antes** de o arquivo que grava esse campo estar no ar. **O estado do meio (documento em transição) é onde tudo quebrou.**

## 24/08 — os 3 bugs do primeiro post real
Passaram por 46 testes, 2 dry-runs e um verificador verde. Detalhe em [[ARQ - Robo social no ar]].

## 24/08 — `SO_FACEBOOK=1` não funcionava
**O GitHub Actions mascara todo dígito `1` nos logs.** Usar `sim`/`nao`.

## 28/08 — o vault inteiro com nome de arquivo quebrado
`—` lido como cp850 pelo Explorer do Windows na descompactação. 59 de 71 arquivos, e **todos os wikilinks**. Detalhe em [[ARQ - Incidente - nomes de arquivo corrompidos no Windows]].
→ **Nome de arquivo só com ASCII.**

## 28/08 - o git recem-instalado nao tinha identidade
Primeiro commit do vault falhou com `fatal: unable to auto-detect email address (got 'Paulo@PC-PAULO.(none)')`. **Git instalado do zero nao sabe quem voce e**, e sem `user.name` e `user.email` ele recusa qualquer commit.

Pior: o **plugin Git do Obsidian mostra so um aviso vermelho na barra de baixo**, com a mensagem em ingles cortada. Os arquivos ja estavam salvos e no lugar certo - so o commit nao saiu, o que e facil de confundir com "o sync nao funcionou".

Conserto, uma vez por maquina:
```
git config --global user.email "suporte@moviki.com.br"
git config --global user.name "eikosistemas-pj"
```
Nenhum dos dois responde nada. **Silencio e sucesso.**

-> **Maquina nova com git: configurar identidade ANTES do primeiro commit.** Ver [[R - Sync do vault Obsidian Git]].

## 28/08 - o navegador remove hifens do nome no download
`moviki-vault-repo.zip` chegou como `movikivaultrepo.zip`. A regra ja existia no projeto, mas o vault a torna critica: **todo wikilink aponta pelo nome do arquivo**, entao `R - Regras de ouro.md` chegando como `R  Regras de ouro.md` viraria uma nota diferente, com todos os links apontando para ela orfaos.

Conserto estrutural: o `SincronizarVaultMoviki.bat` **reconstroi o nome antes de salvar** - troca o duplo espaco por ` - ` e restaura `LEIA-ME` e `T-`. Testado contra os 72 arquivos do vault, nos dois cenarios (nome intacto e nome mutilado): 72/72.

## 28/08 - o script que inventou um erro que nao existia
O `.bat` de sincronizacao anunciou `[X] Git: To https://github.com/...` e depois `[X] Git: From https://...`. Duas rodadas foram gastas cacando um push e um pull que **nunca falharam** - rodados a mao, os dois respondiam `Current branch main is up to date.`

**Causa:** o git escreve mensagem informativa no **stderr**, nao no stdout - `From https://...`, `To https://...`, contagem de objetos, tudo. O script combinava `$ErrorActionPreference = 'Stop'` com `2>&1`, entao o PowerShell tratava essa saida normal como excecao terminante. O `[X]` era a mensagem do `catch`, nao do git.

**O dano real nao foi o alarme falso, foi o que ele abortou.** O `catch` matou o bloco antes do `git push`, e o commit da renomeacao ficou parado como `[ahead 1]` - o script gritou sobre um problema inexistente e criou um de verdade em silencio.

**Conserto:** quem decide se falhou e o **codigo de saida** (`$LASTEXITCODE`), nunca a presenca de texto no stderr. E todo run termina imprimindo `git status -sb`, que e a verdade nua sobre a sincronizacao.

-> Ver a regra sobre `catch` em [[R - Regras de ouro]]. E a mesma familia do `catch` vazio do Vik, com o sinal trocado: la engolia erro real, aqui inventava erro que nao existia. **Nos dois casos a tela para de refletir a realidade, e voce conserta o que nao esta quebrado.**

## Recorrente - a landing crua
`moviki-ui.css` (com hífen) subiu no lugar de `movikiui.css`. A duplicata byte a byte ainda está no repo → [[P09 - Faxina do repositorio moviki]].
