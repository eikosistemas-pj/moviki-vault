---
type: projeto
status: ativo
prioridade: 2
area: A8 - Conteudo e Social
tags: [conteudo, video, marca, aquisicao]
prazo: 2026-09-30
atualizado: 2026-08-31
---

# P13 — Video institucional da landing

Filme institucional premium da Moviki para `moviki.com.br`, mais quatro cortes
derivados. Roteiro completo em [[R - Roteiro do video institucional]].

## Resultado esperado

Master de ~74 s no ar em lightbox na landing, loop mudo de 8 s no heroi, e o
banco de cenas alimentando midia paga e o robo social.

## Criterio de conclusao

- [ ] 14 cenas montadas em corte travado (picture lock)
- [ ] Locucao humana gravada **sobre o corte travado**, nunca antes
- [ ] Trilha licenciada com stems + certificado guardado
- [ ] `pin.wav` produzido e reaproveitado no app
- [ ] Master exportado a -14 LUFS / -1 dBTP
- [ ] Hospedado no YouTube nao listado e aberto por lightbox
- [ ] `frame-src https://www.youtube-nocookie.com` publicado na CSP
- [ ] Eventos GA4 do filme disparando (`video_start`, `video_progress`, `video_complete`, `video_cta_click`, `hero_loop_view`)
- [ ] Lighthouse rodado antes e depois; LCP mobile nao piorou mais que 0,2 s
- [ ] Cortes 30 s, 15 s 9:16 e bumper 6 s exportados

## Estado em 2026-08-31

**Todas as 13 cenas com geracao de IA estao aprovadas.** C10 e C14 sao 100%
pos-producao, sem Kairogen. O projeto saiu da fase de geracao e entrou em
**preparacao de pos-producao**.

| Frente | Estado |
| --- | --- |
| Geracao de cenas | ✅ concluida — 1.308 creditos, 150 geracoes |
| Inventario de takes | ✅ [[R - Filme institucional - inventario de takes]] |
| Timeline | ✅ 74,1 s — [[R - Filme institucional - inventario de takes]] |
| Gate de assets | 🟠 aberto — [[R - Filme institucional - gate de assets]] |
| Conta demo para captura de tela | 🔴 **bloqueia C08, C09 e C10** — [[R - Filme institucional - conta demo]] |
| Simbolo/logo vetorial | 🔴 pendente de autorizacao para vetorizar |
| Trilha licenciada | 🔴 nao contratada |
| `pin.wav` | 🔴 nao produzido |
| Locucao | ⏸ so depois do picture lock |

## Bloqueadores, em ordem

1. **Conta demo incompleta.** Sem cardapio com fotos, galeria e promocao na
   pagina publica, as tres cenas de UI real nao podem ser gravadas. Checklist
   campo a campo em [[R - Filme institucional - conta demo]].
2. **Captura de tela nao pode ser feita pelo Claude.** O proxy de egresso nega
   conexao direta a `moviki.com.br` e a sessao nao alcanca o computador do
   Paulo. **A gravacao das telas e manual.**
3. **Simbolo em vetor.** O filme precisa de **duas formas**: pino isolado sem
   disco (para os pinos sobre fotografia em C06/C07/C13) e selo completo (C14).
   A arte oficial entregue tem fundo off-white, nao transparente.
4. **Trilha e `pin.wav`.** Sem eles nao existe mixagem.

## Decisoes ja tomadas

- **Hospedagem:** YouTube nao listado em lightbox. Banda zero, custo zero.
  Consequencia: mexer na CSP.
- **CTA do card final:** `Comecar gratis agora` + `30 dias gratis · Sem cartao
  de credito`.
- **`SEM COMISSAO`:** confirmado como fato de produto, pode entrar em tela.
- **Vik nao aparece** no institucional.
- **Nenhuma UI gerada por IA.** Toda tela e captura real.
- **Nenhum numero, nota ou depoimento** enquanto nao houver base real auditavel.

Registro completo em [[ARQ - Decisoes do filme institucional]].

## Riscos

- **Rosto de IA envelhece mal.** Mitigado por contraluz, perfil parcial e maos
  nos planos medios.
- **LCP da landing.** Regra dura ja definida: se piorar > 0,2 s, o loop sai.
- **Reivindicacao de direito autoral** no YouTube derruba anuncio — guardar o
  certificado da faixa.
- **Placa de marca real legivel** em cena gerada. Falta inspecao quadro a quadro
  de C07 (terco centro-direito) e C13 (metade direita).

## Ligacoes

[[R - Roteiro do video institucional]] · [[R - Filme institucional - biblia visual e continuidade]] ·
[[R - Filme institucional - inventario de takes]] · [[R - Filme institucional - gate de assets]] ·
[[R - Filme institucional - conta demo]] · [[ARQ - Armadilhas de geracao por IA]] ·
[[ARQ - Decisoes do filme institucional]] · [[A8 - Conteudo e Social]] ·
[[A11 - Marca e Design System]] · [[P01 - Aquisicao - campanha de trafego pago]]
