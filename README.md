# 🌱 Projeto Semente — Seed Project

> Um experimento autônomo onde uma IA planta uma semente e observa seu próprio crescimento.

---

## Resumo da Evolução

Este projeto é um experimento vivo. Um agente de IA (Claude Sonnet) recebe orientações através de arquivos no diretório `adubo/`, toma suas próprias decisões arquiteturais e constrói uma animação 2D pixelada que representa visualmente o estado e o crescimento do próprio projeto.

Cada ação é commitada neste repositório. Cada dia tem um relatório de crescimento. A animação evolui conforme o projeto evolui.

---

## Linha do Tempo

| Campo | Valor |
|---|---|
| **Data inicial** | 2026-05-29 |
| **Dia atual** | Dia 0 — A Semente Germina |
| **Dias decorridos** | 0 |
| **Status** | 🌱 Germinando |
| **Site** | [jefersonrgomes.github.io/SeedProject](https://jefersonrgomes.github.io/SeedProject/) |

---

## Dia 0 — 2026-05-29

**A semente é plantada. O primeiro adubo é absorvido.**

- Repositório inicializado
- Estrutura de diretórios criada (`adubo/`, `growth/`, `src/`, `conhecimento/`)
- Primeira animação canvas: semente pixelada no solo escuro com pulso lento
- Primeiro adubo processado: documentação do Claude Code — base de conhecimento criada
- Animação atualizada: raiz primária emerge abaixo da semente
- `CLAUDE.md` criado com regras operacionais do projeto
- Idioma de todos os documentos: **português**

---

## Decisões Arquiteturais

| Decisão | Escolha | Motivo |
|---|---|---|
| Plataforma da animação | HTML5 Canvas + Vanilla JS | Sem dependências, sem build step, funciona em qualquer browser, controle pixel a pixel |
| Estilo | CSS mínimo inline | Mantém o footprint de um único arquivo |
| Estado / dados | Arquivos JSON em `src/` | Legível por humanos, versionável, sem banco de dados |
| Canal de orientações | Arquivos em `adubo/` | Input assíncrono — a IA lê e decide quando agir |
| Memória de sessão | `CLAUDE.md` | Regras operacionais persistem entre sessões sem precisar repetir |
| Base de conhecimento | `conhecimento/*.md` | Cada adubo processado gera um arquivo de aprendizado |
| Idioma | Português (BR) | Determinado pelo primeiro adubo recebido |
| Libs 3D (proposta) | Three.js + addons via **import map + CDN ESM** (`src/preview.html`) | Atende ao pedido de "importar as libs" **sem bundler** — mantém o zero-build. Site 2D segue vanilla; 3D é página separada (degrada sozinha se o CDN cair) |

---

## Estrutura de Diretórios

```
/
├── adubo/           # Fertilizante — orientações e docs fornecidas pelo jardineiro
├── conhecimento/    # Base de conhecimento gerada a partir dos adubos processados
├── growth/          # Relatórios diários — um .md por dia
├── src/             # A animação (HTML5 Canvas + Vanilla JS)
└── README.md        # Este arquivo — sempre atualizado
```

---

## Regras Operacionais

1. Máximo de **50 ações por dia** (qualquer ação conta — atualizado em Dia 2)
2. Ações apenas entre **22:00 e 02:00** (horário fora do pico)
3. Toda ação → **commit + push** para este repositório
4. Todo dia → **relatório de crescimento** em `growth/AAAA-MM-DD.md`
5. Toda decisão arquitetural → documentada aqui no README.md
6. Todos os documentos → escritos em **português**
7. Conteúdo do `adubo/` → **apagado após processamento**
8. Ações repetitivas → **transformadas em skills** (ver `specs/03-skills-implementacao.md`)

## Plano Diário (6 fases · 50 ações)

| Fase | Limite | Objetivo |
|---|---|---|
| ① ATIVAR | ≤5 | Adubo + contexto |
| ② CRESCER | ≤15 | Evolução canvas |
| ③ EVOLUIR | ≤15 | UI/features |
| ④ REVISAR | ≤10 | Skills + refactor |
| ⑤ DOCUMENTAR | ≤3 | Growth report |
| ⑥ PUBLICAR | ≤2 | Commit + push |
