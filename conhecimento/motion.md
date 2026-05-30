---
tags: [conhecimento, motion, animacao, frontend, javascript]
relacionado: "[[conhecimento/frontend-design]], [[specs/02-plano-diario]]"
---
# Conhecimento: Motion (Framer Motion)

> Fonte: https://github.com/motiondivision/motion | https://motion.dev/docs
> Processado em: 2026-05-30

## O que é

Motion é a biblioteca de animação JavaScript moderna (sucessora do Framer Motion).
Usa um motor híbrido: JavaScript + WAAPI (Web Animations API) nativa = 120fps com GPU.

## Como usar no projeto (sem bundler)

```html
<script type="module">
  import { animate, stagger } from 'https://cdn.jsdelivr.net/npm/motion@latest/+esm';
</script>
```

Requer `type="module"` no script tag. Funções globais devem ser expostas via `window.fn = fn`.

## API principal

```javascript
// Animar elemento
animate(element, { opacity: [0, 1], y: [10, 0] }, { duration: 0.4, ease: [0.4, 0, 0.2, 1] });

// Stagger (escalonamento automático)
animate('.item', { opacity: [0, 1] }, { delay: stagger(0.08, { start: 0.2 }) });

// Contador numérico
animate(0, 100, { duration: 1.5, onUpdate: v => el.textContent = Math.round(v) });

// Spring
animate(el, { scale: [0.95, 1] }, { type: 'spring', bounce: 0.25 });
```

## Implementação no projeto

**Usado em:** `src/index.html` como `type="module"` script
**CDN:** `https://cdn.jsdelivr.net/npm/motion@latest/+esm`
**npm:** `motion` (declarado em `package.json`, instalado localmente)

**Animações ativas:**
- Header: fade + translateY
- Canvas: fade + scale(0.97→1)
- Sidebar esquerda: stagger x(-10→0)
- Sidebar direita: stagger x(10→0)
- Growth list: stagger x(-4→0) cascade
- Footer: fade delayed
- Day counter: animate(0→N) com onUpdate

## Próximas aplicações

- Hover effects no canvas-wrap (glow intensifica)
- Transição quando novos elementos do canvas aparecem
- Entrada suave do contador de dias a cada nova sessão
