---
type: projeto
status: ativo
area: A14 - Material de apoio do parceiro
tags: [parceiro, videoaulas, live, trava, gaveta, conformidade]
prioridade: 2
prazo: dia do lancamento do Modo Live
atualizado: 2026-09-15
---

# P33 — Aulas do Modo Live para o parceiro

Dar ao parceiro o conhecimento da venda ao vivo **sem transformar o painel dele
num curso de estúdio** e **sem expor a live antes do dia D**.

Continua [[A14 - Material de apoio do parceiro]] · depende de
[[P28 - Videoaulas do Modo Live]] e de [[P24 - Modo Live - lancamento]] ·
irmão de [[P32 - Material de apoio da live para o parceiro]].

---

## 1. A resposta técnica pedida: o que o teste grátis dá de live

Conferido em 15/09/2026 lendo `moviki/api/live.js` e `moviki-app/live.html` —
não de memória.

| Pergunta | Resposta no código |
| --- | --- |
| Quantas lives no teste grátis? | **Não existe limite de quantidade.** Nenhum contador de lives por dia, semana ou mês em nenhuma camada |
| O que limita, então? | **A duração de cada live.** `NIVEIS.premium.limiteMin = 60` → 1 hora por transmissão |
| Sacolinha no teste | **5 produtos** (`sacolaMax: 5`) |
| Pix dentro da live no teste | **Não.** Pix é `ehEnterprise`, sem exceção para teste |
| Por quanto tempo | Os **30 dias** do teste grátis, 1x por conta |
| Enterprise, para comparar | 180 min por live, sacolinha de 20, Pix ligado |

**A frase certa para o parceiro falar:** *"No teste grátis você já pode fazer
live, quantas quiser, de até uma hora cada, com até cinco produtos na sacolinha.
Receber por Pix dentro da live é do plano Enterprise."*

### Duas armadilhas achadas ao conferir

1. **O teste grátis é vendido como "30 dias de Pró", mas na live ele entra como
   Premium** (`if (periodo === 'trial') return NIVEIS.premium`). O parceiro que
   ler a tabela de planos vai dizer que não tem live no teste — e vai estar
   errado. A aula precisa dizer isso com todas as letras.
2. **O teto de 60 minutos só existe na tela do estúdio** (`limiteMin*60` no
   relógio do `live.html`), não no servidor. Já está registrado como pendência
   em [[P24 - Modo Live - lancamento]]. **Consequência para esta nota:** a aula
   fala "até uma hora" como regra do plano, nunca como trava técnica — e nenhuma
   peça de divulgação promete "live ilimitada".

---

## 2. A crítica ao plano original

A ideia do Paulo em 15/09: *uma aula de introdução para o parceiro e, depois
dela, jogar o parceiro para assistir a sequência de aulas que já foi produzida
para o cliente.*

A primeira metade está certa. A segunda, do jeito descrito, quebra três coisas.

### 2.1 A trava da Divulgação passaria de 12 para 25 aulas

`todas()` no `parceiro.html` percorre **todos** os módulos com `id` e a
Divulgação — link, materiais e crachá — só abre com 90% de **todas** elas.
As 13 aulas do Modo Live somam 12 a 13 minutos. Somadas às 12 atuais, o parceiro
novo passaria a precisar de **~25 aulas** para conseguir o próprio link.

É a pior coisa que se pode fazer com a ativação de parceiro: o cadastro acontece
no impulso, e o link é o que transforma impulso em ação. *Aula nova não retranca
quem já tem `aulasEm`* — o estrago é inteiro no parceiro novo, que é exatamente
quem importa.

### 2.2 O parceiro não vai operar o estúdio — ele vende

As 13 aulas ensinam **a fazer live**: virar a câmera, marcar a sacolinha, ligar
o cupom, gravar corte. O parceiro não transmite. Ele precisa saber **o que a
live faz, para quem serve, em que plano está e como falar dela sem prometer
resultado**. Ensinar operação para quem não opera é o caminho mais curto para
ele não assistir nada.

### 2.3 Nada disso pode subir hoje

O Modo Live está em beta fechado por causa do teto de 10 subcontas no Asaas, e a
auditoria de 14/09 registra *"Painel do parceiro e material de apoio: conferido,
zero menções"*. O título de uma aula dentro do `MOVIKI_TUTORIAIS` é **texto do
HTML** — legível por qualquer um que abra o fonte, com ou sem `id` de vídeo.
Subir a estrutura "sem os links" **não é gaveta**: é a mesma porta lateral que
pegou `aovivo.html` e `regras-da-live.html`.

**Vale aqui a mesma decisão da P32: gaveta = fora do repositório.**

---

## 3. A solução — obrigatório curto, opcional profundo

### 3.1 Uma aula nova, e só uma, conta para a trava

`mod-parc-live` — *"A venda ao vivo: o que é e como falar dela"*, ~2:40.
Módulo próprio **Venda ao vivo**, sem `sel` (não existe seção de live no painel
do parceiro), na mesma lógica da abertura e da conduta.

Ela entra na trava porque é a aula que diz **o que não pode ser prometido** sobre
a live — o par exato da `mod-parc-conduta`. Conformidade é sempre obrigatória.

### 3.2 As 13 do lojista entram como módulo OPCIONAL

Módulo **"Conhecer o estúdio por dentro"**, com as mesmas 13 aulas do Modo Live
(os mesmos `id` do YouTube — vídeo não listado embute em qualquer página), com
um aviso de uma linha: *"São as aulas que o lojista vê. Assista se quiser mostrar
o Moviki por dentro na hora da visita."*

**Isso exige uma mudança no motor**, que hoje não sabe a diferença:

- marcar o módulo com `opcional:true`;
- `todas()` e `quantos()` passam a ignorar módulo opcional → a trava e o selo
  continuam contando **13 aulas** (12 atuais + a nova), não 26;
- a tela de aulas mostra o módulo opcional depois dos obrigatórios, com o
  contador separado e sem visto verde puxando cobrança.

O progresso continua em `parceiros/{uid}.aulasVistas` — sem regra nova, porque
as chaves opcionais caem no mesmo array.

**Ganho de quebra:** o motor passa a aceitar qualquer aula de aprofundamento no
futuro sem tocar na trava. Hoje, toda aula nova é um imposto sobre a ativação.

### 3.3 O que a introdução cobre — e o que ela não cobre

| Cobre | Não cobre |
| --- | --- |
| O que o lojista consegue fazer ao vivo, em uma frase | Como operar qualquer aba do estúdio |
| Planos: live no Premium e no Enterprise; Pix só no Enterprise | Preço de tarifa do Asaas (envelhece) |
| O teste grátis com live em nível Premium, 1 h, 5 produtos | Número de lives (não existe limite; não citar número) |
| A objeção "não tenho seguidores" | Promessa de venda, alcance ou faturamento |
| Onde pegar as peças prontas: aba Material de apoio | Qualquer coisa que dependa do link dele estar destravado |
| Que existe um módulo opcional com as aulas do lojista | Quantas aulas existem (a lista cresce) |

---

## 4. O roteiro — `mod-parc-live`

Voz **Malu** (Kairogen). No texto que vai para o motor, "Moviki" vira
**"Mo-víki"**; a legenda e o `.srt` mantêm a grafia certa.

> Agora o Moviki tem venda ao vivo, e isso muda a conversa que você tem com o
> lojista.
>
> Funciona assim: o lojista entra ao vivo pelo próprio celular, direto do painel.
> Sem aplicativo novo, sem estúdio, sem número mínimo de seguidores.
>
> A página dele ganha uma faixa vermelha escrito AO VIVO, e ele tem um endereço
> só da live, para mandar no grupo do bairro e no status.
>
> Quem assiste vê o produto na tela, com o preço, e um botão para pedir. E
> conversa com o lojista pelo chat, na hora.
>
> A venda ao vivo está no Premium e no Enterprise.
>
> E presta atenção nesta parte, porque é a que mais gera dúvida: no período de
> teste, a live já funciona, no nível Premium. Transmissão de até uma hora, com
> até cinco produtos na lista de venda. O lojista pode experimentar antes de
> pagar qualquer coisa.
>
> Receber por Pix dentro da live é do Enterprise. Ali o cliente paga sem sair da
> transmissão, e o dinheiro cai numa conta no nome do lojista. Nunca na conta do
> Moviki.
>
> O Moviki não cobra comissão sobre a venda do lojista.
>
> Agora, o que você não pode falar.
>
> Não prometa venda, faturamento, número de clientes nem alcance. Nem seu, nem
> dele. Você descreve a ferramenta — nunca o resultado.
>
> Não diga que basta ligar a câmera que a audiência aparece. Quem chama o público
> é o lojista, pelo WhatsApp dele, pelo grupo dele, pelos clientes que ele já tem.
>
> E é essa a resposta para a frase que você mais vai ouvir: "mas eu não tenho
> seguidores". Ele não precisa ter. O Moviki é o palco; o megafone ele já tem.
>
> Na aba Material de apoio você encontra as artes, os vídeos e as mensagens
> prontas sobre a venda ao vivo, com o seu link já dentro da legenda.
>
> E se você quiser conhecer a ferramenta por dentro, aqui nas aulas tem um módulo
> opcional com as mesmas aulas que o lojista assiste. Ele não tranca nada: é para
> quando você quiser mostrar o Moviki funcionando, na frente do lojista.

**Tela:** painel do lojista com o botão Fazer live · página pública com a faixa
AO VIVO · tela de quem assiste, com produto e chat · tabela de planos ·
aba Material de apoio do parceiro com as peças da live.

⚠️ **Nenhum valor, nome ou documento real entra no quadro.** Conta de
demonstração, como em toda aula.

---

## 5. Sequenciamento — a correção que economiza uma produção inteira

O plano original produziria a introdução do parceiro **antes** das 13 do lojista.
Isso custa duas montagens do mesmo aparato.

Metade das cenas da introdução é live rodando: câmera falsa no Chromium
(`--use-fake-device-for-media-stream`), `api/live.js` de mentira devolvendo nível
e endereços, vídeo local no lugar do WebRTC do Cloudflare e **segunda aba**
gravando a tela de quem assiste. **Esse aparato é a maior parte do trabalho** —
e é exatamente o mesmo das 13 aulas do lojista.

**Ordem certa: um bloco de produção só, 14 vídeos.**

| Fase | O que | Depende de |
| --- | --- | --- |
| 1 | Aparato Playwright da live (câmera falsa, `api/live.js` de mentira, segunda aba) | — |
| 2 | 13 aulas do lojista → `liveaulas.js` | fase 1 |
| 3 | `mod-parc-live` (introdução do parceiro) | fase 1 |
| 4 | `parceiro.html` com `opcional:true` no motor + os dois módulos novos | fases 2 e 3 |
| 5 | Paulo sobe os 14 no YouTube, **não listados**, e manda os links | fases 2 e 3 |
| 6 | Ids entram em `liveaulas.js` e no `parceiro.html`; `moviki-videoaulas-no-ar.md` atualizado na mesma entrega | fase 5 |
| 7 | **Gaveta** até o dia D | — |

---

## 6. Gaveta e dia D

Nada de live no `parceiro.html` antes do lançamento — **nem título de aula**.

O `parceiro.html` é o arquivo mais disputado do projeto (quatro conversas
entregaram versões dele no mesmo dia em 10/09; a colisão de 11/09 apagou a aba
de material de apoio). Por isso:

- a versão de destino se reconfere **no GitHub, na hora de subir** — hoje está
  `2026-09-15-matcategoria`;
- o arquivo do dia D é montado sobre a marca que estiver no ar **naquele
  momento**, nunca sobre a cópia desta conversa;
- o sintoma da colisão é **silêncio**: a tela abre normal e o recurso não está lá.

**No dia D entram juntos, num movimento só:** `liveaulas.js` com os ids ·
`parceiro.html` com o motor opcional e os dois módulos · as 9 peças da
[[P32 - Material de apoio da live para o parceiro]] · `catalogo.json` com `novo`
zerado nos 17 itens antigos.

---

## 7. Pendências que esta nota abre

- [ ] Decidir se o teto de 60 min sobe para o servidor antes de a live ser
      divulgada pelo parceiro (hoje só na tela) — [[P24 - Modo Live - lancamento]]
- [ ] Corrigir a comunicação "teste grátis = Pró" onde ela conflita com a live
      em nível Premium (tabela de planos, Vik, `aovivo.html`)
- [ ] Montar o aparato Playwright da live (fase 1) — é o gargalo real de tudo
- [ ] `parceiro.html`: flag `opcional` em `todas()`, `quantos()` e na tela de aulas

## Ligações

[[A14 - Material de apoio do parceiro]] · [[A13 - Modo Live]] ·
[[P24 - Modo Live - lancamento]] · [[P28 - Videoaulas do Modo Live]] ·
[[P32 - Material de apoio da live para o parceiro]] ·
[[R - Live - Arquitetura e arquivos]]
