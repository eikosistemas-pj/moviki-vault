---
type: area
status: ativo
tags: [infra, deploy, armadilha]
atualizado: 2026-08-28
---

# A2 — Infraestrutura e Deploy

## Padrão a manter
Entrega é **arquivo completo, nome final, validado antes** — nunca "pedaço de código + onde colar". Todo arquivo entregue vai com **repositório de destino, pasta e se é NOVO ou SUBSTITUI**.

## As armadilhas que mais custaram
- **Teto de 12 funções serverless é POR PROJETO da Vercel.** `moviki-robo` está em 12/12; `moviki` usa 1; `moviki-ai` usa 2. Um 13º arquivo **derruba o deploy inteiro** e o deploy anterior fica no ar — o sintoma é *"Failed to fetch"* com o código certo no GitHub. Antes de espremer uma etapa, **pergunte em qual projeto a função deveria morar**.
- **Env criada DEPOIS do deploy não vale para o deploy que já existe.** Redeploy, ou suba um arquivo para disparar deploy novo.
- **A Vercel não deixa mais RELER o valor de uma env salva.** Ou rotaciona nos dois lados, ou o código aceita **dois** valores (foi o que o `webhook.js` fez com o token do webhook).
- **Função serverless tem ~10 s no Hobby.** Toda chamada externa precisa de plano B: idempotência na origem, recuperação ("já existe? busca e segue") e confirmação assíncrona por webhook.
- **404 é rota de produção.** Domínio sem `vercel.json` serve o `404.html` do repositório em todo endereço inválido. Já aconteceu: o `404.html` do `moviki-app` era cópia de 140 KB da página pública.
- **Upload por arrastar ignora pastas que começam com ponto.** Navegue até `.github/workflows` e use "Add file > Upload files" ali dentro.
- **Nome de arquivo entregue no chat não pode depender de hífen** (o navegador remove hífens no download) — **mas o nome do arquivo vira o endereço na Vercel**. Conferir na hora do upload.
- **Antes de caçar bug, conferir a marca de versão.** `MOVIKI_VERSAO` no Console + o arquivo no GitHub. Metade das caçadas de 27/08 foi arquivo que não tinha subido.
- **Tela antiga quase sempre é cache do navegador.** Ctrl+Shift+R. Não existe service worker nos repos.
- **CSP é a primeira suspeita quando um domínio novo entra no jogo.** Fetch bloqueado por CSP **não aparece no Network** — a requisição nem existe.
- **`catch` vazio em chamada de rede é uma hora de caçada esperando acontecer.** Falhar em silêncio para o USUÁRIO pode estar certo; para o CONSOLE, não.
- **Modelo de IA tem validade.** Modelo aposentado faz a API recusar e o robô ficar mudo sem erro na tela.
- LF, sem CR.

## Projetos vinculados
[[P09 - Faxina do repositorio moviki]] · [[P11 - Pendencias operacionais do dono]] · [[P07 - Aviso de mensagem nova para o lojista]]

## Recursos
[[R - Stack e repositorios]] · [[R - Variaveis de ambiente]] · [[R - Checklist de deploy]] · [[R - Marcas de versao no ar]] · [[ARQ - Incidentes e cacadas de bug]]
