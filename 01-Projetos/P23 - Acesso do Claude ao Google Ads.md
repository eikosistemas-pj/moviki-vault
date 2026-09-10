---
type: projeto
status: ativo
prioridade: 3
prazo: 2026-09-30
area: A6 - Medicao e Analytics
tags: [google-ads, integracao, windsor, medicao]
atualizado: 2026-09-10
---

# P23 - Acesso do Claude ao Google Ads

Diagnostico de 10/09/2026. **Nada para subir no GitHub.**

- O **Meta Ads** e acessado direto, sem intermediario. Funciona.
- O **Google Ads** nao tem conexao direta. A unica ponte e o **Windsor.ai**.
- A ponte esta quebrada **por limite de plano dele**, nao por erro de
  configuracao.

## O que acontece

O Windsor entrega a lista antiga: Google Ads *Eiko Vida 348-398-3644* em vez de
*Eiko Sistemas 718-683-2490*, e Instagram caldeirao.nordestino/eikovida em vez de
moviki.oficial. As contas foram trocadas na tela do Windsor em 06/09 e quatro dias
depois ele continua servindo cache.

A resposta real ao puxar dados: *"You've connected more accounts than your Free
plan allows"*. A **interface** mostra "acesso total, restam X dias do teste" e
deixa conectar 4 fontes; a **porta de API** aplica as regras do plano Free.

## Caminho 1 - enxugar o Windsor (gratis, ~10 min, tentar primeiro)

1. Entrar em windsor.ai
2. Na area de fontes de dados, **desconectar 3 das 4**, deixando so "Anuncios do
   Google" (o Meta ja e acessado direto; Instagram e Pagina do Facebook aparecem
   de graca nos paineis nativos)
3. Na fonte que sobrou, deixar marcada **apenas a 718-683-2490**
4. Salvar e avisar no chat para o teste

Se funcionar, ha leitura **e acao**: criar campanha, grupo, anuncio responsivo,
palavras-chave e negativas, orcamento, estrategia de lance, teto de CPC, idioma,
agenda, pausar/ativar, renomear — e, ao contrario do que a anotacao antiga dizia,
**a segmentacao de local ja aparece na lista de acoes** (`set_campaign_geo_targeting`).
Risco: nenhum. Desconectar fonte no Windsor nao mexe em nada dentro do Google Ads
nem do Meta.

## Caminho 2 - planilha automatica no Drive (gratis, ~30 min, o mais confiavel)

Nao depende de ponte e nao expira: o Google Ads escreve os numeros numa Planilha
Google do Drive do `eikosistemas@gmail.com` todo dia, e o Claude le a planilha.
**So leitura** — mudar continua sendo no painel.

Passos: criar a planilha vazia > copiar o link > Google Ads (conta 718-683-2490) >
**Ferramentas > Acoes em massa > Scripts > + > Novo script** > colar o script >
trocar a primeira linha pelo link > **Autorizar** > **Visualizar** > **Salvar** >
frequencia **Diariamente** (7h) > conferir as abas Campanhas, Palavras e Termos de
busca.

O script usa `AdsApp.report(...).exportToSheet(...)` sobre `campaign`,
`keyword_view` e `search_term_view` nos ultimos 30 dias, mais uma aba "Atualizado
em". Ele **so le**: nao cria, nao pausa e nao altera campanha. `cost_micros` vem em
micros — dividir por 1.000.000. O codigo completo esta em
`claude/moviki-acesso-google-ads.md`, no Project.

## Caminho 3 - assinar o Windsor (US$ 23/mes, ~R$ 120)

O plano Basico permite 3 fontes e provavelmente destrava leitura e acao.
**Recomendacao: nao assinar agora** — R$ 120/mes sao 6 dias de orcamento de
anuncio, e o Moviki ainda nao tem receita. Reavaliar com cliente pagante. Se um
dia assinar, as 3 fontes certas: Google Ads, GA4 e Meta Ads.

## Caminho 4 - API oficial pelo Google Cloud (nao vale agora)

Exige token de desenvolvedor, que so e emitido para conta administradora (MCC);
nasce em modo de teste e precisa de aprovacao manual do Google, de dias a semanas;
a chave nao pode viver em chat nem repositorio; e a sessao nao guarda login.
Semanas de burocracia para fazer o que o Caminho 2 faz em 30 minutos. Arquivado
para o dia em que o Moviki gerenciar Ads de clientes.

## Ligacoes

[[A6 - Medicao e Analytics]] · [[A7 - Aquisicao e Midia Paga]] ·
[[P21 - Google Ads campanha de pesquisa]]
