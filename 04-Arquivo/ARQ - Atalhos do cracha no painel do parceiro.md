---
type: arquivo
status: concluido
area: Painel do parceiro
tags: [cracha, qrcode, divulgacao, trava-aulas, parceiro]
atualizado: 2026-09-04
---

# ARQ - Atalhos do crachá no painel do parceiro

**Entrega de 04/09/2026** no `parceiro.html` (repo `moviki-app`).

## O problema

O crachá com QR é o último cartão da seção **Divulgação**. Quem está na Visão
geral, na folha de compartilhar (botão + da barra do celular) ou no menu Mais
não tem como saber que ele existe — e o crachá só serve se o parceiro lembrar
dele **na hora** em que o comerciante desconfia, na rua, com o celular na mão.

A página `/v/` já tinha esse problema resolvido pelo crachá; o crachá ainda
tinha o mesmo problema para si.

## O que entrou — três portas

| Onde | Forma |
|---|---|
| Card "Compartilhe seu link" (coluna direita / topo no celular) | Botão de **linha inteira** com ícone de QR, abaixo da grade Copiar/WhatsApp/Facebook/Mais |
| Folha `ovShare` (botão + da barra inferior) | Botão "Meu crachá" ocupando a linha inteira do grid |
| Menu `ovMais`, seção Painel | Item "Meu crachá", logo depois de Divulgação |

Todos com `data-cracha="1"`, um único delegador de clique, uma única função
`window.mvIrCracha()`.

**Por que não virou o 5º ícone da grade:** `.rcAcoes` é `repeat(4, 1fr)`. Cinco
ícones no celular espremem o rótulo até a reticência e quebram a linha. Botão de
linha inteira é mais visto e não mexe na grade existente.

## A regra que o atalho respeita

O crachá afirma **"treinamento concluído"** — por isso mora atrás da trava das
aulas. O atalho respeita a mesma trava, com uma diferença deliberada:

> **Travado, o atalho NÃO some.** Sumir cria a dúvida "cadê?" e vira chamado no
> suporte. Ele fica laranja, o subtítulo passa a "Abre quando você terminar as
> aulas" e o clique leva para os tutoriais em vez do crachá.

**Fonte do estado:** a classe `.mvTravado` que o `trava()` já pinta na seção
Divulgação. Ler o estado **já pintado** evita duplicar a regra das 8 aulas em
dois lugares que podem divergir depois — foi decisão de projeto, não atalho de
implementação.

## Detalhes de implementação

- Liberado: fecha as folhas → `mvIrSec('divulgacao')` → `scrollIntoView` no
  `#crachaCard` com pulso ciano de 2 ciclos (`.crFoco`).
- **Espera de 380 ms** antes do `scrollIntoView`: o `irSec()` dispara um
  `scrollTo` suave até o topo, e abaixo disso os dois rolares disputam a tela
  no celular.
- `void c.offsetWidth` antes de re-adicionar `.crFoco` — sem isso a animação não
  reinicia no segundo clique.
- Os botões da folha e do menu levam `soAprovado`: quem não é parceiro aprovado
  não vê porta para um crachá que não existe.

## Como foi verificado

Chromium headless, `parceiro.html` carregado direto do arquivo:

- 3 atalhos presentes, `mvIrCracha` exposta, nenhum erro de página.
- **Travado:** clique chama `abrirTutoriais()` uma vez, **não** navega, **não**
  acende o foco; os 3 atalhos ficam com `.trancado` e o subtítulo trocado.
- **Liberado:** clique navega para `divulgacao`, acende `.crFoco`, e **não**
  chama os tutoriais.
- Atalho da folha `ovShare` e do menu `ovMais` fecham a folha antes de navegar.
- `node --check` nos 6 blocos de script: todos limpos.

Limite honesto: o teste roda sem o módulo Firebase (sem rede em `file://`), então
`mvIrSec` foi conferido com stub. A navegação real depende do painel logado.

## Regra de ouro que nasce daqui

> Atalho para conteúdo travado **não desaparece** — vira cadeado. Sumir é pior
> que trancar: quem não vê não pergunta "como libero?", pergunta "cadê?".

Ver também [[R - Regras de ouro]].
