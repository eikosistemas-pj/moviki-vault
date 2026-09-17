---
data: 2026-09-17
projeto: Moviki
repos: [moviki, moviki-app, moviki-robo, moviki-ai, moviki-assistente-social]
pr: https://github.com/eikosistemas-pj/moviki-app/pull/7 (+ moviki#4, moviki-robo#2, moviki-ai#3, moviki-assistente-social#2)
tags: [moviki, alteracao, equipe]
---

# Equipe de especialistas

## O que mudou

O Moviki deixou de ser tocado por um ajudante genérico e passou a ter um time. São oito cadeiras, cada uma dona de uma parte da empresa:

| Cadeira | De que cuida | Onde mora |
|---|---|---|
| Gabinete | Coordenação, memória, mapa mestre, ordem de aprovação | Nos cinco repositórios |
| Guarda | Segurança, regras do Firestore, LGPD, segredos | Nos cinco (com veto) |
| Tesouraria | Dinheiro: assinatura, Asaas, comissão, saque, preço | moviki-robo |
| Vitrine | Site público, página do negócio, live pública, SEO | moviki |
| Balcão | Painel do lojista, live, videoaulas, painel do dono | moviki-app |
| Canal | Parceiros, material de apoio, treinamento | moviki-app |
| Atendimento | Atendentes de IA do WhatsApp e do painel | moviki-ai |
| Praça | Instagram e Facebook, calendário, compliance | moviki-assistente-social |

Cada cadeira tem escrito, em linguagem de negócio, três coisas: de que cuida, o que decide sozinha, e o que sempre sobe para o Paulo. Nada foi inventado — as regras vieram do mapa mestre e do que já estava valendo no código.

Nenhuma linha de código de produto foi alterada. Nada muda para o lojista, para o parceiro ou para o cliente final hoje.

## Por quê

Toda sessão começava do zero. Quem abria uma conversa no moviki-robo não sabia que preço só muda com autorização; quem abria no moviki não sabia que texto de lojista precisa ser escapado. A regra existia no mapa, mas dependia de alguém lembrar de lê-la inteira.

Agora a regra chega junto com a área. Quem entra no repositório do dinheiro recebe a Tesouraria já sabendo as travas do dinheiro.

O gatilho adicional: ao levantar o time, descobriu-se que o mapa mestre tinha divergido **pela terceira vez** — a linha das videoaulas de 17/09 existia só na cópia do moviki-app. Regra sem dono volta a quebrar. Agora tem dono.

## Decisões tomadas

- **Cada cadeira mora no repositório que governa.** Evita duplicar oito arquivos em cinco lugares e criar exatamente o problema de divergência que já machucou três vezes.
- **Gabinete e Guarda são exceção e moram em todos**, porque coordenação e vazamento não respeitam fronteira de repositório. As duas entraram formalmente na regra de sincronização do mapa.
- **Conferir se as cópias do mapa batem deixou de ser disciplina e virou a primeira tarefa do Gabinete em toda sessão.** Antes dependia de quem editava lembrar; agora é obrigação de alguém.
- **O time nasceu completo, contra a recomendação.** A recomendação era começar com três e crescer, porque especialista sem trabalho recorrente vira arquivo morto. Decisão do Paulo foi criar todos. Compromisso de meio-termo: cadeira parada 60 dias volta para revisão e ou ganha trabalho recorrente ou é fundida com outra.
- **Ordem direta do Paulo vence a regra de qualquer cadeira.** A única exceção: quando colide com dinheiro ou segurança, a cadeira explica o risco em uma frase, pede confirmação explícita e registra no histórico que foi decisão consciente dele.
- **Criar, fundir ou aposentar cadeira é decisão exclusiva do Paulo.**
- A skill Material de apoio, que já existia, continua existindo como ferramenta do Canal.

## O que conferir

Nada para testar no ar — este pacote não altera tela, dado nem cobrança.

O que vale conferir é o **comportamento**: na próxima conversa iniciada em qualquer repositório, pedir algo da área e ver se a cadeira certa assume e cita a regra da área sem precisar de explicação.

## Pendências

- **A sexta cópia do mapa, no moviki-vault, não foi atualizada.** O repositório é privado e não estava anexado à sessão. Enquanto não for, o mapa está sincronizado em cinco de seis — ou seja, a regra continua tecnicamente quebrada.
- As oito cadeiras nasceram com as regras que dava para levantar do repositório. O que está no vault (o porquê de decisões antigas) não entrou. Vale uma sessão com o vault anexado para enriquecer o Gabinete.
- O moviki-vault continua sem auditoria de segurança.

Ver também: [[Moviki - Mapa Mestre]]
