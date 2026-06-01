---
tags: [conhecimento, design, 3d, animacao, referencias]
relacionado: "[[frontend-design]], [[ui-ux-pro-max]], [[motion]]"
origem: adubo 2026-06-01
---
# Design Imersivo 3D — Referências do Jardineiro

Adubo de 2026-06-01 trouxe quatro referências de design web de alto nível.
Como o Projeto Semente é vanilla JS sem bundler (GitHub Pages serve `src/` direto),
**não importamos as libs** — extraímos os princípios e aplicamos com CSS + Motion.

## As referências

### peachweb.io
Estúdio/portfólio com estética "awwwards": web cinematográfica, scroll suave,
tipografia ousada, transições com propósito, spotlight que acompanha o cursor.
- **Princípio aplicável**: brilho ambiente (radial-gradient) seguindo o cursor →
  sensação de luz/foco vivo. Custo zero: variáveis CSS `--mx/--my` atualizadas no `pointermove`.

### threlte.xyz
Three.js declarativo para Svelte. Ensina a pensar a cena como **camadas com
profundidade, luz e câmera** em vez de elementos planos.
- **Princípio aplicável**: hierarquia de profundidade — o elemento principal (canvas)
  reage à "câmera" (cursor) com leve perspectiva.

### theatre.js
Editor de animação com **timeline/sequência coreografada**. Motion orquestrado,
não aleatório — cada elemento entra no seu tempo.
- **Princípio aplicável**: revelação sequenciada das seções no scroll
  (stagger por IntersectionObserver), entradas com ordem deliberada.

### spline.design
Design 3D no browser. Profundidade, parallax, iluminação suave, materiais com brilho.
- **Princípio aplicável**: tilt 3D (rotateX/rotateY via `perspective`) no canvas
  seguindo o mouse + sheen (brilho especular) que se move com a inclinação.
  Dá "feel" 3D a um pixel art 2D sem nenhuma lib.

## Regra de tradução (vanilla, sem lib)

| Referência | O que ensina | Como aplicamos aqui |
|---|---|---|
| spline / threlte | profundidade, câmera | `perspective` no pai + `rotateX/Y` no `.canvas-wrap` no `pointermove` |
| peachweb | luz cinematográfica | spotlight `radial-gradient at var(--mx) var(--my)` no hero |
| spline | material com brilho | `.canvas-sheen` overlay com `mix-blend-mode: screen` |
| theatre.js | sequência | reveal coreografado das seções via IntersectionObserver + Motion |

## Guard-rails (lições do projeto)
- **Nunca** depender de `opacity:0` em CSS que só some via JS/CDN — se Motion falhar,
  o conteúdo fica invisível (bug já vivido). Reveal é enhancement, não dependência.
- Respeitar `prefers-reduced-motion`: desliga tilt e animações grandes.
- Não tocar em `drawSprout`/`CANVAS_STAGE`/áudio/chat/clima — isto é só design (`melhorar`).
