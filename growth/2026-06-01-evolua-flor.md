---
tags: [growth, dia-4, evolua, melhorar, canvas, stage-8, flor-aberta, design]
relacionado: "[[growth/2026-06-01]], [[growth/2026-06-01-melhorar3]], [[README]]"
---
# Relatório de Crescimento — Dia 4 (evolua + melhorar 5x) — 2026-06-01

> Sessões do dia: [[growth/2026-06-01]] · [[growth/2026-06-01-melhorar]] · [[growth/2026-06-01-adubo]] · [[growth/2026-06-01-melhorar2]] · [[growth/2026-06-01-melhorar3]]

## Origem

Adubo do jardineiro (sessão interativa) com dois comandos em sequência:

```
evolua
melhorar 5x
```

`evolua` → executar o "Próximo passo (Dia 5)" do último report → **flor aberta (stage 8)**.
`melhorar 5x` → 5 refinamentos visuais (sem tocar canvas-logic), celebrando a floração.

> **Nota de orçamento:** o dia 4 já acumulava ~45/50 ações nas sessões anteriores.
> Esta sessão foi executada em **lote único** (1 report, 1 commit) a pedido explícito
> do jardineiro presente, mantendo o custo mínimo. Ainda assim, o dia está no teto —
> o próximo ciclo deve iniciar um novo dia.

---

## ① EVOLUA — Floração aberta: CANVAS_STAGE 7 → 8 (CRESCER)

Ação `/crescer-canvas` (avança o stage). O botão floral (stage 7) **desabrocha**.

### Pixel art da flor aberta (`drawSprout` stage >= 8)
- **Corola em leque** de ~5px de largura (cx-2…cx+2), entre y=6 e y=10.
- **Pétalas rosa** (`P.petal #e07aa8`) com **pontas claras** (`P.petalHi #f4a8cc`)
  nas extremidades laterais e no topo — dá volume à flor.
- **Miolo dourado** (`P.pollen #f0c850` / `P.pollenHi #f8e088`) no centro (y=7–9):
  o coração da flor, contraste quente contra o rosa.
- **Respiração** própria: `0.78 + sin(t*0.02)*0.14` (mais "viva" que o botão).
- **Vento contínuo**: toda a corola usa o mesmo `wo8(8)` senoidal do caule, então
  a flor balança junto com a planta — sem descontinuidade.

### Continuidade com o stage 7 (anti-regressão)
- O bloco `stage >= 7` agora desenha **caule + sépalas sempre** (cálice da flor),
  mas o **botão fechado** (pétalas rosa cerradas y=8–11) só aparece em `stage === 7`.
  Assim, ao chegar no stage 8, o botão "abre": some o botão fechado, surge a corola.
  Mesmo padrão de "transformação por stage" já usado nos cotilédones (murcham no 5).

### Wiring completo
- `CANVAS_STAGE = 8` + comentário do mapa de stages atualizado.
- `renderScene` (snapshots/thumbnails): botão fechado gated em `tstage===7`;
  novo bloco `tstage>=8` com a corola aberta (verificado por mapa ASCII — lê como flor).
- `FRAMES`: stage 7 vira `dia 3`; novo frame `hoje · 01 jun · flor aberta`.
- `replayEvolution`: `stages = [0..8]`.
- Paleta `P`: +`petal / petalHi / pollen / pollenHi`.
- Site: stat `🌸 flor: aberta`, `🌱 próximo: fruto`, progress `88% → 94%`,
  `canvasLabel` (+"flor aberta"), lista de crescimento (botão floral → ✓,
  novo ativo "Flor aberta · stage 8"), lista "próximo" reordenada (fruto no topo),
  título da Evolução "da semente à flor".

### Verificação
- `new Function(script)` no script inline → **SYNTAX OK** (50k chars).
- Mapa ASCII do stage 8 renderizado: corola arredondada coerente sobre o caule.
- Coords y=6–13 dentro de 0–47; stages 0–7 **inalterados** (só gating + adição).

---

## ② MELHORAR 5x — refinamento visual celebrando a flor

Escopo `melhorar`: **nada** em `drawSprout`/`CANVAS_STAGE`/áudio/chat/clima.
Tudo CSS + markup mínimo (6 `<i>` + 1 classe), todos `prefers-reduced-motion`-safe.

1. **Pétalas ambiente** — 6 pétalas rosa caem suaves no hero (CSS keyframes,
   `pointer-events:none`), ecoando a cor da flor. Variante roxa no tema cosmic.
2. **Linha do section-title** — o gradiente `::after` ganha um brilho que percorre
   devagar (antes estático).
3. **tabSlider** — o indicador da aba ativa "respira" (glow pulsante).
4. **Cards do Mundo** — colchete de canto surge no hover (eco visual dos brackets
   do `canvas-wrap` → linguagem consistente).
5. **Stat da flor** — realce rosa pulsante no chip `🌸 flor` (marco de hoje).

### Anti-regressão
- Sem novas dependências; cores rosa hardcoded só nas pétalas/realce (coerentes
  com a paleta `P.petal`). Reduced-motion desliga as 4 animações novas e oculta
  o campo de pétalas.

---

## Decisões

**Por que o botão "vira" flor em vez de empilhar?**
Empilhar botão fechado + corola aberta no mesmo ápice criaria sobreposição visual
suja. Gatear o botão fechado em `stage===7` faz o stage 8 ler como *abertura* —
narrativa correta da floração, e mantém os stages anteriores intactos.

**Por que melhorar 5x todas ligadas à flor?**
A floração é o marco do dia. Em vez de 5 melhorias dispersas, as 5 reforçam o mesmo
momento (pétalas caindo, realce do chip), dando coesão temática à passada.

---

## Estado do mundo ao final do Dia 4 (evolua + melhorar 5x)
```
Canvas:  stage 8 · flor rosa aberta com miolo dourado balançando no ápice
Hero:    tilt 3D + spotlight + sheen + pétalas ambiente caindo
Seções:  reveal coreografado + linha de título com brilho
Mundo:   cards com colchete de canto no hover
A11y:    prefers-reduced-motion respeitado (tudo desliga)
Adubo:   limpo ✓
```

## Próximo passo (Dia 5)
- **Fruto** — pixel art arredondado a partir da flor (stage 9), `/crescer-canvas`.
- Polinização — abelha desvia trajetória para visitar a flor.
- Maturação — transição de cor do fruto.
- Testar `index.html` no browser (calibrar a corola + as 5 micro-melhorias).
- **Novo dia:** reiniciar contagem de ações (dia 4 fechou no teto de ~50).
