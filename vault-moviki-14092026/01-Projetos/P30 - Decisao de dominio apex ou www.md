---
type: projeto
status: ativo
area: A2 - Infraestrutura e Deploy
tags: [dominio, vercel, cors, links]
atualizado: 2026-09-14
prioridade: 2
prazo: 2026-09-30
---

# P30 - Decisao de dominio apex ou www

Decidir, de uma vez, qual endereço é o principal do Moviki: `moviki.com.br` ou
`www.moviki.com.br`. Hoje o código e os links apontam para lados diferentes, e
isso já derrubou o estúdio da live uma vez.

## A descoberta de 12/09/2026

Na Vercel, **`moviki.com.br` está configurado como "Redirects to
www.moviki.com.br"**. O domínio principal é o **WWW**; o apex é só um
redirecionamento.

O estúdio não abria, dizendo apenas `(rede)`. Causa: **redirecionamento entre
origens troca a origem do pedido por `null`**, o servidor deixa de reconhecer a
origem e o navegador bloqueia por CORS. Nada estava errado no servidor —
`api/live.js` seguiu em `2026-09-12-beta1` o tempo todo.

Conserto aplicado nos dois arquivos que falam com a API do site:

1. chamar `www.moviki.com.br/api/live` direto, sem salto (o apex ficou de
   reserva);
2. enviar o corpo como `text/plain`, o que dispensa a checagem prévia (OPTIONS)
   que o redirecionamento quebrava;
3. liberar `www.moviki.com.br` na CSP — **este furo só o teste pegou**; trocar o
   endereço sem mexer na CSP trocaria um bloqueio por outro.

O painel do dono tinha o mesmo problema no botão "Encerrar live". Consertado
junto, antes de quebrar.

## O que continua aberto

Os **16 links do site**, os **QR dos crachás** dos parceiros e os **links de
parceiro** apontam para o **apex**. Cada visita paga um salto de
redirecionamento. Pior: QR impresso não se corrige com deploy.

Duas saídas, e só uma pode valer:

| Opção | O que muda | Custo |
| --- | --- | --- |
| Apex vira o principal na Vercel | nada no código; os QR já impressos passam a acertar de primeira | reconfigurar domínio; conferir toda chamada de API, CSP e canonical que hoje assume www |
| Código passa a usar www em tudo | consistência com a configuração atual da Vercel | reescrever 16 links, os crachás e os links de parceiro; QR impresso continua com salto |

## Etapas

- [ ] Levantar todo lugar que grava o endereço: links do site, `canonical`,
      `sitemap.xml`, CSP, crachá do parceiro, link de indicação, materiais
      impressos.
- [ ] Decidir apex ou www, e registrar a decisão como regra de ouro.
- [ ] Aplicar de uma vez só, com a CSP na mesma entrega.
- [ ] Conferir o estúdio da live e o botão Encerrar live depois da mudança.

## Ligações

[[A2 - Infraestrutura e Deploy]] · [[A5 - Programa de Parceiros]] ·
[[R - Links e identificadores]] · [[R - Checklist de deploy]] ·
[[R - Live - Arquitetura e arquivos]] ·
[[ARQ - Modo Live no ar em beta fechado 12092026]] ·
[[R - Live - Exposicao e interruptores do beta]]
