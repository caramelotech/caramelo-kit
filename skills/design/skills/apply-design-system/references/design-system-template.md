# {Nome da marca}

Modelo para documentar um novo design system de referência. Preencha ao menos Cores, Tipografia e Formas antes de usar - são o mínimo necessário para gerar um resultado consistente. As demais seções (Layout, Elevação, Componentes, O que fazer e o que não fazer) melhoram o resultado mas podem ficar incompletas numa primeira versão.

Use `{token.nome}` para qualquer valor que se repete (cor, tamanho, raio) - isso permite reaplicar o DS de forma consistente em slides ou páginas diferentes.

## Visão geral

Duas ou três frases descrevendo a personalidade da marca em palavras (ex: "discreta e confiante, com um único acento de cor", "vibrante e lúdica, cores saturadas em toda parte"). Liste 3 a 5 características-chave em bullets.

## Cores

### Marca e acento
- **{Nome da cor}** (`{colors.primary}` - #hex): onde essa cor aparece e o que ela sinaliza (ação principal? link? ambos?).

### Superfície
- **{Nome}** (`{colors.canvas}` / `{colors.surface}` - #hex): fundo de página e fundo de cards/painéis (podem ser a mesma cor ou duas).

### Texto
- **{Nome}** (`{colors.ink}` - #hex): texto principal.
- **{Nome}** (`{colors.ink-muted}` - #hex): texto secundário/legendas.

### Semântica (opcional)
- Sucesso, erro, aviso - se a marca tiver cores dedicadas para isso.

## Tipografia

### Família da fonte
Nome da fonte principal e sua pilha de fallback (ex: `Inter, system-ui, sans-serif`). Se houver uma segunda família (ex: uma serifada para títulos), declare aqui.

### Hierarquia

| Token | Tamanho | Peso | Altura da linha | Uso |
|---|---|---|---|---|
| `{typography.heading-1}` | | | | Títulos de seção |
| `{typography.body-md}` | | | | Texto de corpo padrão |
| `{typography.button}` | | | | Rótulos de botão |

## Layout

- **Unidade de espaçamento base**: (ex: 8px)
- **Largura máxima de conteúdo**: (ex: 1200px)
- Como as seções se agrupam (espaço em branco generoso? linhas divisórias?)

## Elevação e profundidade (opcional)

Como a marca sinaliza que um elemento está "por cima" de outro: sombra pesada, sombra suave em camadas, ou nenhuma sombra (só borda)?

## Formas

### Escala de raio de borda

| Token | Valor | Uso |
|---|---|---|
| `{rounded.sm}` | | Campos, tags |
| `{rounded.md}` | | Botões, cards |
| `{rounded.full}` | | Pílulas, avatares |

## Componentes (opcional, mas recomendado)

Para cada componente visual recorrente (botão primário, card, cabeçalho de seção, rodapé), descreva: cor de fundo, cor de texto, tipografia, raio, padding, borda/sombra.

## O que fazer e o que não fazer (opcional)

### Faça
- Regras que mantêm a identidade consistente.

### Não faça
- Combinações ou usos que quebram a identidade (ex: "não use a cor de acento em blocos grandes de fundo").
