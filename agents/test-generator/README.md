# Agent: Test Generator

**Tipo:** autônomo  
**Skills utilizadas:** `skills/testing/skills/unit-test-generator/SKILL.md`

## Objetivo

Analisa um módulo ou arquivo completo e gera uma suite de testes cobrindo todas as funções e classes públicas.

## Fluxo de execução

```
1. Recebe o arquivo ou módulo a testar
2. Identifica todas as funções e classes públicas
3. Para cada função/classe, executa a skill unit-test-generator
4. Combina os testes em um único arquivo coeso
5. Verifica se há dependências externas que precisam de mock
```

## Como usar

Forneça o arquivo a ser testado, a linguagem e o framework de testes. O agente retornará um arquivo de testes pronto para uso.

## Inputs

| Parâmetro   | Obrigatório | Descrição                                |
| ----------- | ----------- | ---------------------------------------- |
| `arquivo`   | Sim         | Código fonte a ser testado               |
| `linguagem` | Sim         | Linguagem do código                      |
| `framework` | Sim         | Framework de testes (pytest, jest, etc.) |
| `excluir`   | Não         | Funções/classes a ignorar                |

## Output

Arquivo de testes com:

- Testes para cada função/classe pública
- Cobertura de happy path, edge cases e erros
- Estrutura compatível com o framework escolhido
