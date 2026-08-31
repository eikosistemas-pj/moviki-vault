---
type: recurso
status: referencia
area: A8 - Conteudo e Social
tags: [video, marca, conformidade]
atualizado: 2026-08-31
---

# R — Filme institucional: gate de assets

O que precisa existir, em arquivo, antes de comecar o rough cut. Nada nesta
lista pode ser inventado — asset ausente e marcado **PENDENTE** e pedido.
Projeto: [[P13 - Video institucional da landing]].

## Regra do gate

> **Se um asset necessario nao estiver disponivel, marcar como PENDENTE e pedir
> o asset — nunca inventa-lo.**

Nao inventar UI, logo, pino, telas, depoimentos, metricas ou resultados.

## A — Marca

| Asset | Estado | Nota |
| --- | --- | --- |
| Simbolo oficial (pino com ondas) | ✅ recebido | fundo off-white, **nao transparente** |
| Pino isolado, sem disco, com alfa | 🔴 PENDENTE | necessario para pinos sobre fotografia (C06, C07, C13) |
| Selo completo com disco | 🔴 PENDENTE | necessario para C14 |
| Logotipo em vetor | 🔴 PENDENTE | C14 desenha o logotipo da esquerda para a direita |
| Poppins (arquivos da fonte) | ✅ | ja usada no produto |

**Descoberta:** a geometria oficial do pino **ja existe inline** em
`moviki/premium.html` e nao precisa ser redesenhada:

```
path do pino  M80 148c0 0-44-42-44-71a44 44 0 1 1 88 0c0 29-44 71-44 71z
gradiente     #00D4FF -> #0066FF  (linearGradient x1=0 y1=0 x2=1 y2=1)
miolo         circle r=29 fill #04101e
aro           circle r=29 stroke #fff width 2.5
anel de sinal circle r=16 stroke #00D4FF width 2   (classe .anel, ja animada)
```

O miolo do simbolo oficial **nao e a letra M** — e um anel escuro com ponto
ciano. O miolo diferente que aparece no `premium.html` era placeholder de logo
de lojista.

**As ondas de sinal fazem parte do simbolo.** O pulso da C06 anima as ondas do
proprio simbolo, nao aneis desenhados por cima.

## B — Capturas de tela reais

| Cena | Tela | Estado |
| --- | --- | --- |
| C08 | painel do lojista, aba **Local** | 🔴 PENDENTE |
| C09 | pagina publica `/apelido` — mapa, capa, cardapio | 🔴 PENDENTE |
| C10 | promocao + botao de WhatsApp | 🔴 PENDENTE |

**Rota de captura da C08** (`moviki-app/index.html`, aba `#tab-local`):

- `#gpsInfo` = *"Localizacao ainda nao definida."*
- botao `pegarLocalizacao()` = *"Atualizar minha localizacao"*
- `#mvMapaSelo` vira *"Visivel no mapa"*
- `#mvMapaSub` = *"Seu negocio esta no mapa e no seu link. Quem estiver perto pode te encontrar."*

**Rota de captura de C09/C10** (`moviki/404.html`): secoes `#secDestaques`,
`#secPromo`, `#secOnde`, abas Fotos / Avaliacoes / Promocoes / Eventos /
Informacoes, `abrirCardapio()`, `irParaAba()`.

**Armadilha:** o modo `?demo=1` da pagina publica imprime selo **EXEMPLO** nos
blocos vazios. **Inutilizavel para o filme.** A conta demo tem que estar de
verdade preenchida — ver [[R - Filme institucional - conta demo]].

**A captura e manual.** O proxy de egresso do ambiente do Claude nega conexao
direta a `moviki.com.br`, e a sessao nao alcanca o computador do Paulo. Nao
existe caminho automatizado.

## C — Audio

| Asset | Estado | Especificacao |
| --- | --- | --- |
| Trilha licenciada com stems | 🔴 PENDENTE | ~92 BPM, sem vocal, maior; **guardar o certificado** |
| `pin.wav` | 🔴 PENDENTE | pop de sub + brilho agudo, ~220 ms |
| Locucao humana | ⏸ so apos picture lock | feminina, 32–42, PT-BR neutro, medio-grave |
| Ambientes e SFX | 🔴 PENDENTE | rua ao entardecer, chapa, notificacao abafada, clique haptico |

## D — Conformidade

| Item | Estado |
| --- | --- |
| Nenhum numero, nota ou depoimento em tela | ✅ regra travada no roteiro |
| Nenhuma promessa de resultado | ✅ regra travada no roteiro |
| Nome do estabelecimento em tela nao e MOVIKI nem marca real | 🟠 conferir na conta demo |
| Telefone pessoal fora de quadro | 🟠 conferir na conta demo |
| Atribuicao do provedor de mapa | 🔴 conferir antes de publicar |
| Licenca da trilha arquivada | 🔴 PENDENTE |

**LGPD:** o opt-in `autorizaDivulgacao` do produto **nao cobre o filme**. Ele
promete *"Nunca publicamos seu endereco exato — so a cidade"*, e o filme mostra
o mapa. Por isso a captura sai de **conta demo propria**, nunca de cliente real.

## E — Entrega

| Asset | Estado |
| --- | --- |
| `hero-loop.webm` + `.mp4` + poster WebP | 🔴 depende do picture lock |
| `institucional.mp4` + `.webm` | 🔴 depende do picture lock |
| `institucional-pt.vtt` | 🔴 depende da locucao |
| Cortes 30 s / 15 s 9:16 / bumper 6 s | 🔴 depende do master |

## Ligacoes

[[R - Roteiro do video institucional]] · [[R - Filme institucional - conta demo]] ·
[[R - Filme institucional - inventario de takes]] · [[P13 - Video institucional da landing]] ·
[[R - Checklist conformidade Meta e Google]] · [[A10 - Conformidade e LGPD]]
