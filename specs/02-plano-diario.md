---
tags: [spec, sdd, plano-diario, rotina, fase-0]
relacionado: "[[specs/00-visao-geral]], [[CLAUDE]], [[specs/01-skills]], [[specs/03-skills-implementacao]]"
status: ativo
versão: 2.0
---
# Spec 02 — Plano Diário de Evolução (6 Fases · 50 Ações/Dia)

> Veja também: [[CLAUDE]] | [[specs/00-visao-geral]] | [[specs/03-skills-implementacao]]

## Regra fundamental

- Executa **uma vez por dia**, entre 22:00 e 02:00
- **Limite: 50 ações por dia** (v2.0 — atualizado pelo jardineiro)
- Adubo é o trigger, mas não é obrigatório — o plano roda mesmo sem adubo
- O plano inclui um passo de **REVISÃO** para transformar repetição em skills e agentes

---

## Distribuição de ações (50/dia)

| Fase         | Ações  | Objetivo                              |
|---|---|---|
| ① ATIVAR     | ≤ 5    | Context, adubo, objetivo do dia       |
| ② CRESCER    | ≤ 15   | Evolução visual do canvas             |
| ③ EVOLUIR    | ≤ 15   | UI/UX/arquitetura/features            |
| ④ REVISAR    | ≤ 10   | Eliminar repetição, skills, agentes   |
| ⑤ DOCUMENTAR | ≤ 3    | Growth report, README                 |
| ⑥ PUBLICAR   | ≤ 2    | Commit + push + verificar Pages       |
| **Total**    | **50** |                                       |

---

## Fase 1 — ATIVAR (≤5 ações)

1. Ler `growth/AAAA-MM-DD.md` → quantas ações usadas? Qual foi o último passo?
2. Verificar `adubo/adubo.md` → há adubo? Se sim: `/processar-adubo`
3. Revisar o growth report de ontem → há algo pendente ou prometido?
4. Verificar GitHub Actions → o último deploy foi bem-sucedido?
5. Definir objetivo do dia em uma frase (registrar no growth report)

**Output:** clareza total sobre o contexto antes de agir.

---

## Fase 2 — CRESCER (≤15 ações)

Usar skill `/crescer-canvas`. Roadmap visual:

```
✅ Dia 0    → semente + raiz primária + minhoca + céu base
✅ Dia 1    → raiz lateral + rachadura + estrelas/lua/sol + hotsite + chat + clima
✅ Dia 1+   → hipocótilo etiolado + mood system + 6 skills + 50 ações/dia
   Dia 2    → broto verde + cotilédones + mood-driven theme + refactor unificado
   Dia 3    → cotilédones abertos + caule 3px + sol maior + vento animado
   Dia 4    → 2 folhas verdes + abelha passando + nuvem
   Dia 5    → planta com 4 folhas + pássaro + sombra
   Dia 6    → vaso + janela ao fundo + luz ambiente
   Dia 7    → floração (flor pixel) + borboleta + lua cheia
   Dia 10+  → ecossistema completo (cena exterior animada)
```

> ℹ️ Com 50 ações/dia, cada sessão avança 2-3 estágios. O critério de avanço
> é: elemento implementado + documentado + publicado no GitHub.

**Ações típicas desta fase:**
- 2-3 ações: planejar o elemento (roadmap, coerência visual)
- 6-8 ações: implementar no canvas JS
- 2-3 ações: testar (verificar animação, cores, proporções)
- 1-2 ações: documentar decisão

---

## Fase 3 — EVOLUIR (≤15 ações)

Melhorar um aspecto do hotsite, da arquitetura ou das features. Exemplos por nível de impacto:

**Alto impacto (priorize):**
- Nova feature significativa (nova aba, novo sistema)
- Mood-driven CSS variables (tema muda com o humor)
- Visitante counter via localStorage
- Compartilhamento de estado via URL hash

**Médio impacto:**
- Novas animações Motion (entrada de elementos, hover)
- Melhoria de acessibilidade (aria, focus visible)
- Responsividade mobile melhorada

**Baixo impacto (só se não houver outra coisa):**
- Ajustes de cor ou tipografia
- Reformulação de texto em sidebars

---

## Fase 4 — REVISAR (≤10 ações)

**Esta fase é nova e crítica.** Seu objetivo é evitar que o projeto acumule dívida técnica.

### O que revisar

**Código repetitivo:**
- Há funções canvas com lógica duplicada? → Extrair helper `px2` ou `sprite()`
- Há seleções de DOM repetidas? → Cachear em constantes
- Há strings repetidas (cores, textos)? → Mover para `P` (paleta) ou `CONFIG`

**Padrões que viraram rotina:**
- Toda vez que processo adubo, faço as mesmas 6 coisas → Verificar se a skill `/processar-adubo` cobre isso
- Toda vez que publico, faço 5 passos iguais → Verificar se `/publicar` está completa

**Specs desatualizadas:**
- O roadmap do canvas em `specs/02-plano-diario.md` reflete o estado atual?
- A Fase 0 de `specs/00-visao-geral.md` está marcada como ✅?

**Ações típicas:**
- 2-3 ações: ler código e identificar repetição
- 3-4 ações: refatorar ou atualizar skill
- 2-3 ações: verificar que nada quebrou + registrar

---

## Fase 5 — DOCUMENTAR (≤3 ações)

Usar skill `/growth-report`:

1. Criar `growth/AAAA-MM-DD.md` com:
   - Ações usadas (N/50)
   - O que foi feito em cada fase
   - Decisões arquiteturais + motivos
   - Estado do mundo (árvore de arquivos relevantes)
   - Próximo passo claro
2. Se nova decisão arquitetural → atualizar `README.md`
3. Se nova skill criada → atualizar `specs/03-skills-implementacao.md`

---

## Fase 6 — PUBLICAR (≤2 ações)

Usar skill `/publicar`:

1. `git add --all && git commit -m "[tipo](escopo): [descrição]"`
2. Push com token → limpar URL → verificar GitHub Actions

**Output:** `jefersonrgomes.github.io/SeedProject` atualizado.

---

## Critério de conclusão do dia

- ✅ Growth report escrito com ações contadas
- ✅ Pelo menos 1 elemento canvas evoluído OU 1 feature nova
- ✅ Fase REVISAR executada (mesmo que não haja nada para refatorar — registrar)
- ✅ Commit publicado + GitHub Pages online

---

## Quando usar agentes (Fase 3 do SDD)

Quando uma tarefa de EVOLUIR for grande demais para uma sessão:
- Split em sub-tarefas via `Agent tool`
- Agente Animador → cuida de `drawFunctions` no canvas
- Agente Documentador → cuida de `growth/` + `README.md`
- Agente Arquivista → cuida de `conhecimento/` + `specs/`

Usar quando a tarefa exceder ~15 ações de EVOLUIR.
