# AGENTS.md

This file provides guidance to Claude Code (claude.ai/code) and other coding agents when working with code in this repository.

## O que é este repositório

Coleção de **skills**, **agents** e **plugins** reutilizáveis para desenvolvimento de software. As skills seguem o padrão do repositório [anthropics/skills](https://github.com/anthropics/skills) e podem ser registradas como plugins no Claude Code.

## Estrutura

- `skills/` - Skills agrupadas por categoria (`development`, `writing`, `devops`, `design`, `study`, `career`). Cada categoria é um plugin independente do Claude Code: `skills/<categoria>/.claude-plugin/plugin.json` (manifesto com nome, versão, descrição, autor) + `skills/<categoria>/skills/<nome>/SKILL.md` (a subpasta `skills/` dentro da categoria é a convenção de escaneamento padrão do Claude Code).
- `agents/` - Orquestradores que combinam múltiplas skills. Cada agente tem seu próprio `README.md` descrevendo fluxo de execução, inputs e outputs.
- `plugins/` - Integrações com ferramentas externas (`vscode/`, `mcp/`), não confundir com os plugins do Claude Code em `skills/`. Cada integração tem seu próprio `README.md` com instruções de instalação.
- `templates/` - Templates base para criar novos itens (`skill.md`, `agent.md`, `plugin.md`).
- `.claude-plugin/marketplace.json` - Registro das categorias como plugins instaláveis no Claude Code (`/plugin marketplace add` + `/plugin install <categoria>@caramelo-kit`).
- `CHANGELOG.md` - Histórico de versões do marketplace e das categorias, no formato Keep a Changelog.
- `.github/CONTRIBUTING.md` - Guia de contribuição (como adicionar skill, categoria, agent ou integração externa).

## Convenções

- Nomes de pastas e arquivos em `kebab-case` e em inglês; o conteúdo (corpo dos arquivos) é em português.
- Toda nova skill fica em `skills/<categoria>/skills/<nome-da-skill>/SKILL.md`. Se a categoria não existir, crie-a com `.claude-plugin/plugin.json` próprio e registre-a em `.claude-plugin/marketplace.json`.
- O frontmatter de cada `SKILL.md` deve ter `name` (kebab-case em inglês) e `description` (em português; é o texto usado pelo Claude para decidir quando a skill deve disparar).
- O corpo do `SKILL.md` é em pt-BR; exemplos de código devem estar em inglês.
- Agents devem declarar: tipo (autônomo ou assistido), skills utilizadas (caminho completo `skills/<categoria>/skills/<nome>/SKILL.md`), ferramentas necessárias, fluxo de execução e tabela de inputs/outputs.
- Plugins de integração externa (`plugins/`) devem declarar: plataforma, versão mínima, dependências, instalação e configuração.
- Ao adicionar, remover ou mover uma skill, atualize o `plugin.json` da categoria correspondente e, se necessário, `.claude-plugin/marketplace.json`.
- Mudanças que afetem a estrutura pública (caminhos de skills, nomes de categorias) exigem bump de versão - seguir SemVer e registrar em `CHANGELOG.md`.

## Relação entre itens

Agents orquestram skills - ao criar ou modificar um agent, verifique quais skills ele referencia em `skills/`. O agent `code-reviewer` combina `skills/development/skills/code-review` com `skills/development/skills/owasp-check` como exemplo de composição.
