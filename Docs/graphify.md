# Graphify — Arquitetura do Projeto

> Atualizar após cada implementação que adicione, remova ou altere componentes, integrações ou fluxos.

## Arquitetura Atual

```mermaid
graph TD
    subgraph Shopify
        A[Tema Horizon - OS 2.0] --> B[Página de Produto]
        A --> C[Coleções]
        A --> D[Homepage]
        D --> S1[hero - banner vídeo]
        D --> S2[product-list - carrossel]
        D --> S3[about-brand - seção marca ✅]
        E[(Produtos - 8 DRAFTs)]
        C --> E
        B --> E
    end

    subgraph Apps
        E[Inkybay - Product Customizer]
    end

    subgraph Marketing
        F[Google Ads]
        G[GA4]
        H[TikTok Shop]
        I[Instagram Shop]
    end

    B --> E
    Shopify --> F
    Shopify --> G
    Shopify --> H
    Shopify --> I
```

_Última atualização: 2026-06-18 — seção about-brand criada no tema de desenvolvimento_
