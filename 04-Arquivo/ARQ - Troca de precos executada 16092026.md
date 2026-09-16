---
type: arquivo
status: concluido
area: A4 - Financeiro
tags: [preco, planos, troca, execucao, marcas-de-versao]
atualizado: 2026-09-16
---

# ARQ - Troca de precos executada 16092026

Execucao do cenario B confirmado em 16/09/2026. **13 arquivos em 4 lotes**,
montados a partir do clone dos repositorios no mesmo dia — nao de memoria nem de
busca no Project.

Relacionado: [[ARQ - Decisao de preco antes do lancamento 16092026]] ·
[[R - Troca de precos - onde o valor vive]] · [[R - Planos e precos]]

---

## Os valores

| | Antes | Depois |
| --- | ---: | ---: |
| Pro | R$ 37,90 | **R$ 39,90** |
| Premium | R$ 49,90 | **R$ 69,90** |
| Enterprise | R$ 99,90 | **R$ 129,90** |
| Anual Pro | R$ 379,00 | **R$ 399,00** |
| Anual Premium | R$ 499,00 | **R$ 699,00** |
| Trimestral | 99,90 / 134,90 | **aposentado** |
| Ponto extra Enterprise | R$ 19,90 | **R$ 19,90** (mantido) |
| Comissao N1 Pro | R$ 5,69 | **R$ 5,99** |
| Comissao N1 Premium | R$ 7,49 | **R$ 10,49** |
| Comissao N1 Enterprise | R$ 14,99 | **R$ 19,49** |

Basico continua gratis. Percentual de comissao **nao mudou** — mudou o valor em
reais porque a mensalidade mudou.

---

## A ORDEM DE SUBIDA — nao inverter

**Lote 1 - CONTRATO E O QUE FALA (sobe primeiro).** A regra escrita e o que o
Vik responde precisam estar certos antes de qualquer tela anunciar o valor novo.

| Repo | Arquivo | Marca |
| --- | --- | --- |
| `moviki` | `termos.html` | `2026-09-16-preco1` |
| `moviki-ai` | `lib/catalogoPainel.js` | — |
| `moviki-ai` | `lib/promptAtendimento.js` | — |
| `moviki-robo` | `api/lembrete-trial.js` | — |

**Lote 2 - SITE PUBLICO.**

| Repo | Arquivo | Marca |
| --- | --- | --- |
| `moviki` | `index.html` | `2026-09-16-preco1` |
| `moviki` | `premium.html` | `2026-09-16-preco1` |
| `moviki` | `enterprise.html` | `2026-09-16-preco1` |
| `moviki` | `comerciantes.html` | `2026-09-16-preco1` |
| `moviki` | `parceiros.html` | `2026-09-16-preco1` |

**Lote 3 - PAINEIS.**

| Repo | Arquivo | Marca |
| --- | --- | --- |
| `moviki-app` | `index.html` | `2026-09-16-preco1` |
| `moviki-app` | `parceiro.html` | `2026-09-16-preco1` |
| `moviki-app` | `eikoadm01.html` | `2026-09-16-preco1` |

**Lote 4 - COBRANCA (sobe POR ULTIMO, sozinho).**

| Repo | Arquivo | Marca |
| --- | --- | --- |
| `moviki-robo` | `lib/asaas.js` | — |

> **Por que por ultimo:** se a landing anunciar o preco novo antes de a cobranca
> mudar, o lojista assina um valor e e cobrado outro. Isso e problema de
> consumidor, nao de sistema.

---

## O que foi encontrado na varredura que nao estava no plano

- **Os dois `regulamento.html` NAO tem preco de plano.** So percentuais e marcos.
  A lista original mandava trocar os dois; a leitura do arquivo desmentiu. **Nao
  foram tocados.**
- **`moviki/termos.html` TEM a tabela de planos** e nao estava na lista. E
  contrato — entrou no lote 1, com a data de "Ultima atualizacao" corrigida.
- **`moviki-app/index.html` linha 3691: `var BASE=99.90`** — o resumo de custo
  do multi-ponto. Nao aparece em busca por "R$ 99,90" porque esta escrito com
  ponto. Corrigido para 129.90.
- **JSON-LD com preco em tres paginas** (`index.html`, `premium.html`,
  `enterprise.html`). E o preco que o Google le. Corrigido.
- **`premium.html` tinha DUAS ofertas "Premium anual" no JSON-LD** depois da
  conversao da trimestral — uma de R$ 699 e a antiga de R$ 499. A duplicada foi
  removida e a descricao corrigida para "R$ 58,25 por mes".
- **`comerciantes.html` tem BOM e CRLF.** Salvar em LF quebraria o diff inteiro.
  Preservado byte a byte.

### Falsos positivos descartados (nao mexer)

`quiz-segmentos.js` (preco de creatina num exemplo) · `webhook.js` (payload de
exemplo em comentario) · `404.html` (base64) · `pontos.js` e `contextoUsuario.js`
(ponto extra R$ 19,90, que foi mantido) · `segurancaVik.js` (comentario citando
frase legitima).

---

## A trava do trimestral

O deep-link `?plano=X&periodo=trimestral` existe em link antigo e em conversa de
WhatsApp. Foram postas **duas travas** no painel do lojista:

1. no deep-link: periodo fora de `mensal|anual` vira `mensal`;
2. dentro de `selecionarPlano`: se nao existe rotulo para o par plano/periodo,
   cai no mensal.

E se mesmo assim chegar ao `lib/asaas.js`, o `criar-assinatura.js` recusa com
400 — que e o comportamento correto: **nunca cobrar um valor que a tela nao
mostrou.**

---

## Conferir depois de subir

- [ ] `Ctrl+Shift+R` em cada pagina antes de julgar
- [ ] Painel do lojista > **Meu plano**: valores novos e **nenhum botao de
      trimestral**
- [ ] Abrir `app.moviki.com.br?plano=premium&periodo=trimestral` e ver se cai no
      mensal
- [ ] Perguntar ao Vik "quanto custa o Premium?" e conferir a resposta
- [ ] Assinatura de teste e conferir o valor **cobrado** no Asaas
- [ ] Painel do dono > **Custos e margem**: a receita estimada subiu

## Divida que ficou

- [ ] **Regerar `moviki-img-planos.png` e `moviki-img-parceiros-comissoes.png`**
      — imagem com preco velho nao da erro, nao aparece em busca de texto e
      circula por meses
- [ ] Trocar o PDF do prompt de atendimento na base da Meta
- [ ] Conferir o material de apoio do parceiro (81 pecas) peca a peca
- [ ] Atualizar a secao 2 do `MAPA-MESTRE.md`
