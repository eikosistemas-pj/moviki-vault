---
type: recurso
status: ativo
area: A5 - Programa de Parceiros
tags: [criador, video, captura, gravacao, hamburguermaster, conta-demo]
atualizado: 2026-09-22
---

# R - Roteiro de captura de tela para o vídeo do criador

Tudo o que precisa ser gravado na conta demo para trocar as artes por tela real na v2 do vídeo convite. Uma passada só, na ordem daqui. Eu corto.

Conta demo: **`hamburguermaster`**, uid `rjESfrCf8NPiQBNyDwxnP4BzAzd2`, João Pessoa/PB, plano Enterprise.

## 0. Validade da conta — resolvido

O vencimento foi empurrado para **30/12/2030** no Console do Firebase em 22/09/2026. `assinaturas/{uid}` está com `ativo: true`, `plano: enterprise`, `vence_em` em 2030. **Não há mais prazo para gravar.**

A trava que sobra é outra: o botão **Fazer live** depende de `configuracoes/liveTermos` → `liveBeta` e `liveDesligada`, não do plano. Confira antes de marcar a gravação — detalhe em [[R - Conta demo hamburguermaster - estender a validade]].

## 1. Antes de ligar a câmera

**Na conta `hamburguermaster`:**

- [ ] 6 fotos no negócio — a primeira vira a capa
- [ ] 5 itens de cardápio em 2 categorias, todos com foto, descrição e preço
- [ ] 1 promoção, sem promessa agressiva
- [ ] endereço (rua + bairro), horário, entrega e preço médio preenchidos
- [ ] recado curto, sem exclamação tripla
- [ ] cor do negócio **fora** da faixa ciano/azul da marca (senão a página se confunde com o Moviki na tela)
- [ ] logo enviada, para o pino aparecer com a marca no mapa

Confira pelo painel, salvando cada campo. A página pública demora a refletir; se algo não aparecer, volte ao painel em vez de recarregar dez vezes.

**No aparelho:**

- [ ] Celular em pé, gravador de tela nativo, **1080×1920**, 30 fps
- [ ] Não incomodar ligado, sem notificação entrando em quadro
- [ ] Bateria acima de 50%, brilho no máximo
- [ ] Wi-Fi com sinal cheio — a live usa a internet do aparelho
- [ ] **Segundo aparelho** para o papel de cliente (é ele que gera o pedido da cena 3)

**Regra de ouro da gravação:** 2 segundos parado antes de tocar em qualquer coisa, 2 segundos parado depois. É o que me dá margem para cortar sem engolir o movimento.

## 2. A ordem de gravação

Seis blocos. Pode ser um arquivo só por bloco ou um arquivo único do começo ao fim — eu corto de qualquer jeito.

### Bloco A — Mapa (alimenta as cenas 1 e 2)

1. Abrir `moviki.com.br` no celular, com o mapa carregado e os pinos visíveis.
2. **Take 1:** parado 2 s, depois um zoom lento de pinça até o bairro. Sem toque em pino. ~8 s.
3. **Take 2:** arrastar o mapa devagar passando por 2 ou 3 negócios, o dedo aparecendo. ~8 s.
4. **Take 3:** tocar em um pino e deixar o cartão do negócio abrir. ~6 s.

O pino da hamburgueria precisa estar em quadro com a logo. Se o mapa abrir vazio, mexa a localização do aparelho para João Pessoa antes.

### Bloco B — Página pública (alimenta a cena 4)

1. Abrir `moviki.com.br/hamburguermaster`.
2. **Take 4:** topo da página com o nome, a capa e o **status aberto**. Parado 3 s.
3. **Take 5:** rolagem lenta e contínua até o cardápio, mostrando 2 ou 3 itens com foto e preço. ~10 s. Uma rolagem só, sem ir e voltar.

Se o status estiver fechado no horário da gravação, ajuste o horário de funcionamento no painel antes — aberto é o que prova "em tempo real".

### Bloco C — Estúdio antes do ar (serve de apoio, entra se sobrar cena)

1. Abrir o painel, botão **Fazer live**.
2. **Take 6:** campo do título preenchido com algo real ("Hambúrguer artesanal hoje"), tocar em **Ligar câmera**, aceitar a permissão. ~8 s.
3. **Take 7:** aba **Produtos**, marcar 3 itens na **Sacolinha**. O dedo marcando. ~8 s.

### Bloco D — A live com pedido entrando (alimenta a cena 3 — **a captura mais importante do vídeo**)

Precisa dos dois aparelhos. O celular A grava a tela do estúdio; o celular B é o cliente.

1. No celular A: **Entrar ao vivo**. Deixe a pílula **AO VIVO** com o relógio e o olho visível.
2. No celular B: abrir `moviki.com.br/live/hamburguermaster`, esperar a imagem aparecer.
3. No celular A: tocar em **Destacar** num produto. O card grande sobe na tela de quem assiste.
4. No celular B: abrir a **sacolinha**, tocar em **Quero este**.
5. No celular A, **gravando**: o pedido entra na aba **Fila de pedidos**. Deixe a tela parada 3 s com a linha nova visível.
6. **Take 8:** repita o ciclo mais uma vez, para eu ter duas entradas de pedido para escolher.
7. **Take 9:** aba **Dados ao vivo** com Assistindo agora, Pico e Toques em "Quero" diferentes de zero. Parado 4 s.
8. **Encerrar live** e gravar o resumo que aparece. ~5 s.

**Grave também a tela do celular B** nessa passagem, se der: a tela de quem assiste, com o card do produto sobre o vídeo, é a melhor imagem do vídeo inteiro. Se só der para gravar um, **grave o A**.

Sem WhatsApp aberto em quadro. Quando tocar em "Quero este" no celular B, o WhatsApp abre — **pare a gravação do B antes disso** ou o número e as conversas entram na tela.

### Bloco E — Regulamento (alimenta a primeira metade da cena 7)

1. Abrir `moviki.com.br/regulamento.html`.
2. **Take 10:** rolagem lenta até o trecho da comissão, parando 4 s com "só sobre assinatura paga" legível na tela. ~12 s.

### Bloco F — Painel do parceiro (alimenta a segunda metade da cena 7)

1. Entrar no painel do parceiro com a **sua** conta de teste, nunca com a de outro parceiro.
2. **Take 11:** a lista de negócios indicados, com pelo menos duas linhas. ~6 s.
3. **Take 12:** o link de indicação na tela, com o apelido `teste-criador`. ~5 s.

**Valor de comissão em R$ não pode aparecer.** Se o painel mostrar valor, role até uma parte que não mostre, ou tampe com o dedo — mas o melhor é enquadrar sem.

## 3. De onde sai cada cena

| Cena | Fala | Take | Se o take não existir |
| --- | --- | --- | --- |
| 1 | De criador para criador | A1 (zoom no mapa) | fica a arte atual |
| 2 | Quando foi a última vez… | A2 (rolagem) | fica a arte atual |
| 3 | Negócio da sua rua vendendo ao vivo | **D8** (pedido entrando) | fica a arte — mas é a cena que mais perde |
| 4 | O Moviki põe no mapa e deixa vender ao vivo | A3 + B4 | fica a arte atual |
| 5 | Três criadores | — | arte, por decisão |
| 6 | Comissão · Bônus · Premium | — | arte, por decisão |
| 7 | Regulamento público, painel negócio por negócio | E10 + F11 | fica a arte atual |
| 8 | Você testa antes de indicar | gravação sua com o lojista | fica a arte atual |
| 9 | Quem mostra primeiro | — | arte, por decisão |

Cena a cena, sem pressa: **o vídeo funciona hoje com as artes.** Cada take que chegar melhora uma cena, e eu remonto sem mexer na narração nem nos tempos.

## 4. O que nunca pode aparecer na tela

- Dado de cliente real: nome, telefone, endereço, foto de pessoa
- Chave Pix, QR de pagamento, tela de banco
- Valor de comissão em R$, saldo, extrato
- Nome de pessoa em conversa, WhatsApp aberto, notificação
- Painel de outro parceiro ou conta de lojista real
- Qualquer tela de negócio que não seja a conta demo

A regra por trás: o opt-in de divulgação que o lojista aceita **não cobre esta peça**. Por isso a conta demo existe. Captura de cliente real não entra, nem com autorização verbal.

## 5. Como me mandar

Arquivo bruto, sem editar, sem filtro, sem música. Nome do arquivo com a letra do bloco: `bloco-a.mp4`, `bloco-d-celular-a.mp4`. Se for tudo num arquivo só, me diga mais ou menos em que minuto começa cada bloco.

Devolvo a v2 com as cenas trocadas, o `.srt` recalculado e a descrição atualizada.

## 6. Se a live não der certo no dia

O bloco D é o único que depende de duas mãos e de internet boa. Se travar:

- Grave o bloco D sozinho, em outro dia, e me mande depois. Os outros blocos não dependem dele.
- Enquanto isso eu monto a v2 com A, B, E e F, e a cena 3 continua com a arte.
- Nunca grave "de mentira": tela montada, pedido simulado por foto, print editado. A cena 3 é a prova do vídeo inteiro — se for encenada e alguém perceber, cai a credibilidade das outras oito.

Relacionado: [[ARQ - Video convite do criador montado v1 22092026]] · [[R - Video convite do criador - audios e plano de montagem 21092026]] · [[R - Filme institucional - conta demo]] · [[HANDOFF - Fase 0 do funil de criadores - video convite e DMs 21092026]]
