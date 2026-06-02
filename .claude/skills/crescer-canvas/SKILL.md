---
name: crescer-canvas
description: Use ao avançar o estágio de crescimento visual da semente no canvas pixel-art de src/index.html. Adiciona o próximo estágio botânico em drawSprout, sincroniza renderScene/FRAMES/replayEvolution e atualiza a UI do site (stats, progresso, listas). Aciona quando o jardineiro pedir "evolua", "crescer canvas", próximo stage, ou avançar a planta (fruto, semente nova, etc.).
---

# Skill: crescer-canvas

Avança o `CANVAS_STAGE` da semente em **uma** etapa botânica, mantendo a
arquitetura single-file e zero-build. Cada estágio é uma decisão deliberada,
versionada em um commit (git É a persistência do stage).

## Quando usar
- Comando `evolua` / `siga` / `crescer canvas` do jardineiro.
- O "Próximo passo" do último growth report aponta um novo estágio.

## Quando NÃO usar
- Comando `melhorar` (só design visual — não toca em `drawSprout`/`CANVAS_STAGE`).

## Procedimento

1. **Ler o último growth report** → confirmar qual é o próximo estágio e seu desenho.
2. **Paleta** (`const P`): adicionar as cores novas do estágio (comentar a intenção).
3. **`drawSprout(stage)`**: adicionar bloco `if (stage >= N)`.
   - Reusar a fórmula de vento senoidal (`wo`) para continuidade do balanço.
   - Se o novo estágio *transforma* o anterior (ex.: pétalas → fruto), **gatear**
     o desenho antigo (`if (stage === N-1)` ou multiplicador de fade), nunca apagar
     os blocos dos estágios anteriores.
4. **`CANVAS_STAGE = N`** + atualizar o comentário do mapa de estágios.
5. **`renderScene(...)`** (snapshots/thumbnails): replicar o estágio com `tstage>=N`
   sem vento (posição neutra).
6. **`FRAMES`**: relabelar o frame anterior; adicionar o novo `{ stage:N, label:'hoje', ... }`.
7. **`replayEvolution`**: incluir N no array `stages=[0..N]`.
8. **UI do site**: stats (`🌸 flor`, `🌱 próximo`), `#stageFill` (%), `#canvasLabel`,
   lista de crescimento (anterior → ✓, novo → `active`), lista "próximo".
9. **Verificar** sem browser: `new Function(<script inline>)` → SYNTAX OK; conferir
   coordenadas dentro de 0–47; renderizar um mapa ASCII do ápice para checar a forma.
10. **Documentar** no growth report e **publicar** (skill /publicar).

## Anti-regressão (invariável)
- Nunca introduzir `opacity:0` que dependa de JS para revelar (lição [[feedback_testing]]).
- Estágios 0..N-1 permanecem visualmente intactos (só adição/gating).
