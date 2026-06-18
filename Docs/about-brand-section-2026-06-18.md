# Seção About the Brand — 2026-06-18

## Objetivo

Criar uma seção reutilizável "About the Brand" (Sobre a Marca) para ser exibida abaixo do carrossel de produtos na homepage.

## O que foi feito

- Criado `sections/about-brand.liquid` no tema de desenvolvimento (`gid://shopify/OnlineStoreTheme/161751105794`) via `themeFilesUpsert` GraphQL.
- Criado `templates/index.json` no mesmo tema com a seção `about_brand_section` como único bloco da homepage (versão minimal para preview isolado).
- Ambos os arquivos foram upseridos com sucesso via Shopify Admin API MCP.

## Arquivos Modificados

| Arquivo | Tema | Ação |
|---|---|---|
| `sections/about-brand.liquid` | DEVELOPMENT (#161751105794) | Criado |
| `templates/index.json` | DEVELOPMENT (#161751105794) | Criado |

> ⚠️ O tema MAIN (publicado) **não foi alterado**. Todas as mudanças estão no tema de desenvolvimento.

## Estrutura da Seção

A seção `about-brand` suporta:

| Setting | Tipo | Default |
|---|---|---|
| `image` | image_picker | — |
| `heading` | text | "About Our Brand" |
| `heading_size` | select (h1–h4) | h2 |
| `text` | richtext | — |
| `button_label` | text | — |
| `button_link` | url | — |
| `background_color` | color | transparent |
| `padding_top` | range (0–100px) | 60px |
| `padding_bottom` | range (0–100px) | 60px |

Layout responsivo: coluna única em mobile; grid 1fr/1fr com imagem à esquerda quando image != blank (≥750px).

## Decisões Tomadas

- **Tema dev vazio**: o tema de desenvolvimento (#161751105794) não tinha arquivos. Para incluir `hero` e `product-list` no `templates/index.json`, seria necessário copiar todos os arquivos do tema MAIN via `shopify theme pull`. Optou-se por um `index.json` minimalista (só a seção about-brand) para viabilizar o preview isolado.
- **Sem Blocks**: a seção usa `settings` simples, sem Theme Blocks internos — suficiente para conteúdo estático de marca.
- **CSS inline**: estilos escritos no `<style>` do arquivo Liquid (padrão aceitável para seções únicas no Horizon).

## Como Pré-visualizar

1. Shopify Admin → Online Store → Themes
2. Localizar o tema de desenvolvimento → **Customize**
3. A homepage já exibirá a seção "About Our Brand" com o texto padrão
4. Editar heading, texto, imagem e botão pelo editor visual

## Como Aplicar no Tema MAIN (produção)

Opção A — Via CLI (recomendado):
```bash
shopify theme pull --theme 161734689026   # baixa o MAIN
# editar sections/about-brand.liquid localmente
shopify theme push --theme 161751105794   # faz push no dev para teste
# após validar:
shopify theme push --theme 161734689026   # push no MAIN
```

Opção B — Copy/paste no editor de código do Shopify Admin:
- Online Store → Themes → MAIN → Edit code
- Criar `sections/about-brand.liquid` com o conteúdo do arquivo criado
- Editar `templates/index.json` adicionando a seção no array `order`

## Pontos de Atenção Futura

- ⚠️ Integrar a seção ao `templates/index.json` do tema MAIN após fazer pull completo do tema.
- ⚠️ Adicionar imagem da marca (logo ampliado, foto do processo ou produto) no campo `image`.
- ⚠️ Criar a página `/pages/about` no Shopify para o botão "Learn More" ter destino válido.
- ⚠️ Ajustar o texto padrão para refletir a identidade real da marca do cliente.
