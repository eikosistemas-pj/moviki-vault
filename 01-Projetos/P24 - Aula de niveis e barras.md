---
type: projeto
status: ativo
prioridade: 2
area: A5 - Programa de Parceiros
prazo: 2026-09-15
tags: [parceiros, videoaula, niveis, comissao, conformidade]
atualizado: 2026-09-11
---

# P24 - Aula de niveis e barras

## Resultado esperado
Aula nova no painel do parceiro explicando o card "Seu nível" e as três barras
da calculadora, numa aula só, com a voz Malu.

## Feito em 11/09/2026
- Vídeo `P11-parceiro-niveis.mp4` (2:34, 1080p, legenda queimada) + `.srt`.
  Cena **P11** (P09 = crachá, P10 = conduta).
- Aula NOVA, não substitui a de comissões. Chave `mod-parc-niveis`, módulo
  "Seu nível", embutida no fim do card `#nvCard`.
- `parceiro.html` `2026-09-11-aula-niveis`:
  - barra 1 da calculadora aplica o % do nível (16/17/18% a partir de 26/51/101);
  - linguagem corrigida: "ganhe mais", "ganhe bônus", "todo mês", "sua equipe";
  - slot da aula com id vazio (invisível até o link chegar).
- Narração: 23 falas, 23 créditos Kairogen.

## Definição de pronto
- [ ] `parceiro.html` -> repo **moviki-app**, raiz, SUBSTITUI
- [ ] Vídeo no YouTube, **não listado**, link enviado
- [ ] `parceiro.html` com o id -> repo **moviki-app**, raiz, SUBSTITUI
- [ ] Tabela de videoaulas atualizada

## Consequência conhecida
Com o id no ar, o selo de todo parceiro vira laranja "1 aula nova" e o card
passa a "11 de 12". Ninguém é retrancado (`aulasEm` fica).

## Ligações
[[P19 - Plano de niveis do parceiro]] · [[P20 - Conserto do player e liberacao do link]] ·
[[R - Voz oficial das videoaulas]] · [[A5 - Programa de Parceiros]] · [[R - Marcas de versao no ar]]
