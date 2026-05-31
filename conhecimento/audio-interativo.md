---
tags: [audio, web-audio-api, ux, temas]
---
# Conhecimento: Áudio Interativo + Temas

## Som por padrão (autoplay)

Browsers bloqueiam autoplay até um gesto do usuário. Padrão adotado:
- `musicOn=true` no estado inicial (UI já mostra "on")
- YT API carregada imediatamente no `loadYTApi()` ao iniciar
- Handler `onFirstGesture` nos eventos `click/keydown/touchstart` dispara `playVideo()` na primeira interação
- Após esse gesto, o player inicia e o handler se remove

## Sons de UI (Web Audio API)

Um `AudioContext` reutilizável (`sfxCtx`) evita criar novos contextos a cada beep.
Funções de som curtas e específicas por ação:

| Função      | Ação                        | Tom              |
|-------------|----------------------------|------------------|
| `sfxClick()`  | tabs, toggles              | 660Hz, 60ms      |
| `sfxWater()`  | regar                      | 440→330Hz, cascata |
| `sfxHeart()`  | acariciar                  | 528Hz, 180ms soft |
| `sfxSend()`   | chat enviar                | 880Hz, 70ms      |
| `sfxReply()`  | chat resposta              | 550+660Hz, delay |
| `sfxSuccess()`| share/copy                 | 1100→880Hz       |

## Tema alternativo Roxo/Cosmic

Implementado via `body.theme-roxo` que sobrescreve as CSS variables.
Toggle JS: `document.body.classList.toggle('theme-roxo', themeRoxo)`.
Botão `#themeBtn` na sidebar esquerda, abaixo do soundBtn.

Paleta roxo: accent `#8a5af8` / `#aa7aff`, bg `#100e16`, surfaces `#1a1726/1e30/2e293e`.

## Melhoria degradê

`body::before` agora tem 3 camadas:
1. Radial elipse topo (verde/roxo conforme tema)
2. Radial elipse canto inferior-direito (tonalidade complementar sutil)
3. Grade de pontos (mantida)
