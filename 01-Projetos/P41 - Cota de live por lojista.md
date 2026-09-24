---
type: projeto
status: ativo
area: A13 - Modo Live
tags: [live, cota, custo, video, cloudflare, oferta, conformidade]
prioridade: 1
prazo: 2026-10-15
atualizado: 2026-09-23
---

# P41 - Cota de live por lojista

> Versão de venda da cota de vídeo por lojista, entregue em **19/09/2026**.
> **Estado: entregue, conferir se subiu.** O prazo é o início da cobrança do
> WebRTC no Cloudflare Stream: **15/10/2026**.

## O que ficou fechado

| | Premium | Enterprise | Teste grátis |
| --- | --- | --- | --- |
| Duração por live | 60 min | 180 min | 60 min · 2 lives |
| Espectadores simultâneos | **30** | **100** | **15** |
| Minutos de vídeo por ciclo | **3.000** | **10.000** | **300** |
| Tolerância acima de 100% | 20% | 20% | 20% |

O ciclo renova **todo dia 12** (ciclo de faturamento do Cloudflare, não o mês-calendário).

## Como a conta é feita

- Mora em `moviki-robo/lib/livesessao.js`. **A conta é nossa, não do Cloudflare.**
- A cada pulso (45 s) o servidor conta a presença (`negocios/{uid}/livepresenca`, últimos 100 s) e soma `espectadores × tempo` em `live_cota/{uid}` (`cicloVideo`, `minutosVideo`, `tetoVideo`).
- Live sem ninguém assistindo não gasta. **O número de espectadores nunca vem do navegador do lojista.**
- O limite de espectadores é gravado em `live_sessoes/{uid}.maxEspectadores` na abertura — mudança no painel vale a partir da PRÓXIMA live.

## O que acontece em cada ponto

| Momento | O que acontece |
| --- | --- |
| 80% | aviso no estúdio |
| 100% | a live em andamento **continua**; aviso com quanto resta e quando vira o ciclo; **a próxima live fica barrada** no `live_reservar` |
| 100% + 20% | a live cai com mensagem de limite — **nunca a de moderação** (campo `motivo`) |
| Queda de sinal dentro da tolerância | reconecta se for dentro da carência de 15 min e abaixo do corte |
| Espectador acima do limite | vê **"Live lotada"**, não grava presença, entra sozinho quando abre vaga. Quem já entrou nunca é expulso |
| Antes de entrar ao vivo | o estúdio mostra o saldo (`live_saldo`): minutos usados, pessoas, dia da renovação |

## Onde se ajusta, sem deploy

Painel do dono > Lives > **Teto de vídeo por plano** — `tetoVideoPremium/Enterprise/Trial`, `espectadoresPremium/Enterprise/Trial`, `toleranciaVideo` em `configuracoes/liveTermos`. **Vazio = padrão do código; zero = sem limite.**

## Onde o limite está escrito (é oferta)

`premium.html`, `enterprise.html`, checkout do `moviki-app/index.html` e **Termos 6-D**. Sem "ilimitado" em lugar nenhum (CDC arts. 30 e 35). **Subir limite é livre; baixar exige trocar o texto antes e avisar quem já assinou com 30 dias.**

## Achado da rodada

O teto por plano **já estava no código desde 16/09** (1.500 · 5.000 · 300). O handoff de 18/09 pedia para construir o que já existia. Também se corrigiu o estúdio, que chamava de **infração** o encerramento por limite.

## Arquivos entregues em 19/09

| Repo | Arquivo | Marca entregue |
| --- | --- | --- |
| moviki-robo | `lib/livesessao.js` | `2026-09-19-cotalive` |
| moviki | `api/live.js` | `2026-09-19-cotalive` |
| moviki | `live.html` | `2026-09-19-lotada` |
| moviki | `premium.html` · `enterprise.html` · `termos.html` | `2026-09-19-cotalive` |
| moviki-app | `live.html` | `2026-09-19-cotalive` |
| moviki-app | `eikoadm01.html` | `2026-09-19-cotalive` |
| moviki-app | `index.html` | `2026-09-19-cotalive` |

**Nenhuma regra nova do Firestore** — tudo que a cota grava é Admin SDK.
Eventos GA4 novos: `live_lotada` e `live_encerrada_limite`.

## Para fechar

- [ ] Conferir no GitHub se as marcas acima subiram
- [ ] Testar lotação e tolerância (duas contas assistindo, teto baixo no painel)
- [ ] Ensinar a cota ao Vik (`moviki-ai/lib/catalogoPainel.js`)
- [ ] Pôr os limites na tabela da `/aovivo`
- [ ] Conferir o teto GLOBAL real no painel (12.000 no mapa antigo, 50.000 no vault)
- [ ] Alerta de cobrança no Cloudflare antes de 15/10
- [ ] Pacote de minutos extras: **só depois do 1º lojista pagante real**
- [ ] Rever o bônus B do funil de criadores (R$ 50) contra a margem do Premium com live ativa (≈ R$ 37 no teto)

## Ligações

[[A13 - Modo Live]] · [[P24 - Modo Live - lancamento]] ·
[[P39 - Remuneracao do influenciador e midia dos parceiros]] ·
[[R - Regras de ouro novas de 17 a 23092026]] ·
[[R - Marcas de versao no ar em 19 a 23092026]]

*Reconstruída em 23/09/2026 a partir do MAPA-MESTRE de 23/09. O roteiro de teste detalhado de 19/09 não chegou ao vault.*
