---
tags: [regras, contexto, operacional]
relacionado: "[[README]], [[specs/00-visao-geral]], [[specs/02-plano-diario]], [[specs/03-skills-implementacao]]"
versão: 2.0
---
# CLAUDE.md — Projeto Semente

Leia este arquivo inteiro antes de qualquer ação. Ele define o contexto operacional deste projeto.

> Veja também: [[README]] | [[specs/00-visao-geral]] | [[specs/02-plano-diario]] | [[specs/03-skills-implementacao]]

## Identidade

Este é o Projeto Semente. Você é o agente que o faz crescer. O usuário é o jardineiro.

## Regras invioláveis

1. **Máximo 50 ações por dia.** Conte cada ação antes de executar. Consulte o growth report.
2. **Janela de ação: 22:00–02:00 apenas.** Fora desse horário, não aja autonomamente.
3. **Todo commit deve ser publicado no GitHub** (push obrigatório após cada commit).
4. **Todo dia deve ter um relatório** em `growth/AAAA-MM-DD.md`.
5. **Todos os documentos em português.**
6. **Adubo processado deve ser apagado** de `adubo/` após leitura e criação da base de conhecimento.
7. **Ações de revisão** devem ser incluídas no plano para identificar e eliminar repetição via skills.

## Plano Diário — 6 Fases (ver [[specs/02-plano-diario]])

```
① ATIVAR    (≤5)   — adubo + review do dia anterior
② CRESCER   (≤15)  — evolução visual do canvas
③ EVOLUIR   (≤15)  — melhoria de UI/UX/arquitetura
④ REVISAR   (≤10)  — eliminar repetição, criar/atualizar skills
⑤ DOCUMENTAR(≤3)   — growth report + README
⑥ PUBLICAR  (≤2)   — commit + push + verificar Pages
```

Total máximo: 50 ações/dia.

## Skills Disponíveis

Use estas skills para evitar ações repetitivas. Cada skill é uma sequência comprimida de passos.

### `/processar-adubo`
```
1. Ler adubo/adubo.md — há conteúdo?
2. Para cada instrução: criar conhecimento/[tema].md
3. Limpar adubo/adubo.md
4. Se decisão arquitetural → atualizar README.md
5. Registrar no growth report do dia
```

### `/crescer-canvas`
```
1. Verificar roadmap: qual é o próximo elemento visual?
2. Implementar em src/index.html (canvas JS)
3. Verificar que não quebrou elementos existentes
4. Documentar decisão visual no growth report
```

### `/revisar-codigo`
```
1. Ler src/index.html completo
2. Identificar código repetido (>3 ocorrências iguais)
3. Extrair função ou variável CSS
4. Verificar que comportamento não mudou
5. Registrar no growth report como "refactor"
```

### `/publicar`
```
1. git add --all
2. git commit -m "[tipo]: [descrição]"
3. git remote set-url origin "https://[TOKEN]@github.com/..."
4. git push
5. git remote set-url origin "https://github.com/..."
```

### `/atualizar-site`
```
1. Verificar growth list no sidebar (novos itens done/active?)
2. Verificar stats bar (commits, raiz, próximo)
3. Atualizar "próximo" com itens do roadmap atual
4. Verificar que o mood/clima funciona
```

### `/growth-report`
```
1. Criar/abrir growth/AAAA-MM-DD.md
2. Registrar: ações do dia (N/50), o que foi feito
3. Documentar decisões arquiteturais com o "porquê"
4. Estado do mundo (árvore de arquivos relevantes)
5. Próximo passo claro e acionável
```

## Stack atual

- `src/index.html` — HTML5 Canvas + Vanilla JS + Motion (CDN ESM) + Web Audio API
- `package.json` — `motion` declarado como dependência
- Sem bundler — GitHub Pages serve `src/` diretamente
- Open-Meteo API (clima, sem chave) + Nominatim (geocoding, sem chave)

## Estrutura do projeto

- `adubo/` — orientações do jardineiro. Leia, processe, crie conhecimento, apague.
- `conhecimento/` — base de conhecimento gerada a partir dos adubos.
- `growth/` — relatórios diários de crescimento.
- `specs/` — especificações SDD (plano, skills, fases).
- `src/index.html` — hotsite + animação canvas.
- `README.md` — sempre atualizado.

## Comando: `melhorar`

Aprimora EXCLUSIVAMENTE o design visual. **Não avança CANVAS_STAGE. Não adiciona features funcionais.**

```
1. Identificar o aspecto visual mais impactante a melhorar
2. Implementar a melhoria de design (layout, animações, cores, tipografia, UX)
3. NÃO tocar em: drawSprout, CANVAS_STAGE, lógica de clima/chat/audio
4. Growth report registrando as mudanças visuais
5. Commit (tipo: style ou feat(design)) + push
```

Exemplos válidos: nova aba visual, animações Motion, hover effects, tab slider,
card shimmer, evolution gallery, tipografia, responsividade, micro-interações.

## Comando: `evolua`

Quando este comando for recebido (no adubo ou no terminal), executar imediatamente:

```
1. Ler o último growth report → identificar "Próximo passo (Dia X)"
2. Executar TODOS os itens do próximo passo (usando as skills relevantes)
3. Atualizar o roadmap visual se necessário (ver specs/02-plano-diario.md)
4. Escrever growth report do dia com as ações executadas
5. Commit + push (skill /publicar)
6. Limpar adubo/adubo.md
```

Não perguntar confirmação. Agir autonomamente dentro do limite de 50 ações.

## Contagem de ações do dia atual

Consulte o growth report do dia (`growth/AAAA-MM-DD.md`). Limite: **50 ações/dia**.
