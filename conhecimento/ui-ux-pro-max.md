---
tags: [conhecimento, ui-ux, design, skill, anthropic]
relacionado: "[[conhecimento/frontend-design]], [[specs/02-plano-diario]]"
---
# Conhecimento: UI UX Pro Max Skill

> Fonte: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
> Processado em: 2026-05-30

## O que é

Plugin/skill de design intelligence para Claude Code.
Analisa requisitos e gera recomendações de design completas antes de implementar código.

## Capacidades

- **67 estilos UI** — Glassmorphism, Neumorfismo, Minimalismo, Dark Tech, Biopunk, etc.
- **161 paletas de cores** alinhadas com tipos de produto
- **57 combinações tipográficas** do Google Fonts
- **161 regras de raciocínio** específicas por indústria

## Como instalar (para referência futura)

```bash
# Via CLI
npm install -g uipro-cli
cd /projeto
uipro init --ai claude

# Via Claude Code plugin
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
```

## Aplicação ao Projeto Semente

**Estilo escolhido:** Dark Minimalism + Biopunk (dos 67 disponíveis)
- Fundo ultra-escuro com textura sutil
- Tipografia monospace (terminal aesthetic)
- Acentos verdes orgânicos + âmbar (cores naturais)
- Sem bordas arredondadas (sharp, pixel-precise)

**Paleta aplicada (dos 161):** "Underground Growth"
- `#060908` — fundo (quase preto, toque verde)
- `#7ab84a` — accent (verde folha)
- `#c8a85a` — gold (âmbar da semente)
- `#7a8c7a` — texto (cinza-verde)

**Tipografia (das 57 combos):** JetBrains Mono 300/400/700
- Escolha: tipografia de IDE/terminal para coerência com o tema de desenvolvimento autônomo

## Princípio central aplicado

Antes de implementar: definir o sistema de design.
O `vars` no CSS do projeto já implementa este princípio — toda cor e espaçamento é uma variável.
Mudar o tema do projeto = mudar 10 linhas de CSS variables.

## Próxima evolução de design sugerida

Quando a planta emergir do solo: transição de tema de "underground dark" para "daylight growth" —
fundo muda de `#060908` para `#0d1408` (ainda escuro mas com mais verde),
e o sol pixel aparece no topo do canvas com brilho âmbar no header.
