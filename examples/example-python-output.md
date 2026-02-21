# Example Output: Python / FastAPI Project

This shows what the wizard produces for a FastAPI project with Ruff, pytest, PostgreSQL (SQLAlchemy), Docker, and a GitHub repo.

---

## Phase 1: Detection Results

```
Detected:
- Language: Python 3.12
- Framework: FastAPI
- Package Manager: pip (pyproject.toml)
- Formatter: Ruff
- Linter: Ruff
- Type Checker: mypy
- Test Runner: pytest
- ORM: SQLAlchemy
- Database: PostgreSQL
- Services: GitHub, Docker
- Env files: .env, .env.example
- Existing Claude config: None
```

## Phase 2: Plan

```
I'll install the following for your Python / FastAPI project:

MCP Servers:
  ✓ context7 — live documentation lookups for FastAPI, SQLAlchemy, etc.
  ✓ github — GitHub issues, PRs, and Actions integration

Hooks:
  ✓ PostToolUse: auto-format and lint with Ruff on every file edit
  ✓ PreToolUse: block writes to .env files

Skills:
  ✓ /code-review — review code for bugs, quality, and Python best practices
  ✓ /write-tests — generate pytest tests
  ✓ /security-review — check for SQL injection, auth issues, exposed secrets

Subagents:
  ✓ code-reviewer (sonnet) — proactive code quality review
  ✓ test-writer (sonnet) — pytest test generation

Other:
  ✓ CLAUDE.md — project instructions (commands, structure, conventions)
  ✓ Permissions — auto-allow python/pip/pytest/ruff commands, protect .env files

Shall I proceed with this installation?
```

## Phase 3: Installation Log

```
Installing MCP servers...
  ✓ context7 added (project scope)
  ✓ github added (project scope)

Creating hooks...
  ✓ PostToolUse: Ruff format + lint on Edit|Write|MultiEdit
  ✓ PreToolUse: .env file protection via .claude/hooks/protect-env.sh
  ✓ chmod +x .claude/hooks/protect-env.sh

Creating skills...
  ✓ .claude/skills/code-review/SKILL.md
  ✓ .claude/skills/write-tests/SKILL.md
  ✓ .claude/skills/security-review/SKILL.md

Creating subagents...
  ✓ .claude/agents/code-reviewer.md
  ✓ .claude/agents/test-writer.md

Generating CLAUDE.md...
  ✓ CLAUDE.md created (42 lines)

Configuring permissions...
  ✓ Allow: python *, pip *, pytest *, ruff *, git diff/log/status
  ✓ Deny: Read(.env), Read(.env.*)
```

## Phase 4: Summary

```
## Claude Code Setup Complete

### Detected Stack
- **Language**: Python 3.12
- **Framework**: FastAPI 0.109
- **Test Runner**: pytest
- **Formatter/Linter**: Ruff
- **Type Checker**: mypy

### What Was Installed

#### MCP Servers
| Server | Purpose | How to use |
|--------|---------|------------|
| context7 | Live docs for any library | "look up the FastAPI dependency injection docs" |
| github | GitHub integration | "show me open issues" or "create a PR" |

#### Hooks (run automatically)
| Trigger | What happens |
|---------|-------------|
| Every file edit | Auto-formats and lints with Ruff |
| Write to .env* | Blocked — use .env.example instead |

#### Skills
| Command | What it does |
|---------|-------------|
| /code-review | Reviews code for bugs, type issues, and Python best practices |
| /write-tests app/api/routes/users.py | Generates pytest tests for the specified file |
| /security-review | Scans for SQL injection, auth issues, exposed secrets |

#### Subagents (Claude delegates to these automatically)
| Agent | Purpose |
|-------|---------|
| code-reviewer | Reviews code changes after edits (sonnet) |
| test-writer | Generates pytest tests when asked (sonnet) |

#### Files Created
- `.claude/settings.json` — hooks and permissions
- `.claude/hooks/protect-env.sh` — env file protection
- `.claude/skills/code-review/SKILL.md`
- `.claude/skills/write-tests/SKILL.md`
- `.claude/skills/security-review/SKILL.md`
- `.claude/agents/code-reviewer.md`
- `.claude/agents/test-writer.md`
- `.mcp.json` — MCP server configs
- `CLAUDE.md` — project instructions

### Quick Tips
- Your code is auto-formatted and linted with Ruff on every edit — no action needed
- Type `/code-review` after making changes for a quality check
- Type `/security-review` before deploying for a security scan
- Type `/write-tests app/models/user.py` to generate tests
- Commit `.claude/` and `.mcp.json` to share this setup with your team
- Edit `CLAUDE.md` to add any project-specific instructions Claude should know
```
