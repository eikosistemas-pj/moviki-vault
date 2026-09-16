---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [regra, armadilha, live, video, entrega]
atualizado: 2026-09-16
---

# R - Regras de ouro novas de 15 e 16092026

Segundo apendice de regras de ouro. Nasceram em 15 e 16/09/2026 e ainda **nao**
estao em [[R - Regras de ouro]]. O apendice anterior e
[[R - Regras de ouro novas de 11 a 14092026]].

## Bancada de gravacao

- **Relogio falsificado governa o JavaScript, nao a midia.** `<video>`, audio e
  animacao CSS correm no tempo real da maquina. Numa bancada lenta, a diferenca
  entre os dois relogios e o fator de aceleracao do resultado.
- **`seeked` nao quer dizer "pintado".** Depois de todo seek, esperar dois
  `requestAnimationFrame` antes de capturar.
- **Video sem `Range` nao e seekable.** Rota propria que serve midia responde
  **206**, ou `video.seekable.end(0)` devolve `0` e todo seek e ignorado em
  silencio.
- **Ativo gerado com fps errado que "fica bom" esconde defeito de motor.**
- **Medir a folga da tela antes de gravar, no sub-seletor certo.**
- **Escolha de narracao e por bloco, nunca por leva inteira.**

## Interface do painel e do estudio

- **O painel re-embrulha suas proprias funcoes em `setInterval`.** Wrapper posto
  por cima some sozinho. Para reagir a troca de aba, usar **listener de clique**.
- **Trava so reabre o que ela mesma fechou.** Botao fechado por duas causas
  diferentes precisa guardar a autoria.
- **Alerta de novidade se mede por data, nunca por contagem.**
- **Faixa que rola sem dizer que rola esconde conteudo.** (16/09) Barra de
  rolagem escondida sem esmaecido na borda faz o usuario concluir que o que
  esta fora da tela nao existe. E o esmaecido so aparece **medindo depois de
  pintar** — nunca por suposicao.
- **Emoji nao e imagem.** (16/09) E um caractere que cada sistema desenha do seu
  jeito, e some em Windows antigo. Interface que precisa ser igual para todo
  mundo usa PNG, com o emoji escondido atras como reserva.

## Travas e seguranca

- **Regra do Firestore nao tem "deny".** Varios `match` que casam somam
  permissoes. Colecao de autoridade vai para a **raiz**.
- **Trava silenciosa precisa de tela.** (16/09) Mecanismo que se protege sozinho
  sem mostrar **o que decidiu e por que** e indistinguivel de mecanismo
  quebrado. Custou um teste inteiro no teto de video e dois dias de modo
  cauteloso do Vik.
- **Falha aberta se declara, se justifica e fica sozinha.** (16/09) O projeto
  tem **uma** trava que falha aberta — o teto de video — porque depende de um
  terceiro fora do caminho critico. Toda outra falha fechada. Falha aberta que
  ninguem escreveu e bug.
- **Criptografia nao resolve problema de custo.** (16/09) Token por espectador
  nao contem prejuizo quando o endpoint que emite o token e publico. O que
  contem prejuizo e **teto**, que e configuracao.
- **Ciclo de faturamento de fornecedor nao e o mes-calendario.** (16/09) Medir
  do dia 1 da o numero errado todo mes.

## Compartilhamento e previa

- **Web Share API com arquivo nao leva texto junto.** (16/09) O WhatsApp no
  Android **descarta o arquivo** quando recebe `files` + `text`, e **aceita** o
  share sem avisar. Um dos dois, nunca os dois.
- **O crawler de previa le o HTML antes de rodar JavaScript.** (16/09) Metatag
  funciona ate em pagina que so redireciona.
- **Dado estruturado se gera a partir do HTML visivel, nunca se escreve a
  mao.** (16/09) Texto da tela muda e a marcacao fica para tras — e a pagina
  passa a afirmar ao Google uma coisa que nao mostra ao visitante.
- **Numero em mockup e promessa.** (16/09) Mockup usa numero pequeno e
  plausivel, ou nenhum.

## Entrega e conferencia

- **Lista de pendencias herdada de outra sessao se confere no codigo, nunca no
  texto da lista.**
- **Pacote de outra sessao se confere abrindo no navegador, nao lendo o diff.**
- **Bloco de `<head>` se injeta depois de limpar o que ja existe.**
- **`replace` com string expande `$&`, `` $` `` e `$'`.** Conteudo de usuario
  entra por **funcao de substituicao**, sempre.
- **Marca de versao errada com conteudo certo e pior que arquivo sem marca.**
- **Antes de corrigir a segunda vez, gerar o artefato com o codigo que esta no
  ar e medir.** (16/09) Duas correcoes seguidas no mesmo numero quase sempre
  significam que a primeira nunca chegou a ser vista — e o culpado costuma ser
  **cache do navegador**.
- **Painel que sobe, tabela de marca do Vik sobe junto, na MESMA rodada.**
  (16/09) Marca velha ali nao quebra nada: degrada tudo, devagar e sem ruido.
- **Comentario no codigo que descreve ausencia envelhece na hora.** (16/09)
  "Este arquivo ainda nao existe" vira mentira no minuto em que o arquivo sobe.
  Comentario que fala de estado se corrige na mesma rodada que muda o estado.

## Ligacoes

[[R - Regras de ouro]] · [[R - Regras de ouro novas de 11 a 14092026]] ·
[[R - Regras de ouro de producao de video]] · [[R - Marcas de versao no ar]] ·
[[R - Teto de gasto de video no Cloudflare]] ·
[[ARQ - Incidente - camera e animacoes aceleradas na bancada]] ·
[[ARQ - Previa do link da live no WhatsApp 15092026]] ·
[[ARQ - Modulo de aulas da live com trava 15092026]] ·
[[ARQ - Teto de gasto de video no ar 16092026]] ·
[[ARQ - Conferencia do material de apoio 16092026]] ·
[[ARQ - Incidente - modo cauteloso do Vik ligado sem aviso]]
