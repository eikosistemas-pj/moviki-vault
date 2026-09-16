---
type: projeto
status: ativo
prioridade: 1
prazo: 2026-10-16
area: A5 - Programa de Parceiros
tags: [prospeccao, parceiro, influenciador, funil, conformidade, midia-paga]
atualizado: 2026-09-16
---

# P37 - Prospeccao de parceiros e influenciadores

> Auditoria do funil do parceiro feita em 16/09/2026 contra o estado no ar, mais
> o plano de acao acordado com o Paulo. **A conclusao: da para arquitetar a
> prospecao agora, nao da para ligar — o que trava e produto e medicao, nao
> anuncio.**

Relacionado: [[A5 - Programa de Parceiros]] ·
[[ARQ - Falso alarme das amplas e Meta pausada 16092026]] ·
[[P16 - Perfil do criador de conteudo no quiz]] ·
[[R - Checklist conformidade Meta e Google]]

---

## 1. As tres travas de produto

1. **`configuracoes/liveTermos.liveBeta` nao foi esvaziada.** A live segue em
   beta fechado. Prospectar com o argumento da live entrega ao lojista um recurso
   que ele assina e nao consegue ligar.
2. **Teste de fumaca da live nunca foi feito** — presenca, denuncia, Vik, card de
   consumo, teto com duas pessoas assistindo.
3. **Zero prova.** Nenhum lojista pagante real, nenhuma live rodada fora da conta
   do Paulo. E a primeira pergunta de qualquer influenciador.

## 2. As sete brechas do funil do parceiro

1. **O funil do parceiro e invisivel para anuncio.** O `novo-parceiro.js` avisa o
   Telegram e nao dispara evento para a Meta — o `Lead` da CAPI so existe no
   `novo-cliente.js`, que e o cadastro de lojista. O GA4 mede o ramo desde 27/08,
   mas GA4 nao otimiza campanha. Campanha de recrutamento rodaria cega.
2. **Nenhuma pagina de parceiro cita a live.** `index.html` e `comerciantes.html`
   foram reposicionadas em 16/09 para live commerce; `parceiros.html`,
   `parceiros-ganhos.html` e `seja-parceiro.html` (marca `2026-09-04`) seguem
   vendendo so mapa.
3. **`parceiros.html` contradiz a si mesma.** O bloco "Como comecar" manda falar
   no WhatsApp; o CTA final manda para o formulario de cadastro.
4. **A friccao pos-cadastro nao e avisada antes.** Aprovacao manual mais 13 aulas
   obrigatorias para destravar a Divulgacao. A trava e correta por CONAR, mas
   descobrir depois do cadastro derruba a ativacao. Tem que estar na landing,
   como filtro de qualidade.
5. **Nao existe material para recrutar parceiro.** As 81 pecas sao para o
   parceiro falar com LOJISTA. Nao ha kit para chamar outro parceiro (`/pp/`) nem
   midia kit de influenciador. E o pacote inteiro esta parado esperando a
   `liveBeta`.
6. **A oferta e igual para todo mundo.** 15% recorrente vale o mesmo para o
   feirante e para quem tem audiencia. Sem uma segunda moeda — cache fixo por
   peca, bonus por ativacao, cupom proprio — a conversa com criador morre no
   preco.
7. **`/v/apelido` esta fora da prospecao.** A pagina de verificacao e o ativo
   anti-golpe mais forte do projeto e nao aparece em argumento nenhum.

## 3. Os cinco videos que faltam

| # | Peca | Por que |
| --- | --- | --- |
| 1 | Video de venda do programa, 60-90s, na `parceiros.html` | a landing nao tem video nenhum |
| 2 | Corte vertical de 30s para DM e story | recrutamento sem promessa de renda |
| 3 | **Live real gravada do inicio ao fim** | unica resposta para "isso funciona?" |
| 4 | Midia kit em video para influenciador | o que pode falar, `#publi`, como o link rastreia, como recebe |
| 5 | Abertura do criador (P16) | desenho aprovado em 06/09, nunca produzido |

Os itens 3 e 4 valem mais que os outros tres juntos.

## 4. Decisao de midia — vale como regra

> **Nao anunciar recrutamento de parceiro na Meta.** Anuncio de comissao por
> indicacao para publico frio e o padrao classico de restricao de conta, e a
> `@moviki.app` **ja foi restringida uma vez**. Influenciador se prospecta 1-a-1:
> DM, e-mail, WhatsApp. Anuncio pago fica para captacao de LOJISTA, que e onde a
> mensalidade entra.

## 5. Plano de acao

### Fase 0 - destravar

- [ ] Subir o pacote `moviki-icones-3d-16092026.zip` (icones antes do HTML)
- [ ] Teste de fumaca da live, com duas pessoas e `tetoMinutosMes = 1`
- [ ] Esvaziar `liveBeta`
- [ ] Subir o material de apoio e revisar a instrucao do Vik na mesma rodada
- [ ] Disparar `Lead` da CAPI no cadastro de parceiro, com `content_name` proprio

### Fase 1 - armar a oferta

- [ ] `parceiros.html` e `seja-parceiro.html` reescritas no eixo live commerce,
      com video, trilha de aulas declarada antes do cadastro e a verificacao como
      argumento
- [ ] Corrigir a contradicao dos passos da `parceiros.html`
- [ ] Gravar a live real com um lojista de verdade em Joao Pessoa
- [ ] Produzir os videos 1, 2 e 4 e a abertura do criador
- [ ] Definir a condicao de influenciador (cache, bonus de ativacao ou cupom)

### Fase 2 - ligar

- [ ] Google: conferir a conversao Inscricao, depois repor saldo, faixa R$ 15-20/dia
- [ ] Meta: religar so quando a `comerciantes.html` nova tiver conversao propria
- [ ] Lista de 20 a 30 criadores locais de Joao Pessoa, abordagem 1-a-1 com o
      video da live real
- [ ] Criterio de parada: 30 dias ou 10 parceiros aprovados, o que vier primeiro

## 6. Feito em 16/09

- Meta pausada (9 dias, zero lead).
- As 3 palavras BROAD do Grupo 1: remocao tentada, Google devolveu
  "Resource was not found" nos tres ids. **Nunca voltaram** — era erro de leitura
  da rotina. Ver [[ARQ - Falso alarme das amplas e Meta pausada 16092026]].
