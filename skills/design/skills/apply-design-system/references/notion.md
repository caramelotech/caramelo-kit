# Notion

## Visão geral

O Notion parece uma mesa bem organizada sob boa luz natural. A superfície dominante não é branco puro, e sim um off-white quente, com aspecto de papel - `{colors.canvas-soft}` (#f6f5f4) -, que tira o tom clínico da tela e faz páginas longas parecerem um documento, não um aplicativo. O texto é composto em `NotionInter` (uma variação ajustada da Inter) em um preto quase puro `{colors.ink}`, com pesos grandes e tracking bem apertado, de forma que os títulos leem como afirmações confiantes, com pouquíssima folga no espaçamento entre letras nos tamanhos de destaque (`{typography.display-1}` aplica −2,125px de tracking a 64px). Todo o sistema fala baixo em cinzas e pretos, e então diz exatamente uma coisa em cor: um único azul confiável, `{colors.primary}` (#0075de), reservado quase inteiramente para o call-to-action principal e para links em texto.

Contra esse fundo discreto, o Notion deixa uma **paleta lúdica multicolor de "stickers"** carregar toda a personalidade da marca - roxo, rosa, laranja, azul-petróleo, verde e azul-céu aparecem como pequenos blocos ilustrados, stickers de ícones de app e pontos de categoria espalhados pelas páginas de marketing. Essas cores nunca estruturam o layout nem pintam um CTA; elas decoram. A disciplina é deliberada: a interface permanece monocromática-mais-azul para que o conteúdo (e as ilustrações alegres) possam respirar. A única exceção a essa "luz do dia" é o hero da home, que se inverte numa faixa "noturna" em índigo profundo (`{colors.secondary}`) com texto branco e constelações de stickers brilhando - uma única ilha escura em um documento, do resto, claro.

As superfícies são definidas por linhas finas (hairlines) e sombras sutilíssimas em camadas, em vez de elevação pesada. Os cards arredondam em um amigável 12px (`{rounded.lg}`), os CTAs de marketing são totalmente em formato de pílula (`{rounded.full}`), e os botões utilitários arredondam em um 8px mais discreto (`{rounded.md}`). Nada é gritante; o caráter da marca vem da contenção somada a um único respingo bem colocado de alegria.

**Características-chave:**
- Canvas quente, com aspecto de papel `{colors.canvas-soft}`, sobre o branco puro - nunca clínico
- Texto quase-preto `{colors.ink}` em `NotionInter`, com tracking negativo apertado nos tamanhos de destaque (`{typography.display-1}`)
- Exatamente um acento estrutural - o azul do Notion `{colors.primary}` - reservado para CTAs e links
- Uma paleta multicolor de stickers, puramente decorativa (`{colors.accent-purple}`, `{colors.accent-pink}`, `{colors.accent-orange}`, `{colors.accent-teal}`, `{colors.accent-green}`, `{colors.accent-sky}`), que adiciona personalidade sem jamais pintar estrutura
- CTAs de marketing em formato de pílula (`{rounded.full}`) em contraste com botões utilitários de 8px (`{rounded.md}`)
- Elevação por hairline + sombra em camadas quase imperceptível, não por drop-shadows pesados
- Uma única faixa escura "noturna" em índigo (`{colors.secondary}`) que inverte o ritmo diurno do restante da página

## Cores

> Páginas de origem analisadas: a home do Notion, além de Pricing, Enterprise, Product (AI), Product (Agents) e Startups. Toda página secundária resolveu para a mesma paleta central - o Notion roda um único sistema, bem delimitado, em todo o site de marketing.

### Marca e acento
- **Azul Notion** (`{colors.primary}` - #0075de): o único acento estrutural. Preenchimento do CTA principal ("Get Notion free"), cor de link em texto, sinal de aba ativa e de foco. É a única cor que pinta uma ação.
- **Azul Pressionado** (`{colors.primary-active}` - #005bab): o estado de pressionado (mais escuro) do CTA principal.
- **Índigo Profundo** (`{colors.secondary}` - #213183): o fundo da faixa "noturna" do hero e seu campo de constelação de stickers; um azul-marca profundo usado em seções invertidas de ponta a ponta.

As demais cores formam a **paleta decorativa de stickers** do Notion - aparecem só como blocos ilustrados, stickers de app e pontos de categoria, nunca como CTAs ou preenchimentos estruturais:
- **Sticker Céu** (`{colors.accent-sky}` - #62aef0)
- **Sticker Roxo** (`{colors.accent-purple}` - #d6b6f6) / **Roxo Profundo** (`{colors.accent-purple-deep}` - #391c57)
- **Sticker Rosa** (`{colors.accent-pink}` - #ff64c8)
- **Sticker Laranja** (`{colors.accent-orange}` - #dd5b00) / **Laranja Profundo** (`{colors.accent-orange-deep}` - #793400)
- **Sticker Petróleo** (`{colors.accent-teal}` - #2a9d99)
- **Sticker Verde** (`{colors.accent-green}` - #1aae39)
- **Sticker Marrom** (`{colors.accent-brown}` - #523410)

### Superfície
- **Branco** (`{colors.canvas}` / `{colors.surface}` - #ffffff): superfícies de card e painel, barra de navegação, campos de formulário.
- **Papel Quente** (`{colors.canvas-soft}` - #f6f5f4): o canvas de página característico e a faixa do rodapé - um off-white quente que dá a todo o site sua calma de documento.
- **Hairline** (`{colors.hairline}` - #e6e6e6): bordas de card e divisores de 1px, uma mistura de preto a 10% sobre branco mantida sólida para reuso do token.

### Texto
- **Tinta** (`{colors.ink}` - #000000): títulos e texto de corpo principais (renderizado a ~95% de opacidade, para um preto verdadeiro mais suave).
- **Carvão Quente** (`{colors.ink-secondary}` - #31302e): texto de corpo secundário e texto do rodapé.
- **Pedra** (`{colors.ink-muted}` - #615d59): texto de apoio / atenuado.
- **Cinza-claro** (`{colors.ink-faint}` - #a39e98): legendas, metadados, texto de placeholder.

### Semântica
As superfícies de marketing do Notion não expõem uma paleta dedicada de erro/sucesso no chrome do sistema - o status é carregado pela paleta de stickers (ex.: `{colors.accent-green}` para marcações afirmativas), em vez de uma rampa semântica separada.

## Tipografia

### Família da fonte
Todo o sistema é composto em **`NotionInter`** - o corte ajustado da Inter feito pelo Notion -, com uma pilha de fallback `Inter, -apple-system, system-ui, "Segoe UI", Helvetica, Arial`. Uma única família carrega tudo, de títulos de destaque de 64px a eyebrows de 12px; não há serifada, nem fonte monoespaçada de destaque. Os recursos OpenType `lnum` (numerais alinhados) e `locl` estão habilitados nos papéis de corpo e título.

### Hierarquia

| Token | Tamanho | Peso | Altura da linha | Espaçamento entre letras | Uso |
|---|---|---|---|---|---|
| `{typography.display-1}` | 64px | 700 | 1,0 | −2,125px | Título do hero ("Meet the night shift") |
| `{typography.display-2}` | 54px | 700 | 1,04 | −1,875px | Títulos grandes de seção |
| `{typography.heading-1}` | 40px | 700 | 1,1 | −1px | Títulos de seção ("Plans and features") |
| `{typography.heading-2}` | 26px | 700 | 1,23 | −0,625px | Títulos de subseção |
| `{typography.heading-3}` | 22px | 700 | 1,27 | −0,25px | Títulos de card |
| `{typography.title}` | 20px | 600 | 1,4 | −0,125px | Títulos de funcionalidade, callouts |
| `{typography.body-md}` | 16px | 400 | 1,5 | 0 | Texto de corpo padrão |
| `{typography.body-sm}` | 15px | 400 | 1,33 | 0 | Corpo denso, linhas de tabela, navegação |
| `{typography.button}` | 16px | 500 | 1,5 | 0 | Rótulos de botão |
| `{typography.caption}` | 14px | 400 | 1,43 | 0 | Legendas, notas de rodapé |
| `{typography.eyebrow}` | 12px | 600 | 1,33 | +0,125px | Pílulas de destaque, rótulos pequenos |

### Princípios
A voz tipográfica do Notion é **apertada, pesada e discretamente confiante**. Os títulos se apoiam no peso 700 e em tracking negativo agressivo (mais negativo quanto maior o tamanho), de forma que o texto de destaque pareça ajustado, não esticado. O texto de corpo mantém uma altura de linha confortável de 1,5, para leitura de documento. O contraste entre um título pesado em 700 e um corpo calmo em 400 é a principal alavanca expressiva - não há tipografia decorativa, só uma hierarquia clara.

### Nota sobre fontes substitutas
`NotionInter` é um ajuste proprietário da família open-source **Inter** - substitua diretamente por Inter. Para aproximar a tensão de destaque do Notion, aplique explicitamente os valores de espaçamento negativo entre letras da tabela acima (a Inter no tracking padrão vai ler mais soltar do que `NotionInter`).

## Layout

### Sistema de espaçamento
- **Unidade base**: 8px.
- **Tokens (front matter)**: `{spacing.xxs}` 4px · `{spacing.xs}` 8px · `{spacing.sm}` 12px · `{spacing.md}` 16px · `{spacing.lg}` 24px · `{spacing.xl}` 28px · `{spacing.xxl}` 32px.
- O padding interno de card fica em torno de `{spacing.lg}` (24px); botões utilitários usam um 4px/14px apertado; campos de formulário usam um padding na escala de `{spacing.xxs}`, de 6px. Os espaçamentos entre seções empilham os passos maiores.

### Grid e container
O conteúdo é centralizado em uma coluna larga de max-width (~1080-1300px no desktop, conforme os breakpoints extraídos), com gutters externos generosos. As seções de funcionalidades alternam entre blocos de texto de largura total e grids de cards 2-up / 3-up; a página de preços amplia para uma tabela de planos de 4 colunas. O hero escuro ocupa a largura total de ponta a ponta, enquanto as seções de corpo respeitam o container centralizado.

### Filosofia de espaço em branco
O espaço em branco é o principal recurso de agrupamento. As seções são separadas por grandes espaços verticais, em vez de linhas, e os cards ficam sobre o canvas quente com hairlines discretas em vez de molduras pesadas. O efeito é parecido com um documento: arejado, fácil de escanear e nunca apertado.

### Estratégia responsiva

#### Breakpoints
| Nome | Largura | Principais mudanças |
|---|---|---|
| Wide | 1440px+ | Grids multi-coluna completos, container mais largo |
| Desktop | 1080-1300px | Container centralizado padrão, grids de card 3-up |
| Tablet | 768-840px | Grids colapsam para 2-up, navegação começa a condensar |
| Mobile | ≤600px | Pilhas de coluna única, navegação em menu hambúrguer, CTAs de largura total |

#### Áreas de toque
CTAs em pílula (`button-primary`, `button-secondary`) e botões utilitários (`button-utility`) carregam padding de toque confortável; buscar uma área mínima de toque de 44×44px no mobile, preservando o padding vertical mesmo quando os rótulos encolhem.

#### Estratégia de colapso
A navegação superior condensa para um menu hambúrguer abaixo do breakpoint de tablet; grids de card multi-coluna colapsam para uma única coluna empilhada; a tabela de planos de preços reflui de 4 colunas lado a lado para cards de plano empilhados. O padding de seção se reduz, mas o ritmo do canvas quente é preservado.

#### Comportamento de imagem
Screenshots de produto e blocos de ilustração ficam dentro de molduras arredondadas `{rounded.lg}` e escalam fluidamente dentro de sua célula de grid. As ilustrações de sticker são assets decorativos pequenos, de escala fixa, que refluem mas não são cortados.

## Elevação e profundidade

| Nível | Tratamento | Uso |
|---|---|---|
| 0 - Plano | Borda hairline `{colors.hairline}`, sem sombra | Cards padrão sobre o canvas quente |
| 1 - Suave | Micro-sombra em camadas: `rgba(0,0,0,0.01) 0 0.175px 1.041px`, `0.02 0 0.8px 2.925px`, `0.027 0 2.025px 7.847px`, `0.04 0 4px 18px` | Cards de funcionalidade elevados, botões flutuantes |
| 2 - Elevado | Pilha mais profunda, de 5 camadas, terminando em `rgba(0,0,0,0.05) 0 23px 52px` | Modais, popovers, a pílula branca elevada sobre o hero escuro |

A filosofia de elevação do Notion é **quase imperceptível**: as sombras são construídas a partir de muitas camadas quase transparentes, de forma que as superfícies pareçam suavemente levantadas do papel, em vez de dramaticamente projetadas. A maioria dos cards depende só de um hairline.

### Profundidade decorativa
O verdadeiro sinal de profundidade da marca é a **ilustração**, não a sombra. O hero escuro em índigo (`{colors.secondary}`) usa stickers brilhantes e um campo de estrelas para criar a sensação de uma cena noturna iluminada, e as seções de funcionalidades sobrepõem pequenos stickers coloridos de ícone de app sobre superfícies simples, para adicionar dimensionalidade lúdica. Blocos ilustrados coloridos (cabeçalhos roxo, rosa, laranja, petróleo em cards que, do resto, são brancos) dão ritmo visual.

## Formas

### Escala de raio de borda

| Token | Valor | Uso |
|---|---|---|
| `{rounded.xs}` | 4px | Campos de formulário, tags pequenas, chips em texto |
| `{rounded.sm}` | 5px | Itens de menu, linhas de lista, pílulas de status |
| `{rounded.md}` | 8px | Botões utilitários / de navegação, cards menores |
| `{rounded.lg}` | 12px | Cards de funcionalidade, molduras de ilustração, blocos de conteúdo |
| `{rounded.xl}` | 16px | Containers grandes, poços de imagem |
| `{rounded.full}` | 9999px | CTAs em pílula de marketing, badges, botões de ícone circulares |

### Geometria fotográfica
Screenshots de produto são emoldurados em poços arredondados `{rounded.lg}` / `{rounded.xl}`, normalmente de ponta a ponta dentro do seu container, com uma borda hairline. Blocos de ilustração usam faixas de cabeçalho coloridas sobre corpos de card brancos. Avatares e stickers de ícone de app são pequenos, às vezes totalmente circulares (`{rounded.full}`). Não há corte pesado de direção de arte - as imagens escalam dentro de sua moldura arredondada.

## Componentes

> **Nenhum estado de hover documentado.** Cada especificação abaixo documenta apenas os estados Padrão e Ativo/Pressionado. As variantes vivem como entradas separadas de `components:` no front-matter e são descritas em seus próprios sub-blocos.

### Navegação

**`nav-bar`** - Navegação superior
- Superfície branca `{colors.canvas}`, texto de link `{colors.ink}` em `{typography.body-sm}`, padding `{spacing.md}`. Fica como uma barra fina e fixa (sticky); wordmark à esquerda, links de menu de produto/soluções ao centro, link em texto "Log in" à direita mais um CTA `button-utility` "Get Notion free". Condensa para um menu hambúrguer abaixo do breakpoint de tablet.

### Botões

**`button-primary`** - CTA principal ("Get Notion free")
- Fundo `{colors.primary}`, texto `{colors.on-primary}`, tipografia `{typography.button}`, totalmente em formato de pílula `{rounded.full}`. A única ação azul em qualquer página.
- O estado pressionado vive em `button-primary-pressed` (fundo `{colors.primary-active}`); botões de marketing também aplicam uma transformação breve de `scale(0.9)` ao pressionar.

**`button-primary-pressed`**
- Fundo `{colors.primary-active}`, texto `{colors.on-primary}` - o estado pressionado do CTA principal.

**`button-secondary`** - CTA secundário ("Request a demo")
- Superfície branca `{colors.surface}`, texto `{colors.ink}`, tipografia `{typography.button}`, pílula `{rounded.full}`, carregando a sombra suave de Nível 1. Fica ao lado do `button-primary` no hero.

**`button-utility`** - Botão de navegação / seleção de plano
- Superfície branca `{colors.surface}`, texto `{colors.ink}`, tipografia `{typography.button}`, `{rounded.md}` mais apertado (8px), padding `4px 14px`, borda `{colors.hairline}` de 1px. Usado no CTA da navegação e nos botões de seleção de plano de preços, onde a pílula de marketing seria grande demais.

**`button-icon-circular`** - Controle de carrossel / mídia
- Controle circular `{rounded.full}` com preenchimento translúcido `rgba(0,0,0,0.05)` e glifo `{colors.on-primary}`, usado em controles de slide e play/pause; aplica uma transformação de `scale(0.9)` ao pressionar.

### Cards e containers

**`feature-card`** - Card de conteúdo / funcionalidade
- Superfície branca `{colors.surface}`, texto `{colors.ink}`, `{typography.body-md}`, arredondado `{rounded.lg}` (12px), padding `{spacing.lg}` (24px). O card de marketing mais usado; frequentemente encimado por uma faixa de ilustração colorida da paleta de stickers. A elevação padrão é plana (só hairline).

**`feature-card-elevated`** - Card de funcionalidade elevado
- Mesmo chrome do `feature-card`, com a sombra suave em camadas de Nível 1, para cards que flutuam sobre o canvas (depoimentos, painéis de produto flutuantes).

**`pricing-plan-card`** - Coluna de plano de preços
- Superfície branca `{colors.surface}`, texto `{colors.ink}`, `{typography.body-sm}`, arredondado `{rounded.md}` (8px), padding `{spacing.lg}`. Uma coluna com borda listando o preço e o checklist de funcionalidades de um plano, com uma ação de seleção `button-utility`.

**`pricing-plan-card-featured`** - Coluna de plano em destaque
- Preenchimento quente `{colors.canvas-soft}` para levantar o tier recomendado em relação aos irmãos brancos, mesma forma `{rounded.md}` e padding. Se distingue pelo tom de superfície, não por uma borda colorida.

### Inputs e formulários

**`text-input`** - Campo de texto / número
- Superfície branca `{colors.surface}`, texto `{colors.ink}`, `{typography.body-sm}`, borda `rgb(221,221,221)` de 1px, arredondado `{rounded.xs}` (4px), padding `6px`. Cantos deliberadamente mais quadrados e mais apertados que os CTAs em pílula. O foco adiciona a sombra suave de Nível 1.

### Componentes de assinatura

**`hero-band`** - Hero escuro "noturno"
- Faixa de ponta a ponta em índigo profundo `{colors.secondary}`, carregando o título branco `{typography.display-1}`, um campo de constelação de stickers, e um par de CTAs `button-primary` + `button-secondary`. A única ilha escura invertida em uma página, do resto, diurna.

**`badge-pill`** - Pílula de destaque / categoria
- Superfície branca `{colors.surface}`, texto `{colors.primary}`, `{typography.eyebrow}` (12px / 600), pílula completa `{rounded.full}`, padding `4px 8px`. Rótulos pequenos, como o eyebrow "Essential for staying organized" da página de preços e tags de categoria.

**`footer`** - Rodapé do site
- Faixa quente `{colors.canvas-soft}`, texto de link `{colors.ink-secondary}` em `{typography.caption}`, padding `{spacing.xxl}`. Diretório de links multi-coluna que encerra toda página.

### Exemplos (ilustrativos)

> Superfícies de demonstração que espelham o kit. Cada entrada `ex-*` referencia primitivas nativas da marca, para que consumidores downstream (`/preview-design`, `/generate-kit`) revistam as mesmas 10 superfícies de forma consistente.

**`ex-pricing-tier`** - Card de tier de preços padrão. Reusa o chrome do feature-card com a superfície canvas-soft da marca.
- Propriedades: `backgroundColor`, `textColor`, `borderColor`, `rounded`, `padding`

**`ex-pricing-tier-featured`** - Tier em destaque/featured - superfície com polaridade invertida (preenchimento escuro + texto claro no modo claro, preenchimento claro + texto escuro no modo escuro).
- Propriedades: `backgroundColor`, `textColor`, `rounded`, `padding`

**`ex-product-selector`** - Card de resumo "O que está incluído" - reaproveitado para verticais SaaS / B2B (NÃO é uma galeria de produto literal).
- Propriedades: `backgroundColor`, `rounded`, `padding`

**`ex-cart-drawer`** - Resumo de assinatura - reaproveitado para SaaS / B2B (itens de linha por add-on, não um carrinho literal).
- Propriedades: `backgroundColor`, `rounded`, `padding`, `item-divider`

**`ex-app-shell-row`** - Linha de navegação lateral dentro do exemplo de App Shell. O estado ativo usa o primary da marca como indicador.
- Propriedades: `backgroundColor`, `activeIndicator`, `rounded`, `padding`

**`ex-data-table-cell`** - Chrome padrão de th + td de tabela de dados. O cabeçalho usa tipografia eyebrow em caixa alta mono; o corpo usa body-sm.
- Propriedades: `headerBackground`, `headerTypography`, `bodyTypography`, `cellPadding`, `rowBorder`

**`ex-auth-form-card`** - Card de login / cadastro. Reusa o chrome do feature-card com primitivas de text-input por dentro.
- Propriedades: `backgroundColor`, `rounded`, `padding`

**`ex-modal-card`** - Superfície de diálogo modal - mesmo chrome do feature-card, com sombra elevada.
- Propriedades: `backgroundColor`, `rounded`, `padding`

**`ex-empty-state-card`** - Moldura de ilustração de estado vazio.
- Propriedades: `backgroundColor`, `rounded`, `padding`, `captionTypography`

**`ex-toast`** - Superfície de notificação toast - forma do feature-card + sombra média.
- Propriedades: `backgroundColor`, `rounded`, `padding`, `typography`

## O que fazer e o que não fazer

### Faça
- Reserve `{colors.primary}` para a ação principal, links em texto e o sinal de ativo/foco - nada decorativo.
- Mantenha a página sobre o canvas quente `{colors.canvas-soft}`; use branco puro `{colors.surface}` para cards e campos, criando um figura/fundo suave.
- Deixe a paleta de stickers (`{colors.accent-pink}`, `{colors.accent-teal}`, `{colors.accent-orange}`, ...) viver só em ilustrações, blocos de ícone e pontos de categoria.
- Componha títulos em `{typography.display-1}`/`{typography.heading-1}` pesados, aplicando explicitamente o tracking negativo.
- Use pílula `{rounded.full}` para CTAs de marketing e `{rounded.md}` mais apertado para botões de navegação/utilitários - o contraste é intencional.
- Defina superfícies com `{colors.hairline}` e a sombra quase imperceptível de Nível 1, em vez de drop-shadows pesados.
- Reserve o tratamento "noturno" em índigo profundo `{colors.secondary}` para um único momento de hero, não para faixas repetidas.

### Não faça
- Não pinte um CTA ou preenchimento estrutural em nenhuma cor da paleta de stickers - essas são só decoração.
- Não introduza um segundo acento estrutural ao lado de `{colors.primary}`.
- Não coloque raios em pílula `{rounded.full}` em campos de formulário - inputs ficam apertados em `{rounded.xs}` (4px).
- Não solte sombras pesadas; a elevação do Notion é feita de muitas camadas quase transparentes, nunca uma projeção dura.
- Não componha o texto de corpo em um peso pesado - mantenha 400 para legibilidade e deixe o peso 700 só para títulos.
- Não coloque texto sobre branco puro e clínico em páginas inteiras; o `{colors.canvas-soft}` quente é parte central da calma da marca.
