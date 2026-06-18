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

_Nenhum snippet customizado ainda._

## Blocos (Blocks)

_Nenhum bloco customizado ainda._
