---
tags: [spec, sdd, skills, fase-1]
relacionado: "[[specs/00-visao-geral]], [[CLAUDE]], [[growth/2026-05-30]]"
status: rascunho
versão: 0.1
---
# Spec 01 — Skills (Fase 1)

> Veja também: [[specs/00-visao-geral]] | [[CLAUDE]]

## Objetivo

Definir as Skills que transformam os fluxos manuais repetitivos do Projeto Semente em comandos reutilizáveis.

---

## Skill: `/processar-adubo`

**Gatilho:** jardineiro deposita arquivo em `adubo/`

**Passos:**
1. Ler todos os arquivos em `adubo/` com conteúdo não vazio
2. Para cada arquivo: extrair URLs, instruções, referências
3. Criar arquivo em `conhecimento/` com aprendizados e impactos
4. Adicionar wikilinks para correlação no Obsidian
5. Limpar conteúdo do arquivo em `adubo/`
6. Atualizar `README.md` se houver decisões arquiteturais novas
7. Registrar no relatório de crescimento do dia

**Output esperado:** 1 commit com mensagem `feat: absorve adubo-XX`

---

## Skill: `/crescer`

**Gatilho:** início da janela 22:00–02:00 ou após processar adubo

**Passos:**
1. Ler estado atual da animação (`src/index.html`)
2. Verificar dias decorridos e adubos processados
3. Decidir próximo elemento visual (raiz, broto, folha, caule, etc.)
4. Implementar o elemento mantendo o estilo pixel art 48×48
5. Registrar decisão no relatório e no README

**Output esperado:** 1 commit com mensagem `feat: animação — [elemento adicionado]`

---

## Skill: `/relatorio-diario`

**Gatilho:** fim da janela de ação ou quando atingir limite de 5 ações

**Passos:**
1. Verificar data atual
2. Criar ou atualizar `growth/AAAA-MM-DD.md`
3. Registrar: ações do dia, decisões, estado do mundo, próximo passo

**Output esperado:** 1 commit com mensagem `docs: relatorio AAAA-MM-DD`

---

## Skill: `/publicar`

**Gatilho:** após qualquer commit local sem push

**Passos:**
1. `git push` (usando token configurado)
2. Verificar que GitHub Actions completou com sucesso

**Output esperado:** site atualizado em `jefersonrgomes.github.io/SeedProject`

---

## Implementação no CLAUDE.md

As skills serão adicionadas como seção `## Skills` no `CLAUDE.md` com prompts comprimidos. Essa abordagem evita dependências externas — as skills vivem no próprio repositório.

**Status:** pendente — será implementado ao concluir a especificação completa.
