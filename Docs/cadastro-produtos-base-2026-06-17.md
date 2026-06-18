# Cadastro de Produtos Base — 2026-06-17

## Objetivo

Cadastrar os produtos base (blanks) do fornecedor MerchSupplier na loja Shopify de teste, com nome, descrição, preço e SKU originais do fornecedor. Produtos cadastrados como DRAFT sem imagens (pendente upload manual dos mockups).

## O que foi feito

- Acessado o site https://www.merchsupplier.com/ e extraídos nome, descrição, preço e SKU de cada produto com match nos mockups locais.
- Cruzamento entre os 13 arquivos PNG da pasta `Desing Source/mockups/` e os produtos listados no MerchSupplier.
- **8 produtos com match** cadastrados na loja `lojateste-20221163.myshopify.com` via Shopify MCP connector.
- **4 produtos sem match** identificados (não encontrados pelo nome na homepage do MerchSupplier — podem estar em outras páginas ou com nomenclatura diferente).

## Produtos Cadastrados

| Produto | Vendor | SKU | Preço (USD) | Shopify ID |
|---|---|---|---|---|
| Yupoong Wool Blend Classic Snapback | YP Classics | 6089M | $9.50 | 9463948017922 |
| Yupoong Five-Panel Flat Bill Cap | YP Classics | 6007 | $8.50 | 9463948050690 |
| Retro Trucker Cap | YP Classics | 6606 | $10.82 | 9463948083458 |
| OTTO Washed Dad Hat | OTTO Cap | 18-772 | $5.95 | 9463948116226 |
| Pom-Pom 12" Knit Beanie | Sportsman | SP15 | $6.50 | 9463948148994 |
| 12 Inch Knit Beanie | Sportsman | SP12T | $5.90 | 9463948181762 |
| Softstyle T-Shirt | Gildan | 64000 | $6.95 | 9463948214530 |
| Heavy Blend Full-Zip Hooded Sweatshirt | Gildan | 18600 | $35.35 | 9463948247298 |

## Mockups Sem Match (pendente investigação)

- `Bucket Cap.png`
- `Heavyweight Long Sleeve T-Shirt.png`
- `Short Sleeve Easy Care Shirt.png`
- `Mockups touca 3.png`

## Arquivos Modificados

Nenhum arquivo local foi modificado — todos os produtos foram criados diretamente via Shopify Admin API (MCP connector).

## Decisões Tomadas

- **Status DRAFT:** produtos cadastrados como rascunho para evitar publicação acidental antes de ter imagens e variantes configuradas.
- **Preços do fornecedor:** foram usados os preços de custo do MerchSupplier — antes de publicar, definir margem e atualizar para preço de venda ao consumidor.
- **Variante única:** por ora cada produto tem uma variante "Default". Para produtos com opções (cor, tamanho), as variantes devem ser adicionadas manualmente no Shopify Admin.
- **Sem imagens:** o MCP Shopify connector exige URLs HTTPS públicas para imagens. Os mockups locais (PNG) não podem ser enviados diretamente. Ver seção "Pontos de Atenção".

## Pontos de Atenção Futura

- ⚠️ **Imagens pendentes:** fazer upload dos mockups PNG via Shopify Admin → cada produto → "Add media". Ou usar a mutation GraphQL `stagedUploadsCreate` para upload via API.
- ⚠️ **Preços de venda:** os preços atuais são custo do fornecedor (wholesale). Definir margem e atualizar antes de publicar.
- ⚠️ **Variantes de cor/tamanho:** adicionar variantes (Size, Color) em cada produto conforme as opções disponíveis no MerchSupplier.
- ⚠️ **4 mockups sem match:** investigar em outras páginas do MerchSupplier (`/create/Hats`, `/create/Apparel`) ou verificar se os nomes diferem.
- ⚠️ **Moeda:** a loja de teste está configurada em BRL. Para a loja de produção nos EUA, a moeda será USD — os preços já estão em USD na origem.
