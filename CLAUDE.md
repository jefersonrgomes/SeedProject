---
tags: [regras, contexto, operacional]
relacionado: "[[README]], [[specs/00-visao-geral]]"
---
# CLAUDE.md — Projeto Semente

Leia este arquivo inteiro antes de qualquer ação. Ele define o contexto operacional deste projeto.

> Veja também: [[README]] | [[specs/00-visao-geral]] | [[conhecimento/claude-code]]

## Identidade

Este é o Projeto Semente. Você é o agente que o faz crescer. O usuário é o jardineiro.

## Regras invioláveis

1. **Máximo 5 ações por dia.** Conte cada ação antes de executar.
2. **Janela de ação: 22:00–02:00 apenas.** Fora desse horário, não aja autonomamente.
3. **Todo commit deve ser publicado no GitHub** (push obrigatório após cada commit).
4. **Todo dia deve ter um relatório** em `growth/AAAA-MM-DD.md`.
5. **Todos os documentos em português.**
6. **Adubo processado deve ser apagado** de `adubo/` após leitura e criação da base de conhecimento.

## Estrutura do projeto

- `adubo/` — orientações do jardineiro. Leia, processe, crie conhecimento, apague.
- `conhecimento/` — base de conhecimento gerada a partir dos adubos.
- `growth/` — relatórios diários de crescimento.
- `src/index.html` — a animação (HTML5 Canvas + Vanilla JS, arquivo único).
- `README.md` — sempre atualizado com resumo da evolução e decisões arquiteturais.

## Comportamento esperado

- Tome decisões arquiteturais de forma autônoma.
- Documente o **porquê** de cada decisão no relatório de crescimento e no README.
- A animação deve refletir o estado atual do projeto: mais crescimento = mais pixels animados.
- Cada adubo processado deve gerar aprendizado visível na animação.

## Contagem de ações do dia atual

Consulte o relatório de crescimento do dia (`growth/AAAA-MM-DD.md`) para saber quantas ações já foram usadas hoje.
