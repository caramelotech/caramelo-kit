---
name: code-review
description: Revisa código em busca de bugs, vulnerabilidades de segurança, problemas de performance e manutenibilidade. Use quando for solicitado revisar, analisar ou dar feedback sobre código.
---

# Code Review

Revise o código fornecido com foco em corretude, segurança, legibilidade e manutenibilidade, seguindo boas práticas da linguagem utilizada.

## Como revisar

Organize a revisão nas seguintes categorias:

**Bugs e corretude**
Liste problemas que causam ou podem causar comportamento incorreto.

**Segurança**
Aponte vulnerabilidades (injeção, exposição de dados, permissões, etc.).

**Performance**
Identifique gargalos ou operações desnecessariamente custosas.

**Legibilidade e manutenção**
Sugira melhorias de nomenclatura, estrutura e clareza.

**Pontos positivos**
Destaque o que está bem implementado.

Para cada problema encontrado, informe:

- Severidade: `crítico` | `importante` | `sugestão`
- Linha ou trecho afetado
- Sugestão de correção

## Variáveis

| Variável        | Descrição             | Exemplo                          |
| --------------- | --------------------- | -------------------------------- |
| `{{linguagem}}` | Linguagem do código   | `TypeScript`                     |
| `{{contexto}}`  | O que o código faz    | `Middleware de autenticação JWT` |
| `{{codigo}}`    | Código a ser revisado | _(trecho ou diff)_               |

## Exemplo

**Input:**

```python
# linguagem: Python
# contexto: Função que valida e salva usuário no banco

def save_user(name, email, db):
    query = f"INSERT INTO users VALUES ('{name}', '{email}')"
    db.execute(query)
```

**Output esperado:**

```
**Bugs e corretude**
- A ausência de tratamento de erro em db.execute pode causar falhas silenciosas.

**Segurança**
- [CRÍTICO] Linha 2: SQL Injection via interpolação direta de variáveis na query.
  Correção: db.execute("INSERT INTO users VALUES (?, ?)", (name, email))

**Performance**
- Sem problemas evidentes para o escopo atual.

**Legibilidade e manutenção**
- [SUGESTÃO] Adicione validação dos inputs antes de persistir.

**Pontos positivos**
- Assinatura simples e responsabilidade única bem definida.
```

## Notas

- Para diffs grandes, revise por arquivo ou por função
- Informe o contexto do PR para revisões mais precisas
- Combine com a skill `owasp-check` para revisões focadas em segurança
