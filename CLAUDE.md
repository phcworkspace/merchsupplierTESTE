# E-Commerce EUA — Loja de Bonés e Camisetas (Las Vegas)

## Contexto do Projeto

Duas lojas de vestuário nos EUA, gerenciadas remotamente do Brasil:

- **Loja de Bonés** — customização de bonés bordados via Inkybay. Migração de Deco Network para Shopify.
- **Loja de Camisetas** — novo projeto. Estoque físico em Las Vegas, DTF, banco de artes por nicho, tráfego 100% pago.

**Stack:** Shopify (Liquid, Online Store 2.0) + Inkybay + Shopify CLI + MCP  
**Integrações de marketing:** Google Ads, GA4, Google Shopping, TikTok Shop, Instagram Shop, e-mail marketing

---

## Regras de Desenvolvimento

Estas regras devem ser seguidas **em toda implementação**, sem exceção.

### 1. Graphify (Grafo Visual do Projeto)

- Manter um arquivo `Docs/graphify.md` com o mapa visual atualizado da arquitetura do projeto (tema, seções, apps, integrações, fluxos de dados).
- **Atualizar após cada implementação** que adicione, remova ou altere componentes, integrações ou fluxos.
- Usar formato Mermaid para os diagramas.

### 2. Storybook

- Manter um arquivo `Docs/storybook.md` com o catálogo de componentes e seções do tema (snippets, sections, blocks).
- Para cada componente documentar: nome, descrição, variantes, parâmetros do schema e screenshot/exemplo.
- **Atualizar após cada implementação** que crie ou modifique componentes Liquid.

### 3. Documentação de Implementações

- Ao concluir qualquer implementação, criar um arquivo em `Docs/` com o nome no formato `nome-da-implementacao-YYYY-MM-DD.md`.
- O arquivo deve conter: objetivo, o que foi feito, arquivos modificados, decisões tomadas e pontos de atenção futura.
- Manter um índice atualizado em `Docs/README.md`.

### 4. Sugestão de Commit Git

- Ao final de cada implementação, sugerir uma mensagem de commit em inglês seguindo o padrão Conventional Commits:
  ```
  type(scope): short description
  ```
  Tipos comuns: `feat`, `fix`, `chore`, `refactor`, `docs`, `style`.
  Exemplo: `feat(product-page): add Inkybay customizer button integration`

---

## Padrões Técnicos

- **Tema base:** Dawn (Online Store 2.0) como ponto de partida
- **Liquid:** usar `render` em vez de `include`; nunca editar o tema publicado diretamente
- **Workflow:** `theme pull → dev em tema separado → theme push → validar → publicar`
- **Inkybay:** configurações via painel do app; CSS customizado via campo Extended CSS (não editar Liquid do app)
- **MCP conectado:** `@shopify/dev-mcp` para docs + Admin API MCP para gestão da loja via Claude

---

## Estrutura de Pastas Esperada

```
/
├── CLAUDE.md              ← este arquivo
├── Docs/
│   ├── README.md          ← índice de todas as implementações
│   ├── graphify.md        ← arquitetura visual (Mermaid)
│   ├── storybook.md       ← catálogo de componentes
│   └── *.md               ← docs de implementações (nome-YYYY-MM-DD.md)
└── [arquivos do tema Shopify quando exportados]
```
