---
type: arquivo
status: concluido
area: A5 - Programa de Parceiros
tags: [parceiros, painel-parceiro, cracha, qr-code, armadilha, entrega]
atualizado: 2026-09-10
---

# ARQ - Foto do parceiro e o CORS da pagina de verificacao

**No ar em 10/09/2026** — `v.html` na marca `2026-09-10-foto-parceiro`,
`upload-imagem.js`, `novo-parceiro.js` e `espelhoParceiro.js` com o campo `foto`,
conferido no repositorio.

Duas coisas pedidas, resolvidas juntas porque sao o mesmo assunto: **quem manda
na foto do parceiro**.

## 1. O parceiro escolhe a propria foto

Antes a foto era, obrigatoriamente, a do Instagram do @ dele: quem nao tem
Instagram ficava so com a inicial, e quem tem foto melhor nao podia usar.

Agora, na aba **Meus dados**, o bloco **"Sua foto"** com previa redonda,
**Trocar foto** e **Remover**. O navegador reduz para um quadrado de 320px, corte
no centro (a foto sempre aparece dentro de um circulo) e comprime ate caber.
Vale em quatro lugares de uma vez: cabecalho, coluna lateral, previa e **cracha**,
inclusive no cracha baixado como imagem.

Prioridade: **foto escolhida por ele > foto do Instagram > inicial do nome.** Quem
trocou na mao nunca ve a do Instagram voltar sozinha.

## 2. O bug: a foto nao chegava a quem lia o QR Code

**Sintoma:** o painel do parceiro tinha foto, a pagina de confirmacao nao.
Nenhum erro na tela.

**Causa:** a `v.html` mora em `moviki.com.br`; o robo carimbava a resposta com
**um endereco so**, `app.moviki.com.br`. O navegador do comerciante buscava a
foto, via que o carimbo nao batia e **jogava fora, calado**.

> Defeito que nao aparece em teste nenhum feito de dentro do painel: la funciona.

**As duas correcoes, em camadas:**

1. O robo passou a reconhecer os tres enderecos (`app.moviki.com.br`,
   `moviki.com.br`, `www.moviki.com.br`), com `Vary: Origin` junto — sem ele a
   CDN guardaria a resposta de um endereco e serviria para o outro, e o bug
   voltaria de forma intermitente.
2. A foto passou a viajar **dentro do proprio documento** que a pagina do QR ja
   le. Nesse caminho nao existe busca na rede: a foto aparece no instante em que
   a pagina abre.

## Onde a foto fica guardada

Como **data: URI** em `parceiros/{uid}.foto`, copiada para o espelho publico
`parceiros_publicos/{slug}.foto`.

**Por que nao no Storage:** a foto e desenhada dentro de um `<canvas>` na hora de
baixar o cracha. Imagem de outro dominio contamina o canvas e o navegador proibe
o download — o botao "Baixar como imagem" pararia de funcionar.

**Por que passa pelo robo:** a regra do Firestore so deixa o parceiro mexer em
`nome`, `pix` e no progresso das aulas. O robo grava pelo Admin SDK — **nenhuma
regra nova precisou ser publicada**.

Tamanhos: o painel envia perto de 40 KB, o robo recusa acima de 200 KB, o espelho
ignora o que nao for imagem. Teto do Firestore e 1 MB por documento.

## Aprendizados

- **Endpoint do robo chamado por pagina fora do app precisa entrar na lista de
  enderecos permitidos.** Sintoma de esquecer: funciona no painel, nao funciona
  no site, e nenhum erro na tela.
- Imagem desenhada em `<canvas>` precisa ser **embutida**, nunca de outro
  dominio — senao o download morre.
- Quando a regra do Firestore nao permite um campo novo, gravar pelo robo evita
  publicar regra e evita o risco de esquecer de publicar.

## Validacao

85 verificacoes, 0 falhas: painel (38), pagina do QR (21) e robo (26), incluindo
**o Pix nao vaza para o espelho publico** e o download do cracha continua
funcionando.

## Ligacoes

[[A5 - Programa de Parceiros]] · [[A2 - Infraestrutura e Deploy]] ·
[[P14 - Verificacao de parceiro]] · [[R - Marcas de versao no ar]]
