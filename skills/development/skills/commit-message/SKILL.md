---
name: commit-message
description: Gera mensagens de commit claras e padronizadas seguindo a especificação Conventional Commits. Use quando for solicitado escrever ou sugerir uma mensagem de commit.
---

# Commit Message Writer

Gere uma mensagem de commit clara e padronizada seguindo a especificação [Conventional Commits](https://www.conventionalcommits.org).

## Formato

```
<tipo>(<escopo>): <descrição>

[corpo opcional - explique o "porquê", não o "o quê"]

[rodapé opcional - BREAKING CHANGE: descrição]
```

## Regras

- Tipos válidos: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `perf`, `ci`
- Descrição em português, modo imperativo, sem ponto final, máximo 72 caracteres
- O escopo é opcional, mas recomendado em repositórios com múltiplos domínios
- Use `!` após o tipo para breaking changes: `feat!: novo formato de resposta da API`
- Adicione `BREAKING CHANGE:` no rodapé com a descrição do impacto

Retorne apenas a mensagem de commit, sem explicações adicionais.

## Variáveis

| Variável                | Descrição                      | Exemplo                                    |
| ----------------------- | ------------------------------ | ------------------------------------------ |
| `{{descricao_ou_diff}}` | Descrição das mudanças ou diff | `Adicionei validação de email no cadastro` |

## Exemplo

**Input:**

```
Corrigi um bug onde usuários conseguiam se cadastrar com emails duplicados.
Adicionei uma verificação no service antes de persistir no banco.
```

**Output esperado:**

```
fix(auth): impede cadastro com email já existente

Sem a verificação, era possível criar múltiplas contas com o mesmo
email, quebrando a unicidade esperada e causando conflitos no login.
```

## Notas

- Para mudanças complexas, prefira múltiplos commits atômicos em vez de um commit gigante
- O corpo do commit deve responder "por que essa mudança foi necessária?"
- Evite descrever o que o diff já mostra - foque no contexto e motivação
