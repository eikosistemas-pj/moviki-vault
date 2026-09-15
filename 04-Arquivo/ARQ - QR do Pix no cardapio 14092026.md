---
type: arquivo
status: concluido
area: "[[A13 - Modo Live]]"
tags: [qr, pix, mvqr, cardapio, pagina-publica, entrega]
atualizado: 2026-09-14
---

# ARQ - QR do Pix no cardapio 14092026

Fecha o que tinha ficado de fora em
[[ARQ - Cardapio compravel na pagina publica 14092026]]. Substitui o projeto
P32, que nasceu e morreu na mesma noite.

## Arquivos

| Repositorio | Arquivo | Marca | Tipo |
|---|---|---|---|
| moviki | `mvqr.js` | 2026-09-14-mvqr2 | NOVO |
| moviki-app | `mvqr.js` | 2026-09-14-mvqr2 | SUBSTITUI |
| moviki | `404.html` | 2026-09-15-compra3 | SUBSTITUI |

O mesmo arquivo nos dois repositorios, de proposito: duas copias divergentes do
gerador seriam dois lugares para consertar o mesmo bug — foi por isso que ele
saiu do `parceiro.html` em 04/09.

## Por que o QR nao existia

O `mvqr.js` cobria as versoes **1 a 6**, nivel M: teto de **108 bytes**. Um BR
Code Pix fica entre **130 e 190 bytes**, mesmo com chave curta — so a chave
aleatoria tem 36 caracteres. Na pratica **nao cabia em nenhum caso**: `mvQR`
devolvia `null` em toda venda.

## O que entrou

Versoes **7 a 13** (teto de 331 bytes), e com elas tres coisas que nao existiam
no arquivo:

1. **Tabela de blocos e correcao** das versoes 7 a 13.
2. **Contador de 16 bits a partir da versao 10** — ate a 9 sao 8 bits. Errar
   isso produz um codigo que fecha o CRC e que nenhum leitor abre.
3. **Bloco de version info**: 18 bits de BCH(18,6), gerador `0x1F25`, escritos
   em DOIS cantos. Obrigatorio da versao 7 em diante; sem ele o leitor nao sabe
   o tamanho do simbolo.

A escolha da versao passou a somar o cabecalho real em vez do `+2` fixo: na
fronteira da versao 10 o contador muda de tamanho e o `+2` erraria por um byte.

## Como foi validado, sem biblioteca de referencia

PyPI e npm recusam os pacotes de QR neste ambiente e o Chromium do sandbox nao
tem `BarcodeDetector`. A prova foi a mesma do cracha, de 03/09:

- **Decodificador independente**, escrito do lado inverso da especificacao, sem
  compartilhar funcao nenhuma com o gerador: reconstroi o mapa de modulos
  reservados, le as duas copias do format info e do version info separadamente,
  desmascara, desintercala os blocos e calcula as sindromes de Reed-Solomon.
- **Prova cruzada da tabela**: o numero de modulos livres do simbolo tem que dar
  exatamente o total de codewords da tabela. Tabela errada nao passa.
- **331 casos, zero falhas**: as 13 versoes, as fronteiras exatas de capacidade
  de cada uma (14, 26, 42, 62, 84, 106, 122, 152, 180, 213, 251, 287, 331
  bytes), 300 textos aleatorios, acentuacao, 5 payloads Pix reais (chave
  aleatoria, CNPJ, CPF, e-mail longo e telefone) e as 8 mascaras exercitadas.
- **Regressao**: para as versoes 1 a 6 a matriz e **identica modulo a modulo** a
  do gerador que esta no ar desde 03/09. O cracha do parceiro e o do dono nao
  mudam de desenho — e por isso o `mvqr.js` do `moviki-app` pode ser substituido
  sem risco.
- **Lido de volta do canvas renderizado** no Chromium, nao so da matriz em
  memoria: o teste acha a moldura pelos pixels, deduz o passo, reamostra os
  modulos e decodifica. Isso valida tambem o deslocamento, o passo e as cores do
  desenho.

## Na tela

O QR e desenhado a partir do **copia-e-cola que o servidor mandou**. A pagina
continua sem montar payload de Pix — montar no navegador e entregar o ataque de
QR trocado de bandeja. Se o gerador nao carregar, ou o texto nao couber, a caixa
some sozinha e o copia-e-cola segue fazendo o trabalho.

No modo Asaas nada muda: la a imagem ja vem pronta do gateway.

## Pendencia aberta no teste do Paulo

A chave cadastrada na Hamburgueria Master e de um gerador de Pix de teste, mas
**titular e documento continuam sendo os da EIKO** — a tela do comprador mostra
"EIKO SISTEMAS DESENVOLVIMENTO DE SOFTWARE LTDA" e o CNPJ da empresa. Duas
consequencias:

- chave de gerador de teste **nao existe no DICT**: o banco do comprador recusa
  na hora de pagar;
- se a chave fosse boa, o dinheiro de cliente de lojista cairia na conta da
  EIKO, que e exatamente o que a [[R - Doutrina de seguranca financeira]] existe
  para impedir.

Para o teste real: chave EVP de conta pessoal, com titular, documento e cidade
correspondentes.
