---
tags: [conhecimento, frontend, design, anthropic, plugin]
relacionado: "[[README]], [[specs/00-visao-geral]], [[growth/2026-05-30]]"
---
# Conhecimento: Frontend Design (Plugin Oficial Anthropic)

> Fonte: https://github.com/anthropics/claude-plugins-official/tree/main/plugins/frontend-design
> Cookbook: https://github.com/anthropics/claude-cookbooks/blob/main/coding/prompting_for_frontend_aesthetics.ipynb
> Processado em: 2026-05-30

## Princípios aprendidos

### O problema padrão
Claude tende a convergir para designs genéricos ("aesthetic de IA"). Solução: especificidade explícita + criatividade interpretativa.

### Tipografia
Evitar: Arial, Inter, Roboto, Space Grotesk.
Usar: JetBrains Mono, Syne, Clash Display, Playfair Display.
Técnica: pesos extremos (300 vs 700), letter-spacing alto em labels.

### Cor e Tema
- Comprometer-se com paleta coesa via CSS variables
- Cores dominantes com acentos agudos > paletas tímidas
- Inspirar em: estéticas de IDE, temas culturais, biopunk, solarpunk

### Movimento
- Priorizar CSS animations sobre JavaScript quando possível
- "Staggered reveals": animações de entrada escalonadas por delay
- Um carregamento orquestrado > microinterações dispersas

### Fundos
- Gradientes em camadas (não roxo-branco clichê)
- Padrões geométricos via CSS (dot grid, crosshatch)
- Criar atmosfera e profundidade

### Anti-padrões a evitar
- Gradientes roxo-branco genéricos
- Layouts previsíveis e sem personalidade
- Fontes "safe" sem caráter

## Aplicação no Projeto Semente

**Tema implementado:** "Biopunk Terminal"
- Fundo: `#060908` com grade de pontos opacity 0.35
- Fonte: JetBrains Mono (do Google Fonts)
- Paleta: verde-musgo + âmbar (espelha as cores da semente)
- Layout: 3 colunas (info | canvas | evolução)
- Entrada: staggered reveal (delay escalonado 0.05s–0.35s)
- Detalhe: cantos decorativos no canvas com CSS borders

## Decisão arquitetural gerada

O hotsite transforma `src/index.html` de uma página simples em uma landing page que comunica o projeto visualmente. Isso cria valor para visitantes que chegam pelo GitHub Pages sem contexto — eles veem o projeto, entendem o conceito, e observam a animação em contexto.

**Próxima evolução visual sugerida:** quando a planta emergir do solo, adicionar animação de parallax sutil no fundo (céu aparece gradualmente acima do solo).
