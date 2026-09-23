---
type: arquivo
status: concluido
area: parceiros
tags: [criadores, parceiro-html, redes-sociais, robo-social, entrega]
atualizado: 2026-09-23
---

# Área do criador no painel do parceiro

Entregue em 22/09/2026. Fecha o lado do influenciador do fluxo de duas chaves.

## O que é
Menu **Área do criador** no `parceiro.html` (marca `2026-09-22-criador`). Só aparece para parceiro **aprovado** com `parceiros/{uid}.criador == true` (marcado pelo dono no menu Criadores).

## Abas
- **Enviar peça** — feed, story ou reel. O navegador confere antes de subir o mesmo que o robô confere depois:
  - proporção: feed 4:5 a 1,91:1; story e reel 9:16
  - resolução mínima 540 px (aviso abaixo de 1080)
  - vídeo: reel 3 a 90 s, **story 3 a 60 s**
  - até 100 MB; JPG, PNG ou MP4
  - termos proibidos na legenda (mesma trava do robô)
  - capa do vídeo gerada no navegador
  - se a gravação falhar, o arquivo que subiu é apagado
- **Minhas peças** — status do dono (aguardando, aprovada, recusada com motivo, suspensa), **Autorizar / Revogar** (termo 3.1, validade 12 meses) e **Apagar** (peça e arquivo).
- **Meus resultados** — link `/c/apelido` com botões por canal (`?canal=`), visitas por dia e por canal, cadastros, pagantes, comissões e posts nas redes do Moviki.
- **Regras** — o que entra, o que não entra, crédito "Conteúdo de @arroba".

## Decisões
- As visitas vêm do `POST www.moviki.com.br/api/criadores` com `acao: meu_trafego`. **O slug sai do registro do parceiro no servidor, nunca do pedido** — um criador não consegue ver o tráfego de outro.
- O GA4 tem cache de 10 minutos no servidor e uma consulta só (400 dias) serve o dono e todos os criadores.
- Vídeo em story limitado a 60 s (limite da Meta para story); reel continua 3 a 90 s. Mesma regra no robô, no painel do dono e no painel do criador.
- Conteúdo aprovado não se edita: para trocar, apaga e envia outra.

## Arquivos
- `moviki-app/parceiro.html` `2026-09-22-criador`
- `moviki-app/eikoadm01.html` `2026-09-22-criadores2` (triagem de story em vídeo até 60 s)
- `moviki/api/criadores.js` `2026-09-22-criadores2`
- `moviki-assistente-social/src/config.py` `2026-09-22-criador`, `src/criadores.py`, `tests/test_criadores.py`, `conteudo/CRIADORES-CONTRATO.md`

## Ligado em 22/09/2026
- Regras v27 (Firestore) e `criadores/{uid}` (Storage) publicadas.
- Secret `CRIADORES_URL` criado no robô social.
- GA4: conta de serviço do site como Leitor + Google Analytics Data API ativada.
- Primeiro criador (@lucianopessoa) marcado e testado de ponta a ponta — story no ar às 23h26. Ver [[ARQ - Primeiro story de criador no ar 22092026]].

## Depois de 22/09
- Porta própria `app.moviki.com.br/criador` e card na Visão geral — [[ARQ - Porta dos criadores - decisao 22092026]].
- Vik em modo criador — [[ARQ - Vik em modo criador 22092026]].
- A marca do `parceiro.html` andou para `2026-09-23-rodada2` (outro chat); a Área do criador foi conferida intacta.

## Pendências
- Rodar os 13 casos de `firebase/testes/regras.test.js` no emulador (Claude Code).
- Conferir se o texto de autorização da tela e o termo v3.1 dizem a mesma coisa, e se o termo condiciona o bônus ao convite direto.

## Ligações
- [[R - Marcas de versao - area do criador 22092026]]
- [[R - Marcas de versao no ar]]
