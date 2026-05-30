---
tags: [conhecimento, claude-code, anthropic, ia]
relacionado: "[[README]], [[CLAUDE]], [[specs/00-visao-geral]], [[growth/2026-05-29]]"
---
# Conhecimento: Claude Code

> Fonte: https://code.claude.com/docs/pt/overview
> Processado em: 2026-05-29
> Veja também: [[specs/00-visao-geral]] | [[growth/2026-05-29]] | [[CLAUDE]]

## O que aprendi

Claude Code é uma ferramenta de codificação agêntica. Opera em terminal, VS Code, JetBrains, desktop e web. Lê a base de código, edita arquivos, executa comandos e se integra com ferramentas de desenvolvimento.

## Capacidades relevantes para este projeto

### Rotinas (Routines)
Executam em infraestrutura gerenciada pela Anthropic — continuam funcionando mesmo com o computador desligado. Podem ser acionadas por chamadas de API, eventos do GitHub ou cronograma. **Impacto direto:** é o mecanismo ideal para automatizar as ações noturnas entre 22:00–02:00 sem depender da máquina do usuário.

### Tarefas Agendadas do Desktop
Rodam na máquina local, com acesso direto aos arquivos. Alternativa às Routines quando a operação precisa tocar o sistema de arquivos local.

### Hooks
Comandos shell executados antes/depois de ações do Claude Code. Exemplo: formatar automaticamente após edição, rodar lint antes de commit. **Impacto:** pode garantir que todo commit segue o padrão do projeto.

### CLAUDE.md
Arquivo lido no início de cada sessão. Contém padrões de codificação, decisões de arquitetura, bibliotecas preferidas. **Impacto:** devo criar um `CLAUDE.md` neste projeto com as regras do Projeto Semente para que cada sessão futura já saiba o contexto.

### MCP (Model Context Protocol)
Padrão aberto para conectar IA a fontes externas: Google Drive, Jira, Slack, ferramentas customizadas. **Impacto futuro:** quando o projeto crescer, posso consumir adubo diretamente do Drive ou Slack.

### Sub-agentes e Agent SDK
Múltiplos agentes trabalhando em paralelo, coordenados por um líder. **Impacto futuro:** para tarefas complexas, posso delegar partes da animação a sub-agentes especializados.

### CLI Composable
Piping, scripting, integração com CI. Exemplo: `tail -200 app.log | claude -p "analise"`. **Impacto:** a animação pode futuramente receber dados do git log via pipe para representar visualmente o histórico de commits.

## Decisão arquitetural gerada por este conhecimento

**Devo criar um `CLAUDE.md`** neste projeto com as regras operacionais. Assim, toda sessão futura começa já sabendo: limite de 5 ações, janela 22:00–02:00, idioma português, regras de commit, estrutura de diretórios.

**Próximo passo investigar:** Routines — como configurar para executar automaticamente neste projeto na janela 22:00–02:00.
