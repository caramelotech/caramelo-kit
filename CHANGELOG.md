# Changelog

Todas as mudanças notáveis deste repositório são documentadas neste arquivo.

O formato segue [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/) e o projeto adota [Versionamento Semântico](https://semver.org/lang/pt-BR/).

Cada categoria em `skills/` tem sua própria versão, declarada em `.claude-plugin/plugin.json`. A versão listada aqui no topo é a do marketplace (`.claude-plugin/marketplace.json`) como um todo. Como o repositório ainda não teve nenhuma versão publicada, todo o trabalho até aqui faz parte do primeiro lançamento (1.0.0) - a partir do próximo commit e push, mudanças estruturais passam a exigir um novo bump de versão.

## [1.1.0] - 2026-10-10

### Adicionado

- Categoria `study` (1.0.0), registrada no marketplace, com a skill `lecture-notes`: transforma uma aula (transcrição, notas e/ou título) em uma nota de estudo didática para revisão, com referencial teórico pesquisado em fontes confiáveis. Pergunta o destino a cada chamada e guarda cursos e pastas em `~/.claude/lecture-notes/courses.json` para oferecê-los nas próximas.
- Categoria `career` (1.0.0), registrada no marketplace, com três skills que compartilham um perfil de carreira (`~/.claude/career/profile.json`, procedimento em `skills/career/shared/profile.md`): no primeiro uso coletam trajetória, destino, idioma e formato; nas chamadas seguintes só a vaga é necessária. Quando a pessoa não informa a trajetória profissional, as skills explicam por que ela é necessária e ajudam a obtê-la: a partir de arquivo, currículo em PDF ou `.docx`, LinkedIn (via export em PDF ou texto colado, sem login), portfólio e GitHub, ou por criação guiada, consolidando tudo em `Trajetoria Profissional.md`.
  - `cover-letter`: carta de apresentação completa para e-mail, LinkedIn ou anexo, em nota, `.docx`, PDF ou só no chat.
  - `interview-prep`: nota de candidatura com análise da vaga e preparação para entrevista (perguntas prováveis, pontos fortes, lacunas e perguntas para a pessoa entrevistadora).
  - `application-text`: texto curto para o campo de candidatura (Gupy, 1500 caracteres por padrão, ou outro limite), rodando a `interview-prep` antes e contando caracteres com precisão.

## [development 1.1.0] - 2026-10-10

### Adicionado

- Seção "Princípios de execução" nas skills `code-review` e `commit-message`, com diretrizes comportamentais para reduzir erros comuns de assistentes de IA (presunção de contexto, abstrações especulativas, mistura de bug com preferência de estilo, falta de critério verificável), adaptadas ao escopo de cada skill.

## [1.0.0] - 2026-10-10

### Adicionado

- Estrutura inicial do repositório: skills organizadas por categoria em `skills/<categoria>/skills/<nome>/SKILL.md`, cada categoria como plugin independente do Claude Code (`development`, `writing`, `testing`, `devops`, `security`, `design`), com `.claude-plugin/plugin.json` próprio (nome, versão, descrição, autor, licença, keywords).
- Skills: `code-review` e `commit-message` (`development`); `unit-test-generator` (`testing`); `text-writer` e `text-humanizer` (`writing`); `dockerfile-review` (`devops`); `owasp-check` (`security`); `apply-design-system` (`design`), com o design system do Notion catalogado como primeira referência em `references/notion.md`.
- Agents: `code-reviewer`, `test-generator`, `doc-writer`.
- `templates/` para criar novas skills, agents e integrações externas.
- `.claude-plugin/marketplace.json` registrando as categorias como plugins instaláveis via `/plugin marketplace add` e `/plugin install <categoria>@caramelo-kit`.
- `.github/CONTRIBUTING.md` com o guia de contribuição (skills, categorias, agents e integrações externas).
- Este `CHANGELOG.md`.
- Licença MIT.
