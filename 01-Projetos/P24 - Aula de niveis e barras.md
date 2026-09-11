---
type: projeto
status: concluido
prioridade: 2
area: A5 - Programa de Parceiros
prazo: 2026-09-15
tags: [parceiros, videoaula, niveis, comissao, conformidade]
atualizado: 2026-09-11
---

# P24 - Aula de niveis e barras

## Resultado
Aula nova no painel do parceiro explicando o card "Seu nível" e as três barras
da calculadora, numa aula só, com a voz Malu. **No ar em 11/09/2026.**

| | |
| --- | --- |
| Cena | `P11-parceiro-niveis` (P09 = crachá, P10 = conduta) |
| YouTube | `6E3z6cbOXJ4`, não listado |
| Duração | 2:34 |
| Chave | `mod-parc-niveis`, módulo "Seu nível" |
| Onde aparece | fim do card `#nvCard` (visão geral) e tela de aulas |
| Versão do painel | `parceiro.html` `2026-09-11-aula-niveis-id` |

## O que veio junto no parceiro.html
- Barra 1 da calculadora aplica o % do nível (16/17/18% a partir de 26/51/101).
- Linguagem corrigida: "ganhe mais", "ganhe bônus", "todo mês", "sua equipe".
- Narração: 23 falas, 23 créditos Kairogen.

## Definição de pronto
- [x] `parceiro.html` com o slot -> moviki-app, raiz
- [x] Vídeo no YouTube, não listado
- [ ] `parceiro.html` com o id -> moviki-app, raiz, SUBSTITUI
- [x] Tabela de videoaulas atualizada

## Consequência conhecida
Parceiros já formados veem "11 de 12" e o selo "1 aula nova". Ninguém é
retrancado (`aulasEm` fica). Parceiro novo precisa das 12 para abrir o link.

## Ligações
[[P19 - Plano de niveis do parceiro]] · [[P20 - Conserto do player e liberacao do link]] ·
[[R - Voz oficial das videoaulas]] · [[A5 - Programa de Parceiros]] · [[R - Marcas de versao no ar]]
