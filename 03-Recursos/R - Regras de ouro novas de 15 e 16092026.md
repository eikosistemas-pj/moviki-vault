---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [regra, armadilha, live, video]
atualizado: 2026-09-16
---

# R - Regras de ouro novas de 15 e 16092026

Segundo apêndice de regras de ouro. Nasceram em 15 e 16/09/2026 e ainda **não**
estão em [[R - Regras de ouro]]. O apêndice anterior é
[[R - Regras de ouro novas de 11 a 14092026]].

## Bancada de gravação

- **Relógio falsificado governa o JavaScript, não a mídia.** `<video>`, áudio e
  animação CSS correm no tempo real da máquina. Numa bancada lenta, a diferença
  entre os dois relógios é o fator de aceleração do resultado.
- **`seeked` não quer dizer "pintado".** Depois de todo seek, esperar dois
  `requestAnimationFrame` antes de capturar, ou um quadro em cada dois sai com a
  imagem anterior.
- **Vídeo sem `Range` não é seekable.** Rota própria que serve mídia responde
  **206**, ou `video.seekable.end(0)` devolve `0` e todo seek é ignorado em
  silêncio.
- **Ativo gerado com fps errado que "fica bom" esconde defeito de motor.** Quando
  o motor for consertado, o ativo quebra — e o conserto parece o culpado.
- **Medir a folga da tela antes de gravar, no sub-seletor certo.** Painel que não
  cabe e página que não rola saem com corte no quadro, e isso só se vê no vídeo
  pronto.
- **Escolha de narração é por bloco, nunca por leva inteira.** Regravar um bloco
  não deve obrigar a usar a leva inteira daquele bloco.

## Interface do painel e do estúdio

- **O painel re-embrulha suas próprias funções em `setInterval`.** Wrapper posto
  por cima some sozinho. Para reagir a troca de aba, usar **listener de clique** —
  o DOM não se reescreve, o wrapper sim.
- **Trava só reabre o que ela mesma fechou.** Botão fechado por duas causas
  diferentes precisa guardar a autoria, ou a trava menor reabre o que o
  interruptor mestre derrubou de propósito.
- **Alerta de novidade se mede por data, nunca por contagem.** Contar o que falta
  mistura "nunca viu" com "foi acrescentado depois" e acusa de atraso quem está
  em dia.

## Entrega e conferência

- **Lista de pendências herdada de outra sessão se confere no código, nunca no
  texto da lista.** Item escrito antes de uma entrega continua escrito depois
  dela.
- **Pacote de outra sessão se confere abrindo no navegador, não lendo o diff.**
  O CSS do diff não diz onde o elemento cai na tela.
- **Bloco de `<head>` se injeta depois de limpar o que já existe**, e o corte da
  limpeza para no primeiro `<script>` ou `<style>`.
- **`replace` com string expande `$&`, ``$` `` e `$'`.** Conteúdo escrito por
  usuário entra por **função de substituição**, sempre.
- **Marca de versão errada com conteúdo certo é pior que arquivo sem marca.**
  Conferir a marca no repositório depois de subir, não no arquivo que foi
  entregue.

## Ligações

[[R - Regras de ouro]] · [[R - Regras de ouro novas de 11 a 14092026]] ·
[[R - Regras de ouro de producao de video]] · [[R - Marcas de versao no ar]] ·
[[ARQ - Incidente - camera e animacoes aceleradas na bancada]] ·
[[ARQ - Previa do link da live no WhatsApp 15092026]] ·
[[ARQ - Modulo de aulas da live com trava 15092026]]
