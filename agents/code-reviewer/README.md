# Agent: Code Reviewer

**Tipo:** assistido  
**Skills utilizadas:** `skills/development/skills/code-review/SKILL.md`, `skills/security/skills/owasp-check/SKILL.md`

## Objetivo

Orquestra uma revisão completa de código combinando análise geral e verificação de segurança, produzindo um relatório unificado.

## Fluxo de execução

```
1. Recebe o diff ou arquivos do PR
2. Executa a skill code-review no código alterado
3. Executa a skill owasp-check nos trechos críticos identificados
4. Consolida os resultados em um relatório único
5. Gera lista de action items por prioridade
```

## Como usar

Forneça ao agente o diff ou os arquivos alterados e o contexto do PR. O agente retornará um relatório consolidado com todos os problemas encontrados e ações recomendadas.

## Inputs

| Parâmetro   | Obrigatório | Descrição                        |
| ----------- | ----------- | -------------------------------- |
| `diff`      | Sim         | Diff do PR ou arquivos alterados |
| `contexto`  | Recomendado | Descrição do que o PR faz        |
| `linguagem` | Sim         | Linguagem principal do código    |

## Output

Relatório com:

- Problemas agrupados por severidade
- Vulnerabilidades de segurança identificadas
- Lista de action items ordenada por prioridade
- Estimativa de esforço para correção
