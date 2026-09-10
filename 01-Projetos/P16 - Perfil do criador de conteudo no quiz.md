---
type: projeto
status: ativo
prioridade: 2
prazo: 2026-09-30
area: A5 - Programa de Parceiros
tags: [quiz, parceiro, influenciador, videoaula, onboarding, conar]
atualizado: 2026-09-10
---

# P16 - Perfil do criador de conteudo no quiz

> Nota represada de 05-06/09, nunca subida. O numero **P16 esta livre** no vault
> e fica com este assunto.

## O problema, nas palavras dele

> "Eu entrei como parceiro, e vamos dizer que eu seja influenciador. A parte de
> videoaulas para um influenciador nao precisa ter aquela primeira videoaula do
> parceiro falando da barraca, do carrinho, da tenda."

O diagnostico esta certo. A abertura (`mod-parc-abertura`, P00, 2:54) fala de
feira, carrinho e barraca. Um criador ouve isso na primeira tela e conclui que o
programa nao e para ele. **A dor e real e e de recepcao.**

## O que foi recusado, e por que

Ele propos **duas trilhas separadas de aulas**. Tres furos:

1. **Trilha separada vira atalho.** Se a do criador for menor, todo mundo marca
   "sou criador" para destravar o link mais rapido — e o botao e autodeclarado.
2. **A conduta e MAIS critica para o criador, nao menos.** Quem aciona o CONAR e a
   responsabilidade solidaria e justamente quem publica.
3. **Duas trilhas dobram a manutencao.** Hoje sao 11 aulas; viram 22 pontos para
   atualizar, e uma delas sempre fica velha.

## O desenho aprovado por ele em 06/09

1. **Nucleo comum + abertura dupla**, nao duas trilhas. As aulas obrigatorias que
   destravam o link sao as mesmas para todos, **inclusive a conduta (P10)**.
2. **Nao precisa campo novo no quiz.** A tela `qzB2` ja pergunta *"Onde voce vai
   divulgar o seu link oficial do Moviki?"*, com multi-selecao, e grava em
   `parceiros/{uid}.canais` (`instagram` / `whatsapp` / `associacoes`).
   **Some a regra nova e some mexer no `index.html`.**
3. **Quem marcou `instagram` ve a abertura do criador**, mesmo tendo marcado
   outros. Sem `canais` (parceiro antigo) cai na abertura de campo, que e a de
   hoje.
4. **Ele quer os modulos extras junto**, nao so a abertura.

## A ARMADILHA que o desenho resolve

Os modulos do criador entram marcados como **`extra: true`**, e
`chavesPublicadas()` **ignora extras**. Assim o total obrigatorio continua o mesmo
para todo mundo e a trava segue valida.

**Sem isso, filtrar por perfil derrubaria a contagem abaixo de `MIN_AULAS = 8` e a
trava DESLIGA INTEIRA** — o link abriria para qualquer um sem assistir nada. Quem
mexer no filtro refaz a conta da trava junto.

## Os 5 videos a produzir

| # | Cena | O que ensina |
| --- | --- | --- |
| 1 | abertura do criador | boas-vindas falando de audiencia e conteudo, no lugar de feira e carrinho. **E a dor original dele** |
| 2 | a etiqueta em cada rede | a P10 diz QUE precisa marcar; esta diz ONDE fica no feed, story, Reels e TikTok |
| 3 | o que mostrar na tela do Moviki | quais telas gravar, e o que nunca pode aparecer: dado de cliente real, valor de comissao, painel de outra pessoa |
| 4 | roteiro de 30 segundos | estrutura que funciona sem prometer nada |
| 5 | quando alguem responde no direct | para influenciador a conversao acontece no privado, e e la que a promessa errada escapa |

**Dois modulos foram DESCARTADOS por duplicarem a P10:** "#publi na pratica" e "o
que nunca gravar" — o miolo dos dois ja e a aula de conduta.

**Nada foi gerado ainda.** Regra do projeto: roteiro aprovado antes de qualquer
geracao. Proximo passo: escrever os 5 roteiros num documento so.

## Ressalva de prioridade

Existe **um** parceiro real (Alexandre) mais o cadastro do proprio Paulo
(`paulopj`). Construir duas trilhas completas agora e caro para o tamanho da base.
O minimo que resolve a dor e a abertura certa para cada um.

## Atencao a voz

Os roteiros novos serao narrados pela **Malu** (`fhtZMBwha5du5OxuvexO`), nao mais
pelo padrao de 04/09 — ver [[R - Voz oficial das videoaulas]].

## Ligacoes

[[A5 - Programa de Parceiros]] · [[A1 - Produto e Paineis]] ·
[[A10 - Conformidade e LGPD]] · [[P18 - Aula de conduta do divulgador]] ·
[[R - Voz oficial das videoaulas]]
