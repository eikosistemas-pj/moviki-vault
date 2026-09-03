---
type: recurso
status: referencia
area: A3 — Dados e Regras
tags: [armadilha, regra]
atualizado: 2026-09-03
---

# R — Regras de ouro

> A nota mais importante do vault. Ler antes de mexer em qualquer coisa.

## Dinheiro, servidor e segurança
- **Dinheiro e status = server-side.** Gate que afeta dinheiro precisa existir NO SERVIDOR, não só na UI.
- **Repo de dinheiro isolado do conversacional.**
- **NUNCA criar arquivo novo em `moviki-robo/api`** — 12/12. Um 13º **derruba o deploy inteiro**; sintoma: *"Failed to fetch"* com o código certo no GitHub. Função nova entra como **etapa** dentro de um endpoint existente, ou como **módulo em `lib/`**.
- **O teto de 12 é POR PROJETO da Vercel.** Antes de espremer, pergunte em qual projeto a função deveria morar.
- **Função serverless tem ~10 s no Hobby.** Toda chamada externa precisa de idempotência na origem, recuperação e confirmação assíncrona por webhook.
- **Conferência de assinatura NUNCA pode falhar aberto.** `if (!secret) return true` transforma uma env esquecida em porta destrancada, e ninguém percebe — o endpoint responde 200 normalmente. Sem o segredo, ninguém entra. *(Foi assim que o `atendimento.js` ficou exposto — v19, 03/09.)*
- **Env de chave de administrador fica só em Production**, nunca em Preview: toda deployment de branch herdaria a chave.
- **Segredo não viaja por query string.** `?secret=` fica em log de servidor. Preferir o cabeçalho `Authorization`.

## Regras do Firestore
- `hasOnly`: campo novo entra como **opcional** (`!('x' in d) || …`).
- Pensar nos **três estados**: sem o campo · ganhando o campo · com o campo. **O do meio é onde tudo quebra.**
- **Nunca publicar regra que EXIGE campo novo antes de o arquivo que grava esse campo estar no ar.** E, no sentido inverso: **publicar a regra ANTES do arquivo** quando o arquivo passa a gravar campo novo.
- **Regra não é tela.** Todo limite que a tela impõe — tamanho de texto, valor máximo, "só um por vez" — precisa existir também na regra. Quem chama o Firestore direto não passa pela sua tela. *(v19.)*
- **Regra do Firestore libera o documento INTEIRO ou nada.** Documento que mistura dado público com dado sensível pede **ESPELHO em coleção separada**, escrito pelo Admin SDK. *(v20, `parceiros_publicos` — a chave Pix mora em `parceiros/{uid}`.)*
- Em `update`, `request.resource.data` é o **documento inteiro mesclado**.
- Campo novo do Admin SDK **precisa entrar no `hasOnly` que o cliente atravessa**.
- `setDoc` com `merge` em documento com `hasOnly` apertado é armadilha → `setDoc` completo na criação, `updateDoc` depois.
- **Trocar regras do Storage pode apagar imagem da tela** — manter `logos/{uid}` e `produtos/{uid}` com `read: if true`.
- **A cópia das regras no Project pode estar atrás do Console. O Console é a verdade.**
- **Apagar o documento não apaga a subcoleção, nem o apelido, nem o arquivo.**
- **Ler o documento ANTES de apagá-lo** quando algo depende do que está dentro.
- **TTL do Firestore só existe no Console do Google Cloud.**
- **`hasOnly` em coleção que SÓ o admin escreve é segurança de mentira.** Não barra ninguém que já não esteja barrado e quebra o painel a cada campo novo. Validar **tipo**, nunca conjunto fechado. *(v16.)*
- **`allow write` cobre delete, e em delete `request.resource` é NULO** — a expressão erra e nega. Separar `create, update` de `delete` sempre.
- **Campo dentro de `hasOnly` sem `is <tipo>` e sem `.size()` não está validado** — só está na lista.
- **`create` anônimo de documento agregado precisa travar o VALOR INICIAL, não só o incremento.** Travar o `update` em +1 não serve de nada se o `create` aceita começar em 100.000. *(v19, `resumo/avaliacoes`.)*
- **`match /{documento=**}` com `read: if true` publica toda subcoleção FUTURA.** Subcoleção nova de negócio nasce pública — decidir antes de criar, não depois.
- **Escrita negada pelas regras falha CALADA.** A barra anda na tela e ao recarregar volta do zero, sem erro nenhum. Conferir a regra antes de culpar o código.

## App Check
- **Só se enforça depois que TODA página que fala com o Firebase o inicializa.** Enforçar com uma página de fora derruba aquela página inteira, calada.
- **Página nova que fala com o Firebase nasce fora do App Check.** Toda página nova leva o bloco no mesmo dia. *(O `v.html` nasceu depois da rodada que instalou nas sete e ficou de fora.)*
- **App Check não vê só o navegador.** Todo pedaço que fala com o Firebase **de servidor** (`api/og.js` lê por REST) não carrega token e vira "não verificado". Antes de enforçar, listar quem fala de fora do navegador e dar a esses o Admin SDK.
- **App Check traz a insígnia do reCAPTCHA junto.** Nasce colada no canto inferior direito e bate em barra fixa de rodapé. Escondê-la obriga a texto de atribuição visível (regra do Google) — mais simples é reposicionar por CSS.

## Deploy e diagnóstico
- **Antes de caçar bug, conferir a marca de versão** (`MOVIKI_VERSAO` no Console + o arquivo no GitHub).
- **A marca sobe JUNTO com o conteúdo.** Arquivo que ganha funcionalidade e mantém a marca antiga é pior que arquivo sem marca: afirma um estado falso e o diagnóstico começa no lugar errado. *(03/09 à noite: três arquivos assim.)*
- **"Entregue" e "no ar" são estados diferentes, e só o repositório sabe qual é qual.** Documento registra o que foi produzido. Antes de dar rodada por encerrada, conferir o código publicado. *(Ver [[ARQ - Entregue e nao subiu 03092026]].)*
- **Tela antiga quase sempre é cache.** Ctrl+Shift+R. Não existe service worker.
- **Env criada depois do deploy não vale para o deploy existente.**
- **A Vercel não deixa mais reler env salva** → rotacionar nos dois lados, ou o código aceita dois valores.
- **O `vercel.json` não aceita chave inventada.** A Vercel valida contra um formato fechado e recusa qualquer chave fora da lista — inclusive comentário tipo `$comment`. O deploy falha com *"should NOT have additional properties"* e **o deploy anterior fica no ar**: nenhum sintoma aparece.
- **Domínio novo no jogo? A CSP é a primeira suspeita.** Fetch bloqueado por CSP **não aparece no Network**.
- **CSP não é só do arquivo novo** — imagem do Storage pede `firebasestorage.googleapis.com` no `img-src`; YouTube pede `frame-src`, `img-src https://i.ytimg.com` e, para medir o assistido, `script-src https://www.youtube.com`.
- **`frame-src` do CSP precisa de `'self'` quando o login é no domínio próprio.** O Firebase abre um quadro invisível no endereço do `authDomain`. Sem `'self'` na lista, o CSP **bloqueia calado** e o login não completa.
- **Classifique erro pelo CÓDIGO, nunca pelo texto da mensagem.** Quando um erro nosso e uma resposta legítima chegam pelo mesmo caminho, ler a mensagem com expressão regular é chute — `"does not exist"` cabia no perfil procurado **e** na nossa própria conta, e o diagnóstico saía invertido na tela. **E registre o erro cru sempre: log economizado é diagnóstico perdido.**
- **"Funcionou uma vez" não é prova.** O QR das versões 1 a 3 lia com o nível de correção escrito errado, porque o corretor do leitor compensava — num celular pior, não leria. Onde existir implementação de referência, **comparar com ela**, não confiar no resultado observado.
- **A tela tem que refletir a realidade — nos dois sentidos.** `catch` vazio engole erro real; `catch` que grita sem checar o código de saída inventa erro que não existe. Em script, quem decide se falhou é o **código de saída do processo**, nunca texto no stderr — **o git escreve informação no stderr**.
- **`catch` vazio em chamada de rede é uma hora de caçada esperando acontecer.** Falhar calado para o usuário pode; para o console, não. *(Exceções deliberadas: os ouvintes da caixa de mensagens e o bloco de tutoriais.)*
- **Modelo de IA tem validade.** Fixar o id na env, que troca sem deploy.
- **404 é rota de produção.** Domínio sem `vercel.json` serve o `404.html` do repo em todo endereço inválido.
- **Conferir o arquivo ao vivo depois de upload envolvendo `/api`.**
- **Nunca "pedaço de código + onde colar".** Arquivo completo, nome final, validado antes, com repositório + pasta + NOVO/SUBSTITUI. **Entrega cumulativa:** cada arquivo contém tudo dos anteriores.
- **Upload por arrastar ignora pastas com ponto.**
- **Nome de arquivo não pode depender de hífen** no download — **mas o nome vira o endereço na Vercel**.
- **Proxy git bloqueia push.** Claude entrega arquivos; upload é manual.
- **O alcance de rede do sandbox VARIA por conta e por sessão.** Já houve sessão que clonava o GitHub e não alcançava a internet pública, e sessão com o inverso. **Testar antes de assumir** — e nunca concluir "está fora do ar" a partir de uma chamada que o próprio ambiente bloqueou.
- **Nome de arquivo só com ASCII.** Travessão, acento e til nos NOMES quebram: o Explorer do Windows lê os nomes de dentro do `.zip` como cp850, e `—` vira `ÔÇö`. Já aconteceu com o vault inteiro. O conteúdo pode ter acento à vontade; o nome, não.
- LF, sem CR.

## Front-end
- **A página pública é servida em `/qualquer-apelido`** — TODO caminho de arquivo tem que ser **absoluto**.
- **CSS é ordem, não especificidade.** Media query nova vem DEPOIS da regra base. Conferir medindo (`getComputedStyle`), não no olho.
- **Componente novo leva CSS próprio.** Reusar classe de outro arquivo do projeto é como o botão laranja das aulas do parceiro nasceu quebrado.
- **Teste de janela mede GEOMETRIA, não classe.** `position:fixed`, cobrir a tela, `z-index` alto.
- `grid-template-columns:1fr` estoura no celular → `minmax(0,1fr)` + `min-width:0`.
- **Escape de XSS (`esc()`)** em todo texto do lojista na página pública **e** em toda mensagem da caixa.
- **`data-ev` sem ouvinte não mede nada.** O `mvmetrica.js` não faz delegação — cada página traz o seu próprio ouvinte inline. Copiar o atributo sem copiar o ouvinte deixa o CTA mudo no GA4.
- **Foto de usuário entra como `background-image`**, nunca como `<img>` dentro de elemento que também recebe `textContent`.
- Gate de plano inclui `enterprise` em **todos** os gates.
- **Botão que muda estado muda o rótulo junto.**
- **Upload sem barra de progresso vira arquivo duplicado.**
- **HEIC/HEIF do iPhone sobe e não abre** — recusar na entrada.
- **Ação sem volta pede confirmação DIGITADA**, não `confirm()`.
- **Busca de pessoa procura por nome, apelido e e-mail.**
- **Um vídeo de cada vez.** Começar um para todos; as funções de navegação param antes de trocar a tela; varredura pós-clique mata o que saiu da tela.
- **`<script type="module">` é adiado** e sobrescreve no `window` o que um script clássico embrulhou antes. Amarrar mais de uma vez, de forma idempotente.
- **Página montada no navegador não pode ser auditada por leitura de HTML.** O HTML estático traz todas as seções, inclusive as ocultas. A verdade é o `updateTime` do documento.
- **Painel `index.html` tem 2 escopos isolados** (module e comum). `node --check` não pega erro de escopo.

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

## Conformidade e credibilidade
- **Descreva a REGRA, nunca o RESULTADO.**
- **Conformidade tem que chegar até a página do FORMULÁRIO.**
- **Antes de instalar rastreador, ler a própria política de privacidade.**
- **Autorização permanente:** achou violação de Meta/Google, conserta direto.
- **Opt-in de um lugar não vale para outro.** O `autorizaDivulgacao` autoriza a vitrine social, **não** o filme institucional. Material que exibe tela do produto sai de **conta demo própria**, nunca de cliente real.
- **Selo só vale quando existe quem NÃO tem.** Selo que todo mundo ganha não informa nada.
- **Nada de nível, medalha ou ranking de parceiro** — é a estética exata do multinível.
- **Número que ninguém contou destrói o resto.** Quando o lojista percebe que um número não bate, ele deixa de acreditar em todo o painel.
- **A página de verificação protege antes de vender.** O bloco que diz *"você não paga nada a ele"* vem **antes** de qualquer botão. Verificação que vende antes de proteger vira propaganda — e aí não serve nem para vender.
- **Quando não confirma, a página não acusa ninguém.** E se a rede cair, diz que o problema é nosso — jamais "não é parceiro".

## IA e atendimento
- **Robô que fala com o cliente nasce DESLIGADO, conversa a conversa.**
- A resposta nunca nasce como `'admin'` — sem `'bot'`, não há como separar robô de gente depois.
- **Nome de gente é só para gente.** Os cinco atendentes valem apenas para `de:'admin'`; o robô continua assinando "Vik - assistente". Nome humano em resposta automática faz a pessoa achar que falou com alguém quando não falou — destrói autoridade em vez de construir.
- **Nome de atendente é determinístico, nunca sorteado.** Sorteio mudaria o nome a cada F5 e o lojista veria um nome enquanto o dono veria outro na MESMA mensagem.
- **Prompt não é trava de segurança.** Filtro em código também.
- **Ativação antes de venda.**

## Vídeo e narração
- **Texto de vídeo nunca cita a quantidade de itens de uma lista que pode crescer.** Falar da lista, nunca do número. **Vídeo não se corrige com um deploy.** *(A P00 dizia "oito aulas"; no dia em que ela mesma subir, viram dez.)*
- **Dicionário de pronúncia é por motor de voz.** O `PRONUNCIA` do `narrar.py` foi feito para o Kokoro; trocando a voz, ele não vale mais.
- **O áudio é a fonte de verdade quando a narração foi regravada** — a estrutura fica no roteiro, a redação final está no áudio.
- **O link do YouTube é o identificador da aula.** Refazer gera **id novo**. **Nunca apagar o antigo antes de o painel apontar para o novo.**
- **Nunca gravar tela com dado real** — valor, nome de cliente, e-mail de terceiro, chave Pix. Não listado ≠ privado.
- **Título de vídeo é honesto.** Vídeo que cobre parte da tela mantém título estreito.
- **Nenhuma geração antes da bíblia visual escrita e aprovada.**
- **Keyframe still primeiro, vídeo depois.** Uma cena por vez, sem variação automática.
- **Em image-to-video, o `first_frame` governa a POSIÇÃO; o prompt só governa o MOVIMENTO.**
- **Física não se conserta por prompt.** Objeto que atravessa objeto só tem uma solução: remover o objeto.
- **Veo aceita 4, 6 ou 8 segundos. 5 s não existe.**
- **Timeout do MCP não significa geração cancelada** — ela continua e é cobrada. Conferir por `get_credits` + `list_my_gallery` antes de retentar.
- **Toda UI do filme é captura real.** Nunca gerar interface, logo ou pino por IA.
- **Asset ausente é PENDENTE, não improviso.**
- **Prioridade que decide empate:** qualidade cinematográfica > consistência > eficiência de créditos > velocidade.

## Testes
- **Dry-run valida conteúdo; só a publicação real valida integração.**
- Sandbox do Claude não alcança CDN nem emulador do Firebase. O que funciona: stubs de Leaflet/Firestore/Auth/Storage, `python3 -m http.server`, Playwright no Chromium local. **O emulador de regras NÃO roda** — regra se confere à mão.
- **O sandbox não alcança o HuggingFace**: não dá para baixar modelo de transcrição. **Áudio entregue só se confere por medição** (duração, loudness, silêncio, formato) — conteúdo e pronúncia dependem do Paulo ouvir e confirmar.
- Clique sintético no Playwright precisa de `cancelable:true`.
- Checkbox de switch é invisível (`opacity:0;width:0`) — clique no trilho (`.swT`).
- `node --check` não pega erro de escopo.

## Ligações
[[ARQ - Furos nas regras v16]] · [[ARQ - Erros de implementacao 03092026]] · [[ARQ - Entregue e nao subiu 03092026]] · [[ARQ - Auditoria de seguranca 03092026]] · [[ARQ - Incidentes e cacadas de bug]] · [[A3 - Dados e Regras]] · [[R - Historico de regras do Firestore]] · [[R - Verificacao publica de parceiro]]
