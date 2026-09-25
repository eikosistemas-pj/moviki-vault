---
data: 2026-09-25
projeto: Moviki
repos: [moviki, moviki-app, moviki-robo, moviki-ai, moviki-assistente-social]
pr: subida manual pelo GitHub web
tags: [moviki, alteracao, seguranca, anuncio]
---

# Pacote A — o que precisava estar certo antes de anunciar para lojistas

## O que mudou
- **Pagamento do plano:** o plano pago passa a contar da data de vencimento da cobrança paga. Quem paga adiantado não perde dias, e um plano em dia nunca encurta. O mesmo pagamento não liga o plano duas vezes. Aviso de "vencido" ou "removido" não derruba quem está no teste grátis.
- **Teste grátis:** quem clica em Assinar antes de confirmar o e-mail continua ganhando o teste depois (antes perdia).
- **Vik (caixa de mensagens do painel):** só responde quem tem cadastro de lojista ou parceiro. Sem e-mail confirmado, 5 respostas por dia. Existe um teto do dia para todos somados (1.500, ajustável na Vercel do moviki-ai em `VIK_TETO_GLOBAL_DIA`). Se bater, o Vik para até a virada do dia e o Paulo recebe um aviso no Telegram.
- **Regras do banco (v31):**
  - o lojista só responde avaliação; não troca a nota nem o texto do cliente, e apagar avaliação é só da equipe;
  - endereço de negócio não pode pegar o endereço de um ponto;
  - o parceiro só se cadastra com o apelido que ele mesmo reservou;
  - a lista de quem está bloqueado na live só o dono vê;
  - a peça de criador só aceita arquivo do Storage do Moviki, na pasta do próprio criador.
- **Página /aovivo:** a live aparece como do Premium (antes dizia Pró). "Compra ali mesmo" virou "pede ali mesmo: pelo WhatsApp ou, no Enterprise, por Pix". A tabela ganhou pessoas assistindo e minutos de vídeo do mês.
- **Meu Plano (painel):** antes de pagar, a tela mostra três regras:
  - o plano renova sozinho;
  - para cancelar: WhatsApp (41) 2018-6848 ou suporte@moviki.com.br;
  - são 7 dias para desistir, contados do primeiro pagamento.

  Também aparece a caixa "Li e aceito os Termos". Os Termos (cláusula 5) e o FAQ do site dizem o mesmo.
- **"Não medir":** o arquivo do Google Analytics nem é baixado.
- **Página pública do negócio:** o mapa vem do próprio site, não do unpkg.

## Por quê
- Tudo isso atinge exatamente quem chega pelo anúncio, ou é regra de anúncio da Meta e do Google:
  - prometer recurso de outro plano;
  - não mostrar a renovação e o jeito de cancelar antes da cobrança.
- O Vik sem trava por conta nova deixava contas descartáveis gastarem a verba da Anthropic.

## Decisões tomadas
- Cancelamento continua pela equipe (WhatsApp ou e-mail). O botão de cancelar no painel fica para um pacote futuro.
- O prazo de arrependimento é contado do primeiro pagamento, e não da assinatura. Isso é mais favorável ao cliente e resolve quem assina durante o teste.
- O Pacote B vem antes do primeiro saque de parceiro. Ele inclui:
  - comissão de cartão liberada antes do dinheiro compensar;
  - corrida de dois saques;
  - pontos extras não cancelados na exclusão;
  - outros ajustes do robô do dinheiro.

## O que conferir
- Painel → Meu Plano: escolha um plano. Aparecem as 3 regras e a caixa. Sem marcar a caixa, o botão avisa (não precisa pagar).
- Responder uma avaliação no painel continua funcionando.
- moviki.com.br/<um negócio>: o mapa aparece.
- moviki.com.br/aovivo: a tabela mostra "Premium | Enterprise".
- Vik: mandar uma pergunta no painel e ele responde.
- Painel do dono → Live: a lista de bloqueados abre.

## Pendências
- Fechar de novo `moviki-app`, `moviki-robo` e `moviki-ai` (voltar a privados).
- Pacote B antes do primeiro saque; Pacote C (ajustes de texto e detalhes) depois.

Ver também: [[Moviki - Mapa Mestre]]
