# Storybook — Catálogo de Componentes

> Atualizar após cada implementação que crie ou modifique componentes Liquid.

## Seções (Sections)

### `about-brand`

**Arquivo:** `sections/about-brand.liquid`  
**Descrição:** Seção de apresentação da marca para a homepage. Layout responsivo — coluna única em mobile, grid 1fr/1fr com imagem em desktop (quando imagem configurada).

**Variantes:**
- Sem imagem: bloco de texto centralizado com heading, richtext e botão opcional
- Com imagem: grid lado a lado (imagem à esquerda, texto à direita)

**Schema — Settings:**

| ID | Tipo | Default | Descrição |
|---|---|---|---|
| `image` | image_picker | — | Imagem lateral (opcional) |
| `heading` | text | "About Our Brand" | Título da seção |
| `heading_size` | select | h2 | Tamanho do título (h1–h4) |
| `text` | richtext | — | Texto descritivo da marca |
| `button_label` | text | — | Label do CTA (opcional) |
| `button_link` | url | — | Destino do CTA |
| `background_color` | color | transparent | Cor de fundo |
| `padding_top` | range 0–100px | 60px | Espaçamento superior |
| `padding_bottom` | range 0–100px | 60px | Espaçamento inferior |

**Preset:** "About the Brand" (disponível no tema editor → Add section)

## Snippets

### `variant-main-picker` (customizado)

**Arquivo:** `snippets/variant-main-picker.liquid` (base Horizon, modificado)
**Descrição:** Renderiza o seletor de variantes na página de produto. Modos: `buttons`, `dropdowns`, `swatch`, `swatch_dropdown`.

**Customização (2026-06-19):** quando a option value tem **swatch nativo** (`swatch.color` ou `swatch.image`), o swatch nativo tem prioridade sobre a imagem de variante (`featured_media`) na renderização do quadradinho — exibindo um swatch de cor/textura limpo em vez do mockup do produto encolhido. Produtos sem swatch nativo continuam usando a imagem de variante como swatch.

**Depende de:**
- Bloco variant-picker com `show_swatches: true`
- Swatch nativo configurado na option value, OU imagem de variante + `settings.show_variant_image`
- Snippet `swatch.liquid` (renderização do quadradinho)

Ver: [Swatches de Cor na Página de Produto](./variant-color-swatches-2026-06-19.md)

### `custom-fonts` (criado)

**Arquivo:** `snippets/custom-fonts.liquid`
**Descrição:** Declara os `@font-face` da fonte de marca **GT Alpina (Standard)** a partir dos `.woff2` em `assets/` e sobrescreve `--font-body--family` e `--font-heading--family`. Renderizado em `layout/theme.liquid` após `theme-styles-variables`.

**Cortes incluídos:** Regular (400), Medium (500), Bold (700) + itálicos — todos `woff2`, `font-display: swap`.

> ⚠️ Arquivos atuais são **Trial** (uso só em teste). Produção exige licença Webfont da Grilli Type.

Ver: [Importação da Fonte Custom GT Alpina](./import-fonte-gt-alpina-2026-06-19.md)

## Blocos (Blocks)

_Nenhum bloco customizado ainda._
