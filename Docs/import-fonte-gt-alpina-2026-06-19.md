# Importação da Fonte Custom GT Alpina — 2026-06-19

## Objetivo

Importar a fonte de marca **GT Alpina (Standard)** para o tema Horizon, aplicando-a em **corpo + títulos**. O Horizon usa `font_picker` (apenas fontes da biblioteca Shopify), então fonte própria exige `@font-face` + override das variáveis CSS do tema.

## ⚠️ Licença (ponto crítico)

Os arquivos de origem em `Desing Source/Font/GT-Alpina/` são **versão Trial** da Grilli Type — licenciados **apenas para teste/mockup**. **É proibido usar em loja publicada/comercial.** Para produção, comprar a **licença Webfont** da Grilli Type e substituir os arquivos em `assets/` (mantendo os mesmos nomes).

## O que foi feito

1. **Conversão** dos 6 cortes `.otf` (GT Alpina Standard) → **`.woff2`** via `fontTools` + `brotli`:
   - Regular / Regular Italic (peso 400)
   - Medium / Medium Italic (peso 500)
   - Bold / Bold Italic (peso 700)
2. Arquivos `.woff2` colocados em `assets/` (~12–13 KB cada — a Trial tem charset reduzido).
3. Criado snippet **`snippets/custom-fonts.liquid`** com os `@font-face` e o override:
   ```css
   :root {
     --font-body--family: "GT Alpina", Georgia, "Times New Roman", serif;
     --font-heading--family: "GT Alpina", Georgia, "Times New Roman", serif;
   }
   ```
4. Renderizado em **`layout/theme.liquid`** logo **após** `theme-styles-variables` (para vencer a cascata das variáveis de fonte).

## Arquivos Modificados / Criados

| Arquivo | Ação |
|---|---|
| `assets/gt-alpina-standard-regular.woff2` | Criado |
| `assets/gt-alpina-standard-regular-italic.woff2` | Criado |
| `assets/gt-alpina-standard-medium.woff2` | Criado |
| `assets/gt-alpina-standard-medium-italic.woff2` | Criado |
| `assets/gt-alpina-standard-bold.woff2` | Criado |
| `assets/gt-alpina-standard-bold-italic.woff2` | Criado |
| `snippets/custom-fonts.liquid` | Criado |
| `layout/theme.liquid` | `render 'custom-fonts'` após `theme-styles-variables` |

## Decisões Tomadas

- **WOFF2** em vez de OTF/WOFF: padrão web moderno, ~30% menor, suportado por todos os navegadores atuais. Instalado `brotli` para habilitar a compressão.
- **6 cortes (Standard)**: cobrem corpo (regular/itálico/bold) e títulos sem carregar dezenas de arquivos. As demais subfamílias (Fine, Condensed, Extended, Typewriter) não foram importadas.
- **Override via variável CSS** (`--font-body--family` / `--font-heading--family`) em vez de mexer no `font_picker`: não dá pra subir fonte custom no `font_picker`, e o override é a forma limpa e reversível.
- **`font-display: swap`**: evita texto invisível enquanto a fonte carrega.

## Como Pré-visualizar

`shopify theme dev` → qualquer página. Títulos e corpo devem renderizar em GT Alpina (serifada). Verificar em DevTools: `computed → font-family` deve mostrar "GT Alpina".

## Pontos de Atenção Futura

- ⚠️ **Licença**: trocar os Trial pelos arquivos da licença Webfont antes de publicar.
- ⚠️ **Glyphset reduzido**: a Trial pode não ter todos os acentos (á, ã, ç, õ…). Onde faltar, cai no fallback Georgia. A fonte licenciada completa resolve.
- ⚠️ **Subheading/Accent**: ficaram com a fonte original do tema (escopo foi corpo + títulos). Se quiser unificar, sobrescrever também `--font-subheading--family` e `--font-accent--family` no `custom-fonts.liquid`.
- ⚠️ Avaliar **preload** do corte Regular para reduzir FOUT, se a performance pedir.
- ⚠️ Os `.woff2` são binários novos em `assets/` — entram no commit.
