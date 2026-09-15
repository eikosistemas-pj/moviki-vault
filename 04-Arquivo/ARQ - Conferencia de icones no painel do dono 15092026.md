---
type: arquivo
status: concluido
area: "[[A1 - Produto e Paineis]]"
tags: [icones, painel-dono, ferramenta, manutencao]
atualizado: 2026-09-15
---

# ARQ - Conferencia de icones no painel do dono 15092026

Fecha [[ARQ - Varredura de icones dos tres paineis 15092026]]. O
`conferir-icones.html` solto na raiz vira um botao dentro do painel do dono.

## Arquivos

| Repositorio | Arquivo | Marca | Tipo |
|---|---|---|---|
| moviki-app | `eikoadm01.html` | 2026-09-15-conferir | SUBSTITUI |
| moviki-app | `conferir-icones.html` | — | **APAGAR** |

Montado sobre a marca `2026-09-12-www1`, que era a que estava no GitHub.

## O resultado da conferencia de 15/09

**49 de 49 no lugar, nenhum faltando.** Os cinco entregues nesta rodada
(`financeiro`, `vender`, `vendas`, `mensagens`, `tutoriais`) ja estavam no ar
quando o Paulo rodou. A questao dos icones fecha aqui.

## Por que o arquivo solto nao fica

O Paulo perguntou se dava para deixa-lo no repositorio para o futuro. Nao:

- **Era publico.** `app.moviki.com.br/conferir-icones.html` abria sem login e
  mostrava a estrutura interna dos tres paineis — `exclusoes`, `comissoes`,
  `parceiros`, `multipontos`. Nao vaza dado de ninguem, mas e reconhecimento de
  graca para quem estiver olhando.
- **Envelhecia em silencio**, que e o defeito grave. A lista dos 49 nomes estava
  escrita dentro do arquivo. No dia em que um painel ganhasse um icone novo, a
  pagina continuaria dizendo "nenhum faltando" — sem ter conferido o novo. Uma
  ferramenta de conferencia que mente e pior que nenhuma.

## Como o botao resolve as duas coisas

Fica em **Atalhos do dono**, atras do login de admin. E **nao tem lista escrita
a mao**: ao clicar, ele busca `index.html`, `parceiro.html` e `eikoadm01.html`
no proprio servidor, tira de cada um os nomes pedidos em `icones/` e testa
arquivo por arquivo. Painel que ganhar icone novo entra na conferencia sozinho,
para sempre.

- Mesma origem, entao o `connect-src 'self'` da CSP ja cobre — nenhuma mudanca
  de cabecalho.
- Cada pedido leva `?v=<agora>`: cache de navegador escondendo arquivo recem
  subido daria falso negativo.
- So le. Nao grava nada, nao chama o robo, nao toca no Firestore.
- Mostra quantos paineis conseguiu ler ("lidos 3 de 3"). Se um falhar, o numero
  denuncia — sem isso, um painel ilegivel viraria "nenhum faltando".
- Lista do que falta com botao de copiar, pronta para colar aqui.

## O que ele nao alcanca

Os icones do **site** (`moviki.com.br/icones-premium/`) ficam de fora. Ler o
HTML de outra origem esbarra em CORS e no proprio `connect-src` da CSP. Se um
dia fizer falta, o caminho e um botao igual dentro do site, nao afrouxar a CSP
do painel do dono.

## Conferido fora do ar

14 verificacoes no Chromium com Firebase de mentira: o botao aparecendo nos
Atalhos, a caixa de faltantes comecando escondida, os **tres paineis lidos
sozinhos**, os 47 nomes descobertos sem nada escrito a mao, uma celula por
arquivo, arquivo existente ficando fora da lista de faltantes, arquivo ausente
entrando nela, e nenhum erro de JavaScript. Balanceamento de `<div>` e
`<section>` conferido contra o original, e o arquivo entregue em **UTF-8 sem
BOM, com LF** — que e exatamente como o `eikoadm01.html` ja estava (diferente do
`index.html`, que exige BOM + CRLF).
