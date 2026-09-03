---
type: incidente
status: concluido
area: Moviki
tags: [moviki, incidente, qrcode, instagram, licao]
atualizado: 2026-09-03
---

# ARQ - Erros de implementacao 03092026

Dois defeitos da rodada da noite. Os dois tinham o mesmo formato: **o codigo parecia
funcionar e mentia sobre o proprio estado.** Ficam registrados pela licao, nao pelo
conserto.

## 1. O erro da busca do @ se disfarcava de resposta normal

**Sintoma:** a busca do @ subiu, e `@natgeo`, `@nasa` e `@spotify` voltavam
"nao achei esse @ como conta profissional". O Paulo testou conta atras de conta
achando que o problema eram elas.

**Causa raiz:** duas, empilhadas.

**(a) O `IG_USER_ID` estava errado.** A instrucao mandava copiar a "Identificacao" em
Configuracoes do Negocio > Contas do Instagram. **Aquele e outro numero para a mesma
conta.** O que a Graph API usa sai de `1312620718595159?fields=instagram_business_account`.

**(b) E o erro mentia.** A v1 classificava a recusa da Meta lendo a *mensagem* com
expressao regular, e `"does not exist"` cabia tanto no perfil procurado quanto **na
nossa propria conta**. Entao um erro de configuracao nosso aparecia na tela como
"essa conta nao e profissional" - o diagnostico exatamente invertido.

**Conserto:** classificar pelo **codigo** do erro (`id_errado`, `token`, `permissao`,
`nao_profissional`), **sempre** registrar a mensagem crua no log, e um modo de
diagnostico protegido pelo `CRON_SECRET` que devolve a resposta crua da Meta e ignora
o cache. O cache ganhou carimbo de versao, que invalida sozinho o que a versao
anterior gravou errado.

**Licao:** quando um erro nosso e uma resposta legitima chegam pelo mesmo caminho,
ler a mensagem com expressao regular e chute. **Classifique por codigo, e registre o
cru sempre - log economizado e diagnostico perdido.**

## 2. O QR code lia "por sorte" com o nivel de correcao errado

**Sintoma:** o gerador de QR escrito a mao (a CSP do painel nao deixa carregar
biblioteca de fora). As versoes 1 a 3 decodificaram de primeira num leitor real. As
versoes 4, 5 e 6 nao liam.

**Causa raiz:** o fluxo de bytes estava **identico** ao de uma implementacao de
referencia - codificacao, divisao em blocos, Reed-Solomon e intercalacao, tudo certo.
O defeito eram **16 modulos, todos na area de informacao de formato**: estava escrito
o nivel de correcao **L** onde era **M** (os dois bits do nivel M sao `00`, e estava
`01`).

**O que assusta:** as versoes pequenas **ainda liam**, porque o corretor de erros do
leitor compensava. Num celular de verdade, com camera pior, podiam nao ler. Se o teste
tivesse parado em "decodificou, esta bom", o cracha ia pra rua quebrado.

**Conserto:** dois bits. E a verificacao passou a comparar a matriz **modulo por
modulo** com uma implementacao de referencia - da v3 a v6 saem 100% identicas.

**Licao:** **"funcionou uma vez" nao e prova.** Onde existir implementacao de
referencia, compare com ela em vez de confiar no resultado observado.

## O que os dois tem em comum

Nos dois casos o sistema **respondia normalmente** e o sintoma apontava para o lugar
errado - as contas do Instagram, no primeiro; nada, no segundo. Sistema que erra
gritando custa uma hora. Sistema que erra em silencio custa a tarde, e as vezes vai
para producao.

Ver [[P16 - Rodada da credibilidade]] e [[R - Regras de ouro]].
