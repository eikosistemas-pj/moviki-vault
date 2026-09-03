---
type: incidente
status: ativo
area: A2 — Infraestrutura e Deploy
tags: [deploy, armadilha, infra]
atualizado: 2026-09-03
---

# ARQ — Entregue e não subiu, 03/09/2026

Conferência feita no fim do dia 03/09, clonando os três repositórios e comparando
arquivo por arquivo com o que o Mapa Mestre afirma.

**O mapa está certo sobre o que foi PRODUZIDO. O repositório diz o que está NO AR.
Nesta rodada os dois se separaram** — parte da rodada da credibilidade foi entregue e
nunca subiu.

O próprio mapa avisa, na seção 10: *"as marcas em negrito valem para os arquivos
entregues"*. Entregue não é o mesmo que no ar.

## Últimos commits conferidos

| Repositório | Último commit |
| --- | --- |
| `moviki` | 03/09, 16h35 |
| `moviki-app` | 03/09, **15h35** |
| `moviki-robo` | 03/09, 14h07 |

O `moviki-app` parou às 15h35 — **antes da rodada da noite**. É de lá que vem quase
todo o descompasso.

## O que ESTÁ no ar, conferido no código

- Página de verificação `moviki/v.html`, marca `2026-09-03-verificacao-appcheck`,
  com App Check, CSP e medição dos CTAs.
- Rota `/v/:slug` no `vercel.json`.
- Regras **v20** publicadas (confirmado pelo Paulo no Console).
- `moviki-robo/lib/espelhoParceiro.js` e `lib/instagram.js`.
- `parceiro.html`: os cinco atendentes, o selo do certificado, a chamada
  `?espelho=1` e a foto do parceiro vinda da busca do @.
- `eikoadm01.html`: os cinco atendentes.
- `404.html`: o selo "Atualizado hoje" na página pública do negócio.
- App Check presente nas **8** páginas que falam com o Firebase.
- `authDomain` do painel do lojista continua `app.moviki.com.br`.

## O que NÃO está no ar

**1. O crachá com QR code.** `mvQR` não existe em nenhum arquivo dos dois
repositórios. O `parceiro.html` publicado tem uma única menção a crachá, e ela está
dentro de um comentário. **Consequência séria:** a página `/v/{apelido}` está no ar e
funcionando, mas **nenhum parceiro tem crachá para mostrar** — a peça que leva o
comerciante até lá não existe. A verificação virou uma porta sem corredor.

**2. Os cinco atendentes no painel do LOJISTA.** `moviki-app/index.html` não tem a
lista `ATENDENTES`. O painel do dono e o do parceiro têm; o do lojista, não. Hoje o
dono responde assinando "você - Karina" e **o lojista recebe sem nome nenhum** — o
oposto do que a mudança existe para fazer.

**3. O rodapé institucional no painel do lojista.** O CNPJ não aparece no
`moviki-app/index.html`.

## As marcas de versão estão mentindo

Esta é a parte que mais custa tempo depois. Três arquivos ganharam conteúdo novo e
**ficaram com a marca antiga**:

| Arquivo | Marca no ar | Marca que o mapa afirma | Conteúdo novo? |
| --- | --- | --- | --- |
| `moviki/404.html` | `2026-09-03-appcheck` | `2026-09-03-frescor` | **sim** (selo "Atualizado hoje") |
| `moviki-app/parceiro.html` | `2026-09-03-appcheck` | `2026-09-03-cracha` | **em parte** (sem o crachá) |
| `moviki-app/eikoadm01.html` | `2026-09-03-appcheck` | `2026-09-03-atendentes` | **sim** (os atendentes) |
| `moviki-app/index.html` | `2026-09-03-authdominio` | `2026-09-03-atendentes` | **não** |

Diagnosticar por marca, aqui, dá a resposta errada nos quatro casos.

## A regra de ouro que nasce daqui

> **Marca de versão só vale se sobe junto com o conteúdo.** Arquivo que ganha
> funcionalidade e mantém a marca antiga é pior que arquivo sem marca nenhuma: ele
> afirma um estado falso, e o diagnóstico começa no lugar errado.

> **"Entregue" e "no ar" são estados diferentes, e só o repositório sabe qual é qual.**
> Documento registra o que foi produzido. Antes de dar uma rodada por encerrada,
> conferir o código publicado — não a lista de arquivos entregues.

## O que fazer

1. Achar, no chat da rodada da credibilidade, os arquivos finais do `parceiro.html`
   (com `mvQR`), do `index.html` e do `eikoadm01.html` do `moviki-app`, e o
   `404.html` do `moviki`.
2. Subir os quatro.
3. Conferir ao vivo pelo `MOVIKI_VERSAO` — as marcas novas só valem depois disso.
4. Só então marcar [[P16 - Rodada da credibilidade]] como concluído.

## Ligações

[[P16 - Rodada da credibilidade]] · [[P14 - Verificacao de parceiro]] · [[R - Marcas de versao no ar]] · [[R - Regras de ouro]] · [[A2 - Infraestrutura e Deploy]]
