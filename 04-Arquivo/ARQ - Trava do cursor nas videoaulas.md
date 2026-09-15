---
type: incidente
status: concluido
area: A1 - Produto e Paineis
tags: [videoaulas, trava, parceiro, lojista, armadilha, regra-de-ouro]
atualizado: 2026-09-15
---

# A trava do cursor, e o visto verde que sumia — 15/09/2026

Achado pelo Paulo na conta de teste (Karina, Enterprise), testando o
[[ARQ - Ajuste do freio da live - B5a]]. Duas queixas na mesma frase, e as duas
eram defeito de verdade.

Entrega: `moviki-aulas-trava-cursor-15092026.zip` — dois arquivos.

---

## 1. O que ele viu

> "Assisti duas. Quando terminei de assistir a terceira, a primeira e a segunda
> foram marcadas como verde. Mas a terceira nao. Assisti ela duas vezes e mesmo
> assim o card nao ficou verde. E ainda esta aquela situacao que o cliente pode
> adiantar: eu so fui arrastar o cursor e deixei proximo ao final e ja deu como
> concluida."

## 2. O conserto de 10/09 nunca foi trazido para o painel do lojista

Em 10/09 o `parceiro.html` ganhou a medicao por **caminho percorrido**, que
substituiu a medicao por **posicao da agulha**. O `index.html` do lojista
**ficou com a versao antiga** — continuou perguntando `tempo atual / duracao
>= 0,9`, que e exatamente "onde esta o cursor".

⚠️ **REGRA DE OURO:** conserto feito num painel tem que ser conferido no outro
**na mesma rodada**. Os dois carregam o mesmo motor de aulas, copiado; um
conserto que fica so num lado nao e conserto, e divida — e ela cobra cinco dias
depois, com o Paulo achando defeito novo no que ja tinha sido resolvido.

## 3. Por que a aula assistida nao ficava verde

Nao era a mesma causa de 03/09 nem a de 10/09. No painel do lojista, a marcacao
dependia de o iframe continuar **vivo** ate o proximo tique do relogio (1 s).

- chegou nos 90% e trocou de aula antes do tique → **perdeu a aula inteira**;
- a medicao vivia **dentro do iframe**, entao reassistir pela metade **comecava
  do zero** e nunca fechava.

Era esse o "assisti duas vezes e mesmo assim nao ficou verde". Provado no
laboratorio: arrastar e pular em 0,4 s deixa a aula sem marca; as outras, em que
ele esperou, ficaram verdes. Bate com o relato — inclusive com a ordem.

## 4. O furo que sobrava ATE no parceiro

O parceiro media o percurso, sim, mas o estado **ENDED** marcava a aula
**incondicionalmente**:

```
if(e.data===ENDED){ if(!f.__contado){ f.__contado=1; marcar(v.k); } }
```

⚠️ **Quem arrasta a agulha ate o fim cai no mesmo ENDED de quem assistiu
inteiro.** A trava de percurso existia e podia ser contornada em dois segundos —
e e ela que abre a **Divulgacao** do parceiro. Comprovado: no arquivo no ar,
arrastar + deixar acabar marca a aula.

## 5. O motor novo, igual nos dois arquivos

| O que | Como |
| --- | --- |
| Vale o caminho, nao a posicao | a cada 500 ms anota o segundo que toca; o salto so entra se couber no tempo real decorrido (folga 1,6x — **2x continua valendo**) |
| O fim do video nao prova nada | ENDED so fecha a aula se os 90% percorridos ja estiverem la; senao avisa *"Voce adiantou o video"* |
| O percurso nao se perde | fica guardado **por aula** (`PERCORRIDO`), nao por player: trocar, fechar e voltar continua de onde parou |
| O cliente ve o progresso | *"Assistido 63%"* embaixo do video |
| A troca automatica respeita quem adiantou | `acabou()` nao pula para a proxima quando a atual nao contou |

O item do medidor nao e enfeite: **trava sem medidor vira "o sistema esta
quebrado"** na cabeca de quem esta assistindo — e vira chamado no Vik.

## 6. Entrega

| Arquivo | Acao | Marca |
| --- | --- | --- |
| `moviki-app/index.html` | SUBSTITUI | `2026-09-15-aulatrava` |
| `moviki-app/parceiro.html` | SUBSTITUI | `2026-09-15-aulatrava` |

**Envs:** nenhuma. **Regras do Firestore:** nenhuma. O progresso continua em
`negocios/{uid}/estado/boasvindas` (lojista) e `parceiros/{uid}.aulasVistas`
(parceiro).

## 7. Testes — 10/10 no lojista, 5/5 no parceiro

Com Chromium de verdade e um dublê da API do YouTube, medindo tempo real:

arrastar nao conta · ENDED sem percurso nao conta · avisa que adiantou ·
assistir conta · o percurso soma entre idas e vindas · mostra "Assistido N%" ·
2x conta · a troca automatica nao passa por cima · 4 de 4 conclui · grava o
carimbo de conclusao. Mais a checagem de sintaxe do JavaScript dos dois `.html`.

**A mesma bateria rodada nos arquivos que estao no ar reprova em 5 pontos no
lojista e em 2 no parceiro** — e o que prova que o defeito era real.

## 8. O que a varredura encontrou de resto

- O **estudio da live (`live.html`)** nao tem aula nenhuma embutida ainda. As 13
  aulas do Modo Live sao plano, nao codigo — continuam em
  [[P33 - Aulas do Modo Live para o parceiro]].
- Nenhum outro arquivo do projeto carrega o motor de aulas. So estes dois.
- **Quem ja passou adiantando continua passado.** Nao ha migracao: `aulasVistas`
  e `boasvindas.vistas` permanecem como estao. A trava vale daqui para a frente.

## Ligacoes

[[ARQ - Bug do visto verde nas videoaulas 03092026]] ·
[[P33 - Aulas do Modo Live para o parceiro]] · [[A1 - Produto e Paineis]] ·
[[R - Regras de ouro]]
