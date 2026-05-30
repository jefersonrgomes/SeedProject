---
tags: [spec, sdd, plano-diario, rotina, fase-0]
relacionado: "[[specs/00-visao-geral]], [[CLAUDE]], [[specs/01-skills]]"
status: ativo
versão: 1.0
---
# Spec 02 — Plano Diário de Evolução (5 Passos)

> Veja também: [[CLAUDE]] | [[specs/00-visao-geral]] | [[specs/01-skills]]

## Regra fundamental

Este plano executa **uma vez por dia**, entre 22:00 e 02:00.
O adubo pode ser o trigger, mas **não é obrigatório** — o plano roda mesmo sem adubo novo.
Se há adubo: o adubo define a pauta. Se não há: executar o plano padrão abaixo.

---

## Os 5 Passos

### Passo 1 — ATIVAR (5 min)

**O que fazer:**
1. Ler `growth/AAAA-MM-DD.md` do dia — quantas ações já foram usadas?
2. Verificar `adubo/adubo.md` — há conteúdo novo?
   - Se sim: o adubo define a pauta do dia (processe antes de avançar)
   - Se não: seguir o plano padrão (passos 2 a 5)
3. Definir o objetivo principal do dia em uma frase

**Output:** clareza sobre o que será feito hoje.

---

### Passo 2 — CRESCER (15 min)

**O que fazer:**
Adicionar ou evoluir **pelo menos 1 elemento visual** no canvas seguindo o roadmap:

```
Dia 0-1  → semente + raiz primária + minhoca         ✅ feito
Dia 2-3  → raiz secundária + rachadura no solo
Dia 4-5  → hipocótilo emerge (pixel acima da semente)
Dia 7-10 → broto rompe a superfície
Dia 14+  → cotilédones (primeiras folhas)
Dia 20+  → caule cresce + sol aparece no topo
Dia 30+  → planta completa + abelha + passarinho
Dia 60+  → floração + janela + ambiente externo
```

O elemento deve ser visualmente coerente com o estágio atual.
Documentar a decisão visual no growth report.

---

### Passo 3 — EVOLUIR (15 min)

**O que fazer:**
Melhorar **um aspecto** do hotsite ou da arquitetura:

Exemplos (escolher o mais impactante do dia):
- Nova animação com Motion (entrada, hover, transição)
- Ajuste de layout ou tipografia
- Novo conteúdo no sidebar (stats, links, info)
- Melhoria de acessibilidade (aria-labels, contraste)
- Refatoração de código para clareza
- Avanço na implementação das Skills (Fase 1 SDD)

---

### Passo 4 — DOCUMENTAR (10 min)

**O que fazer:**
1. Criar ou atualizar `growth/AAAA-MM-DD.md` com:
   - Ações do dia (N de 5)
   - O que foi feito em cada passo
   - Por que cada decisão foi tomada
   - Estado do mundo ao final do dia
   - Próximo passo
2. Se houver nova decisão arquitetural: atualizar `README.md`
3. Se houver mudança de fase: atualizar `specs/00-visao-geral.md`

---

### Passo 5 — PUBLICAR (5 min)

**O que fazer:**
1. `git add .`
2. `git commit -m "feat/fix/docs: [descrição concisa]"`
3. `git push` (com token — limpar URL após push)
4. Verificar que GitHub Actions completou com sucesso
5. Limpar `adubo/adubo.md` se havia adubo processado

**Output:** site atualizado em `jefersonrgomes.github.io/SeedProject`

---

## Critério de conclusão

O dia está completo quando:
- ✅ Growth report escrito
- ✅ Pelo menos 1 elemento visual evoluído (Passo 2) OU 1 melhoria UI (Passo 3)
- ✅ Commit publicado no GitHub
- ✅ Site funcionando em `jefersonrgomes.github.io/SeedProject`
