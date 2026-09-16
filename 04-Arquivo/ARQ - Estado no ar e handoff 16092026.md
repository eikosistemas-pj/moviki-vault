---
type: arquivo
status: ativo
area: A1 - Produto e Paineis
tags: [handoff, estado-no-ar, marcas-de-versao, pendencias, retomada]
atualizado: 2026-09-16
---

# ARQ - Estado no ar e handoff 16092026

**Conferido por clone dos quatro repositorios em 16/09/2026, apos a subida.**
Nao e memoria nem RAG: e hash de arquivo comparado um a um.

Esta nota e o ponto de partida de qualquer sessao nova. Leia esta primeiro.

---

## O QUE ESTA NO AR — 17 de 19 arquivos conferidos byte a byte

### Repo `moviki` (site)

| Arquivo | Marca | O que carrega |
| --- | --- | --- |
| `index.html` | `2026-09-16-preco2` | precos novos, JSON-LD, Enterprise responde ao toggle anual |
| `premium.html` | `2026-09-16-preco1` | tabela, JSON-LD sem duplicata, trimestral removido |
| `enterprise.html` | `2026-09-16-preco1` | R$ 129,90, ponto extra R$ 19,90 |
| `comerciantes.html` | `2026-09-16-preco1` | tres precos (BOM e CRLF preservados) |
| `parceiros.html` | `2026-09-16-preco1` | comissoes 5,99 / 10,49 / 19,49 |
| `parceiros-ganhos.html` | `2026-09-16-simulador` | **simulador de tres barras** |
| `termos.html` | `2026-09-16-preco1` | tabela de planos, data 16/09, sem trimestral |

### Repo `moviki-app` (paineis) — todos `2026-09-16-preco1`

`index.html` (botoes sem trimestral, duas travas de deep-link, `BASE=129.90`) ·
`parceiro.html` (abas, `cvValor` R$ 5,99, PLANOS novos) ·
`eikoadm01.html` (PLANOS do painel do dono e aba Custos e margem)

### Repo `moviki-robo`

`lib/asaas.js` — **conferido: cobra 39,90 / 399 / 69,90 / 699 / 129,90, sem
trimestral.** · `api/lembrete-trial.js` · `README.md`

### Repo `moviki-ai`

`lib/catalogoPainel.js` · `lib/promptAtendimento.js` · `lib/segurancaVik.js` ·
`lib/segurancaVik.test.js` — **teste executado no repo real: 0 falhas.**

### Varredura final

**Zero ocorrencias** de 37,90 / 49,90 / 99,90 / 5,69 / 7,49 / 14,99 / 379 / 499 /
134,90 em qualquer `.html`, `.js`, `.json` ou `.md` dos quatro repositorios.
(Os dois falsos positivos conhecidos — `quiz-segmentos.js` e `webhook.js` — sao
exemplo de produto e payload de comentario, nao mexer.)

---

## ⚠️ O QUE FALTOU SUBIR

| Arquivo | Estado |
| --- | --- |
| `moviki/parceiros.pdf` | **AINDA O ANTIGO.** 324.223 bytes. Contem o grafico R$57/R$171/R$284 e as palavras renda, ganhe, ganho, rendem |
| `moviki/comerciantes.pdf` | **AINDA O ANTIGO.** 768.957 bytes. Precos 37,90 / 49,90 / 99,90 |

Os dois estao publicos por URL direta em `moviki.com.br/<nome>.pdf`. Os novos
(120.953 e 82.412 bytes) estao montados e conferidos — so precisam subir na
**raiz do repo `moviki`**. Ver
[[ARQ - Incidente PDF de parceiros com projecao de ganho 16092026]].

---

## A FILA, EM ORDEM

### 1. Subir os dois PDFs
Um comando. Fecha a unica violacao de conformidade aberta.

### 2. Teto de minutos de live por plano
**A margem da live nao tem freio nenhum hoje.** Premium a R$ 69,90 com uso
"Ativo" (4 lives x 60 min x 30 espectadores = 7.200 min entregues) consome
US$ 7,20, e a Cloudflare Stream cobra por minuto **entregue**, sem teto proprio
de gasto. Proposta ja calculada: Premium 1.500 min/mes, Enterprise 5.000,
teste gratis 300, pacote extra R$ 19,90 por 1.000 min (custo real R$ 5,40).

### 3. Teste de fumaca da live
**Nunca foi feito. E o gargalo para abrir o produto.** Uma live de ponta a
ponta: abrir estudio, transmitir, um espectador entrar, sacolinha, Pix, fechar.

### 4. Vik em modo cauteloso
`MARCAS_CONFERIDAS` em `moviki-ai/lib/catalogoPainel.js`.

### 5. Esvaziar `liveBeta` e disparar `Lead` da CAPI no cadastro de parceiro

### 6. Midia
Google: conferir a conversao "Inscricao" antes de repor saldo.
Meta: religar so quando a pagina converter. **Hoje sao zero cadastros.**

### 7. Producao
Videos V1 a V5 · 8 avatares · trocar o PDF do prompt na base da Meta ·
conferir os 4 videos de `moviki-app/material/` (audio e legenda nao aparecem
em grep) · atualizar a secao 2 do `MAPA-MESTRE.md`.

---

## REGRAS DE OURO QUE ESTA RODADA DEIXOU

> **1.** Presenca numa leitura com `include_inactive` nao significa palavra ativa.
> Para saber o estado real, tentar a escrita — a recusa e a resposta.

> **2.** Arquivo binario publico e material da marca, mesmo sem link. PDF, imagem
> e video na raiz de um repositorio nao aparecem em busca de texto e e por isso
> que a violacao sobrevive neles por mais tempo.

> **3.** Numero que projeta ganho, quem escolhe e o visitante. A marca publica o
> percentual e a regra; a conta e feita na tela, com o valor que a pessoa moveu,
> sempre com "pode ser zero".

> **4.** Card de plano dentro de um toggle de ciclo precisa responder aos dois
> estados. Card mudo nao le como "nao se aplica" — le como preco fora da curva.

> **5.** Documentacao e teste sao lugares onde o preco vive. Uma troca de preco
> so termina quando o README bate com o `lib/asaas.js`.

> **6.** WebFetch pega cache de CDN. Para saber o que esta no ar, **clonar o
> repositorio** — `git clone --depth 1 https://github.com/eikosistemas-pj/<repo>.git`
> funciona sem credencial nos quatro repos de codigo.

---

## PARAMETROS QUE VALEM AGORA

| | |
| --- | --- |
| Planos | Pro 39,90 · Premium 69,90 · Enterprise 129,90 · Basico gratis |
| Anual | Pro 399 · Premium 699 · **Enterprise nao tem anual** |
| Trimestral | **aposentado em 16/09** |
| Ponto extra Enterprise | R$ 19,90/mes, assinatura separada |
| Comissao N1 | 5,99 / 10,49 / 19,49 · escada 16/17/18% do Ouro para cima |
| N2 e N3 | 7,5% e 5%, bonus unico no 1o pagamento |
| Aliquota | 6% (Simples Nacional, Anexo III) |
| Tarifa Asaas | R$ 2,00 por cobranca |
| Video | US$ 1 por 1.000 min **entregues** (Cloudflare Stream) |
| Vik | `claude-haiku-4-5`, ~US$ 0,004/resposta, teto 40/conta/dia. **API paga, conta separada da assinatura do claude.ai** |
| Equilibrio | 46-47 lojistas pagantes |
| Projecao 12 meses | 460 ativos · R$ 189.150 faturados · R$ 120.022 de lucro |
| Clientes pagantes hoje | **zero** |

## O QUE NAO MEXER

- Os dois `regulamento.html` — **nao tem preco de plano**, so percentual
- `moviki-app/quiz/quiz-segmentos.js` — o 99,90 e preco de creatina
- `moviki-robo/api/webhook.js` — o 99.90 e payload de exemplo em comentario
- `moviki-app/icones/comissoes.png` — icone de moeda, sem valor escrito
- As 84 pecas de `moviki-app/material/` — **nenhuma escreve valor**, conferido
  no `catalogo.json`
