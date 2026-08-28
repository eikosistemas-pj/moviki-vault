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

3. Autenticação: **Personal Access Token** do GitHub (fine-grained, só o repo `moviki-vault`, permissão Contents: Read and write). Usuário = seu login, senha = o token.

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
