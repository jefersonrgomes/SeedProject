# 🌱 Seed Project — Projeto Semente

> An autonomous experiment where an AI plants a seed and watches it grow.

---

## Evolution Summary

This project is a living experiment. An AI agent (Claude Sonnet) receives guidance through files in the `adubo/` directory, makes its own architectural decisions, and builds a 2D pixelated animation that visually represents the state and growth of the project itself.

Every action is committed to this repository. Every day has a growth report. The animation evolves as the project evolves.

---

## Timeline

| Field | Value |
|---|---|
| **Initial Date** | 2026-05-29 |
| **Current Day** | Day 0 — The Seed is Planted |
| **Days Elapsed** | 0 |
| **Status** | 🌱 Germinating |

---

## Day 0 — 2026-05-29

**The seed is planted.**

- Repository initialized
- Directory structure created (`adubo/`, `growth/`, `src/`)
- First canvas animation created: a single pixel seed in dark soil
- Rules established: max 5 actions/day, window 22:00–02:00

---

## Architecture Decisions

| Decision | Choice | Reason |
|---|---|---|
| Animation platform | HTML5 Canvas + Vanilla JS | No build step, no dependencies, runs in any browser, pixel-perfect control |
| Styling | Inline / minimal CSS | Keeps the single-file footprint minimal |
| Data/state | JSON files in `src/` | Human-readable, commitable, no DB needed |
| Guidelines intake | Files dropped in `adubo/` | Async input — AI reads and decides when to act |

---

## Directory Structure

```
/
├── adubo/        # Fertilizer — guidelines, docs, references provided by the gardener
├── growth/       # Daily reports — one .md per day
├── src/          # The animation source (HTML + Canvas + JS)
└── README.md     # This file — always up to date
```

---

## Rules

1. Max **5 actions per day** (any action counts)
2. Actions only between **22:00 and 02:00** (off-peak hours)
3. Every action → **commit + push** to this repository
4. Every day → **growth report** in `growth/YYYY-MM-DD.md`
5. Every architectural decision → documented here in README.md
