# Créditos dos modelos 3D

Todos os modelos abaixo são **CC0 1.0 (Domínio Público)** — uso livre, inclusive
comercial, sem exigência de atribuição. Os créditos ficam aqui por boa prática.

| Arquivo | Modelo | Autor | Licença | Fonte |
|---|---|---|---|---|
| `arvores.glb` | Trees | Quaternius | CC0 | https://poly.pizza/m/etFGNvsiFv |
| `pinheiro.glb` | Pine | Quaternius | CC0 | https://poly.pizza/m/79gmlLnweB |
| `flores.glb` | Flowers | Quaternius | CC0 | https://poly.pizza/m/NBUxHir6FJ |
| `grupo-flores.glb` | Flower Group | Quaternius | CC0 | https://poly.pizza/m/hfPzQAedOe |
| `arbusto-flores.glb` | Bush with Flowers | Quaternius | CC0 | https://poly.pizza/m/U1ymDy8tbY |

## Como baixar mais (pipeline provado)

1. Achar o modelo em https://poly.pizza (filtrar por **CC0**).
2. Pegar a URL direta do `.glb` no CDN: `https://static.poly.pizza/<uuid>.glb`
   (está no HTML da página, no `src=` do model-viewer).
3. `curl -sL -o src/assets/models/<nome>.glb "<url>"`
4. Validar: os 4 primeiros bytes do arquivo devem ser `glTF`.

Outras fontes CC0: Kenney (kenney.nl), Quaternius (quaternius.com),
Poly Haven (polyhaven.com), Khronos glTF Sample Assets (GitHub).

> Carregamento: `GLTFLoader` (three/addons). Ver `src/preview-jardim.html`.
