# Claude Code Setup Wizard

One prompt to configure Claude Code for any project with a beginner-safe flow: backup first, global-plugin consent, plugin-powered setup, then a simple workflow handoff.

## What It Does

1. Runs a required local safety checkpoint before changing repo setup files
2. Checks plugins, asks one bulk consent for global installs, and installs missing plugins only
3. Detects your stack with plugin tools + manual repo analysis
4. Installs project automations (MCP, hooks, skills, subagents, permissions) additively
5. Produces a beginner workflow card showing exactly how to use `/commands` and automations

## Quick Start

1. Open Claude Code inside your project:
   ```bash
   cd your-project
   claude
   ```
2. Copy the full contents of [`SETUP_PROMPT.md`](./SETUP_PROMPT.md) and paste as your first message
3. Complete checkpoints when asked:
   - Type `I have a backup`
   - Approve global plugin installs (`yes`/`no`)
   - Type `ready`
   - Approve install plan (`yes`/`no`)
   - Optional setup commit (`yes`/`no`)

You should not need to run setup commands manually in normal flow; the wizard executes setup actions after your confirmations.

## Safety and Scope

- Local file writes are limited to `.claude/`, `.mcp.json`, and `CLAUDE.md`
- Plugin installs are global (all Claude projects), so the wizard asks explicit bulk consent
- Existing setup is preserved: merge/append behavior only
- Missing plugins are added; existing plugins are never removed/disabled

## Plugin-First Behavior

The wizard treats plugins as operational tools, not just install targets:

- Uses automation recommender command alias for detection when available
- Uses CLAUDE.md improver command alias for `CLAUDE.md` generation when available
- Offers commit command alias at the end for clean setup commits
- Resolves command aliases from `/help` so workflow survives command name differences

## What Gets Installed

| Category | What | When |
|---|---|---|
| Plugins (global) | Essential + conditional plugins | Missing-only, after consent |
| MCP servers | `context7` + stack-based servers | Based on detection |
| Hooks | Auto-format/lint and `.env*` write protection | Based on tooling/signals |
| Skills | `/code-review`, `/write-tests`, `/security-review` | Always |
| Subagents | `code-reviewer`, `test-writer`, `code-explorer` | Based on project size/tooling |
| CLAUDE.md | Plugin-generated (fallback manual) + workflow section | Always |
| Permissions | Language-safe command allows + env read denies | Always |

## Beginner Output

Final output includes:

- Technical setup summary
- Resolved command aliases used in your environment
- **Beginner Workflow Card** (daily steps)
- Simple explainer of project automations:
  - Hooks
  - MCP servers
  - Skills/subagents

## Examples

- [Node.js / React / TypeScript example output](./examples/example-nodejs-output.md)
- [Python / FastAPI example output](./examples/example-python-output.md)

## Requirements

- [Claude Code](https://claude.ai/code) installed and authenticated
- A project repository to configure

## License

MIT
