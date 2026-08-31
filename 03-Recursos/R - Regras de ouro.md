---
type: recurso
status: referencia
tags: [armadilha, regra]
atualizado: 2026-08-31
---

# R — Regras de ouro

> A nota mais importante do vault. Ler antes de mexer em qualquer coisa.

## Dinheiro e servidor
- **Dinheiro e status = server-side.** Gate que afeta dinheiro precisa existir NO SERVIDOR, não só na UI.
- **Repo de dinheiro isolado do conversacional.**
- **NUNCA criar arquivo novo em `moviki-robo/api`** — 12/12. Um 13º **derruba o deploy inteiro**; sintoma: *"Failed to fetch"* com o código certo no GitHub. Função nova entra como **etapa** dentro de um endpoint existente.
- **O teto de 12 é POR PROJETO da Vercel.** Antes de espremer, pergunte em qual projeto a função deveria morar.
- **Função serverless tem ~10 s no Hobby.** Toda chamada externa precisa de idempotência na origem, recuperação e confirmação assíncrona por webhook.

## Regras do Firestore
- `hasOnly`: campo novo entra como **opcional** (`!('x' in d) || …`).
- Pensar nos **três estados**: sem o campo · ganhando o campo · com o campo. **O do meio é onde tudo quebra.**
- **Nunca publicar regra que EXIGE campo novo antes de o arquivo que grava esse campo estar no ar.**
- Em `update`, `request.resource.data` é o **documento inteiro mesclado**.
- Campo novo do Admin SDK **precisa entrar no `hasOnly` que o cliente atravessa**.
- `setDoc` com `merge` em documento com `hasOnly` apertado é armadilha → `setDoc` completo na criação, `updateDoc` depois.
- **Trocar regras do Storage pode apagar imagem da tela** — manter `logos/{uid}` e `produtos/{uid}` com `read: if true`.
- **A cópia das regras no Project pode estar atrás do Console. O Console é a verdade.**
- **Apagar o documento não apaga a subcoleção, nem o apelido, nem o arquivo.**
- **Ler o documento ANTES de apagá-lo** quando algo depende do que está dentro.
- **TTL do Firestore só existe no Console do Google Cloud.**
- **`hasOnly` em coleção que SÓ o admin escreve é segurança de mentira.** Não barra ninguém que já não esteja barrado e quebra o painel a cada campo novo. Validar **tipo**, nunca conjunto fechado. *(v16, `configuracoes/sistema`.)*
- **`allow write` cobre delete, e em delete `request.resource` é NULO** — a expressão erra e nega. Separar `create, update` de `delete` sempre.
- **Campo dentro de `hasOnly` sem `is <tipo>` e sem `.size()` não está validado** — só está na lista. *(É o caso de `comentario` na avaliação hoje.)*
- **`create` anônimo de documento agregado precisa travar o VALOR INICIAL, não só o incremento.** Travar o `update` em +1 não serve de nada se o `create` aceita começar em 100.000. *(É o caso de `resumo/avaliacoes` hoje — ver [[ARQ - Furos nas regras v16]].)*
- **`match /{documento=**}` com `read: if true` publica toda subcoleção FUTURA.** Subcoleção nova de negócio nasce pública — decidir antes de criar, não depois. *(Foi por isso que `metricas` virou coleção de topo.)*

## Deploy e diagnóstico
- **Antes de caçar bug, conferir a marca de versão** (`MOVIKI_VERSAO` no Console + o arquivo no GitHub).
- **Tela antiga quase sempre é cache.** Ctrl+Shift+R. Não existe service worker.
- **Env criada depois do deploy não vale para o deploy existente.**
- **A Vercel não deixa mais reler env salva** → rotacionar nos dois lados, ou o código aceita dois valores.
- **Domínio novo no jogo? A CSP é a primeira suspeita.** Fetch bloqueado por CSP **não aparece no Network**.
- **CSP não é só do arquivo novo** — página que passa a mostrar imagem do Storage precisa de `firebasestorage.googleapis.com` no `img-src`.
- **A tela tem que refletir a realidade — nos dois sentidos.** `catch` vazio engole erro real; `catch` que grita sem checar o código de saída inventa erro que não existe. Em script, quem decide se falhou é o **código de saída do processo**, nunca a presença de texto no stderr — **o git escreve informação no stderr** (`From ...`, `To ...`, contagem de objetos). Já custou duas rodadas caçando um push que nunca falhou.
- **`catch` vazio em chamada de rede é uma hora de caçada esperando acontecer.** Falhar calado para o usuário pode; para o console, não. *(Exceção deliberada: os ouvintes da caixa de mensagens — painel de lojista não pode cair por causa de mensagem.)*
- **Modelo de IA tem validade.** Fixar o id na env, que troca sem deploy.
- **404 é rota de produção.** Domínio sem `vercel.json` serve o `404.html` do repo em todo endereço inválido.
- **Conferir o arquivo ao vivo depois de upload envolvendo `/api`.**
- **Nunca "pedaço de código + onde colar".** Arquivo completo, nome final, validado antes, com repositório + pasta + NOVO/SUBSTITUI.
- **Upload por arrastar ignora pastas com ponto.**
- **Nome de arquivo não pode depender de hífen** no download — **mas o nome vira o endereço na Vercel**.
- **Proxy git bloqueia push.** Claude entrega arquivos; upload é manual.
- **O proxy também bloqueia LEITURA do GitHub e o domínio `moviki.com.br`.** `github.com`, `raw.githubusercontent.com` e conexão direta ao site são negados; o que passa é o WebFetch, e ele **não executa JavaScript**. Consequência: o Claude não audita página montada no navegador e não clona o vault — leitura de dado do produto sai da **REST do Firestore**, que é pública em `/negocios` e `/assinaturas`.
- **Nome de arquivo só com ASCII.** Travessão, acento e til nos NOMES quebram: o Explorer do Windows lê os nomes de dentro do `.zip` como cp850, e `—` vira `ÔÇö`. Já aconteceu com o vault inteiro — 59 de 71 arquivos e todos os wikilinks. O conteúdo pode ter acento à vontade; o nome, não.
- LF, sem CR.

## Front-end
- **A página pública é servida em `/qualquer-apelido`** — TODO caminho de arquivo tem que ser **absoluto**.
- **CSS é ordem, não especificidade.**
- `grid-template-columns:1fr` estoura no celular → `minmax(0,1fr)` + `min-width:0`.
- **Escape de XSS (`esc()`)** em todo texto do lojista na página pública **e** em toda mensagem da caixa.
- Gate de plano inclui `enterprise` em **todos** os gates.
- **Botão que muda estado muda o rótulo junto.**
- **Upload sem barra de progresso vira arquivo duplicado.**
- **HEIC/HEIF do iPhone sobe e não abre** — recusar na entrada.
- **Ação sem volta pede confirmação DIGITADA**, não `confirm()`.
- **Busca de pessoa procura por nome, apelido e e-mail.**
- **Página montada no navegador não pode ser auditada por leitura de HTML.** O HTML estático traz todas as seções, inclusive as ocultas e os textos de estado vazio — uma leitura crua parece cheia ou vazia sem relação com o dado. A verdade é o `updateTime` do documento.

## Medição
- **Medição nunca derruba cobrança — e tráfego pago nunca antes da medição.**
- **`mvmetrica.js` NÃO escreve no Firestore.**
- **Não mexer no `mvmetrica.js` sem necessidade.** Medição de página nova entra inline.
- **Página que redireciona na hora não carrega GA** — carimbe UTM no destino.
- **Carimbar UTM só vale se o DESTINO medir.**
- **Evento de venda sozinho não tira campanha do aprendizado.**
- **`action_source` descreve de onde o evento NASCEU.**
- **Campo de correspondência vazio não se manda para a Meta.**
- **Nunca travar a coleta de dado — travar só a exibição.**

## SEO e compartilhamento
- **Página montada no navegador não tem preview nem SEO.** Se o link é para ser compartilhado, as tags saem do servidor — e **iguais para robô e para gente** (diferente é *cloaking*).
- **Página servida como 404 responde 404.** Nada indexa isso.
- **Canonical nunca sai do host da requisição.** Fixar no domínio do CNAME.
- **Preview e indexação são decisões separadas.** Cadastro de teste indexado derruba a reputação do domínio, que é um só para todos os lojistas.
- **Nunca usar endereço como sinal de negócio completo.** O Moviki existe para quem NÃO tem endereço fixo.

## Conformidade
- **Descreva a REGRA, nunca o RESULTADO.**
- **Conformidade tem que chegar até a página do FORMULÁRIO.**
- **Antes de instalar rastreador, ler a própria política de privacidade.**
- **Autorização permanente:** achou violação de Meta/Google, conserta direto.
- **Opt-in de um lugar não vale para outro.** O `autorizaDivulgacao` promete "nunca publicamos seu endereço exato — só a cidade": ele autoriza a vitrine social, **não** o filme institucional, que mostra o mapa. Material que exibe tela do produto sai de **conta demo própria**, nunca de cliente real.

## IA
- **Robô que fala com o cliente nasce DESLIGADO, conversa a conversa.**
- A resposta nunca nasce como `'admin'` — sem `'bot'`, não há como separar robô de gente depois.
- **Prompt não é trava de segurança.** Filtro em código também.
- **Ativação antes de venda.**

## Produção de vídeo e geração por IA
- **Nenhuma geração antes da bíblia visual escrita e aprovada.** Direção de arte mandada gerar sem validação já custou mais de 200 créditos numa rodada.
- **Keyframe still primeiro, vídeo depois.** Still aprovado → image-to-video → inspeção humana → próxima cena. Uma cena por vez, sem variação automática.
- **Em image-to-video, o `first_frame` governa a POSIÇÃO; o prompt só governa o MOVIMENTO.** Enquadramento errado se conserta no keyframe, nunca no texto.
- **Física não se conserta por prompt.** Modelo de vídeo não simula corpo rígido. Objeto que atravessa objeto só tem uma solução: remover o objeto.
- **Veo aceita 4, 6 ou 8 segundos. 5 s não existe.**
- **Timeout do MCP não significa geração cancelada** — ela continua e é cobrada. Conferir por `get_credits` + `list_my_gallery` antes de qualquer retentativa.
- **Toda UI do filme é captura real.** Nunca gerar interface, logo ou pino por IA; nunca reconstruir interface em After Effects.
- **Asset ausente é PENDENTE, não improviso.** Não inventar UI, logo, telas, depoimentos, métricas ou resultados.
- **Autenticidade não significa precariedade.**
- **Prioridade que decide empate:** qualidade cinematográfica > consistência > eficiência de créditos > velocidade.
- **Buscar antes de pedir. Usar o oficial antes de recriar. Produto real antes de mockup. Precisão antes de velocidade.**

## Testes
- **Dry-run valida conteúdo; só a publicação real valida integração.**
- Sandbox do Claude não alcança CDN nem emulador do Firebase. O que funciona: `prev/` com stub de Leaflet e do Firestore/Auth/Storage, `python3 -m http.server`, Playwright no Chromium local. **O emulador de regras NÃO roda.**
- Clique sintético no Playwright precisa de `cancelable:true`.
- Checkbox de switch é invisível (`opacity:0;width:0`) — clique no trilho (`.swT`).
- `node --check` não pega erro de escopo.

## Ligações
[[ARQ - Furos nas regras v16]] · [[ARQ - Armadilhas de geracao por IA]] · [[ARQ - Incidentes e cacadas de bug]] · [[A3 - Dados e Regras]] · [[P13 - Video institucional da landing]]
