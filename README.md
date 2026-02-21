# Claude Code Setup Wizard

One prompt to fully configure Claude Code for any project. Paste it into Claude Code, and it detects your stack, installs all relevant optimizations, and tells you how to use them.

## What It Does

1. **Detects** your language, framework, tooling, and services
2. **Shows a plan** of everything it will install and waits for your OK
3. **Installs** MCP servers, hooks, skills, subagents, CLAUDE.md, and permissions
4. **Outputs a summary** showing exactly how to use each feature

## Quick Start

1. Open Claude Code inside your project:
   ```bash
   cd your-project
   claude
   ```
2. Copy the entire contents of [`SETUP_PROMPT.md`](./SETUP_PROMPT.md) and paste it as your first message
3. Review the installation plan Claude shows you
4. Type `y` to proceed
5. Done — your project is now fully configured

## What Gets Installed

| Category | What | When |
|----------|------|------|
| **MCP Servers** | context7, playwright, github, supabase | Based on your stack |
| **Hooks** | Auto-format on every edit, block writes to `.env` files | Based on your tooling |
| **Skills** | `/code-review`, `/write-tests`, `/security-review` | Always |
| **Subagents** | code-reviewer, test-writer, code-explorer | Based on project size & tooling |
| **CLAUDE.md** | Project instructions with commands, structure, conventions | Always |
| **Permissions** | Auto-allow safe commands, protect secrets | Always |

## Detection Matrix

The wizard reads your project files and maps them to configurations:

| If it finds... | It installs... |
|-----------------|---------------|
| `package.json` with React/Next/Vue | Frontend-aware skills, Playwright MCP |
| `package.json` with Express/Fastify | Backend-aware skills, context7 MCP |
| `.prettierrc` or Prettier in devDeps | Auto-format hook (Prettier) |
| `.eslintrc` or ESLint in devDeps | Auto-lint hook (ESLint) |
| `pyproject.toml` with Ruff | Auto-format hook (Ruff) |
| `pyproject.toml` with Black | Auto-format hook (Black) |
| `pyproject.toml` with pytest | Test-writer skill configured for pytest |
| Jest/Vitest in devDeps | Test-writer skill configured for Jest/Vitest |
| Playwright/Cypress config | Playwright MCP server |
| `.github/` directory | GitHub MCP server |
| `Cargo.toml` | Auto-format hook (cargo fmt) |
| `go.mod` | Auto-format hook (gofmt) |
| `.env` or `.env.example` | File protection hook (blocks writes to .env) |
| Supabase config/deps | Supabase MCP server |
| 200+ files in codebase | Code-explorer subagent |

## Examples

See what the wizard produces for different project types:

- [Node.js / React / TypeScript project](./examples/example-nodejs-output.md)
- [Python / FastAPI project](./examples/example-python-output.md)

## How It Works

The prompt in `SETUP_PROMPT.md` is a structured instruction document that tells Claude Code exactly what to do in 4 phases. It contains detection rules, installation templates, and output formats — so Claude can analyze any repo and configure itself optimally.

All configurations are saved to your project's `.claude/` directory and `.mcp.json`, which you can commit to git to share the setup with your team.

### Files Created

```
your-project/
├── .claude/
│   ├── settings.json          # Hooks and permissions
│   ├── hooks/
│   │   └── protect-env.sh     # File protection script
│   ├── skills/
│   │   ├── code-review/SKILL.md
│   │   ├── write-tests/SKILL.md
│   │   └── security-review/SKILL.md
│   └── agents/
│       ├── code-reviewer.md
│       └── test-writer.md
├── .mcp.json                  # MCP server configs
└── CLAUDE.md                  # Project instructions
```

## Requirements

- [Claude Code](https://claude.ai/code) installed and authenticated
- A project repository to configure

## License

MIT
