---
name: commit-message
description: Avalia alterações no working tree, decide se podem ser particionadas em commits menores e executa os commits seguindo Conventional Commits, sem co-autores e sem referências a qualquer agent. Lembra as preferências da pessoa entre sessões (commitar ou não em branch protegida como a main, commitar sem confirmar o plano, fazer push, assinar com Signed-off-by, idioma da mensagem), inclusive por repositório, para trabalhar de forma autônoma quando ela quiser. Parâmetros opcionais: nome da nova branch, --sign, --no-sign, --push, --no-push, --reconfigurar e --preferencias. Ex: /commit-message feat/branch --sign
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, AskUserQuestion
---

# Commit Workflow

## Regras inegociáveis

Valem em qualquer modo de autonomia e não podem ser mudadas por preferência:

- **Nunca** adicionar co-autores (`Co-Authored-By`) nas mensagens de commit.
- **Nunca** mencionar Codex, Claude, IA, assistente ou qualquer agent em commits ou branches.
- Seguir estritamente o formato **Conventional Commits**.
- **Nunca** usar `git add .` ou `git add -A` - sempre analisar as alterações e adicionar arquivos específicos.
- **Nunca** commitar arquivos com segredos ou credenciais (`.env`, chaves, tokens).
- **Nunca** fazer `git push --force`, `rebase` ou `reset` de commits já enviados.
- **Nunca** fazer push sem que a preferência `push` ou a flag `--push` permita.

## 0. Preferências

Leia e siga `../../shared/preferences.md` (caminho relativo à pasta desta skill). Esta skill usa `autonomy` e as preferências abaixo, em `skills.commit-message` (ou em `repos.<repositório>.commit-message`, que têm prioridade):

| Preferência             | Valores                      | Padrão                                   | O que controla                                                                            |
| ----------------------- | ---------------------------- | ---------------------------------------- | ----------------------------------------------------------------------------------------- |
| `protectedBranches`     | lista de nomes               | `main`, `master`, `develop`, `developer` | Branches em que commitar direto exige atenção                                             |
| `protectedBranchPolicy` | `ask`, `allow`, `new-branch` | `ask`                                    | Em branch protegida: perguntar, commitar direto, ou criar uma branch nova automaticamente |
| `confirmPlan`           | `inherit`, `always`, `never` | `inherit`                                | Confirmar o plano de commits antes de executar. `inherit` segue `autonomy`                |
| `push`                  | `never`, `ask`, `auto`       | `never`                                  | Depois dos commits: não fazer push, perguntar, ou fazer push automaticamente              |
| `signoff`               | `true`, `false`              | `false`                                  | Adicionar `Signed-off-by` por padrão                                                      |
| `language`              | código de idioma             | `en`                                     | Idioma das mensagens de commit                                                            |

Perguntas da configuração inicial (junto com a de autonomia, se faltar):

- **Branch protegida** (header `Branch`): `Perguntar sempre` (Recommended), `Commitar direto`, `Criar branch nova`.
- **Push** (header `Push`): `Nunca fazer push` (Recommended), `Perguntar depois dos commits`, `Push automático`.
- **Assinatura** (header `Assinatura`): `Sem Signed-off-by` (Recommended), `Com Signed-off-by`.

`confirmPlan` começa em `inherit` e `language` em `en`; os dois mudam por reconfiguração ou pedido em linguagem natural (ex: "não precisa mais confirmar o plano", "escreva os commits em português").

Se a pessoa disser algo como "pode commitar direto na main neste repositório", grave em `repos.<repositório>.commit-message`, como descrito no arquivo compartilhado.

## 1. Parâmetros

O skill recebe os args passados após `/commit-message`. Podem vir em qualquer ordem e têm prioridade sobre as preferências, só nesta chamada:

- **Argumento sem `--`** (ex: `feat/ajuste-login`, `fix/bug-x`) - nome da nova branch a criar antes de commitar.
- **`--sign`** / **`--no-sign`** - força ou desliga o `Signed-off-by`.
- **`--push`** / **`--no-push`** - força ou desliga o push ao final.
- **`--reconfigurar`** - refaz as perguntas de preferências antes de seguir.
- **`--preferencias`** - mostra as preferências em uso (globais, da skill e do repositório) e não commita nada.

Exemplos:

- `/commit-message` - segue as preferências salvas
- `/commit-message feat/nova-feature` - cria a branch e commita nela
- `/commit-message --sign --push` - assina e faz push nesta chamada
- `/commit-message --preferencias` - só mostra as preferências

Se for criar branch:

```bash
git checkout -b <nome-da-branch>
```

### Branch protegida

Se nenhuma branch for passada e a branch atual (`git branch --show-current`) estiver em `protectedBranches`, siga `protectedBranchPolicy`:

- **`allow`**: commite direto na branch atual.
- **`new-branch`**: crie uma branch `<tipo>/<descrição-curta>` (prefixo de acordo com a natureza predominante das alterações levantadas na etapa 2) e commite nela, sem perguntar. Informe o nome no relatório final.
- **`ask`**: no modo `assistido`, avise e pergunte se deseja commitar direto ou criar a branch sugerida; a decisão é da pessoa. No modo `autonomo` ou sem ninguém para responder, use o padrão seguro: crie a branch sugerida e informe no relatório final.

Para obter nome e e-mail do git (usado no `Signed-off-by`):

```bash
git config user.name
git config user.email
```

Se o `Signed-off-by` estiver ativo e o repositório exigir assinatura criptográfica (`commit.gpgsign=true`) sem chave configurada, o commit falhará. Informe isso antes de prosseguir - `--signoff` sozinho funciona sem GPG, porque só adiciona a linha `Signed-off-by`.

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

- Não o inclua em nenhum commit planejado, em nenhum modo.
- Avise e sugira adicioná-lo ao `.gitignore`. No modo `autonomo`, siga com os demais arquivos e destaque o aviso no relatório final.

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

Monte o plano:

```
Planejo fazer X commit(s):

1. feat(auth): add JWT validation
   Arquivos: src/lib/auth.ts, src/middleware.ts

2. test(auth): cover JWT validation
   Arquivos: src/lib/__tests__/auth.test.ts
```

### Confirmar ou executar

Resolva `confirmPlan`: `inherit` vira `always` no modo `assistido` e `never` no modo `autonomo`.

- **`always`**: apresente o plano e aguarde a confirmação ("ok", "sim", "pode ir", "s" ou variantes). Se a pessoa ajustar o plano, incorpore e confirme antes de executar.
- **`never`**: apresente o plano e execute em seguida, sem esperar resposta.

## 4. Formato Conventional Commits

```
<type>(<scope>): <descrição no imperativo, minúsculo>
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

A mensagem de commit é escrita no idioma da preferência `language` (padrão: inglês).

### Escopo

O escopo é opcional, mas use sempre que identificável. Exemplos: `auth`, `api`, `db`, `ui`, `layout`, `members`, `accounts`.

### Descrição

- Imperativo, minúsculo, sem ponto final
- No idioma de `language`
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

**Sem `Signed-off-by`:**

```bash
git add <arquivo1> <arquivo2> ...
git commit -m "<mensagem conventional commit>"
```

**Com `Signed-off-by`:**

```bash
git add <arquivo1> <arquivo2> ...
git commit --signoff -m "<mensagem conventional commit>"
```

O `--signoff` acrescenta automaticamente `Signed-off-by: Nome <email>` no rodapé usando os dados de `git config user.name` e `git config user.email`.

Nunca inclua na mensagem:

- `Co-Authored-By: ...`
- Referências a Codex, Claude, IA, assistant ou qualquer agent
- Qualquer rodapé além do `Signed-off-by` (quando ativo)

Se um commit falhar (hook, assinatura, conflito), pare a sequência, não tente contornar o hook e informe o erro com a saída do comando.

## 6. Push

Resolva o push pela flag (`--push` / `--no-push`) ou pela preferência `push`:

- **`never`**: não faça push. Informe que os commits estão só no repositório local.
- **`ask`**: pergunte se deve fazer push. No modo `autonomo` ou sem ninguém para responder, não faça e informe.
- **`auto`**: faça `git push` (com `-u origin <branch>` se a branch ainda não tiver upstream). Se o push for rejeitado (por exemplo, a branch remota avançou), não force: informe o erro e sugira `git pull --rebase` antes de tentar de novo.

## 7. Relatório final

Após os commits, execute:

```bash
git log --oneline -<n>
```

Onde `<n>` é o número de commits feitos. Mostre o resultado e, em poucas linhas:

- a branch usada (e se foi criada por causa de `protectedBranchPolicy`);
- se houve push e para onde;
- arquivos deixados de fora (segredos, arquivos de build) e o motivo;
- decisões tomadas por padrão seguro, por falta de preferência;
- na primeira execução, onde as preferências foram salvas e como mudá-las (`--reconfigurar`, `--preferencias` ou pedido em linguagem natural).
