---
type: recurso
status: referencia
area: A11 - Marca e Design System
tags: [motion, animacao, interface, design-system, performance, lazy]
atualizado: 2026-09-23
---

# R - Motion principles

Sistema único de movimento e carregamento preguiçoso do Moviki, criado em
23/09/2026. Vale para toda tela nova.

## Arquivos

- `mvmotion.js` — o motor. Marca `2026-09-23-motion1` (`mvMotion.versao` no console).
- Seção **16. MOTION** do `movikiui.css`.
- Os dois sobem **idênticos** em `moviki` e `moviki-app`.
- O `mvmetrica.js` injeta o `mvmotion.js`: **as 15 páginas que carregam o `mvmetrica.js` receberam o movimento sem nenhum HTML mudar.**
- Página nova carrega o `mvmetrica.js` **ou** a linha `<script src="/mvmotion.js" defer></script>`.

## Os seis princípios

1. **Movimento explica, nunca enfeita.**
2. Só anima `opacity`, `translate`, `scale` e `transform` — nunca layout.
3. **Curto e assimétrico:** a entrada assenta, a saída acelera e é mais curta.
4. **Ferramenta não espera:** painel não tem revelação por rolagem.
5. **`prefers-reduced-motion` desliga tudo**, inclusive o pulso da página.
6. **Estado oculto só nasce no JS, e só abaixo da dobra.** Se o JS falhar, a página aparece inteira.

## Tokens

| Token | Valor |
| --- | --- |
| `--mv-dur-micro` | 120 ms |
| `--mv-dur-rapido` | 180 ms |
| `--mv-dur-base` | 240 ms |
| `--mv-dur-medio` | 320 ms |
| `--mv-dur-lento` | 560 ms |
| `--mv-ease` | mudança de estado |
| `--mv-ease-entra` | entrada |
| `--mv-ease-sai` | saída |

**Nenhuma animação com duração ou curva solta.** Sempre pelos tokens.

## Os três modos (saem do endereço)

| Modo | Onde | O que acontece |
| --- | --- | --- |
| **Página** | site, `/apelido`, `/v/`, `seja-parceiro` | toque .97 · foco ciano · entrada do que aparece · revelação por rolagem com cascata de 70 ms · fade da imagem `lazy` · âncora suave · prefetch do HTML no hover (só o site, mesma origem) · transição entre páginas |
| **Painel** | `app.` index, parceiro, eikoadm01, `/criador` | toque · foco · entrada do que aparece (aba, modal com caixa que sobe, folha de baixo, aviso preso) · transição entre páginas |
| **Live** | `/live/…`, estúdio | toque · foco · entrada do que aparece |

## Detector de aparição

Escuta `class`, `style` e `hidden`, e só anima quando o estado ANTERIOR era
escondido (`hide`, `escondido`, `oculto`, `mv-oculto`, `qzEscondido`,
`display:none`, `hidden`). Ignora quem já tem fade próprio, o Leaflet, vídeo e
canvas.

## Chaves

- **Chave-mestra:** `MV_MOTION_LIGADO` no topo do `mvmotion.js` (subir nos dois repos).
- **Diagnóstico por visitante:** `?motion=0` no endereço.
- **Trecho que não se mexe:** atributo `data-mv-sem-motion`.
- A chave fica **no arquivo, não no painel do dono, de propósito**: ler o Firestore em toda visita para um módulo cosmético custa leitura e depende do App Check.

## API para tela nova

`mvMotion.entrar(el)` · `mvMotion.sair(el, fim)` · `mvMotion.revelar(el)` ·
classes `mv-entra` e `mv-skel`.

## Carregamento preguiçoso (lazy)

- **Ícone de interface: no máximo 256 px e ~15 KB.** Otimiza-se com o **mesmo nome e a mesma dimensão** — nenhum HTML muda.
- **Imagem em menu fechado leva `loading="lazy"`**. Logo e herói, nunca (herói leva `fetchpriority="high"`).
- **Biblioteca que só o `<script type="module">` usa vai com `defer`** (ex.: Leaflet).
- Vídeo com `preload="none"`, YouTube em fachada.

## Não fazer

- Não pôr `loading="lazy"` no logo nem na imagem principal do herói.
- Não mexer no `mvmotion.js` por dentro de um HTML — ele é compartilhado.
- Não criar revelação por rolagem em painel.

## Ligações

[[A11 - Marca e Design System]] · [[ARQ - Motion e lazy loading 23092026]] ·
[[R - Regras de ouro novas de 17 a 23092026]]

*Reconstruída em 23/09/2026 a partir do MAPA-MESTRE de 23/09.*
