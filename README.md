# Bun Monorepo Template

A Bun × TypeScript × React monorepo template with a Coding Agent native architecture. Provides a cross-agent foundation centered around Claude Code, with support for Codex, Cursor, and other AI coding agents.

## Tech Stack

| Category | Tool |
|---|---|
| Runtime / Package Manager | [Bun](https://bun.sh/) 1.3.9 |
| Version Management | [mise](https://mise.jdx.dev/) |
| Language | TypeScript 5.9 (`@tsconfig/strictest`) |
| Type Checker | [tsgo](https://github.com/nicolo-ribaudo/tsgo) (TypeScript native preview) |
| Linter | [oxlint](https://oxc.rs/docs/guide/usage/linter.html) (type-aware) |
| Formatter | [oxfmt](https://oxc.rs/docs/guide/usage/formatter.html) |
| Auth | [Better Auth](https://better-auth.com/) |

## Project Structure

```
bun-monorepo-template/
├── apps/
│   └── server/              # @bun-monorepo-template/server
├── packages/
│   └── shared/              # @bun-monorepo-template/shared
├── .agents/
│   ├── INSTRUCTIONS.md      # Agent instructions (canonical)
│   └── skills/              # Skill definitions (canonical)
├── skills/                  # → .agents/skills/* (symlink)
├── .cursor/skills/          # → .agents/skills/* (symlink)
├── CLAUDE.md                # → .agents/INSTRUCTIONS.md (symlink)
├── AGENTS.md                # → .agents/INSTRUCTIONS.md (symlink)
├── .mcp.json                # MCP server configuration
└── package.json
```

## Prerequisites

- [mise](https://mise.jdx.dev/) (for Bun version management)
- [Bun](https://bun.sh/) 1.3.9+

## Getting Started

```bash
git clone https://github.com/otofu-square/bun-monorepo-template.git
cd bun-monorepo-template

# Apply Bun version via mise
mise install

# Install dependencies
bun install

# Start the server
bun run dev:server
```

## Scripts

```bash
bun run dev:server   # Start server in watch mode
bun run typecheck    # Type check all packages (tsgo)
bun run lint         # Check with oxlint + oxfmt
bun run format       # Auto-fix oxlint issues + format with oxfmt
```

## AI / Agent Tooling

This repository adopts a **Coding Agent native** architecture.

### Centralized Agent Instructions

`.agents/INSTRUCTIONS.md` serves as the single source of truth. Each agent reads its own file via symlinks:

```
.agents/INSTRUCTIONS.md   ← canonical source
  ├── CLAUDE.md            (symlink for Claude Code)
  └── AGENTS.md            (symlink for Codex / other agents)
```

### Centralized Skills

`.agents/skills/` serves as the canonical source. Skills are distributed to each agent platform via symlinks:

```
.agents/skills/            ← canonical source
  ├── skills/*              (symlinks for Claude Code)
  └── .cursor/skills/*      (symlinks for Cursor)
```

### MCP Servers

The following MCP servers are configured in `.mcp.json`:

| Server | Purpose |
|---|---|
| better-auth | Better Auth documentation & guidance |
| next-devtools | Next.js dev server tooling |
| playwright | Browser automation & testing |
| codex | Codex MCP server |

### Supported Agents

- **Claude Code** — `CLAUDE.md` + `skills/` + `.mcp.json`
- **Codex** — `AGENTS.md` + `.mcp.json` (Codex MCP server)
- **Cursor** — `.cursor/skills/` + `.mcp.json`

## License

[MIT](LICENSE)
