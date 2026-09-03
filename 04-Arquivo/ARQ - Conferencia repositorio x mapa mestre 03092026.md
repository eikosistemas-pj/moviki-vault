---
type: decisao
status: concluido
area: A2 — Infraestrutura e Deploy
tags: [infra, deploy, armadilha, meta]
atualizado: 2026-09-03
---

# ARQ — Conferência repositório × mapa mestre, 03/09/2026

Os 6 repositórios foram clonados e conferidos contra o mapa mestre das 15h56 de 03/09. Motivo: o projeto avançou vários dias por outra conta do Claude, e o mapa foi atualizado só em parte.

**Conclusão: o projeto está íntegro e pode continuar.** O que estava desalinhado era a documentação, não o código — com duas exceções, viradas em projeto ([[P14 - Verificacao de parceiro]] e [[P15 - Enforcement do App Check]]).

## O que bateu

- 5 repositórios de código clonáveis anonimamente. **`moviki-vault` é privado** — chega ao Claude só pela Base de Conhecimento, não por clone.
- `moviki-robo/api`: **12 arquivos, no teto do plano Hobby**, confirmado. Nada novo cabe lá.
- `moviki-ai`: 2 funções, `chat.js` e `atendimento.js`.
- Marcas de versão do GitHub batem com a tabela do mapa nas 7 páginas listadas.

## As dez divergências encontradas

O arquivo de regras anexado ao Project é a **v20**, não a v19 — o mapa parava na v19. Além disso, não constavam do mapa:

1. `moviki/v.html` — a página de verificação de parceiro, já no ar
2. a coleção `parceiros_publicos`
3. `moviki-robo/lib/espelhoParceiro.js`
4. `moviki-robo/lib/instagram.js` — busca do @ no cadastro do parceiro
5. `moviki-robo/lib/meta.js` — a Conversions API
6. a rota `/v/:slug` no `moviki/vercel.json`
7. `moviki/excluir-conta.html` + `api/excluir-conta.js` + `api/exclusoes.js`
8. `moviki-app/404.html` (`2026-08-28-404vik`), fora da tabela de versões
9. `moviki/sitemap.xml` e `moviki/robots.txt`
10. oito variáveis de ambiente em uso e não documentadas — `IG_TOKEN`, `IG_USER_ID`, `IG_API_VERSION`, `META_API_VERSION`, `META_TEST_CODE`, `FIREBASE_STORAGE_BUCKET` no robô; `CHAT_ORIGENS` e `ANTHROPIC_TIMEOUT` no `moviki-ai`

Corrigido junto: o mapa dizia que o projeto Vercel do site "usa zero função das 12" — usa **uma**, o `api/og.js`.

## Achados que viraram trabalho

| Achado | Onde foi parar |
| --- | --- |
| `v.html` sem App Check, sem CSP, com CTAs não medidos | corrigido em 03/09 · [[P14 - Verificacao de parceiro]] |
| Enforcement bloqueado pelo `og.js` | [[P15 - Enforcement do App Check]] |
| Nenhuma porta de entrada para o `/v/` no site | [[P14 - Verificacao de parceiro]] |
| `moviki/moviki-ui.css` é cópia byte a byte de `movikiui.css`, órfã | [[P09 - Faxina do repositorio moviki]] |
| `css/moviki-3d.css` e `js/moviki-3d.js` órfãos | [[P09 - Faxina do repositorio moviki]] |
| `premium.html` sem marca de versão | [[R - Marcas de versao no ar]] |

**O `moviki-ui.css` merece nota:** nome com hífen já subiu a landing crua uma vez. Uma cópia idêntica, com o nome errado, parada na raiz, é a armadilha esperando ser referenciada por engano.

## As duas lições

> **O mapa mestre não é o repositório.** Quando o trabalho acontece em outro lugar — outra conta, outra sessão — a única conferência que vale é clonar e comparar. Documento envelhece sem avisar.

> **Documento de apoio citado e ausente é pior que documento inexistente.** O mapa aponta para cerca de 25 arquivos `claude/...` que não existem nesta conta. O mais crítico é `claude/moviki-videoaulas-no-ar.md`, a tabela que amarra id do YouTube → aula → cena do estúdio: sem ela, um link de vídeo não é identificável, e a regra combinada de refazer aula não funciona.

## Ligações

[[A2 - Infraestrutura e Deploy]] · [[P09 - Faxina do repositorio moviki]] · [[P14 - Verificacao de parceiro]] · [[P15 - Enforcement do App Check]] · [[R - Variaveis de ambiente]] · [[R - Marcas de versao no ar]] · [[R - Historico de regras do Firestore]]
