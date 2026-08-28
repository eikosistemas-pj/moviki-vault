---
type: recurso
status: referencia
area: A2 — Infraestrutura e Deploy
tags: [infra, meta]
atualizado: 2026-08-28
---

# R — Sync do vault (Obsidian Git)

O vault vive em **`github.com/eikosistemas-pj/moviki-vault`** (privado). A raiz do repositório **é** a raiz do vault — o Obsidian Git roda `git` na pasta do cofre, então o vault não pode estar numa subpasta.

## Instalação, uma vez

1. Obsidian → **Configurações → Plugins da comunidade → Procurar** → `Obsidian Git` → Instalar → Ativar.
2. **Configurações → Obsidian Git**:

| Opção | Valor | Por quê |
| --- | --- | --- |
| Vault backup interval (minutes) | **10** | commit + push automático |
| Auto pull on startup | **ligado** | pega o que outra máquina subiu |
| Commit message | `vault: {{date}}` | histórico legível |
| Pull before push | **ligado** | evita conflito |

3. Autenticação: **Personal Access Token** do GitHub (fine-grained, só o repo `moviki-vault`, permissão Contents: Read and write). Usuário = seu login, senha = o token. Alternativa mais simples no Windows: o **Git Credential Manager** abre o login no navegador.

## ⚠️ Antes do primeiro commit: identidade do git

**Git recém-instalado não sabe quem você é e recusa qualquer commit.** O plugin do Obsidian falha com um aviso vermelho em inglês, cortado, na barra de baixo — fácil de confundir com "o sync não funcionou".

Uma vez por máquina, no Prompt de Comando:

```
git config --global user.email "suporte@moviki.com.br"
git config --global user.name "eikosistemas-pj"
```

Nenhum dos dois responde nada. **Silêncio é sucesso.** Ver [[ARQ - Incidentes e cacadas de bug]].

## O caminho que funcionou no Windows

O comando `Git: Clone an existing remote repo` do plugin **falha em silêncio quando o cofre não está vazio** (o `.obsidian` já existe). O que funcionou foi clonar por linha de comando, preservando a config e os plugins:

```
cd /d "D:\PROJETO MOVIKI\COFRE OBISIDIAN MOVIKI\Moviki"
git init
git remote add origin https://github.com/eikosistemas-pj/moviki-vault.git
git fetch origin
git checkout main
```

E o plugin **exige o Git instalado no Windows** (2.29+, de git-scm.com). Ele não traz o próprio, e o GitHub Desktop não substitui.

## O atalho do dia a dia: `SincronizarVaultMoviki.bat`

Na Área de Trabalho. Um duplo clique: pega os `.md` e `.zip` soltos, **reconstrói o nome que o navegador mutilou**, roteia pela pasta certa lendo o prefixo, mostra NOVO/SUBSTITUI, faz commit e push, e arquiva os originais em `_enviados-vault\<data_hora>`.

O que ele não reconhecer, **deixa na Área de Trabalho e avisa** — nunca move às cegas. E o `git add` é só dos arquivos que ele copiou: não commita `.obsidian` nem carrega junto alterações suas em andamento.

## Regras deste vault no git

- **Nunca commitar chave, token ou service account.** Chaves vivem só na Vercel e nos Secrets do GitHub. Um vault versionado é um lugar perigoso para copiar segredo "só para lembrar".
- `.obsidian/workspace.json` está no `.gitignore` — ele muda a cada clique e polui todo commit.
- Plugins e temas também estão ignorados. Se quiser o mesmo setup em duas máquinas, remova essas duas linhas do `.gitignore`.
- Conflito de merge no Obsidian Git aparece como marcador `<<<<<<<` dentro da nota. Resolver na própria nota e commitar.

## Como o Claude lê

O repositório é a **6ª fonte GitHub** na Base de Conhecimento do Project "Moviki", com filtro excluindo `.obsidian/`.

**Consequência:** o que não foi commitado, o Claude não vê. Nota escrita e não sincronizada é nota invisível — o intervalo de 10 minutos existe para essa janela ser curta.

## Limitações aceitas neste desenho

- **Leitura, não escrita.** O Claude lê o vault; para alterar uma nota, ele entrega o arquivo e você commita — mesmo fluxo dos 5 repos de código.
- **RAG, não índice.** A busca é por relevância semântica da Base de Conhecimento, não por `type`/`status`/`area` do frontmatter.

Se essas duas doerem, o próximo passo é o **MCP remoto próprio** (BM25, busca por frontmatter, backlinks, escrita pela API do GitHub) — decisão registrada, não executada.

→ [[LEIA-ME - Como usar este vault]] · [[R - Stack e repositorios]]
