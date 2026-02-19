# Bun Monorepo Template

Bun × TypeScript × React monorepo template with Coding Agent native architecture.

## Tech Stack

- **Runtime / Package Manager**: Bun 1.3.9 (managed via mise)
- **Language**: TypeScript 5.9 (`@tsconfig/strictest`, `erasableSyntaxOnly`)
- **Type Checker**: `tsgo` (TypeScript native preview) for per-package type checking
- **Linter**: oxlint (with `typescript` and `import` plugins, type-aware mode)
- **Formatter**: oxfmt (printWidth: 100, 2 spaces, no tabs)
- **Auth**: Better Auth — reference: https://better-auth.com/llms.txt

## Monorepo Structure

```
apps/
  server/          → @bun-monorepo-template/server (Bun server app)
packages/
  shared/          → @bun-monorepo-template/shared (shared utilities)
```

Workspaces are declared in root `package.json` (`apps/*`, `packages/*`).

## Coding Conventions

- **ESM only**: All packages use `"type": "module"`
- **Subpath imports**: Use `#src/*` for internal imports (e.g., `import { foo } from "#src/utils"`)
- **Package naming**: `@bun-monorepo-template/<name>`
- **Package manager**: Always use `bun` (never npm/yarn/pnpm)
- **No eslint / No prettier**: Use `oxlint` for linting and `oxfmt` for formatting exclusively
- **Strict TypeScript**: Extends `@tsconfig/strictest` with `erasableSyntaxOnly` (no enums, no namespaces)
- **Type checking**: Run `tsgo` per package (via `bun run typecheck`)

## Scripts (root)

| Command | Description |
|---|---|
| `bun run dev:server` | Start server app in watch mode |
| `bun run typecheck` | Run `tsgo` across all packages |
| `bun run lint` | Run oxlint + oxfmt check |
| `bun run format` | Auto-fix oxlint issues + format with oxfmt |

## MCP Servers

Configured in `.mcp.json`:

- **better-auth** — Better Auth documentation & guidance (HTTP)
- **next-devtools** — Next.js dev server tooling
- **playwright** — Browser automation & testing
- **codex** — Codex MCP server

## Agent Tooling

### Skills

Skills are canonically stored in `.agents/skills/` and distributed via symlinks:

- `skills/` → `.agents/skills/*` (for Claude Code)
- `.cursor/skills/` → `.agents/skills/*` (for Cursor)

### Instructions

This file (`.agents/INSTRUCTIONS.md`) is the single source of truth for agent instructions:

- `CLAUDE.md` → `.agents/INSTRUCTIONS.md` (for Claude Code)
- `AGENTS.md` → `.agents/INSTRUCTIONS.md` (for Codex and other agents)
