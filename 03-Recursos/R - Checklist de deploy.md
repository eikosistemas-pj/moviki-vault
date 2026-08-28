---
type: recurso
status: referencia
area: A2 — Infraestrutura e Deploy
tags: [deploy, checklist]
atualizado: 2026-08-28
---

# R — Checklist de deploy

## Antes de entregar o arquivo
- [ ] Arquivo **completo**, nome final, validado — nunca "pedaço + onde colar"
- [ ] Diz o **repositório**, a **pasta** e se é **NOVO ou SUBSTITUI**
- [ ] Nome não depende de hífen para o download — **e** o nome vira o endereço na Vercel
- [ ] Marca de versão nova (`window.MOVIKI_VERSAO`)
- [ ] LF, sem CR
- [ ] Se é função nova: **em qual projeto Vercel ela cabe?** (`moviki` 1/12 · `moviki-robo` 12/12 · `moviki-ai` 2/12)
- [ ] Domínio novo no jogo? **Linha na CSP** dos arquivos que vão chamá-lo (`connect-src`, `img-src`, `script-src`)
- [ ] Env nova? Criar **e depois** disparar deploy novo
- [ ] Regra nova? O arquivo que grava o campo **sobe primeiro**

## Depois do upload
- [ ] Abrir a página, F12 > Console > `MOVIKI_VERSAO` > Enter
- [ ] Valor antigo ou `undefined` = cache → Ctrl+Shift+R
- [ ] Envolveu `/api`? **Conferir ao vivo** (`GET` no endpoint do Vik responde 405 = deploy no ar)
- [ ] Página de destino de UTM: o GA dela está medindo?

## Ordem de sobe quando há regra envolvida
1. Arquivo que **grava** o campo novo
2. Conferir ao vivo
3. Só então publicar a regra que **conhece** o campo
4. Comparar com o Console antes de publicar — **o Console é a verdade**
