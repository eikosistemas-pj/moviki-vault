---
type: projeto
status: ativo
prioridade: 2
prazo:
area: Conteudo
tags: [reel, video, kairogen, kling, pos-producao, instagram]
atualizado: 2026-09-11
---

# P24 - Reel 01 "Cada negócio tem sua rotina"

Reel vertical institucional de 18 s, 9:16, 1080×1920, 30 fps.
Fonte única de roteiro, prompts e mixagem: `GUIA_DE_PRODUCAO.md` do pacote
`MOVIKI_Reel01_Pacote_Completo.zip`. Locução pela Malu (`fhtZMBwha5du5OxuvexO`),
ver [[R - Voz oficial das videoaulas]].

## Regra de produção

- **Uma cena por vez.** Nenhuma geração nova nem retentativa sem autorização
  explícita do Paulo.
- Só imagem para vídeo. Sem texto para vídeo, sem redesenho, sem KairoBoost, sem
  áudio na geração. Prompt do guia usado **literalmente**.
- Modelo padrão: **Kling V3.0 Pro** (`kling-v3-0-pro`), 1080p, sem som, 1 saída.
  Único da conta com 3 s e 4 s exatos e boa fidelidade à imagem.
- Nenhum modelo da conta tem máscara de movimento, controle por região ou
  negative prompt. A proteção de texto e logo fica só no prompt.
- O conector da Kairogen só recebe imagem pelo widget de upload; o Paulo sobe e
  devolve a URL do CDN.

## Andamento

| Cena | Imagem | Dur | Status | Créditos |
| --- | --- | --- | --- | --- |
| 1 | `01_abertura_rotina.png` | 3 s | **Aprovada com ajuste de pós** | 14 |
| 2 | `02_painel_clientes_informados.png` | 4 s | **Reprovada como vídeo de IA** - vira animação de edição | 19 (perdidos) |
| 3 | `03_recursos_em_um_so_lugar.png` | 5 s | **Reprovada como vídeo de IA** - vira animação de edição | 23 (perdidos) |
| 4 | `04_negocios_moveis_pontos_fixos.png` | 3 s | Gerada, aguardando avaliação | 14 |
| 5 | `05_card_final.png` | 3 s | Pendente | - |

## Cena 1 - orientação obrigatória para a montagem

- Arquivo original, **manter intacto**:
  `https://cdn.kairogen.ai/gallery/videos/6a85cb71af7328d006a48d4c/2d653228-9f42-44f7-9b38-942f977b1836.mp4`
  (geração `6aa3713b547578459c649942`).
- **Reproduzir o clipe de trás para frente.** No original a comerciante fecha a
  porta; invertido, ela abre a loja, como pede o roteiro.
- Efeitos colaterais da inversão, conferir na timeline:
  - a aproximação da câmera vira **afastamento**. Compensar com zoom digital de
    100% para 105% ao longo dos 3 s, depois da inversão;
  - o food truck passa a andar **para trás**;
  - se as luzes do truck acenderam no original, **apagam** no invertido. Se isso
    aparecer, cortar a metade esquerda do clipe invertido pela linha ciano
    diagonal e usar ali a metade esquerda do clipe original;
  - o último quadro do invertido é a imagem original (luzes acesas e loja
    aberta): **é o quadro da capa do Reel**.
- Nova geração da Cena 1: **proibida**, sem consumo de créditos.

## Cena 2 - reprovada, solução de pós-produção

A Kairogen alterou e deformou as informações da tela oficial do MOVIKI. O vídeo
gerado (`6aa3737295bd5dc6e3d59bbc`) **não pode ser usado**. Nova geração:
**proibida**, sem consumo de créditos.

Montagem no editor:

- usar a imagem original `02_painel_clientes_informados.png` por **4 s**;
- aplicar só aproximação digital suave de **100% para 104%**;
- interface, textos, logo e botões **totalmente intactos**;
- cursor e destaque ciano entram **só como elementos de edição**, sem IA.

## Cena 3 - reprovada, solução de pós-produção

A Kairogen deformou os nomes dos recursos ("Vídeos" virou "Fíoos", "Horários"
virou "Viíaes") e modificou a tela do celular. O vídeo gerado
(`6aa374c3547578459c64a61c`) **não pode ser usado**. Nova geração: **proibida**,
sem consumo de créditos.

Montagem no editor:

- usar a imagem original `03_recursos_em_um_so_lugar.png` por **5 s**;
- aproximação suave de **100% para 103%**;
- pequeno movimento vertical;
- destaque sequencial de Cardápio, Promoções, Fotos, Vídeos, Horários e WhatsApp,
  **todos feitos no editor**;
- imagem, tela, logo e textos originais **totalmente intactos**.

## Cena 4 - gerada, aguardando avaliação

- Geração `6aa3765af0f873dcfb84ac0c`, Kling V3.0 Pro, 3 s, 9:16, 1080p, sem som:
  `https://cdn.kairogen.ai/gallery/videos/6a85cb71af7328d006a48d4c/42e14c77-a755-4414-955d-d8a2525f9b69.mp4`
- Na miniatura: FOOD TRUCK, FEIRA, LOJA, ESCRITÓRIO, logo e título corretos.
- Desvios vistos: linhas ciano novas saem só de FOOD TRUCK e FEIRA (assimétrico);
  houve aproximação de câmera não pedida, que corta "PRODUTO" no quadro da feira;
  a lojista trocou o saco de papel por um pote verde; a dupla do escritório virou
  o rosto uma para a outra.

## Regra proposta - aguarda confirmação do Paulo

**Tela real do sistema MOVIKI não passa por geração de vídeo por IA.** Nenhum
modelo da conta tem máscara ou proteção de região; o modelo reescreve texto
pequeno de interface. Cena com tela vira imagem original + movimento de edição.

## Ligações

[[P08 - Aquecimento do Instagram]] · [[R - Voz oficial das videoaulas]]
