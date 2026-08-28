---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [meta, protocolo]
atualizado: 2026-08-28
---

# R - Protocolo Claude e vault

Como o Claude lê este vault e como as notas nascem. Decidido em 28/08/2026.

## O que o Claude NÃO acessa

**O Obsidian.** Nunca — nem aberto, nem minimizado. Obsidian fechado ou PC desligado é indiferente.

O que ele lê é o **repositório no GitHub**, uma cópia na nuvem:

```
você escreve no Obsidian
      ↓  plugin Git (a cada 10 min)
GitHub  ←── o Claude lê AQUI
      ↓  sincronização da Base de Conhecimento
o Claude, em qualquer chat
```

**Duas consequências que valem lembrar:**

1. **O que não foi commitado, o Claude não vê.** Nota escrita há 2 minutos, com o plugin no intervalo de 10, é invisível. Quando precisar que ele leia já: `Ctrl+P` → `Git: Commit and sync`.
2. **A Base de Conhecimento não reindexa no instante do push.** Se o Claude não achar algo recém-subido, é atraso de sincronização — não é o vault quebrado.

## Como as notas nascem

O Claude tem **leitura apenas**. Ele não escreve no vault; entrega o arquivo pronto e você salva.

**Automático:** ao fim de qualquer rodada que produza algo durável, ele gera a nota sem esperar pedido.

**Durável é:** decisão de arquitetura · regra nova · incidente com causa e conserto · entrega concluída · pendência nova.
**Não é:** dúvida respondida · código entregue sem decisão nova · conversa exploratória.

**`/nota`** força a geração, mesmo do que ele não julgaria durável.

**`/atualizarmapa`** passa a fechar as duas pontas na mesma rodada: o bloco do Mapa Mestre **e** as notas do vault afetadas.

## Onde cada coisa cai

| O que é | Pasta e prefixo |
| --- | --- |
| Pendência com fim e data | `01-Projetos/P<nn> - <titulo>.md` |
| Responsabilidade contínua | `02-Areas/A<n> - <titulo>.md` (atualizar; criar é raro) |
| Referência sem ação | `03-Recursos/R - <titulo>.md` |
| Concluído, decisão, incidente | `04-Arquivo/ARQ - <titulo>.md` |
| **Regra de ouro nova** | sempre TAMBÉM em [[R - Regras de ouro]] |
| **Upload de arquivo** | sempre TAMBÉM em [[R - Marcas de versao no ar]] |

## Formato obrigatório

- Frontmatter com `type`, `status`, `area`, `tags`, `atualizado` — mais `prioridade` e `prazo` em projeto
- Wikilinks `[[...]]` pelo **nome exato do arquivo**
- **Nome de arquivo só ASCII.** Separador é hífen simples ` - `, nunca travessão. Ver [[ARQ - Incidente - nomes de arquivo corrompidos no Windows]]
- Entrega sempre com a **pasta exata** e se é **NOVO ou SUBSTITUI** — nunca "trecho + onde colar"

## Onde você salva

```
D:\PROJETO MOVIKI\COFRE OBISIDIAN MOVIKI\Moviki\<pasta>
```

O plugin Git commita em até 10 minutos.

## A peça que faz isso valer em chat novo

**Chat novo não lembra de conversa antiga.** Este protocolo só funciona porque está nas **instruções do Project** (seção 6), que o Claude lê em toda conversa.

Mudou o protocolo aqui? **Mude lá também**, ou o Claude segue o antigo.

→ [[R - Sync do vault Obsidian Git]] · [[R - Mapa Mestre ponteiro]] · [[LEIA-ME - Como usar este vault]]
