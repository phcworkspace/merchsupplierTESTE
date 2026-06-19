# Swatches de Cor na Página de Produto — 2026-06-19

## Objetivo

Exibir as opções de cor da página de produto como **swatches de imagem/cor limpos** (igual à referência do cliente), em vez de botões de texto. Caso de teste: **Yupoong - Wool Blend Classic Snapback** (`gid://shopify/Product/9463768744194`), com as cores `Black/Camo` e `Preto`.

## Diagnóstico (causa raiz)

O tema **já suportava** swatches por imagem (commits `fdc3206` e `8faf88d`). O produto continuava mostrando botões por **dois** motivos combinados:

1. **Config do bloco**: o variant-picker em `templates/product.json` estava com `"show_swatches": false`.
2. **Dados do produto**: as variantes não tinham swatch nativo nem imagem de variante. (Depois o cliente atribuiu mockups como imagem de variante e configuraria os swatches nativos.)

Detalhe de renderização descoberto em `snippets/swatch.liquid` (linha 16): quando `settings.show_variant_image` está ligado e a variante tem `featured_media`, o tema usa **a imagem da variante como swatch** — o que faria o swatch mostrar o **mockup do boné inteiro encolhido**, e não um swatch de cor limpo.

## O que foi feito

- **`templates/product.json`** → `show_swatches: false` → `true` no bloco `variant_picker_R3rGDr`.
- **`snippets/variant-main-picker.liquid`** → prioridade do swatch nativo sobre a imagem de variante: quando a option value tem `swatch.color` ou `swatch.image`, zera o `featured_media` passado ao snippet `swatch`, garantindo o swatch limpo. Produtos que só têm imagem de variante (sem swatch nativo) continuam funcionando como antes.

## Arquivos Modificados

| Arquivo | Ação |
|---|---|
| `templates/product.json` | `show_swatches` → `true` |
| `snippets/variant-main-picker.liquid` | Swatch nativo tem prioridade sobre imagem de variante |

> Edições feitas nos **arquivos locais do tema** (repositório). Aplicar na loja via `shopify theme push` para o tema de desenvolvimento e, após validar, para o MAIN.

## Decisões Tomadas

- **Swatch nativo, não imagem de variante** (apesar de a imagem de variante ter sido a 1ª escolha): a referência do cliente mostra swatches limpos (textura camuflada + preto sólido). O arquivo `Desing Source/colores/Black-Camo.jpg` é uma textura de swatch limpa, confirmando a intenção.
- **Manter mockups como imagem de variante**: assim a foto principal da galeria troca conforme a cor selecionada, enquanto o swatch usa a cor/textura limpa.
- **Ajuste no tema em vez de desligar `show_variant_image` global**: o tweak no `variant-main-picker.liquid` resolve só onde há swatch nativo, sem efeito colateral em outros produtos.
- **Configuração dos swatches feita pelo cliente no admin** (a pedido do cliente).

## Configuração dos Swatches no Admin (passo do cliente)

1. Abrir o produto → seção **Variants** → clicar na opção **Color**.
2. Para **Preto** → swatch tipo **Color** → preto (`#000000`).
3. Para **Black/Camo** → swatch tipo **Image** → upload de `Desing Source/colores/Black-Camo.jpg`.
4. **Save**.

Após salvar, `optionValues[].swatch` deixa de ser `null` e o tema renderiza os swatches limpos automaticamente.

## Como Pré-visualizar

```bash
shopify theme dev --store lojateste-20221163.myshopify.com --store-password <senha-da-vitrine>
```

Abrir a página do Yupoong Snapback → as cores aparecem como swatches (camuflado + preto), e a foto principal troca ao selecionar cada cor.

## Pontos de Atenção Futura

- ⚠️ Padronizar o idioma dos nomes de cor: hoje estão misturados (`Preto` em PT, `Black/Camo` em EN).
- ⚠️ Replicar o swatch nativo para os demais produtos/cores conforme o catálogo crescer.
- ⚠️ Validar o comportamento também nos **cards de coleção** (`snippets/variant-swatches.liquid` / `blocks/swatches.liquid`) — o ajuste atual foi no picker da página de produto.
- ⚠️ Após validar no tema dev, fazer `theme push` no tema MAIN (#161734689026).
