---
type: projeto
status: ativo
area: A13 - Modo Live
tags: [live, videoaulas, producao]
atualizado: 2026-09-14
prioridade: 2
prazo: 2026-09-30
---

# P28 - Videoaulas do Modo Live

Produzir os treze vídeos do módulo de videoaulas do Modo Live e ligá-los.
A estrutura já está pronta, conferida no navegador e no ar. Falta só o vídeo.

## Estado

- `moviki-app/liveaulas.js` no ar, marca `2026-09-13-liveaulas1`.
- Motor do estúdio no ar, marca `2026-09-14-aulas-beta`.
- Nenhuma aula tem `id` — e **aula sem `id` não aparece em lugar nenhum**, então
  nada quebra enquanto os vídeos não existem.
- Durante o beta as aulas só aparecem para quem está na lista `liveBeta`.

## Etapas

- [ ] Montar as peças novas do estúdio Playwright: câmera falsa no Chromium
      (`--use-fake-device-for-media-stream`), `api/live.js` de mentira devolvendo
      nível e endereços, vídeo local no lugar do WebRTC do Cloudflare e uma
      segunda aba gravando a tela de quem assiste. **Esta é a maior parte do
      trabalho.**
- [ ] Gerar as treze narrações com a voz Malu (`fhtZMBwha5du5OxuvexO`), em falas
      curtas, com a grafia **Mo-víki** no texto que vai para o motor.
- [ ] Montar os treze `.mp4` mais os `.srt`.
- [ ] Paulo sobe no YouTube como **não listados** e manda os links.
- [ ] Preencher `id` e `d` de cada aula em `liveaulas.js` — só esse arquivo muda.
- [ ] Atualizar o documento de videoaulas no ar na mesma entrega.
- [ ] Conferir no ar: contador certo no botão Aulas, caixa em cada aba, visto
      verde na segunda aula (o defeito clássico) e nenhuma aula abrindo com a
      live no ar.

## Travas a respeitar na gravação

- Nenhum valor, nome ou documento real entra no quadro nas aulas que mostram o
  Pix.
- Nenhum roteiro promete resultado; todos descrevem a regra ou a ferramenta.
- Nenhum roteiro diz quantas aulas ou quantas ferramentas existem.
- A aula 7 é a única que fala um número (a tarifa fixa do Asaas por Pix
  recebido). Se a tarifa mudar, é a única a refazer.

## Risco

A aula 7 depende da decisão do [[P29 - Teto de 10 subcontas no Asaas]]: se a
tarifa ou o pedido mínimo mudarem antes da gravação, grava-se errado. Gravar a
7 por último.

## Ligações

[[A13 - Modo Live]] · [[R - Live - Videoaulas do modulo]] ·
[[R - Voz oficial das videoaulas]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[P29 - Teto de 10 subcontas no Asaas]] · [[P24 - Modo Live - lancamento]]
