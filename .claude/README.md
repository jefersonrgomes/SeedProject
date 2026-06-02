# `.claude/` — estrutura oficial de extensões do agente

> Adubo dia 5: *"implemente na sua estrutura do claude o padrão de arquivos
> recomendado na documentação oficial para criar skills, agentes, multi-agentes."*

Este diretório segue o padrão oficial do Claude Code para **skills** e **subagentes**.
É a evolução das "skills" que viviam como prosa no `CLAUDE.md` — agora arquivos
reais que o harness descobre e carrega.

## Estrutura

```
.claude/
├── skills/
│   └── <nome-skill>/
│       └── SKILL.md        # frontmatter: name + description (+ instruções no corpo)
├── agents/
│   └── <nome-agente>.md    # frontmatter: name, description, tools, model (+ system prompt)
├── settings.local.json     # permissões locais (não versionar segredos)
└── README.md               # este arquivo
```

## Skills (`.claude/skills/<nome>/SKILL.md`)

Procedimento comprimido e reutilizável. O `name` (kebab-case) casa com o nome da
pasta; a `description` diz **quando** acionar (o harness usa isso para sugerir/rodar).

- **`crescer-canvas`** — avança o `CANVAS_STAGE` da semente (próximo estágio botânico)
  com todo o wiring (drawSprout, renderScene, FRAMES, replay, UI). 1ª skill formal.

> As skills em prosa do `CLAUDE.md` (`/processar-adubo`, `/publicar`, `/growth-report`
> etc.) seguem válidas; serão migradas para este padrão conforme forem refinadas.

## Agentes (`.claude/agents/<nome>.md`)

Subagente com contexto isolado, conjunto de `tools` próprio e `model` definido.
Invocável pelo agente principal para delegar uma tarefa focada.

- **`jardineiro-visual`** — especialista no comando `melhorar` (design visual de
  `src/index.html`), com escopo duro: nunca toca em canvas-logic. 1º agente formal.

## Multi-agentes (orquestração)

O padrão multi-agente = o **agente principal orquestra subagentes**, cada um com
contexto e ferramentas próprios, e integra os resultados. No Projeto Semente o fluxo
diário mapeia naturalmente para isso:

```
agente-principal (orquestrador do dia / 6 fases)
   ├─ skill  crescer-canvas      → ② CRESCER (avança o stage)
   ├─ agente jardineiro-visual   → ③ EVOLUIR (passadas "melhorar")
   └─ skills /processar-adubo, /growth-report, /publicar → ①④⑤⑥
```

Próximos candidatos a formalizar: agente `jardineiro-botanico` (desenho de novos
estágios pixel-art) e skill `processar-adubo` (já em prosa no CLAUDE.md).
