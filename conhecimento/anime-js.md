---
tags: [conhecimento, anime-js, animacao, biblioteca, referencia]
fonte: "https://animejs.com/documentation/ (adubo dia 5)"
relacionado: "[[conhecimento/motion]], [[conhecimento/design-imersivo-3d]]"
---
# anime.js v4 — biblioteca de animação (referência)

> Adubo do jardineiro (dia 5, 02 jun 2026): *"baixe a lib, entenda ao máximo e use como referência."*

## O que é

Motor de animação JavaScript leve e sem dependências. A v4 foi reescrita em
módulos ESM tree-shakeable. Anima **CSS, transforms, atributos HTML/SVG, objetos
JS, cores e valores numéricos** com controles de playback sofisticados.

## API principal (v4)

| Função | Para quê |
|---|---|
| `animate(targets, params)` | cria/roda uma animação (substitui o `anime()` da v3) |
| `createTimeline()` | orquestra sequências multi-animação sincronizadas |
| `stagger(value, opts)` | distribui timing entre N elementos (sequência / grid) |
| `splitText()` | quebra texto em linhas/palavras/chars para animar |
| `scrambleText()` | revelação de texto com embaralhamento de caracteres |
| `morphTo()` | morphing entre paths SVG |
| `createDrawable()` | animação de traço SVG (efeito "desenhar") |
| `onScroll()` | liga animação à posição de scroll (thresholds) |

Hooks: `onBegin`, `onUpdate`, `onComplete`. Playback: `play/pause/reverse/seek`.
Usa a **Web Animations API** (aceleração por hardware) quando possível.

## Import — compatível com nossa arquitetura zero-build ✅

Ao contrário de threlte/theatre/spline, anime.js **roda direto via CDN ESM**, sem
bundler — exatamente como já fazemos com Motion:

```js
import { animate, stagger } from 'https://cdn.jsdelivr.net/npm/animejs/+esm';
```

Logo, adotar anime.js **não quebra** o "single-file, sem build" do `src/index.html`.

## Como aplicamos / decisão

O projeto já usa **Motion** (CDN ESM) para os reveals. anime.js e Motion se
sobrepõem no básico (tween + stagger), então **não trocamos** o que funciona —
evitamos redundância e regressão ([[feedback_testing]]).

**Onde anime.js é superior e vale adotar no futuro:**
- `createDrawable` (desenhar traço SVG) — ideal para "desenhar" o caule/nervuras.
- `morphTo` — transição de forma (ex.: botão → flor → fruto em SVG).
- `scrambleText` / `splitText` — revelação tipográfica do logo/títulos.

**Uso nesta passada (dia 5):** anime.js entra via o **mesmo padrão de import
dinâmico gracioso** do Motion (`import().then().catch()`) para um realce de
*stagger* nos chips de stats no load — se o CDN cair, os chips seguem visíveis
(sem `opacity:0` no CSS). É um "primeiro contato" de baixo risco; o ganho maior
(draw/morph SVG) fica mapeado como próximo passo quando houver camada SVG.

## Princípios que reforçam o design (mesmo sem importar)

- **Stagger** como gramática de entrada (cascata > tudo de uma vez).
- **Easing custom** = peso/profundidade (já usamos `cubic-bezier(0.4,0,0.2,1)`).
- **Timeline** para coreografia (theatre.js dizia o mesmo — ver [[conhecimento/design-imersivo-3d]]).
