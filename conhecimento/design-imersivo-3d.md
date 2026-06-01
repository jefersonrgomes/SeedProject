---
tags: [conhecimento, design, 3d, animacao, referencias]
relacionado: "[[frontend-design]], [[ui-ux-pro-max]], [[motion]]"
origem: adubo 2026-06-01
---
# Design Imersivo 3D — Referências do Jardineiro

Adubo de 2026-06-01 trouxe quatro referências de design web de alto nível.

**Duas abordagens convivem** (decisão revisada no adubo de 2026-06-01, 2ª leva):

1. **Site principal (`src/index.html`) — princípios, sem libs.** Vanilla JS, pixel
   art 2D. Extraímos os *princípios* das referências e aplicamos com CSS + Motion
   (tilt, spotlight, sheen, reveal coreografado, parallax, grão fílmico).
2. **Proposta 3D (`src/preview.html`) — libs de verdade, via CDN ESM.** O jardineiro
   pediu para *importar as libs* e ver uma segunda proposta. Resolvido **sem quebrar
   o zero-build**: Three.js + addons carregados por **import map + CDN ESM**. Acesso
   por um botão `🧊 preview 3D` no hero do site 2D.

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

## Importando as libs sem bundler (a 2ª proposta)

A objeção antiga ("threlte/theatre/spline pedem build") foi **resolvida**, não
abandonada. O caminho zero-build para 3D real:

```html
<script type="importmap">
{ "imports": {
  "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js",
  "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/"
}}
</script>
<script type="module">
  import * as THREE from 'three';
  import { EffectComposer } from 'three/addons/postprocessing/EffectComposer.js';
  import { UnrealBloomPass } from 'three/addons/postprocessing/UnrealBloomPass.js';
</script>
```

| Lib | Via CDN ESM sem build? | Decisão |
|---|---|---|
| **three.js** | ✅ `three.module.js` + `examples/jsm` por import map | **Usado** na proposta 3D |
| **theatre.js** | ✅ `@theatre/core` tem build ESM | Princípio (sequência) já no 2D; lib opcional |
| **spline** | ⚠️ web component `@splinetool/viewer`, mas precisa de cena `.splinecode` autorada no app deles | Não usado — dependência de asset externo |
| **threlte** | ❌ é Svelte (precisa compilar `.svelte`) | Substituído por **three.js puro** (que é o que threlte embrulha) |

**Threlte é Three.js declarativo para Svelte.** Sem Svelte/bundler, vamos direto
ao Three.js imperativo — mesma capacidade, zero build.

## Proposta 3D — `src/preview.html` (melhorar 5x materializado)

Cena WebGL em tempo real que espelha os stages do pixel art (semente → caule →
folhas → botão floral), com 5 camadas de design ("melhorar 5x"):

1. **Cena 3D** — solo com relevo, semente (icosaedro), caule (TubeGeometry numa
   curva S), folhas (Shape bézier dupla face), botão floral (sépalas + pétalas).
   Luzes: ambiente + key direcional + point quente + point verde (glow) + rim azul.
2. **Unreal Bloom** — `EffectComposer` + `UnrealBloomPass` + `OutputPass`. Os
   materiais emissivos (semente dourada, ponta da flor) "sangram" luz → cinema.
3. **Pólen** — `THREE.Points` com `AdditiveBlending`, partículas subindo e
   reembaralhando no topo.
4. **Câmera viva** — parallax amortecido no cursor (`lerp` 0.04) + órbita lenta
   do grupo + respiração (sin) + folhas balançando ao "vento".
5. **Atmosfera** — `FogExp2`, vinheta e grão fílmico (mesma linguagem do 2D),
   `ACESFilmicToneMapping`.

Guard-rails da proposta 3D:
- `try/catch` + overlay de erro com link de volta (WebGL pode faltar / CDN cair).
- `prefers-reduced-motion`: desliga órbita, respiração e animação do grão.
- `setPixelRatio(min(dpr,2))` para não fritar GPUs móveis.
- Mesma paleta/tipografia do site 2D → continuidade de marca.

## Guard-rails (lições do projeto)
- **Nunca** depender de `opacity:0` em CSS que só some via JS/CDN — se Motion falhar,
  o conteúdo fica invisível (bug já vivido). Reveal é enhancement, não dependência.
- Respeitar `prefers-reduced-motion`: desliga tilt e animações grandes.
- Não tocar em `drawSprout`/`CANVAS_STAGE`/áudio/chat/clima — isto é só design (`melhorar`).
- **3D é página separada** (`preview.html`): não arrisca a estabilidade do site 2D
  nem seu zero-dependency. O hero 2D segue funcionando se o CDN do Three.js cair.
