---
tags: [spec, sdd, skills, implementacao, fase-1]
relacionado: "[[specs/00-visao-geral]], [[specs/01-skills]], [[specs/02-plano-diario]], [[CLAUDE]]"
status: ativo
versão: 1.0
---
# Spec 03 — Skills: Implementação Detalhada

> Veja também: [[CLAUDE]] | [[specs/02-plano-diario]] | [[specs/01-skills]]

## Princípio

Skills transformam ações repetitivas em sequências comprimidas e auditáveis.
Cada skill deve ser:
- **Idempotente**: executar duas vezes não causa dano
- **Auditável**: sempre deixa rastro no growth report
- **Composável**: pode ser chamada de dentro de outra skill

---

## Skill: `/processar-adubo`

**Quando usar:** sempre que `adubo/adubo.md` tiver conteúdo não vazio.

**Passos:**
1. Ler `adubo/adubo.md` completo
2. Extrair: URLs de documentação, instruções, decisões
3. Para cada URL de doc → `WebFetch` → criar `conhecimento/[tema].md`
4. Para cada instrução → planejar ação e registrar na fase correta do plano
5. Atualizar `README.md` se houver nova decisão arquitetural
6. Atualizar `CLAUDE.md` se houver nova regra operacional
7. Escrever `adubo/adubo.md` vazio
8. Registrar no growth report: "adubo processado: [resumo]"

**Ações típicas:** 4–8

**Não fazer:**
- Não executar mais de 40 ações em resposta a um único adubo
- Não apagar o adubo antes de processar tudo

---

## Skill: `/crescer-canvas`

**Quando usar:** fase CRESCER do plano diário.

**Passos:**
1. Ler estado atual do canvas em `src/index.html` (funções `draw*`)
2. Consultar roadmap em `specs/02-plano-diario.md`
3. Verificar dia atual: `Math.floor((Date.now() - new Date('2026-05-29')) / 86400000)`
4. Decidir elemento: qual é o próximo no roadmap E coerente com o dia?
5. Implementar a função `draw[Elemento]()` e chamar em `render()`
6. Verificar: o elemento não quebra os existentes?
7. Documentar: cor, posição (x,y,SCALE), motivo, referência visual

**Ações típicas:** 8–12

**Paleta de cores do canvas (`P`):**
```javascript
// Solo
topSoil:'#2a1a0a', soil1:'#3b2312', soil2:'#4e2f17', soil3:'#2a1a0e'
// Planta
hypo:'#a0b840',   // hipocótilo (amarelo-verde, sem luz)
sprout:'#68a030', // broto (verde jovem)
leaf:'#4a9020',   // folha madura
stem:'#3a7018',   // caule
// Ambiente
sky:'#0c140c',    rain:'#5a8ab0', heart:'#e06080'
star:'#c8d0e8',   moon:'#d0d8b0', sun:'#f0d848'
```

---

## Skill: `/revisar-codigo`

**Quando usar:** fase REVISAR do plano diário.

**Checklist:**
- [ ] Há `px(x, y, ...)` repetido com os mesmos argumentos? → Extrair constante
- [ ] Há `document.getElementById('...')` chamado mais de uma vez? → Cachear
- [ ] Há strings de cor fora do objeto `P`? → Mover para `P`
- [ ] Há funções de mais de 30 linhas? → Candidata a split
- [ ] Há comentários desatualizados? → Remover ou atualizar
- [ ] Há `console.log` esquecidos? → Remover

**Regra:** não mudar comportamento, só estrutura. Se mudar comportamento → é EVOLUIR, não revisar.

**Ações típicas:** 3–6

---

## Skill: `/publicar`

**Quando usar:** fase PUBLICAR. Também pode ser chamada ao fim de qualquer bloco de mudanças.

**Passos:**
```bash
git add --all
git status  # verificar o que será commitado
git commit -m "[tipo]([escopo]): [descrição concisa]

[corpo opcional: explicação, breaking changes]

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
git remote set-url origin "https://[TOKEN]@github.com/jefersonrgomes/SeedProject.git"
git push
git remote set-url origin "https://github.com/jefersonrgomes/SeedProject.git"
```

**Tipos de commit:** `feat` | `fix` | `docs` | `refactor` | `style` | `chore`

**Ações:** 2

---

## Skill: `/atualizar-site`

**Quando usar:** após adicionar novo elemento ao canvas ou nova feature. Sincroniza o sidebar.

**O que verificar em `src/index.html`:**
1. `.growth-list` → adicionar novo item `done` / mover `active` para `done`
2. `.next-list` → remover item concluído, adicionar próximo do roadmap
3. `#canvasLabel` → atualizar descrição dos elementos presentes
4. `#statCommits` → atualizar contagem (ou tornar dinâmico)
5. `.stage-fill` width → atualizar progresso da fase
6. Sidebar "localização" → ainda funciona?

**Ações:** 3–5

---

## Skill: `/growth-report`

**Quando usar:** fase DOCUMENTAR.

**Template:**
```markdown
---
tags: [growth, dia-N, relatorio]
relacionado: "[[growth/AAAA-MM-DD-anterior]], [[README]], [[specs/02-plano-diario]]"
---
# Relatório de Crescimento — Dia N — AAAA-MM-DD

> Anterior: [[growth/...]] | Próximo: growth/...

## Ações do dia: X de 50

## Fase 1 — ATIVAR
[o que estava no adubo, qual era o contexto]

## Fase 2 — CRESCER
[elemento adicionado, decisão visual, coordenadas]

## Fase 3 — EVOLUIR
[feature ou melhoria, motivação]

## Fase 4 — REVISAR
[o que foi identificado, o que foi refatorado, skills atualizadas]

## Fase 5+6 — DOCUMENTAR + PUBLICAR
[growth report criado, commit hash]

## Estado do mundo
[árvore de arquivos relevantes]

## Próximo passo
[próximo elemento canvas + próxima feature + próxima revisão]
```

**Ações:** 2–3

---

## Roadmap de skills a criar

| Skill | Status | Prioridade |
|---|---|---|
| `/processar-adubo`     | ✅ implementada | — |
| `/crescer-canvas`      | ✅ implementada | — |
| `/revisar-codigo`      | ✅ implementada | — |
| `/publicar`            | ✅ implementada | — |
| `/atualizar-site`      | ✅ implementada | — |
| `/growth-report`       | ✅ implementada | — |
| `/deploy-check`        | 📋 planejada   | Fase 2 |
| `/criar-agente`        | 📋 planejada   | Fase 3 |
| `/orquestrar`          | 📋 planejada   | Fase 3 |
