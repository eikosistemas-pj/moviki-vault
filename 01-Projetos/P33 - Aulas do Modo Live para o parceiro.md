---
type: projeto
status: ativo
area: A14 - Material de apoio do parceiro
tags: [parceiro, videoaulas, live, conformidade, producao]
prioridade: 1
prazo: 2026-09-18
atualizado: 2026-09-16
---

# P33 — Aulas do Modo Live para o parceiro

Substitui a versão de 15/09. Duas coisas mudaram: **a gaveta caiu** e **o
roteiro passou a ter uma versão só, conferida contra o código no ar**.

Continua [[A14 - Material de apoio do parceiro]] · depende de
[[P28 - Videoaulas do Modo Live]] e de [[P24 - Modo Live - lancamento]] ·
irmão de [[P32 - Material de apoio da live para o parceiro]].

---

## 1. Por que nenhuma aula de live entrou no painel do parceiro até hoje

Não foi esquecimento. Foram quatro causas somadas:

1. **Decisão de gaveta, de 15/09.** Título de aula é texto do HTML, legível no
   fonte com ou sem id de vídeo. Com a live em beta fechado pelo teto de 10
   subcontas do Asaas, subir a estrutura "sem os links" era a mesma porta
   lateral que expôs `aovivo.html` em 14/09. Gaveta = fora do repositório.
2. **A ordem de produção pôs o parceiro por último.** O aparato Playwright da
   live é a maior parte do trabalho e serve às duas frentes: fase 2 eram as 14
   aulas do lojista, fase 3 era a `mod-parc-live`. A fase 2 foi entregue em
   15/09 (`liveaulas.js`, 14 ids no ar). **A fase 3 nunca rodou** — o chat
   fechou antes.
3. **O motor de aulas do `parceiro.html` não sabia o que é aula opcional.**
   `todas()` percorre todo módulo com `id`, e a Divulgação — link, materiais,
   crachá — só abre com 90% de todas. Ligar as 14 do lojista sem a flag faria a
   trava saltar de 13 para 27 aulas, em cima do parceiro novo, que é quem
   importa.
4. **O guarda-corpo virou explicação.** O documento de estado no ar registra
   *"`MvLiveAulas` no `parceiro.html`: zero, e está certo — não acrescente"*.
   É regra anticolisão, escrita para a entrega do material não apagar o painel
   do lojista. Lida fora de contexto, parece decisão de conteúdo.

## 2. O que mudou em 16/09 — a gaveta não protege mais nada

- `index.html`, `comerciantes.html` e `/aovivo` foram reposicionados em live
  commerce, **públicos**. O eixo da marca é "Seu negócio no mapa. E em vídeo."
- O material de apoio tem **peças de live prontas** esperando subida.
- Resultado: o parceiro é hoje **o único elo da cadeia que não sabe falar do
  produto que a home anuncia** — e é ele quem posta com `#publi`.

**Inversão do risco:** o perigo deixou de ser expor a live cedo demais e passou
a ser **peça de live na mão do parceiro sem a aula que diz o que não pode ser
prometido**. Por isso a `mod-parc-live` entra **antes ou junto** com a subida
das peças de live, nunca depois.

## 3. Decisão vigente (não reabrir)

- **Uma aula nova obrigatória:** `mod-parc-live` — *"A venda ao vivo: o que é e
  como falar dela"*, ~2:50. Módulo próprio **Venda ao vivo**, sem `sel`.
  Conta para a trava, porque é a aula de conformidade da live — par exato da
  `mod-parc-conduta`.
- **Módulo opcional "Conhecer o estúdio por dentro":** as 14 aulas do lojista,
  mesmos ids do YouTube. **Não conta para a trava nem para o selo.**
- **Motor:** flag `opcional:true`; `todas()` e `quantos()` ignoram módulo
  opcional; a tela mostra o opcional depois dos obrigatórios, com contador
  separado e sem visto verde cobrando conclusão; progresso continua em
  `parceiros/{uid}.aulasVistas`.
- **Ganho de quebra:** dali em diante, aula de aprofundamento deixa de ser
  imposto sobre a ativação do parceiro.

## 4. O número que o roteiro fala — conferido no código, não na memória

Havia **duas versões do mesmo roteiro** em circulação: o P33 de 15/09 dizia
*"quantas lives quiser"*; o handoff do mesmo dia dizia *"duas lives"*, na
expectativa da P34.

**Vale a segunda, e agora por fato consumado:** `moviki-robo/lib/livesessao.js`
já traz `COTA_TRIAL = 2`, carência de 15 minutos para reabrir sem consumir cota,
e o estúdio já mostra *"Teste grátis: esta é a sua live 1 de 2"*.

| Item | Valor no ar | Onde |
| --- | --- | --- |
| Lives no teste grátis | **2** | `lib/livesessao.js` (`COTA_TRIAL`) |
| Reabrir em até 15 min | não consome cota | `lib/livesessao.js` (`CARENCIA_MS`) |
| Nível da live no teste | **Premium** | `moviki/api/live.js` |
| Duração Premium | 60 min | `NIVEIS.premium.limiteMin` |
| Sacolinha Premium | 5 produtos | `NIVEIS.premium.sacolaMax` |
| Pix na live | só Enterprise | `moviki-robo/lib/checkout.js` |
| Plano pago | sem limite de quantidade | `lib/livesessao.js` |

> **Regra de ouro que nasce daqui:** roteiro vive em **um** documento. Handoff
> aponta para ele, nunca o copia. Roteiro duplicado vira duas verdades, e a que
> for gravada é a errada.

### A armadilha que a aula precisa desarmar

O teste é vendido como **"30 DIAS DE PRÓ"**, mas na live entra como **Premium**.
O parceiro que ler a tabela de planos vai dizer ao lojista que não tem live no
teste — e vai estar errado. O roteiro diz isso com todas as letras.

## 5. Roteiro final — `mod-parc-live`

Voz **Malu** (`fhtZMBwha5du5OxuvexO`). No texto do motor, "Moviki" vira
**"Mo-víki"**; legenda e `.srt` mantêm a grafia certa.

| # | Fala | Tela |
| --- | --- | --- |
| 1 | Agora o Moviki tem venda ao vivo, e isso muda a conversa que você tem com o lojista. Funciona assim: o lojista entra ao vivo pelo próprio celular, direto do painel. Sem aplicativo novo, sem estúdio, sem número mínimo de seguidores. | painel do lojista, botão Fazer live |
| 2 | A página dele ganha uma faixa vermelha escrito AO VIVO, e ele tem um endereço só da live, para mandar no grupo do bairro e no status. Quem assiste vê o produto na tela, com o preço, e um botão para pedir. E conversa com o lojista pelo chat, na hora. | página pública com a faixa · tela de quem assiste |
| 3 | A venda ao vivo está no Premium e no Enterprise. E presta atenção nesta parte, porque é a que mais gera dúvida. No período de teste, a live já funciona. Mesmo a gente chamando o teste de trinta dias de Pró, na live ele entra no nível Premium. | tabela de planos |
| 4 | São duas lives, de até uma hora cada, com até cinco produtos na lista de venda. Dá para o lojista experimentar antes de pagar qualquer coisa. Assinando, deixa de ter limite de quantidade. | aviso de cota no estúdio |
| 5 | Receber por Pix dentro da live é do Enterprise. Ali o cliente paga sem sair da transmissão, e o dinheiro cai numa conta no nome do lojista. Nunca na conta do Moviki. O Moviki não cobra comissão sobre a venda do lojista. | checkout na live, com rodapé "recurso Enterprise" |
| 6 | Agora, o que você não pode falar. Não prometa venda, faturamento, número de clientes nem alcance. Nem seu, nem dele. Você descreve a ferramenta — nunca o resultado. | cartela de conduta |
| 7 | Não diga que basta ligar a câmera que a audiência aparece. Quem chama o público é o lojista: pelo WhatsApp dele, pelo grupo dele, pelos clientes que ele já tem. | cartela de conduta |
| 8 | E é essa a resposta para a frase que você mais vai ouvir: "mas eu não tenho seguidores". Ele não precisa ter. O Moviki é o palco; o megafone ele já tem. | cartela |
| 9 | Na aba Material de apoio você encontra as artes, os vídeos e as mensagens prontas sobre a venda ao vivo, com o seu link já dentro da legenda. | aba Material de apoio, categoria da live |
| 10 | E se você quiser conhecer a ferramenta por dentro, aqui nas aulas tem um módulo opcional com as mesmas aulas que o lojista assiste. Ele não tranca nada: é para quando você quiser mostrar o Moviki funcionando, na frente do lojista. | tela de aulas com o módulo opcional |

⚠️ **Conta de demonstração sempre.** Nenhum valor, nome, documento ou chave Pix
real entra no quadro.

## 6. Estado da produção — CONCLUÍDA em 16/09

- **Narração:** voz Malu, dez blocos, 20 créditos Kairogen.
- **Vídeo:** `mod-parc-live.mp4`, **2:23**, mais o `.srt`. Cenas em cartelas e
  mockup na identidade do painel, gravadas quadro a quadro em Chromium a 25 fps.
  Não é captura do estúdio real — a aula é conceitual, o parceiro não transmite.
- **No ar:** YouTube não listado, id **`H1vk5wAil78`**.
- **Painel:** `parceiro.html` marca `2026-09-16-liveparc2`, com o motor opcional,
  o módulo Venda ao vivo e o módulo opcional das 14 aulas do lojista.
  A trava da Divulgação passou de 12 para **13** aulas.
- **Falta só:** `MARCAS_CONFERIDAS` do Vik na mesma rodada do painel.

## 7. O que não pode entrar

- Prometer faturamento, número de vendas, alcance ou resultado.
- Sugerir que basta ligar a live para aparecer audiência.
- Dizer que os cortes saem automáticos.
- A palavra "trial" — é "teste grátis" ou "período de teste".
- Dizer **quantas** aulas existem. A lista cresce; vídeo não se corrige com deploy.
- Nível, medalha ou escada de parceiro em peça que saia do painel logado.

## 8. Pendências que esta nota deixa

- [ ] Montar `.mp4` + `.srt` da `mod-parc-live`
- [ ] `parceiro.html`: `opcional:true` em `todas()`, `quantos()` e na tela
- [ ] Teto de 60 min ainda é só de tela, não do servidor — [[P24 - Modo Live - lancamento]]
- [ ] 12 das 14 aulas do lojista foram gravadas com a câmera acelerada. Vão
      aparecer para o parceiro no módulo opcional. Regravar é decisão aberta.
- [ ] A aula 07 do lojista (`mod-live-pix`) cita a tarifa do Asaas. É a única
      que envelhece, e o módulo opcional a expõe ao parceiro.

## Ligações

[[A14 - Material de apoio do parceiro]] · [[A13 - Modo Live]] ·
[[P24 - Modo Live - lancamento]] · [[P28 - Videoaulas do Modo Live]] ·
[[P32 - Material de apoio da live para o parceiro]] ·
[[P34 - Travas contra abuso do teste gratis]] ·
[[R - Live - Arquitetura e arquivos]]
