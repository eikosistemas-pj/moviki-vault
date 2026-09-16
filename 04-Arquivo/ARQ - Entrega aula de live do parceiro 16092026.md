---
type: arquivo
status: concluido
area: A14 - Material de apoio do parceiro
tags: [parceiro, videoaulas, live, entrega, parceiro-html]
atualizado: 2026-09-16
---

# ARQ - Entrega aula de live do parceiro 16092026

Fecha a rodada aberta em [[ARQ - Aula de live do parceiro sai da gaveta]].
Detalhe e roteiro em [[P33 - Aulas do Modo Live para o parceiro]].

## Arquivos entregues

| Repo | Pasta | Arquivo | Ação | Marca nova | Montado sobre |
| --- | --- | --- | --- | --- | --- |
| moviki-app | / | `parceiro.html` | SUBSTITUI | `2026-09-16-liveparc2` | `2026-09-16-caticones` |
| — | — | `mod-parc-live.mp4` + `.srt` | vídeo novo | — | — |

## O que mudou no painel

- Módulo **Venda ao vivo** (obrigatório, sem `sel`) com a aula `mod-parc-live`,
  id **`H1vk5wAil78`**, 2:23. A trava da Divulgação passou de 12 para **13**.
- Módulo **Conhecer o estúdio por dentro**, com `opcional:true` e as 14 aulas
  do lojista.
- Motor: `obrigatorios()` e `opcionais()` novos; `todas()`, `quantos()` e
  `chavesPublicadas()` passam a enxergar só os obrigatórios; `extras()` guarda
  os opcionais; a tela de aulas ganhou faixa própria para o módulo opcional,
  com contador separado; `acabou()` avança dentro da lista certa.
- Progresso: `aulasVistas` passa a guardar também as chaves opcionais, no mesmo
  array, **sem regra nova do Firestore**. A conclusão (`aulasEm`) continua
  contando só as obrigatórias.

## Decisões que viram regra

1. **Módulo opcional é a saída para aula de aprofundamento.** Dali em diante,
   publicar aula nova deixa de ser imposto sobre a ativação do parceiro.
2. **Os ids das 14 aulas da live estão em dois lugares:** `liveaulas.js` e o
   catálogo do `parceiro.html`. Id trocado num tem que ser trocado no outro.
   O `parceiro.html` **não** carrega `liveaulas.js` de propósito — aquele
   script traz o motor do estúdio junto.
3. **Roteiro vive em um documento só.** O handoff aponta para ele, nunca copia.

## Prova de não-regressão — contagens no arquivo entregue

```
parceiro.html   MOVIKI_TUTORIAIS=2  aulasEm=9  catalogo.json=3  MvLiveAulas=0
index.html      não tocado
```

`node --check` nos 9 blocos de script do HTML: **0 erro**. Zero byte de
controle. LF preservado.

## Testado em Chromium, com dublê da ponte do Firebase

| Cenário | Resultado |
| --- | --- |
| Tela de aulas com o catálogo novo | contador **0 de 13**, 27 itens na lista |
| Faixa do módulo opcional | "Opcional · Conhecer o estúdio por dentro (0 de 14)" |
| Assistir **uma opcional** | contador e selo não mudam · cadeado continua · chave **é salva** |
| Assistir as 12 obrigatórias | 12 de 12 · cadeado cai · selo "Aulas em dia" · a opcional continua salva |
| Selo do parceiro novo | "Conclua as 13 para liberar o seu link" |
| Parceiro já formado (`aulasEm`) | "1 aula nova · seu link continua liberado" — **não retranca** |

## Produção do vídeo

- Voz **Malu**, dez blocos, 20 créditos Kairogen. 2:23 no total. YouTube não
  listado: `H1vk5wAil78`.
- Cenas: cartelas e mockup em HTML/CSS na identidade do painel, gravadas quadro
  a quadro em Chromium a 25 fps. **Não** é captura do estúdio real — a aula do
  parceiro é conceitual, ele não opera a live.
- Conformidade conferida no quadro: nenhuma promessa de resultado, nenhum
  endereço de site escrito, "30 DIAS DE PRÓ" com acento, mockup com
  "Atualizado agora", rodapé "recurso do plano Enterprise" na cena do Pix,
  conta de demonstração.

## O que fica pendente

- [ ] `moviki-ai/lib/catalogoPainel.js`: `MARCAS_CONFERIDAS` do parceiro para
      `2026-09-16-liveparc`, mais a descrição do módulo de aulas da live no
      painel do parceiro. **Sem isso o Vik entra em modo cauteloso de novo.**
- [ ] Subir as peças de live do material de apoio — agora podem, porque a aula
      de conformidade existe.

## Ligações

[[P33 - Aulas do Modo Live para o parceiro]] ·
[[ARQ - Aula de live do parceiro sai da gaveta]] ·
[[A14 - Material de apoio do parceiro]] · [[R - Marcas de versao no ar]] ·
[[R - Regras de ouro]]
