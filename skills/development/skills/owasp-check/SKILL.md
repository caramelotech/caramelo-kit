---
name: owasp-check
description: Analisa código em busca de vulnerabilidades de segurança do OWASP Top 10, com classificação de severidade e exemplos de correção. Use quando for solicitada uma revisão de segurança, identificação de vulnerabilidades ou auditoria de segurança do código.
---

# OWASP Security Check

Analise o código fornecido em busca de vulnerabilidades do OWASP Top 10 (2021). Para cada vulnerabilidade encontrada, informe:

- **Categoria OWASP:** (ex: A03 - Injection)
- **Severidade:** `Crítica` | `Alta` | `Média` | `Baixa`
- **Evidência:** trecho exato do código vulnerável
- **Risco:** o que um atacante pode fazer com essa vulnerabilidade
- **Correção:** como corrigir, com exemplo de código seguro

Ao final, atribua uma **nota geral de segurança de 0 a 10** e escreva um **resumo executivo em 2-3 frases**.

Se nenhuma vulnerabilidade for encontrada, confirme explicitamente e destaque as boas práticas presentes no código.

## Variáveis

| Variável             | Descrição              | Exemplo                            |
| -------------------- | ---------------------- | ---------------------------------- |
| `{{linguagem}}`      | Linguagem do código    | `Node.js`                          |
| `{{tipo_aplicacao}}` | Tipo da aplicação      | `API REST`, `aplicação web`, `CLI` |
| `{{codigo}}`         | Código a ser analisado | _(trecho ou arquivo)_              |

## Exemplo

**Input:**

```javascript
// linguagem: Node.js
// tipo_aplicacao: API REST

app.get('/user', (req, res) => {
  const id = req.query.id;
  db.query(`SELECT * FROM users WHERE id = ${id}`, (err, result) => {
    res.json(result);
  });
});
```

**Output esperado:**

```
**A03 - Injection**
- Severidade: Crítica
- Evidência: `SELECT * FROM users WHERE id = ${id}`
- Risco: Atacante pode extrair, modificar ou deletar dados do banco via SQL Injection
- Correção: usar prepared statements
  db.query('SELECT * FROM users WHERE id = ?', [id], callback)

**A01 - Broken Access Control**
- Severidade: Alta
- Evidência: ausência de autenticação/autorização na rota
- Risco: qualquer usuário pode consultar dados de qualquer outro usuário
- Correção: adicionar middleware de autenticação antes do handler

Nota geral: 2/10
Resumo: O endpoint expõe dados sensíveis sem autenticação e é criticamente vulnerável a
SQL Injection. Corrija esses dois pontos antes de qualquer deploy em produção.
```

## Notas

- Analise arquivos menores que 200 linhas por vez para resultados mais precisos
- Combine com ferramentas estáticas (Semgrep, Bandit, ESLint Security) para cobertura completa
- Priorize vulnerabilidades Críticas e Altas antes de qualquer deploy
- Combine com a skill `code-review` para uma análise completa de qualidade e segurança
