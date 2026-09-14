---
type: recurso
status: referencia
area: A1 - Produto e Paineis
tags: [vik, atendimento, prompt, catalogo, conformidade]
atualizado: 2026-09-13
---

# R — Vik: catálogo do painel

O que o Vik sabe do painel, de onde vem esse conhecimento e quais travas o
impedem de errar. No ar desde **13/09/2026**.

## Onde mora o conhecimento

| Arquivo | Repo / pasta | Papel |
| --- | --- | --- |
| `catalogoPainel.js` | `moviki-ai` / `lib` | **Fonte única** do conhecimento de produto |
| `promptPainel.js` | `moviki-ai` / `lib` | Só comportamento e travas de conformidade |
| `contextoUsuario.js` | `moviki-ai` / `lib` | O que o Vik sabe da pessoa que está falando |
| `chat.js` | `moviki-ai` / `api` | Injeta o catálogo do papel certo |
| `index.html` / `parceiro.html` | `moviki-app` / raiz | Marca `2026-09-13-vikpainel` |

**Conhecimento de produto e regra de comportamento moram em arquivos
diferentes** — um muda toda semana, o outro quase nunca. Atualizar o Vik virou
um arquivo pequeno, sem encostar nas travas.

Blocos do `catalogoPainel.js`: `PRODUTO` (planos, preços e o gating conferido no
código), `LOJISTA`, `PARCEIRO`, `NAO_EXISTE` e `MARCAS_CONFERIDAS`.

## Catálogo por papel

O painel manda `painel: 'lojista'|'parceiro'` no corpo do pedido e o `chat.js`
injeta **só** o catálogo daquele lado. Sem o campo, vale o que a conta é; sendo
os dois, o prompt manda **perguntar de qual lado é a pergunta** antes de dar o
caminho. O uid continua vindo só do token.

## As travas

1. **Nunca dizer que algo não existe.** Frases proibidas, com a única exceção de
   uma lista fechada (`NAO_EXISTE`). Fora dela: procurar pelo sinônimo que a
   pessoa usou, perguntar em que tela ela está, ou dizer que vai conferir com o
   time. Num produto que muda toda semana, negar derruba a confiança na hora — e
   é evitável por regra, não por atualização em dia.
2. **Detector de catálogo velho.** O painel manda `window.MOVIKI_VERSAO` a cada
   mensagem; divergiu de `MARCAS_CONFERIDAS`, o Vik entra em **modo cauteloso**
   sozinho e o servidor anota em `vik_status/paineis` — coleção nova, sem `match`
   nas regras, só Admin SDK.
3. As travas de conformidade do `promptPainel.js` seguem intactas
   (`lib/segurancaVik.test.js` com 0 falhas na conferência).

## O que o Vik passou a saber

- Telas que faltavam: **Fotos e vídeos**, capa, **Modo Live**, crachá, aulas,
  **material de apoio** e níveis.
- Correções de plano que ele repetia errado: **avaliações são de todos os
  planos** (dizia Premium) e **fotos são do Premium** (dizia Pró), liberadas
  também no **teste grátis** — função `estadoFotos()` do painel.
- Do contexto já lido: foto própria do parceiro, treinamento concluído, aceite da
  conduta, nível e clientes pagantes; do lado do lojista, vídeos, capa e logo do
  pino.
- **Sabe do beta da live:** a única leitura nova é `configuracoes/liveTermos`
  (cache de 5 min) — sem ela o Vik não sabe se aquele lojista enxerga o botão
  **"Fazer live"** (beta fechado).

## O que a conferência achou antes de subir

1. **`MARCAS_CONFERIDAS` nasceu com as marcas antigas** dos painéis — o modo
   cauteloso nasceria ligado para todo mundo.
2. **`aulasEm` é string ISO, não Timestamp** — o Vik diria "treinamento
   concluído" sem a data.

Os seis arquivos foram conferidos clonando os repositórios: byte a byte iguais
ao entregue. Três testes na conta real passaram: a marca responde nos dois
painéis; "onde troco a foto do meu crachá?" leva a **Meus dados > Sua foto >
Trocar foto**; avaliações são respondidas como de todos os planos.

## Custo

Prompt de ~2.700 para ~5.600 tokens (só o catálogo do papel entra). Cerca de
**US$ 0,003 a mais por resposta**, com teto de **40 respostas por conta/dia**.

## Origem

Em 09/09, na caixa do painel do parceiro, o Vik respondeu **"não consigo
localizar uma funcionalidade de 'crachá'"** e ofereceu duas telas do **lojista**.
A memória (`vik_memoria`) guardou o erro como objeção do cliente; o resumo
daquele parceiro foi zerado pelo cartão "O que o Vik aprendeu desta pessoa", no
painel do dono (as mensagens da conversa não são tocadas por esse botão).

## Em aberto

- [ ] `lib/promptAtendimento.js` (WhatsApp) continua com o **catálogo antigo** —
      preço e trava de plano desatualizados. Está em stand-by; quem ligar sem
      revisar liga um atendente que fala errado.
- [ ] `seja-parceiro.html` parado em `2026-09-04-conta-existente`.
- [ ] `premium.html` sem marca de versão — é a landing do tráfego pago.

## Ligações

[[A1 - Produto e Paineis]] · [[A13 - Modo Live]] ·
[[A14 - Material de apoio do parceiro]] ·
[[R - Live - Exposicao e interruptores do beta]] ·
[[ARQ - Modo Live no ar em beta fechado 12092026]] ·
[[R - Planos e precos]] · [[R - Colecoes do Firestore]] ·
[[R - Marcas de versao no ar]]
