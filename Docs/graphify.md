# Graphify — Arquitetura do Projeto

> Atualizar após cada implementação que adicione, remova ou altere componentes, integrações ou fluxos.

## Arquitetura Atual

```mermaid
graph TD
    subgraph Shopify
        A[Tema Dawn - OS 2.0] --> B[Página de Produto]
        A --> C[Coleções]
        A --> D[Homepage]
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

_Última atualização: setup inicial_
