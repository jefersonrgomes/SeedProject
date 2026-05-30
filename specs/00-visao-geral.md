---
tags: [spec, sdd, ia, plataforma, evolução]
relacionado: "[[README]], [[CLAUDE]], [[conhecimento/claude-code]], [[specs/01-skills]]"
status: em-andamento
versão: 0.1
---
# Spec 00 — Visão Geral: Plataforma de IA Evolutiva

> Veja também: [[CLAUDE]] | [[conhecimento/claude-code]] | [[specs/01-skills]]

## Objetivo

Construir uma plataforma de IA evolutiva seguindo as melhores práticas de **SDD (Spec Driven Development)**:
escrever a especificação primeiro, implementar segundo, validar terceiro.

A evolução segue 4 fases, do mais simples ao mais autônomo.

---

## Fases de Evolução

### Fase 0 — Estado Atual ✅
**Descrição:** Claude Code operado manualmente via conversas. Regras no CLAUDE.md. Adubo como canal de input.

**Componentes ativos:**
- `CLAUDE.md` — memória de sessão e regras operacionais
- `adubo/` — canal de input assíncrono do jardineiro
- `growth/` — rastreamento diário
- `src/index.html` — animação canvas

**Critério de conclusão:** projeto versionado, publicado, animação viva. ✅

---

### Fase 1 — Skills 🔄
**Descrição:** Transformar fluxos repetitivos em Skills reutilizáveis (comandos `/skill-name` acionáveis diretamente no Claude Code).

**Skills a criar:**
| Skill | Descrição |
|---|---|
| `/processar-adubo` | Lê `adubo/`, cria conhecimento, limpa, commita |
| `/crescer` | Decide próximo estágio visual da animação e implementa |
| `/relatorio-diario` | Gera o growth report do dia e commita |
| `/publicar` | Faz commit + push de todas as mudanças pendentes |

**Implementação:** cada skill é um bloco em `CLAUDE.md` sob `## Skills` com prompt comprimido.

**Critério de conclusão:** todos os fluxos diários executáveis com um único comando.

---

### Fase 2 — Agente Único 📋
**Descrição:** Claude Code operando autonomamente via Routines da Anthropic. Sem intervenção manual para ações noturnas.

**Componentes a criar:**
- Routine agendada: 22:30 todo dia → processa adubo + cresce + publica
- Hook de pré-commit: valida estrutura de arquivos obrigatórios
- Hook de pós-commit: atualiza README com data/dias decorridos

**Critério de conclusão:** projeto cresce sozinho toda noite sem o jardineiro precisar agir.

---

### Fase 3 — Multi-Agentes 📋
**Descrição:** Agentes especializados trabalhando em paralelo, coordenados por um orquestrador.

**Agentes planejados:**
| Agente | Responsabilidade |
|---|---|
| Orquestrador | Recebe adubo, decompõe em tarefas, distribui |
| Animador | Responsável exclusivo por `src/index.html` |
| Documentador | Mantém README, CLAUDE.md, growth reports |
| Arquivista | Processa adubo, atualiza `conhecimento/` |

**Critério de conclusão:** tarefa complexa (ex: novo ciclo visual completo) concluída em paralelo por agentes sem conflito.

---

## Princípios SDD aplicados

1. **Spec antes de código** — este arquivo existe antes da implementação
2. **Critérios de conclusão explícitos** — cada fase tem uma definição clara de "feito"
3. **Evolução incremental** — Fase N só começa quando Fase N-1 está completa
4. **Documentação como código** — specs versionadas no git, atualizadas a cada mudança

---

## Referências

- [[conhecimento/claude-code]] — capacidades do Claude Code relevantes para cada fase
- [[CLAUDE]] — regras operacionais atuais
- [[specs/01-skills]] — detalhamento das Skills da Fase 1
