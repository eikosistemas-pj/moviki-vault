---
type: decisao
status: concluido
area: A5 — Programa de Parceiros
tags: [moviki, qrcode, parceiros, armadilha, teste]
atualizado: 2026-09-03
---

# ARQ — Gerador de QR do crachá, 03/09/2026

O `mvQR` entrou no `parceiro.html` (marca `2026-09-03-cracha`). Modo byte,
correção **M**, versões 1 a 6 — escrito à mão porque a CSP do painel não deixa
carregar biblioteca de fora.

Detalhe completo em `claude/moviki-qr-do-cracha.md`.

## Não havia implementação de referência, e isso mudou o método

A lição do incidente anterior mandava comparar com uma referência. **Não dava:**
o PyPI deste ambiente não tem `segno` nem `qrcode`, o npm recusa o pacote
`qrcode` por política, e o Chromium headless **não tem `BarcodeDetector`**
(conferido, devolve `false`).

**A saída foi escrever o inverso: um decodificador independente**, do outro lado
da especificação, sem compartilhar uma linha com o gerador. Ele reconstrói do
zero o mapa de módulos reservados, lê o *format info* das duas cópias
separadamente, desmascara, desintercala e calcula as síndromes de Reed-Solomon.

Nove conferências por código: texto de volta · nível lido é **M** · format info
com distância 0 · as duas cópias iguais · síndromes zeradas · finders · timing ·
**módulo escuro** · máscara declarada igual à usada.

**22 casos dirigidos + 800 apelidos aleatórios, zero falhas**, as 8 máscaras
exercitadas. E o QR é lido de volta do **canvas renderizado** e da **imagem PNG
baixada**, não só da matriz em memória — o que valida também passo,
deslocamento e cor do desenho.

## O erro que o teste pegou

O **módulo escuro fixo** vinha apagado. Ao escrever a segunda cópia do format
info, o corte estava em 8 em vez de 7 — e o oitavo módulo daquela coluna **é** o
módulo escuro.

O sintoma seria traiçoeiro: leitor que usa a primeira cópia do format info leria
normalmente; leitor que usa a segunda leria errado. **Funcionaria em alguns
aparelhos e não em outros** — o mesmo formato do defeito anterior, em que as
versões pequenas liam "por sorte".

Foi o `moduloEscuro: false` do decodificador que apontou. Sem essa conferência,
o crachá ia para a rua quebrado pela segunda vez.

## O que continua dependendo do Paulo

**Apontar a câmera.** Round-trip contra decodificador próprio prova que a matriz
está certa pela especificação — não prova leitura em campo. Contraste, brilho,
moiré de LCD e distância não existem no teste.

## A regra de ouro que nasce daqui

> Sem implementação de referência, **escreva o inverso**. Um decodificador
> independente pega a mesma classe de erro que a comparação pegaria — desde que
> não compartilhe uma linha com o codificador.

## Ligações

[[P16 - Rodada da credibilidade]] · [[R - Verificacao publica de parceiro]] · [[ARQ - Erros de implementacao 03092026]] · [[R - Regras de ouro]]
