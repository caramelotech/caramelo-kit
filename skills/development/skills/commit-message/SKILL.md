---
name: commit-message
description: Avalia alterações no working tree, decide se podem ser particionadas em commits menores e executa os commits seguindo Conventional Commits, sem co-autores e sem referências a qualquer agent. Parâmetros opcionais: nome da nova branch e flag --sign para assinar com Signed-off-by. Ex: /commit-message feat/branch --sign
allowed-tools: Bash, Read, Glob, Grep
---

# Commit Workflow

## Regras inegociáveis

- **Nunca** adicionar co-autores (`Co-Authored-By`) nas mensagens de commit.
- **Nunca** mencionar Codex, Claude, IA, assistente ou qualquer agent em commits ou branches.
- Seguir estritamente o formato **Conventional Commits**.
- **Nunca** usar `git add .` ou `git add -A` - sempre analisar as alterações e adicionar arquivos específicos.
- **Nunca** fazer `git push` automaticamente.

## 1. Parâmetros

O skill recebe os args passados após `/commit-message`. Podem vir em qualquer ordem. Interprete assim:

- **Argumento sem `--`** (ex: `feat/ajuste-login`, `fix/bug-x`) - nome da nova branch a criar antes de commitar. Se ausente, commita na branch atual.
- **`--sign`** - adiciona `Signed-off-by: Nome <email>` no rodapé de cada commit (usa o nome e e-mail configurados no git). Se ausente, não assina.

Exemplos:

- `/commit-message` - branch atual, sem assinatura
- `/commit-message feat/nova-feature` - cria branch, sem assinatura
- `/commit-message --sign` - branch atual, com assinatura
- `/commit-message feat/nova-feature --sign` - cria branch, com assinatura

Se for criar branch:

```bash
git checkout -b <nome-da-branch>
```

Se nenhuma branch for passada e a branch atual (`git branch --show-current`) for `main`, `master` ou `developer`, avise o usuário e pergunte se deseja prosseguir commitando direto nela ou criar uma nova branch. Sugira um nome seguindo o padrão `<tipo>/<descrição-curta>` (prefixo `feat`, `fix`, `chore`, etc., de acordo com a natureza predominante das alterações levantadas na etapa 2). A decisão final é do usuário - comite na branch atual se ele confirmar, ou crie a branch sugerida (ou outra que ele indicar) caso contrário.

Para obter nome e e-mail do git (usado no `Signed-off-by`):

```bash
git config user.name
git config user.email
```

Se `--sign` for solicitado e o usuário não tiver GPG (ou outro método de assinatura) configurado para o Git, informe isso a ele antes de prosseguir - `--signoff` funciona sem GPG (apenas adiciona a linha `Signed-off-by`), mas se o repositório exigir assinatura criptográfica (`commit.gpgsign=true`) e não houver chave configurada, o commit falhará.

## 2. Levantamento das alterações

Execute em sequência:

```bash
git status
git diff HEAD
git diff --cached
```

Leia a saída completa. Identifique:

- Arquivos modificados, adicionados e removidos
- A natureza de cada mudança (funcionalidade, correção, estilo, configuração, teste, documentação, refactor)
- Agrupamentos lógicos independentes entre si

**Antes de montar o plano de commits**, verifique se há arquivos que não deveriam ser commitados (ex: `.env`, credenciais, chaves, arquivos de build/dependências não versionados). Se encontrar algum:

- Não o inclua em nenhum commit planejado.
- Avise o usuário e sugira adicioná-lo ao `.gitignore`.

## 3. Decisão de particionamento

Avalie se as mudanças formam **um único contexto coeso** ou **contextos independentes** que merecem commits separados.

Critérios para separar em commits distintos:

- Mudanças em camadas diferentes sem dependência direta (ex: UI + API + banco)
- Correção de bug isolada junto com nova funcionalidade
- Alterações de configuração/chore independentes do código de negócio
- Testes adicionados separadamente da implementação

Critérios para manter em um único commit:

- Mudanças que não fazem sentido sem a outra (implementação + migration obrigatória)
- Volume pequeno de arquivos com contexto único
- Correções pontuais em poucos arquivos

**Antes de executar os commits, apresente ao usuário o plano:**

```
Planejo fazer X commit(s):

1. feat(auth): adicionar validação de JWT
   Arquivos: src/lib/auth.ts, src/middleware.ts

2. test(auth): cobrir validação de JWT
   Arquivos: src/lib/__tests__/auth.test.ts
```

Aguarde a confirmação do usuário ("ok", "sim", "pode ir", "s" ou variantes) antes de prosseguir. Se o usuário ajustar o plano, incorpore e confirme antes de executar.

## 4. Formato Conventional Commits

```
<type>(<scope>): <descrição no imperativo, minúsculo, em inglês>
```

### Tipos

| Tipo       | Quando usar                              |
| ---------- | ---------------------------------------- |
| `feat`     | Nova funcionalidade visível ao usuário   |
| `fix`      | Correção de bug                          |
| `refactor` | Refatoração sem mudança de comportamento |
| `test`     | Adição ou ajuste de testes               |
| `chore`    | Configuração, deps, scripts, CI/CD       |
| `docs`     | Documentação                             |
| `style`    | Formatação, lint (sem lógica)            |
| `perf`     | Melhoria de performance                  |
| `build`    | Mudanças no sistema de build             |
| `revert`   | Reverter commit anterior                 |

A mensagem de commit é sempre escrita em inglês, a menos que o usuário solicite outro idioma.

### Escopo

O escopo é opcional, mas use sempre que identificável. Exemplos: `auth`, `api`, `db`, `ui`, `layout`, `members`, `accounts`.

### Descrição

- Imperativo, minúsculo, sem ponto final
- Em inglês
- Máximo ~72 caracteres
- Responde "o que este commit faz?" - não "o que eu fiz?"

Exemplos corretos:

```
feat(members): add member invite endpoint
fix(accounts): fix negative balance calculation
chore(deps): update next version
refactor(api): extract validation logic into helper
```

## 5. Execução dos commits

Para cada commit planejado, adicione apenas os arquivos do escopo e commite:

**Sem `--sign`:**

```bash
git add <arquivo1> <arquivo2> ...
git commit -m "<mensagem conventional commit>"
```

**Com `--sign`:**

```bash
git add <arquivo1> <arquivo2> ...
git commit --signoff -m "<mensagem conventional commit>"
```

O `--signoff` acrescenta automaticamente `Signed-off-by: Nome <email>` no rodapé usando os dados de `git config user.name` e `git config user.email`.

Nunca inclua na mensagem:

- `Co-Authored-By: ...`
- Referências a Codex, Claude, IA, assistant ou qualquer agent
- Qualquer rodapé além do `Signed-off-by` (quando `--sign` for solicitado)

## 6. Confirmação final

Após todos os commits, execute:

```bash
git log --oneline -<n>
```

Onde `<n>` é o número de commits feitos. Mostre o resultado ao usuário.
