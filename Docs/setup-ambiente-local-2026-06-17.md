# Setup do Ambiente de Desenvolvimento Local — 2026-06-17

## Objetivo

Configurar o ambiente local de desenvolvimento para o projeto Shopify (tema base Dawn + app Inkybay): ferramentas de CLI, linter Liquid, MCP servers, estrutura de documentação e versionamento Git.

## O que foi feito

| Etapa | Status | Observações |
|-------|--------|-------------|
| 1. Pré-requisitos | ✅ | Node v24.13.0, npm 11.6.2, Git 2.52.0 — todos acima do mínimo |
| 2. Shopify CLI | ✅ | `@shopify/cli@latest` instalado globalmente — **versão 4.2.0** |
| 3. Theme Check | ✅ (adaptado) | Pacote npm `@shopify/theme-check` **não existe mais** (404). O linter agora vem **embutido na CLI**: `shopify theme check` |
| 4. MCP servers | ✅ | `shopify-dev` e `shopify-admin` adicionados ao `claude_desktop_config.json` (merge sem sobrescrever prefs existentes) |
| 5. Estrutura Docs/ | ✅ | `README.md`, `graphify.md`, `storybook.md` criados |
| 6. Git | ✅ | Repo iniciado em `main`, `.gitignore` criado, commit inicial `f7422ea` |
| 7. Autenticação Shopify | ⏳ Pendente (usuário) | `shopify auth login` é interativo (abre browser) |
| 8. Pull do tema | ⏳ Pendente (usuário) | Requer URL da loja + autenticação |

## Arquivos criados / modificados

- `Docs/README.md` — índice de implementações
- `Docs/graphify.md` — arquitetura visual (Mermaid)
- `Docs/storybook.md` — catálogo de componentes
- `Docs/setup-ambiente-local-2026-06-17.md` — este documento
- `.gitignore` — node_modules, .env, logs, `config/settings_data.json`, etc.
- `C:\Users\pedro\AppData\Roaming\Claude\claude_desktop_config.json` — bloco `mcpServers` adicionado

## Decisões tomadas

- **Theme Check via CLI:** como `@shopify/theme-check` foi descontinuado no npm, usamos `shopify theme check` (embutido na CLI 4.2.0). Nenhuma funcionalidade perdida.
- **Branch `main`:** repositório iniciado com `git init -b main` (convenção moderna) em vez do `master` padrão.
- **MCP merge não-destrutivo:** o bloco `mcpServers` foi inserido preservando todas as preferências existentes do Claude Desktop.
- **Token/URL como placeholders:** `SHOPIFY_ACCESS_TOKEN` e `SHOPIFY_STORE_URL` ficaram como `COLE_..._AQUI` — o usuário deve preencher.

## Pontos de atenção futura

- ⚠️ **Reiniciar o Claude Desktop** por completo para carregar os MCP servers.
- ⚠️ **Gerar o Access Token** no painel Shopify e substituir o placeholder no `claude_desktop_config.json` (server `shopify-admin`).
- ⚠️ **Definir a URL da loja** (`SUA_LOJA.myshopify.com`) nos comandos de auth/pull e no config do MCP admin.
- ⚠️ O `@ajackus/shopify-mcp-server` é um pacote de terceiros — validar manutenção/segurança antes de uso em produção.
- Linha de quebra: arquivos LF serão convertidos para CRLF pelo Git no Windows (avisos esperados, inofensivos).
