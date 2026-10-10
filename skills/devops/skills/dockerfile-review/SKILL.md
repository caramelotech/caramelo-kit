---
name: dockerfile-review
description: Revisa um Dockerfile em busca de problemas de segurança, otimizações de tamanho de imagem e boas práticas. Use quando for solicitado revisar, auditar ou melhorar um Dockerfile.
---

# Dockerfile Review

Revise o Dockerfile fornecido identificando problemas de segurança, oportunidades de redução de tamanho de imagem e desvios de boas práticas.

## O que avaliar

**Segurança**

- Uso de imagem base com tag fixa (não `:latest`)
- Execução como usuário não-root
- Exposição desnecessária de secrets ou variáveis sensíveis
- Superfície de ataque da imagem base

**Tamanho da imagem**

- Oportunidades de usar multi-stage build
- Layers desnecessários ou que poderiam ser combinados
- Arquivos copiados que não deveriam estar na imagem final

**Boas práticas**

- Ordem das instruções para aproveitar o cache do Docker
- Uso de `.dockerignore`
- `HEALTHCHECK` definido
- Uso correto de `ENTRYPOINT` vs `CMD`

Para cada problema, informe a severidade (`crítico` | `importante` | `sugestão`) e mostre como corrigir.

Ao final, apresente uma versão melhorada do Dockerfile.

## Variáveis

| Variável         | Descrição              | Exemplo                           |
| ---------------- | ---------------------- | --------------------------------- |
| `{{runtime}}`    | Linguagem ou runtime   | `Node.js 20`, `Python 3.12`, `Go` |
| `{{dockerfile}}` | Conteúdo do Dockerfile | _(conteúdo do arquivo)_           |

## Exemplo

**Input:**

```dockerfile
# runtime: Node.js 20

FROM node:latest

WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

EXPOSE 3000
CMD ["node", "dist/index.js"]
```

**Output esperado:**

```
**Segurança**
- [CRÍTICO] Imagem base usa :latest - use node:20-alpine para garantir reprodutibilidade.
- [IMPORTANTE] Aplicação rodando como root. Adicione um usuário não-privilegiado.

**Tamanho da imagem**
- [IMPORTANTE] COPY . . antes do npm install invalida o cache a cada mudança de código.
  Copie package.json e package-lock.json primeiro, instale, depois copie o restante.
- [SUGESTÃO] Use multi-stage build para excluir devDependencies da imagem final.

**Boas práticas**
- [SUGESTÃO] Sem HEALTHCHECK definido.

---

Versão melhorada:

FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build

FROM node:20-alpine
WORKDIR /app
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
USER appuser
EXPOSE 3000
HEALTHCHECK --interval=30s CMD wget -qO- http://localhost:3000/health || exit 1
CMD ["node", "dist/index.js"]
```

## Notas

- Combine com `docker scout` ou `trivy` para análise de CVEs na imagem base
- Para imagens de produção, prefira variantes `-alpine` ou `-slim`
- Sempre teste a imagem revisada localmente antes de subir para produção
