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

- **Tema base:** Horizon (ID #161734689026) — tema flagship atual da Shopify com arquitetura de Theme Blocks
- **Arquitetura:** Online Store 2.0 + Theme Blocks (diretório `blocks/` nativo — diferente do Dawn)
- **Liquid:** usar `render` em vez de `include`; nunca editar o tema publicado diretamente
- **Workflow:** `theme pull → dev em tema separado → theme push → validar → publicar`
- **Inkybay:** configurações via painel do app; CSS customizado via campo Extended CSS (não editar Liquid do app)
- **MCP conectado:** `@shopify/dev-mcp` para docs + Admin API MCP para gestão da loja via Claude
- **CLI:** Shopify CLI 4.2.0 — auth é account-level (`shopify auth login` sem `--store`); linter via `shopify theme check`

### Diferenças Horizon vs Dawn (importante)

| Aspecto | Dawn | Horizon |
|---|---|---|
| Diretório `blocks/` | ❌ não existe | ✅ nativo |
| Composição de seções | sections + snippets | sections + blocks + snippets |
| Flexibilidade do lojista | limitada | alta (drag-and-drop de blocks) |
| Padrão de schema | `settings` em sections | `settings` em sections + schema próprio em blocks |

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
├── assets/                ← CSS, JS, imagens do tema
├── blocks/                ← Theme Blocks (exclusivo Horizon)
├── config/                ← settings_schema.json, settings_data.json
├── layout/                ← theme.liquid, password.liquid
├── locales/               ← traduções
├── sections/              ← sections Liquid
├── snippets/              ← snippets reutilizáveis
└── templates/             ← templates JSON e Liquid
```
