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
| 7. Autenticação Shopify | ✅ | `shopify auth login` (sem `--store` — auth é account-level no CLI 4.x). Conta ativa: pedrohcosta.work@gmail.com. Nota: `shopify whoami` não existe no CLI 4.x. |
| 8. Pull do tema | ✅ | Tema ativo **'Horizon'** (#161734689026) puxado de `lojateste-20221163.myshopify.com` (`shopify theme pull --live`) para a raiz do projeto |

## Arquivos criados / modificados

- `Docs/README.md` — índice de implementações
- `Docs/graphify.md` — arquitetura visual (Mermaid)
- `Docs/storybook.md` — catálogo de componentes
- `Docs/setup-ambiente-local-2026-06-17.md` — este documento
- `.gitignore` — node_modules, .env, logs, `config/settings_data.json`, etc.
- `C:\Users\pedro\AppData\Roaming\Claude\claude_desktop_config.json` — bloco `mcpServers` adicionado
- **Arquivos do tema Horizon** puxados para a raiz do projeto: `assets/`, `blocks/`, `config/`, `layout/`, `locales/`, `sections/`, `snippets/`, `templates/` (`config/settings_data.json` está no `.gitignore`)

## Decisões tomadas

- **Theme Check via CLI:** como `@shopify/theme-check` foi descontinuado no npm, usamos `shopify theme check` (embutido na CLI 4.2.0). Nenhuma funcionalidade perdida.
- **Branch `main`:** repositório iniciado com `git init -b main` (convenção moderna) em vez do `master` padrão.
- **MCP merge não-destrutivo:** o bloco `mcpServers` foi inserido preservando todas as preferências existentes do Claude Desktop.
- **Token/URL como placeholders:** `SHOPIFY_ACCESS_TOKEN` e `SHOPIFY_STORE_URL` ficaram como `COLE_..._AQUI` — o usuário deve preencher.

## Pontos de atenção futura

- ⚠️ **Reiniciar o Claude Desktop** por completo para carregar os MCP servers.
- ⚠️ **MCP shopify-admin** ainda sem token real — placeholder no `claude_desktop_config.json`. Loja de teste não gerou `shpat_...` via Custom App. Avaliar necessidade após definir loja de produção.
- ⚠️ O `@ajackus/shopify-mcp-server` é um pacote de terceiros — validar manutenção/segurança antes de uso em produção.
- Linha de quebra: arquivos LF serão convertidos para CRLF pelo Git no Windows (avisos esperados, inofensivos).
- **CLI 4.x — diferenças documentadas:** `auth login` não aceita `--store`; `whoami` não existe; autenticação é account-level.
- ⚠️ **Tema base real é Horizon, não Dawn:** o tema publicado na loja de teste é **Horizon** (#161734689026) — tema flagship mais novo da Shopify (OS 2.0, com diretório `blocks/` e arquitetura de theme blocks), enquanto o `CLAUDE.md` cita **Dawn** como ponto de partida. Confirmar qual é a referência oficial do projeto e, se necessário, atualizar o `CLAUDE.md` (seção "Padrões Técnicos").
