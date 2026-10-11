---
name: unit-test-generator
description: Gera testes unitários para uma função ou classe, cobrindo caminho feliz, casos de borda e cenários de erro. Use quando for solicitado escrever, criar ou gerar testes.
---

# Unit Test Generator

Gere uma suite completa de testes unitários para o código fornecido, cobrindo caminho feliz, casos de borda e cenários de erro.

## Como gerar os testes

- Cubra o caminho feliz (happy path)
- Cubra casos de borda (valores nulos, vazios, extremos)
- Cubra cenários de erro e exceções esperadas
- Use nomes descritivos no padrão: `deve_[resultado]_quando_[condição]`
- Adicione um comentário de uma linha explicando cada grupo de testes
- Não use mocks a menos que sejam estritamente necessários para isolar dependências externas

Retorne apenas o código dos testes, sem explicações adicionais.

## Variáveis

| Variável        | Descrição                 | Exemplo              |
| --------------- | ------------------------- | -------------------- |
| `{{linguagem}}` | Linguagem do código       | `Python`             |
| `{{framework}}` | Framework de testes       | `pytest`             |
| `{{codigo}}`    | Função ou classe a testar | _(trecho de código)_ |

## Exemplo

**Input:**

```python
# linguagem: Python
# framework: pytest

def divide(a, b):
    if b == 0:
        raise ValueError("Divisor cannot be zero")
    return a / b
```

**Output esperado:**

```python
import pytest
from math import isclose
from module import divide

# Happy path
def test_deve_retornar_quociente_quando_divisao_valida():
    assert isclose(divide(10, 2), 5.0)

def test_deve_retornar_float_quando_resultado_nao_inteiro():
    assert isclose(divide(1, 3), 0.3333, rel_tol=1e-4)

# Edge cases
def test_deve_retornar_zero_quando_numerador_zero():
    assert divide(0, 5) == 0

def test_deve_funcionar_com_numeros_negativos():
    assert isclose(divide(-10, 2), -5.0)

def test_deve_funcionar_com_dois_negativos():
    assert isclose(divide(-10, -2), 5.0)

# Error scenarios
def test_deve_lancar_valueerror_quando_divisor_zero():
    with pytest.raises(ValueError, match="Divisor cannot be zero"):
        divide(10, 0)
```

## Notas

- Para classes, solicite testes por método para manter o escopo gerenciável
- Especifique se o projeto usa fixtures ou factories para dados de teste
- Mensagens de erro e strings internas do código devem estar em inglês para manter consistência com o código-fonte
