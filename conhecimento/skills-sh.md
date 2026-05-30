---
tags: [conhecimento, skills, frontend, animacao, tools]
relacionado: "[[conhecimento/frontend-design]], [[conhecimento/motion]], [[specs/02-plano-diario]]"
---
# Conhecimento: Skills.sh

> Fonte: https://www.skills.sh/
> Processado em: 2026-05-30

## O que é

Repositório de centenas de skills reutilizáveis instaláveis via `npx skillsadd <owner/repo>`.
Potencializa agentes como Claude Code com capacidades específicas por domínio.

## Skills relevantes para este projeto

### Frontend & Design
- **frontend-design** (Anthropic) — 480K instalações — já aplicado ✅
- **web-design-guidelines** (Vercel Labs) — 354K — padrões de design web profissional
- **vercel-react-best-practices** (Vercel Labs) — 438K — boas práticas de componentes

### Animação
- **remotion-best-practices** (Remotion Dev) — 339K — animações web de alta qualidade
- **gsap** (HeyGen Hyperframes) — alternativa ao Motion para animações complexas

### Agentes e IA
- **agent-browser** (Vercel Labs) — 326K — automação de browser para agentes

## Decisão de aplicação no projeto

**Skills a explorar nas próximas iterações:**
1. `web-design-guidelines` — aplicar ao redesenho do sidebar quando o broto emergir
2. `remotion-best-practices` — referência para animações mais sofisticadas no canvas
3. `gsap` — alternativa ao Motion para micro-animações que precisem de timeline

**Não instalar por ora:** skills de React/Next.js (o projeto é vanilla JS por decisão arquitetural).

## Como instalar (referência futura)

```bash
npx skillsadd vercel-labs/web-design-guidelines
npx skillsadd remotion-dev/remotion-best-practices
```

## Insight arquitetural

A comunidade de skills revela que o padrão da indústria para web apps de alta qualidade converge em:
1. Tipografia com caráter (JetBrains Mono ✅ já aplicado)
2. Animações com propósito (Motion ✅ já aplicado)
3. Sistema de cores via CSS variables (✅ já aplicado)
4. Dados em tempo real (Open-Meteo ✅ já aplicado)

O projeto já está alinhado com as práticas dos top skills da plataforma.
