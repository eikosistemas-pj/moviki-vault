---
type: decisao
status: entregue
area: "[[A5 - Programa de Parceiros]]"
tags: [criadores, influenciadores, painel-do-dono, aprovacao, ga4, firestore, regras-v27]
atualizado: 2026-09-23
---

# Menu Criadores no painel do dono

Marca do painel: **`2026-09-22-criadores`** (`eikoadm01.html`). Regras do Firestore **v27**.

## O que mudou

- **Menu novo "Criadores"** no painel do dono, com selo de pendência e entrada no sino.
- **Aprovar peças (a segunda chave):** fila com prévia da imagem ou do vídeo, formato, duração, legenda, situação da autorização do criador (termo, data, validade) e pré-triagem (proporção, duração, termo proibido). Botões **Aprovar**, **Recusar** (motivo obrigatório, o criador vê) e **Suspender** (tira do robô na próxima execução). Aprovar vídeo pergunta se ele foi assistido inteiro.
- **Desempenho, criador por criador**, com período de 30, 90 ou 180 dias ou 12 meses:
  - visitas pelos links /c/ e /p/ dele (Google Analytics);
  - cadastros (`indicacoes`), lojistas pagantes e mensalidades pagas (`comissoes`);
  - receita líquida estimada: mensalidade − 6% de imposto − R$ 2 de tarifa;
  - custo: comissões + bônus + custo fixo mensal opcional;
  - resultado e um veredito em uma frase;
  - posts nas redes do Moviki com peça dele (histórico do robô social);
  - 4 gráficos por semana ou por mês e ranking de todos os criadores.
- **Quem é criador:** o dono marca e desmarca (`parceiros/{uid}.criador`). Só criador marcado e com cadastro aprovado envia peça.
- **Endpoint `www.moviki.com.br/api/criadores`** (repo `moviki`): GET para o robô social, com só peça de duas chaves; POST de visitas do GA4, só para admin.
- **Coleção `criador_pecas`** (regras v27) e pasta **`criadores/{uid}/`** no Storage.

## Por que

Decidir com número se cada influenciador vale a parceria. A decisão do funil já era "o dono aprova, o robô nunca aprova". Faltava a tela para aprovar e a conta de retorno.

## Decisões tomadas

- **Conteúdo de peça não se edita** depois de enviado: para trocar, apaga e envia outra. Senão, o vídeo aprovado poderia ser trocado por outro que o dono não viu.
- **O dono não autoriza em nome do criador**, e o criador não aprova a própria peça. Travado na regra, com teste escrito.
- **O crédito "Conteúdo de @arroba" sai do cadastro**, não do que o criador digita na peça.
- **Premium liberado ao criador não conta como custo**: não sai dinheiro. Cachê ou bônus pago por fora vai no campo de custo fixo.
- Histórico do robô passou a guardar **2.000 posts** (eram 500 — com story 2x/dia cobria só ~5 meses).

## O que conferir — tudo feito em 22/09/2026

Regras v27 e Storage publicadas, GA4 liberado (Leitor + Data API), secret `CRIADORES_URL` criado, primeiro criador marcado e testado de ponta a ponta. A marca do painel andou depois: `2026-09-22-criadores5` (link de acesso e oferta de cada criador) e `2026-09-23-vikalarme` (sobre a rodada2 de outro chat).


1. **Publicar as regras v27** no console do Firebase (Firestore) e o `storage.rules` (Storage). O console valida a sintaxe antes de publicar; se reclamar, não publicar e trazer o erro.
2. Subir o painel e abrir o menu **Criadores**: deve carregar sem aviso vermelho (fila vazia é normal).
3. Marcar um parceiro de teste como criador na aba "Quem é criador".
4. **Liberar as visitas** (uma vez só):
   - GA4 > Administrador > Gerenciamento de acesso à propriedade > "+", e-mail `moviki-site-leitura@moviki-app.iam.gserviceaccount.com`, papel **Leitor**;
   - Google Cloud, projeto moviki-app > APIs e serviços > ativar **Google Analytics Data API**.
   Sem isso a aba Desempenho funciona, mas mostra o aviso e "—" em visitas.
5. Criar o secret `CRIADORES_URL` = `https://www.moviki.com.br/api/criadores` no `moviki-assistente-social`. Sem peça aprovada, a lista vem vazia e nada muda.

## Pendências

- ~~Painel do criador~~ — **feito em 22/09**: [[ARQ - Area do criador no painel do parceiro]].
- As regras v27 **não rodaram no emulador** aqui (o ambiente bloqueia o pacote do emulador). Os 13 casos novos estão escritos em `firebase/testes/regras.test.js`; rodar numa sessão do Claude Code antes de confiar em produção.

## Ligações

[[A5 - Programa de Parceiros]] · [[ARQ - Area do criador no painel do parceiro]] · [[ARQ - Oferta do criador por porta de entrada - decisao 22092026]] · [[ARQ - Feed padronizado sobre o material de apoio]] · [[R - Marcas de versao no ar]] · [[R - Regras de ouro]]
