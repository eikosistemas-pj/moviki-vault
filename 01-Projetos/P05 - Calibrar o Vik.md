---
type: projeto
status: ativo
prioridade: 2
area: A9 — IA e Atendimento (Vik)
prazo: 
tags: [ia]
atualizado: 2026-08-28
---

# P05 — Calibrar o Vik nas primeiras semanas

## Resultado esperado
Confiança de que o Vik guarda o que vale e oferece na hora certa — **pré-requisito para ligar o padrão global**.

## Por que subiu de prioridade 3 para 2 em 28/08
Com a LGPD fechada, o que segura o Vik em escala deixou de ser conformidade e passou a ser **calibragem**. O padrão global existe e está DESLIGADO de propósito: ele multiplica qualquer erro de extração de memória por **todas** as conversas de uma vez. Antes era higiene; agora é o gargalo.

## O que fazer
- Abrir o cartão **"O que o Vik aprendeu desta pessoa"** (painel do dono) em algumas contas e conferir se os fatos extraídos fazem sentido.
- **Memória errada envenena todas as conversas seguintes daquela conta, em silêncio.** O botão de apagar zera só o resumo; as mensagens não são tocadas.
- Se estiver oferecendo cedo ou tarde demais, os três números estão no topo de `lib/oportunidade.js`: **20 / 60 / 150** visitas. Mexer neles muda a agressividade comercial do Vik inteiro.

## Definição de pronto
- [ ] 5 contas auditadas
- [ ] Números 20/60/150 confirmados ou ajustados
- [ ] Registro do ajuste em [[R - Vik - travas, prompt, memoria e ofertas]]
- [ ] **Só então:** ligar `vikPadraoLigado` no painel do dono

## Ligações
[[A9 - IA e Atendimento Vik]] · [[ARQ - LGPD do Vik na politica de privacidade]] · [[P06 - Camada 3 do Vik]]
