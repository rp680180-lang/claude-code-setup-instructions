# Claude Code Setup Wizard

A prompt-based setup wizard for configuring Claude Code on any project.

## Active Files

| File | Status | Notes |
|---|---|---|
| `SETUP_PROMPT_V4.md` | **Current** | Use this one |
| `SETUP_PROMPT_V3.md` | Previous | Kept for reference |
| `SETUP_PROMPT_V2.md` | Previous | Kept for reference |
| `SETUP_PROMPT.md` | Original V1 | Kept for reference |

## How to Use

Copy the full contents of `SETUP_PROMPT_V4.md` and paste it as the first message in Claude Code inside any target project.

## Project Structure

```
SETUP_PROMPT_V4.md     # Current wizard prompt
SETUP_PROMPT_V3.md     # Previous version
SETUP_PROMPT_V2.md     # Previous version
SETUP_PROMPT.md        # Original version
README.md              # Human-oriented documentation
examples/              # Example outputs showing wizard results
  example-nodejs-output.md
  example-python-output.md
  example-decline-plugins.md
  example-existing-config.md
```

## Key Conventions

- The wizard only modifies `.claude/`, `.mcp.json`, `CLAUDE.md`, and `claude-setup-report.md` in the **target** project — never source code
- Plugin installs are global (affect all Claude projects) — V3 requires explicit user consent in the plan approval step
- All changes are additive: merge/append only, never overwrite

## V3 Design Decisions

Key architectural choices baked into V3 — understand these before changing the flow:

- **Detect first, recommend second**: Plugin matching happens *after* the full repo scan, not during a vague "quick stack scan". The LLM must read dependency files (not just root config files) before matching plugins.
- **Catalog-driven matching, not hardcoded tables**: Plugin recommendations come from reading `claude plugin list --available --json` descriptions against the detected stack. The prompt gives examples but explicitly says not to treat them as the full list.
- **Single approval gate**: Plugin consent and project-scoped plan approval are combined into one yes/no to reduce friction. The plan clearly labels which items are global vs project-scoped.
- **Plugins install before plugin commands are used**: `AUTOMATION_RECOMMENDER_CMD` and `CLAUDE_MD_IMPROVER_CMD` are both actively invoked in Phase 3 — *after* plugins are installed in 3a. The recommender validates detection; the improver generates CLAUDE.md. Neither is optional or "if available" after install.
- **Setup report to repo root**: `claude-setup-report.md` saves to the repo root (not `.claude/`) so it's immediately visible. Phase 4 chat output is intentionally minimal — just a pointer to the file.

## Editing the Prompt

When iterating on the prompt, save new versions as `SETUP_PROMPT_V4.md` etc. Do not overwrite previous versions.
Keep `README.md` in sync with the current version's behaviour if the flow changes significantly.
