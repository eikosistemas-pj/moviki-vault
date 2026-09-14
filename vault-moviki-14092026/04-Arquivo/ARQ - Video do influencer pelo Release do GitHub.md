---
type: arquivo
status: concluido
area: A14 - Material de apoio do parceiro
tags: [video, github, release, material-de-apoio, ffmpeg]
atualizado: 2026-09-12
---

# ARQ — Vídeo do influencer pelo Release do GitHub

O caminho para **vídeo grande** entrar no material de apoio.

## O problema

Vídeo acima de **25 MB** não entra:

- **não sobe pelo GitHub web** (o arrastar do navegador não aguenta);
- **não entra como anexo do chat**;
- **Google Drive não serve** — a sandbox não baixa o arquivo de lá.

## O caminho que funciona

1. O Paulo publica o arquivo **bruto** como **anexo de Release** do GitHub —
   release `Material_bruto`, no repositório **`moviki-app`**, limite de **2 GB**
   por arquivo.
2. Manda o link do anexo no chat.
3. A sandbox **baixa asset de release sem problema** e devolve: vídeo comprimido
   **≤ 20 MB**, capa e `catalogo.json`.

## Caso real (12/09/2026)

| Etapa | Dado |
| --- | --- |
| Bruto | `video_vertical_influencer_material_apoio_parceiro.MOV` |
| Tamanho | 89 MB |
| Codec | HEVC 10 bits |
| Resolução / duração | 1080x1920 · 1:07 |
| Entregue como | `material/video-influencer-parceiro.mp4` |
| Tamanho final | 17 MB — H.264, **2 passagens a 2 Mbps** |
| Catálogo | `2026-09-12-1` |
| Estado | **No ar em 12/09/2026** |

HEVC 10 bits não toca em todo celular antigo; a reconversão para H.264 8 bits
não é só compressão, é compatibilidade.

## Regra que fica

Vídeo grande **sempre** pelo anexo de Release do `moviki-app`, nunca por Drive,
nunca por anexo de chat. O bruto fica guardado no Release; o repositório só
recebe o comprimido.

## Ligações

[[A14 - Material de apoio do parceiro]] ·
[[ARQ - Aba Material de apoio do parceiro]] ·
[[A8 - Conteudo e Social]] · [[R - Stack e repositorios]] ·
[[R - Links e identificadores]]
