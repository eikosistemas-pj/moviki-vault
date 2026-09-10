---
type: arquivo
status: concluido
area: A1 - Produto e Paineis
tags: [quiz, segmentos, cardapio, conformidade, entrega]
atualizado: 2026-09-10
---

# ARQ - Suplementos sushi e otica no quiz

**No ar em 10/09/2026** — conferido no repositorio: `quiz-segmentos.js` ja tem
sushi, suplementos, naturais e otica.

O quiz de entrada passou de **9 abas / 27 opcoes** para **10 abas / 31 opcoes**.

## O que entrou

**Aba nova: Suplementos e Nutricao** (a 10a), entre Bebidas e Moda. Ficou fora de
Alimentacao de proposito: aqui o lojista **revende produto embalado**, nao prepara
comida na hora. Duas opcoes: *Suplementos / Nutricao Esportiva* e *Produtos
Naturais / Vitaminas*.

**Dentro de Alimentacao:** Sushi / Comida Japonesa — combinados, temaki e porcoes,
bebidas.

**Dentro de Servicos:** Otica / Oculos (de 5 para 6 opcoes) — oculos de sol, de
grau, ajustes e acessorios.

Quem escolher qualquer uma ja entra no painel com o cardapio montado; e so trocar
nome e preco.

## Regras de conformidade, gravadas dentro do codigo

**Suplemento nao pode ser anunciado com promessa de resultado.**
Proibido: emagrece, seca, queima gordura, ganha massa, aumenta imunidade, cura,
previne doenca, "resultado em X dias". Permitido: o fato do produto — peso do
pote, numero de capsulas, porcao, sabor. Base: ANVISA RDC 243/2018 + politicas de
anuncio do Meta e do Google. A chamada do robo social ficou no neutro
"ACHOU NO MOVIKI".

**Otica nao oferece exame de vista.** "Exame de vista", "medimos seu grau" e
"teste de vista gratis" sao atendimento de saude: dependem de profissional
habilitado, derrubam anuncio e trazem risco com a vigilancia sanitaria. O padrao
e vender oculos (de grau, com a receita do oftalmologista) e ajustar armacao.

As duas regras estao como comentario dentro dos proprios arquivos.

## Arquivos

| Repositorio | Caminho | Acao |
| --- | --- | --- |
| `moviki-app` | `quiz/quiz-segmentos.js` | substituiu |
| `moviki-assistente-social` | `src/segmentos.py` | substituiu |
| `moviki-assistente-social` | `assets/fundos/LEIA-ME.md` | substituiu |

`index.html` **nao foi tocado**: o quiz monta as abas sozinho lendo o
`quiz-segmentos.js`. Nenhuma regra do Firebase mudou.

## Como o quiz funciona por dentro

- A arvore inteira vive em `moviki-app/quiz/quiz-segmentos.js`
- **Icone que nao existe vira emoji automaticamente** — nunca quebra a tela
- Aba com uma unica opcao pula a segunda pergunta sozinha
- O robo social tem uma **copia** da lista em `src/segmentos.py`: mexeu numa,
  mexe na outra, senao o post sai com o segmento errado

## Solto

O comentario na linha ~4781 do `index.html` ainda diz "9 macros, 27 subtipos". E
so comentario — nao vale subir um arquivo de 475 KB por causa disso.

## Testes

Suplementos e sushi: 84 verificacoes em 6 larguras. Otica: 40 verificacoes em 5
larguras. Zero falhas nos dois.

## Ligacoes

[[A1 - Produto e Paineis]] · [[A8 - Conteudo e Social]] ·
[[A10 - Conformidade e LGPD]] · [[P22 - Icones 3D pendentes do quiz]]
