# Example Output: Python / FastAPI Project

This example shows the beginner-first, plugin-first flow for a FastAPI project.

---

## Phase -1: Safety Preflight

```text
Safety check before we start:
This setup will write or update: .claude/, .mcp.json, and CLAUDE.md.
It will not edit your app source code.

Recommended backup options:
1) git add -A && git commit -m "pre-claude-setup checkpoint"
2) git checkout -b backup/pre-claude-setup
3) Copy the project folder

Reply with exactly: I have a backup
```

User reply:

```text
I have a backup
```

## Phase 0: Plugin Readiness + Global Consent + Alias Discovery

```text
Global change notice:
Installing plugins affects Claude in all your projects.

Missing plugins:
- commit-commands — needed for clean setup commits
- claude-md-management — needed to generate/update CLAUDE.md

Approve global plugin installs? (yes/no)
```

User reply:

```text
yes
```

```text
Installing missing plugins:
- /plugin install commit-commands
- /plugin install claude-md-management

No action needed from you here; I will run those installs.

When plugin setup is done, reply with: ready
```

User reply:

```text
ready
```

```text
Resolved command aliases from /help:
- AUTOMATION_RECOMMENDER_CMD: /claude-automation-recommender
- CLAUDE_MD_IMPROVER_CMD: /claude-md-improver
- COMMIT_CMD: /commit
```

## Phase 1: Detect

```text
Running plugin recommender first: /claude-automation-recommender
Done. Recommendations captured.

Manual detection summary:
- Language: Python 3.12
- Framework: FastAPI
- Package Manager: pip (pyproject.toml)
- Formatter/Linter: Ruff
- Type Checker: mypy
- Test Runner: pytest
- ORM: SQLAlchemy
- Database: PostgreSQL
- Services: GitHub, Docker
- Env files: .env, .env.example
- Existing Claude config: found, will merge (additive only)
```

## Phase 2: Plan

```text
I found your stack: FastAPI + Ruff + pytest.

I will install/update:

Plugins (global):
- commit-commands — commit workflow
- claude-md-management — CLAUDE.md generation

Command aliases I will use:
- Recommender: /claude-automation-recommender
- CLAUDE.md: /claude-md-improver
- Commit: /commit

MCP servers:
- context7
- github

Hooks:
- Ruff format/lint on edit
- block writes to .env*

Skills:
- /code-review
- /write-tests
- /security-review

Subagents:
- code-reviewer (sonnet)
- test-writer (sonnet)

Proceed with installation? (yes/no)
```

User reply:

```text
yes
```

## Phase 3: Install

```text
Installing MCP servers...
  ✓ context7 added (merge-safe)
  ✓ github added (merge-safe)

Updating hooks (.claude/settings.json, additive merge)...
  ✓ PostToolUse: Ruff format + check --fix
  ✓ PreToolUse: .env protection
  ✓ .claude/hooks/protect-env.sh created
  ✓ chmod +x .claude/hooks/protect-env.sh

Updating skills (additive)...
  ✓ .claude/skills/code-review/SKILL.md
  ✓ .claude/skills/write-tests/SKILL.md
  ✓ .claude/skills/security-review/SKILL.md

Updating subagents (additive)...
  ✓ .claude/agents/code-reviewer.md
  ✓ .claude/agents/test-writer.md

Generating CLAUDE.md with plugin command: /claude-md-improver
  ✓ CLAUDE.md updated and preserved existing notes

Updating permissions (.claude/settings.json, additive merge)...
  ✓ Allow: python/pip/pytest/ruff/git read commands
  ✓ Deny: Read(.env), Read(.env.*), Read(.env.local)
```

Commit step:

```text
Setup is complete.
Commit setup files now? (yes/no)
```

User reply:

```text
yes
```

```text
Running commit command: /commit
✓ Setup commit created
```

## Phase 4: Summary

```text
## Claude Code Setup Complete

### Detected Stack
- Language: Python
- Framework: FastAPI
- Test runner: pytest
- Formatter/Linter: Ruff

### What Was Installed

#### Plugins (global)
| Plugin | Command(s) Found | What it does |
|---|---|---|
| claude-code-setup | /claude-automation-recommender | Re-analyze setup recommendations |
| commit-commands | /commit | Smart commit workflow |
| claude-md-management | /claude-md-improver | Generate/refresh CLAUDE.md |

#### MCP Servers
| Server | Purpose | How to use |
|---|---|---|
| context7 | Live docs lookup | "look up FastAPI dependency injection docs" |
| github | PR/issues workflows | "show open issues" |

#### Hooks (automatic)
| Trigger | Automation |
|---|---|
| Edit/Write | Auto-format/lint with Ruff |
| Write .env* | Blocked to protect secrets |

#### Skills and Subagents
| Item | Purpose |
|---|---|
| /code-review | Review quality and bugs |
| /write-tests | Generate tests for a file/feature |
| /security-review | Scan common vulnerabilities |
| code-reviewer | Delegated quality reviewer |
| test-writer | Delegated test generator |

#### Files Created/Updated
- .claude/settings.json
- .claude/hooks/protect-env.sh
- .claude/skills/*
- .claude/agents/*
- .mcp.json
- CLAUDE.md

### Beginner Workflow Card

1) Start work:
- Use `/feature-dev` when building something new.

2) Write code:
- Edit as normal. Ruff automation runs after edits.

3) Check quality:
- Run `/code-review` after meaningful changes.
- Run `/write-tests <file-or-feature>` to generate tests.
- Run `/security-review` before release.

4) Keep setup fresh:
- Run `/claude-automation-recommender` when stack/tools change.
- Run `/claude-md-improver` to refresh project instructions.

5) Save progress:
- Use `/commit` for a clean commit.

Project automations explained:
- Hooks: auto formatting/linting and .env protection.
- MCP servers: connected tools Claude can call.
- Skills/subagents: reusable specialist workflows Claude can invoke.

If a command does not work:
- Run `/help` and use the alias shown there.
```
