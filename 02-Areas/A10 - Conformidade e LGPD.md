---
type: area
status: ativo
tags: [conformidade, lgpd]
atualizado: 2026-08-28
---

# A10 — Conformidade, Jurídico e LGPD

## Autorização permanente do Paulo
Achou no projeto qualquer coisa que vá contra regra da Meta ou do Google, **corrigir direto e mandar de volta** — sem pedir permissão e sem esperar ele pedir.

## O princípio, para reusar
**Descreva a REGRA, nunca o RESULTADO.**
"15% da mensalidade paga" é regra e é verdade. "R$ 284 por mês" é resultado e é previsão. A primeira passa; a segunda reprova o anúncio.

## As três perguntas antes de publicar qualquer página que fale de dinheiro do parceiro
1. Tem número que projeta **quanto a pessoa vai receber**? Tire.
2. Tem verbo no futuro sem condicional ("você ganha", "vai receber", "todo mês")? Condicione ao pagamento do comerciante.
3. Tem "para sempre", "garantido", "sem risco", "renda"? Troque por "comissão", "enquanto for cliente pagante", "sem custo para participar".

## Regras de ouro desta área
- **Conformidade tem que chegar até a página do FORMULÁRIO.** Landing limpa com página de cadastro prometendo ganho é a mesma reprovação, num lugar onde ninguém olha.
- **Antes de instalar rastreador, ler a própria política de privacidade.** O pixel da Meta foi barrado pela frase que o próprio Moviki publicou.
- **Descadastro de e-mail pede confirmação, não sai em um clique** — cliente de e-mail que pré-carrega links desinscreveria gente sem querer.
- A seção "Isso não é pirâmide?" é **ativo, não problema** — é a distinção legal que um revisor quer ver.
- **Declare o MECANISMO, não a intenção.** Na política do Vik, dizer que CPF, CNPJ, chave Pix e sequências de 8+ dígitos são filtrados **por regex no `memoria.js`** — e não só proibidos no prompt — é o que separa promessa de trava. Prompt não é trava de segurança.
- **Afirmação que depende de contrato de terceiro não se publica sem conferir o contrato.** "A Anthropic não treina modelo com este conteúdo" está no ar e precisa ser confirmada nos termos da conta.

## LGPD — estado
| Item | Estado |
| --- | --- |
| Consentimento e descadastro da newsletter | ✅ no ar |
| Base legal da medição por servidor (Meta) | ✅ na política |
| Exclusão de conta limpando Storage e subcoleções | ✅ no ar |
| `vik_memoria` declarada na política (seção 5) | ✅ **no ar em 28/08** → [[ARQ - LGPD do Vik na politica de privacidade]] |
| Não automatização de decisão (Art. 20) declarada | ✅ no ar — e verdadeira no código |
| Termos da Anthropic conferidos quanto a treino de modelo | 🟠 **pendente** → [[P11 - Pendencias operacionais do dono]] |

## Recursos
[[R - Checklist conformidade Meta e Google]] · [[ARQ - Conformidade Meta e Google nas landings]] · [[R - Vik - travas, prompt, memoria e ofertas]]
