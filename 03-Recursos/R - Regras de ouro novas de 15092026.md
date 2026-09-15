---
type: recurso
status: ativo
area: A1 - Produto e Paineis
tags: [regra-de-ouro, apendice, live, videoaulas, git]
atualizado: 2026-09-15
---

# Regras de ouro novas — 15/09/2026

⚠️ **Apendice de [[R - Regras de ouro]].** Fica separado porque o arquivo
principal nunca chegou integral aqui — substituir sem ele apagaria o que ja
existe. **Fundir na proxima vez que o `R - Regras de ouro.md` for entregue.**
O apendice anterior e `R - Regras de ouro novas de 11 a 14092026`.

---

## 1. Regra do Firestore nao tem "deny"

> Quando varios `match` casam com o mesmo caminho, o acesso e concedido se
> **qualquer um** permitir. Um `match` especifico com `allow write: if false`
> **nao tira** o que um curinga acima ja concedeu.

Custou quase a correcao inteira da sessao da live: a colecao ia nascer em
`negocios/{uid}/estado/liveSessao`, onde o curinga `match /{documento=**}` da
escrita ao dono — a trava teria virado enfeite. Foi para a **raiz**.
Origem: [[ARQ - Sessao da live no servidor]].

## 2. O Console do Firebase nao tem mais simulador de regras

> O botao **"Desenvolver e testar"** hoje so oferece o pacote de emuladores.
> Para provar uma regra contra o ar, subir uma **pagina temporaria** que tente
> a escrita e a leitura logado — e que **inicialize o App Check**, senao tudo e
> negado pelo motivo errado e o teste da um falso "esta protegido".

Origem: [[ARQ - Sessao da live no servidor]].

## 3. Validar a sintaxe do JavaScript DENTRO dos `.html`, nao so dos `.js`

> Identificador repetido derruba o arquivo **inteiro**, nao so a linha. Uma
> declaracao `const` de algo que ja existia no modulo deixou o estudio preso em
> "Carregando...". Os `.js` tinham sido checados; os `.html`, nao.

Origem: [[ARQ - Incidente - estudio preso em carregando]].

## 4. Duas barreiras com a mesma mensagem escondem qual das duas disparou

> Quando dois freios diferentes recusam com o mesmo texto, o diagnostico fica
> impossivel. Cada barreira tem que dizer **quem** barrou e **por quanto tempo**.

O freio da live tinha um limite em memoria (1 a cada 20 s) e um contador duravel
(3/min). A mensagem falava do segundo; quem barrava era o primeiro. So se
descobriu porque o Paulo contou o numero da tentativa.
Origem: [[ARQ - Ajuste do freio da live - B5a]].

## 5. Encerrar de proposito nao e abuso

> Freio de abuso nao pode punir quem usa o produto direito. Quem fecha a live e
> quer reabrir esta operando, nao atacando — o contador do minuto zera no
> encerramento. Hora e dia continuam somando, e o laco de script ainda morre.

Origem: [[ARQ - Ajuste do freio da live - B5a]].

## 6. Conserto feito num painel tem que ser conferido no outro NA MESMA RODADA

> O painel do lojista e o do parceiro carregam o mesmo motor de videoaulas,
> **copiado**. Um conserto que fica so num lado nao e conserto, e divida — e ela
> cobra dias depois, com o dono achando que e defeito novo.

A medicao por caminho percorrido foi feita no `parceiro.html` em 10/09 e nunca
chegou ao `index.html`. Origem: [[ARQ - Trava do cursor nas videoaulas]].

## 7. O fim do video nao prova que a pessoa assistiu

> Quem arrasta a agulha ate o fim cai no mesmo estado `ENDED` de quem assistiu
> inteiro. Medir **caminho percorrido**, nunca posicao do cursor — e o `ENDED` so
> fecha a aula se o percurso ja estiver la.

E o par disso: **trava sem medidor vira "o sistema esta quebrado"** na cabeca de
quem assiste. Quando se trava, mostra-se o progresso.
Origem: [[ARQ - Trava do cursor nas videoaulas]].

## 8. Progresso medido dentro do player morre com o player

> Guardar o quanto foi assistido dentro do iframe faz o cliente perder tudo ao
> trocar de aula ou fechar a tela. O progresso pertence a **aula**, nao ao
> player.

Origem: [[ARQ - Trava do cursor nas videoaulas]].

## 9. Arquivo de codigo so pode conter texto imprimivel

> Um byte de controle gravado no lugar do seu escape roda igual, **some do diff
> do Git** (o arquivo vira binario) e morre no primeiro editor que passar.
> Varrer bytes abaixo de 0x09, entre 0x0e e 0x1f, e 0x7f antes de entregar.

Grave aqui porque o Paulo trabalha **so pela interface web do GitHub**: sem
diff, ele perde a unica conferencia visual que tem.
Origem: [[ARQ - Bytes de controle no livesessao]].

## Ligacoes

[[R - Regras de ouro]] · [[P35 - Auditoria de seguranca do Modo Live]] ·
[[A13 - Modo Live]] · [[A1 - Produto e Paineis]]
