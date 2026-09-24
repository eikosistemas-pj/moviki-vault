---
type: recurso
status: referencia
area: A2 - Infraestrutura e Deploy
tags: [regra-de-ouro, apendice, armadilha]
atualizado: 2026-09-23
---

# R - Regras de ouro novas de 17 a 23092026

⚠️ **Apêndice de [[R - Regras de ouro]].** Separado porque o arquivo principal
nunca chegou integral aqui — substituir sem ele apagaria o histórico.
**Fundir junto com os apêndices anteriores** ([[R - Regras de ouro novas de 11 a 14092026]],
[[R - Regras de ouro novas de 15092026]], [[R - Regras de ouro novas de 15 e 16092026]],
[[R - Regras de ouro novas de 16092026]]).

## Regras do Firestore (17/09, v26)

- **Subcoleção nova dentro de `negocios/{uid}` exige regra própria no mesmo ciclo.** Desde a v26 ela nasce fechada.
- **`match /{documento=**}` com `read: true` publica toda subcoleção FUTURA** — e anula em silêncio o `hasOnly` do documento pai.
- **Regra do Firestore mora no repositório**, com teste automático no emulador. O Console continua sendo a verdade do que está publicado.

## Custo de vídeo e cota (19/09)

- **Limite de uso que a página não mostra é oferta não cumprida.** O número vai primeiro para o plano, o checkout e os Termos; depois para o código. **Baixar limite exige aviso de 30 dias.**
- **Não derrube a live que está vendendo.** Em 100%, a trava de custo bloqueia a PRÓXIMA live; a em andamento só cai no fim de uma tolerância que também tem teto.
- **Corte por limite nunca usa o texto de corte por moderação.** O servidor grava o `motivo`; a tela escolhe a mensagem por ele.
- **Quem entra acima do limite de espectadores não grava presença** — senão paga-se o minuto de quem não viu nada.
- **Recusa que atravessa dois servidores leva os números junto.** O intermediário que descarta campos transforma "3.600 de 3.000" em "0 de 0".
- **Handoff é hipótese; o código é o fato.** O de 18/09 pedia para construir o que já existia desde 16/09.

## Robô social e conteúdo (22/09)

- **Conta de teste na página oficial é prova social falsa.** Vitrine automática só com lojista real — enquanto a base for zero, desligada.
- **Peça feita para o parceiro não vai para a página oficial sem conversão.** Legenda na voz do parceiro (`#publi`, "meu link") é trocada; arte com "link deste parceiro" impresso fica de fora.
- **Robô não afirma o que não sabe** — "está aberto agora", cidade/UF adivinhada, slug que é e-mail. Sem certeza, omite.
- **Criador é parceiro marcado.** Não existe conta só de criador; a separação é só de porta.
- **Peça de criador só vai ao ar com duas chaves:** autorização dele e aprovação do dono.

## Vik (22 e 23/09)

- **Subiu `index.html` ou `parceiro.html`, sobe junto `moviki-ai/lib/catalogoPainel.js`** — `MARCAS_CONFERIDAS`, texto novo e `CATALOGO_VERSAO`, na MESMA entrega. Sem isso o Vik entra em modo cauteloso para todos, sem sintoma. O alarme do painel do dono avisa desde 23/09.
- **Data mostrada ao cliente é em horário de Brasília**, nunca UTC.

## Interface (23/09)

- **Movimento só anima `opacity`, `translate`, `scale` e `transform`**, com duração e curva dos tokens `--mv-dur-*` / `--mv-ease*`.
- **Quem pediu menos movimento no aparelho não vê animação nenhuma.**
- **Ferramenta não espera:** painel não tem revelação por rolagem.
- **Estado oculto só nasce no JS, e só abaixo da dobra.**
- **Ícone de interface: no máximo 256 px e ~15 KB**, otimizado com o mesmo nome e a mesma dimensão.
- **Imagem em menu fechado é `loading="lazy"`**; logo e herói, nunca.
- **Biblioteca que só o `<script type="module">` usa vai com `defer`.**
- **`mvmotion.js`, `mvmetrica.js` e `movikiui.css` sobem idênticos nos dois repos.**

## Infraestrutura (23/09)

- **A Vercel está no plano Pro.** O teto de 12 funções do Hobby caiu — ver [[ARQ - Vercel no plano Pro 23092026]]. O `moviki-robo` continua sendo o repo de dinheiro e **muda o mínimo**.

## Vault

- **Nota do vault não se grava também como doc do Project.** Um caminho só: arquivo no chat → `SincronizarVaultMoviki.bat` → GitHub → sincronização.
- **Nota que não sobe não existe.** De 18 a 23/09 nenhuma nota subiu, e as originais de várias rodadas se perderam — só puderam ser reconstruídas a partir do mapa mestre.

## Ligações

[[R - Regras de ouro]] · [[R - Motion principles]] · [[P41 - Cota de live por lojista]] ·
[[ARQ - Robo social - feed padronizado story e reel 22092026]] ·
[[ARQ - Vik em modo criador 22092026]]
