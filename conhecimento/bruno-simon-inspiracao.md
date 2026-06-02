---
tags: [conhecimento, inspiracao, bruno-simon, webgl, three-js, fisica, gap-analysis]
fonte: "https://bruno-simon.com (adubo dia 5)"
relacionado: "[[conhecimento/design-imersivo-3d]], [[conhecimento/anime-js]], [[README]]"
---
# bruno-simon.com — inspiração & análise de gap

> Adubo do jardineiro (dia 5): *"tente aprender com ele e entender como ele tornou
> o site uma plataforma de jogo incrível; avalie se é possível fazer algo assim e
> o que você precisa de recurso/ferramenta que ele tem e você ainda não."*

## O que faz o site ser "jogo"

Portfólio onde o visitante **dirige um carro 3D** por um mundo navegável. Não é
vídeo nem scroll: é simulação em tempo real com física, câmera e controles.

## Stack dele

| Camada | Ferramenta |
|---|---|
| Render 3D | **Three.js** (com TSL — Three.js Shading Language → WebGL **e** WebGPU) |
| Física | **Rapier** (mecânica do carro, colisões, objetos interativos) |
| Áudio | **Howler.js** (música CC0 + sfx toggláveis) |
| Controles | teclado/mouse (WASD, espaço, shift), toque (1 dedo dirige, 2 dedos câmera), **gamepad** |
| Assets | modelos Blender (open source, MIT no GitHub) |
| Fontes | Amatic SC + Nunito |

## O que JÁ temos

- **Three.js via CDN ESM + import map** já provado em `src/preview.html`
  (cena 3D do broto com bloom). Zero-build mantido. Ver [[conhecimento/design-imersivo-3d]].
- Web Audio API (música ambiente) — análogo leve ao Howler.
- Loop de animação (canvas 2D) e cultura de "degrada sozinho se CDN cair".

## O gap — o que falta (recurso/ferramenta)

1. **Motor de física** — não temos Rapier/Cannon. Sem ele não há carro, colisão,
   gravidade. Rapier roda via WASM + CDN ESM → **viável sem build**, mas é peso novo.
2. **Pipeline de assets 3D** — Bruno modela no Blender e exporta glTF. Hoje nosso
   "asset" é pixel art procedural. Precisaríamos de modelos glTF + loader.
3. **Sistema de controles** — abstração de input (teclado/toque/gamepad) e câmera
   de perseguição. Hoje só temos teclas para a minhoca (Snake).
4. **Orçamento de performance** — mundo 3D navegável pede LOD, instancing, e cuidado
   mobile. Bem além de um canvas 48×48.
5. **Tempo/escopo** — é um projeto de meses dele. Nosso ritmo é ≤50 ações/dia.

## Avaliação de viabilidade (honesta)

**É possível "algo assim"? Sim, em versão semente.** Não um simulador de carro, mas
um **jardim 3D explorável**: a câmera orbita/caminha pela planta que crescemos,
com física leve (ex.: pétalas/folhas caindo com Rapier, vento empurrando partículas).

**Caminho incremental proposto (sem quebrar o zero-build):**
1. Evoluir `preview.html`: `OrbitControls` (já em Three addons) → explorar a planta. ✔ barato
2. Partículas com física leve (pétalas caindo) — primeiro via shader/anime.js; Rapier só se necessário.
3. Howler-equivalente: manter Web Audio; trilha ambiente espacializada.
4. Mais tarde: input unificado (gamepad/toque) + uma "semente jogável".

**Decisão:** registrar como **direção de longo prazo** (Fase 2+). O `preview.html`
é a ponte. Não importamos Rapier ainda — entra quando houver uma interação física
concreta que justifique o peso. Inspiração absorvida; execução faseada.
