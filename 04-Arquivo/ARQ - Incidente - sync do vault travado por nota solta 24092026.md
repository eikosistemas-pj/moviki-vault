---
type: incidente
status: contornado
area: A2 - Infraestrutura e Deploy
tags: [vault, git, sync, incidente]
atualizado: 2026-09-24
---

# ARQ - Incidente - sync do vault travado por nota solta

## Sintoma (24/09/2026, 19:54)

O `SincronizarVaultMoviki.bat` distribuiu a nota e parou no GIT:
`The following untracked working tree files would be overwritten by merge` com 5 notas `04-Arquivo/ARQ - ... 22092026.md` (criador). Nada foi enviado.

## Causa

As 5 notas estavam na pasta do vault **sem commit** e **já existiam no GitHub**, que chegaram por outro caminho. O git não apaga arquivo solto para trazer o do GitHub, então o `pull` aborta. Enquanto isso, toda nota nova distribuída fica solta também: o bloqueio se acumula.

**Falha de desenho do `.bat`:** ele distribui (copia para o vault) **antes** de puxar o GitHub. Se o pull falha, o que foi copiado fica solto, e basta a mesma nota chegar ao GitHub por outro caminho para travar tudo.

## Conserto

- `ConsertarVaultMoviki.bat` (uso único): `fetch`; nota solta igual à do GitHub é apagada; diferente vai para `Área de Trabalho\_conflitos-vault\<data>`; `pull --rebase --autostash`; envia as soltas que o GitHub não tem; termina com `git status -sb`. Testado reproduzindo o erro exato.
- Pendente: corrigir o `SincronizarVaultMoviki.bat` para **puxar antes de distribuir** e aplicar a mesma regra das soltas. Precisa do arquivo atual.

## Regra

Script de sync puxa o remoto **antes** de escrever qualquer coisa na pasta. Erro decidido por `$LASTEXITCODE`, nunca por texto no stderr (ver [[ARQ - Incidentes e cacadas de bug]]).

## Ligações

[[R - Sync do vault Obsidian Git]] · [[ARQ - Incidentes e cacadas de bug]]
