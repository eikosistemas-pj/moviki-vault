---
type: area
status: ativo
tags: [produto]
atualizado: 2026-08-28
---

# A1 — Produto e Painéis

## Padrão a manter
O que a tela promete, o banco entrega. **Número inventado é propaganda enganosa.** Onde a arte pede um dado que não existe, não se inventa o dado — troca-se o rótulo.

## O que está no ar
**Lojista:** login/cadastro, verificação de e-mail, onboarding em 3 passos, painel como casca de aplicativo, cardápio 2.0, promoções, eventos, galeria (12 fotos), avaliações, WhatsApp, localização, status aberto/fechado, informações (horário, endereço, entrega, preço médio), card "Seu desempenho", caixa de mensagens.

**Página pública `/apelido`:** herói + faixa de unidades + promoção + destaques do cardápio + mapa Leaflet + abas Fotos/Avaliações/Promoções/Eventos/Informações. Respiro lateral por `--gut` (14→22→36→56→80px). Favorito por localStorage, geolocalização só se já liberada, pinos numerados, busca de unidade a partir de 6, badge "mais perto". Modo demonstração `?demo=1`.

**Painel do parceiro:** 7 seções + a 8ª "Falar com o Moviki".
**Painel do dono (`eikoadm01.html`):** 13 seções.

## Regras de ouro desta área
- `grid-template-columns:1fr` estoura no celular → use `minmax(0,1fr)` com `min-width:0` nos filhos.
- **CSS é ordem, não especificidade.** Media query nova vem DEPOIS da base. Conferir medindo (`getComputedStyle`), não no olho.
- Botão que muda estado **muda o rótulo junto**. Interruptor ligado dizendo "Desligado" custa mais confiança que um bug.
- Busca de pessoa procura por **tudo que ela usa para se identificar**: nome, apelido do link, e-mail. Só por nome falha no primeiro uso real.
- Upload sem barra de progresso vira arquivo duplicado. Barra **e** trava no botão.
- HEIC/HEIF do iPhone sobe e não abre → recusar na entrada com a instrução (Ajustes › Câmera › Formatos › "Mais compatível").
- Ação sem volta pede confirmação **digitada**, não `confirm()`.
- `index.html` do painel tem 2 escopos isolados (module e comum). `node --check` não pega erro de escopo.
- Gate de plano inclui `enterprise` em **todos** os gates.

## O que a arte pedia e NÃO entrou, por não existir dado
"Alcance", "Como encontraram você", rosca "+18% vs semana anterior", atividades recentes, modo escuro, "Nível do parceiro/Diamante".

## Projetos vinculados
[[P07 - Aviso de mensagem nova para o lojista]] · [[P12 - Metricas por ponto no Enterprise]]

## Recursos
[[R - Planos e precos]] · [[R - Marcas de versao no ar]] · [[ARQ - Redesign 2.0 (Fases 0 a 6)]]
