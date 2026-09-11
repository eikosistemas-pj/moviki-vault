---
type: arquivo
status: no-ar
area: A13 - Material de apoio do parceiro
tags: [parceiro, material-de-apoio, panfleto, qr, conar]
atualizado: 2026-09-11
---

# Aba Material de apoio do parceiro

Entregue em 11/09/2026. Marca: `parceiro.html` **2026-09-11-material**, montada
sobre a **2026-09-10-icones-nivel** (conferida no GitHub antes da entrega).

## O que é
- Aba nova no painel do parceiro com panfleto, posts de feed, stories, vídeos e textos prontos.
- Destaque: botão largo no topo da Visão geral (a barra de baixo já tem 5 lugares), item verde no menu lateral e no menu Mais, etiqueta NOVO.
- Ícone 3D novo: `icones/material.png` e `icones/material-48.png`.

## Decisões
- **Catálogo estático** `material/catalogo.json` no `moviki-app`. Nada no Firestore: zero leitura paga, zero regra nova. Material novo não mexe no `parceiro.html`.
- **Panfleto com QR sem arquivo por parceiro**: uma arte só; o QR do parceiro é desenhado por cima no navegador dele, na posição do catálogo (`qr:{x,y,l}`). Mesmo destino do crachá, `moviki.com.br/v/apelido`, com `utm_source=panfleto&utm_medium=qr` para o GA4 separar quem veio do papel. Embaixo do QR vai o endereço escrito.
- **Mesmas portas do link**: baixar e enviar só com cadastro aprovado, aulas concluídas e compromisso de divulgação aceito. Lido do estado já pintado na tela (`.mvTravado`, `#condBox.ok`).
- **Toda legenda começa com #publi** e já leva o link do parceiro (`{link}`).
- **Botões Instagram, Facebook e WhatsApp em cada material** (marca **2026-09-11-postar**). Instagram e Facebook não aceitam postar imagem por link vindo de site: no celular o toque abre a lista de apps do próprio aparelho com o ARQUIVO já anexado e a legenda copiada — ele toca na rede e cai na tela de postar. No computador: a rede abre numa aba, o arquivo baixa e a legenda vai para a área de transferência. Safari: se o arquivo ainda não estava pronto, o 1º toque prepara e o botão pisca "Toque de novo".
- **Peso**: na abertura do painel só o catálogo (7 KB, 6 s depois). Capas WebP de 320 px (20 a 36 KB) só quando a aba abre. Arquivo cheio só na prévia.
- Estrutura no ar com subpastas (`capas/`, `feed/`, `panfletos/`, `stories/`); arquivo novo entra em pasta que já existe.
- Vídeo: MP4 até 20 MB, solto em `material/` com a capa; maior vai como anexo de Release do GitHub. 1º vídeo: `video-cada-negocio-tem-sua-rotina.mp4` (27 MB → 6,4 MB), catálogo `2026-09-11-2`.

## Kit inicial (artes do Paulo)
- 1 panfleto A5 (ampliado 2x para impressão: 2110x2982)
- 5 feed 4:5 + 2 quadrados 1:1
- 3 stories 9:16
- 3 textos prontos: primeira mensagem ao comerciante, "você é mesmo do Moviki?", bio
- De ~2 MB (PNG) para ~350 KB (JPG) por arte, sem diferença visível

## Testado
- Chromium com Firebase simulado, celular e desktop, três perfis (livre, sem aceite, pendente)
- QR do panfleto decodificado em tamanho cheio e comprimido como no WhatsApp (844 a 1604 px)

## Pendências
- NO AR em 11/09 (conferido clonando): `parceiro.html` 2026-09-11-material, `icones/material*.png` e `material/` inteira. Registrar em [[R - Marcas de versao no ar]]
- Vídeo no ar em 11/09 (catálogo `2026-09-11-2`)
- `parceiro.html` 2026-09-11-postar NO AR em 11/09 (conferido clonando) e confirmado pelo Paulo
- Trocar "Atualizado há 7 dias" por "Atualizado agora" no celular desenhado do panfleto e do vídeo
- Arte do panfleto em resolução de impressão (1748x2480 ou maior), se existir o original

Relacionado: [[A13 - Material de apoio do parceiro]] · [[R - Regras de ouro]]
