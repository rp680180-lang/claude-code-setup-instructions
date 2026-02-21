# Example Output: Declining Plugin Installs

This example shows what happens when you say **no** to the global plugin consent step. Setup still completes fully — the only difference is manual fallbacks are used instead of plugin commands.

Stack used in this example: Python / FastAPI (same as `example-python-output.md` for comparison).

---

## Phase -1: Safety Preflight

```text
Safety check before we start:
This setup will write or update: .claude/, .mcp.json, and CLAUDE.md.
It will not edit your app source code.

Recommended backup options (pick one):
1) git add -A && git commit -m "pre-claude-setup checkpoint"
2) git checkout -b backup/pre-claude-setup
3) Copy the project folder to a backup location.

What this means (simple): If you don't like the setup, you can roll back quickly.
Why I'm asking: This protects your current repo state.
Reply with exactly: I have a backup
```

User reply:

```text
I have a backup
```

## Phase 0: Plugin Readiness + Global Consent + Alias Discovery

```text
Global change notice:
Installing plugins affects Claude in all your projects, not just this repo.

Missing plugins:
- claude-code-setup — used to detect and recommend automations
- commit-commands — needed for clean setup commits
- claude-md-management — needed to generate/update CLAUDE.md

What this means (simple): These tools would become available everywhere in Claude.
Why I'm asking: Plugin installation is a global change.
Approve global plugin installs? (yes/no)
```

User reply:

```text
no
```

```text
No problem. Running in reduced mode:
- No plugins will be installed.
- CLAUDE.md will be generated directly (no plugin command).
- The final commit step will use standard git commands instead of /commit.
- Everything else (MCP servers, hooks, skills, subagents, permissions) installs as normal.

Your setup will be complete and fully functional. You can install plugins later at any time using /plugin install <name>.

When you're ready to continue, reply with: ready
```

User reply:

```text
ready
```

```text
Command aliases (reduced mode):
- AUTOMATION_RECOMMENDER_CMD: manual fallback (no plugin available)
- CLAUDE_MD_IMPROVER_CMD: manual fallback (no plugin available)
- COMMIT_CMD: manual fallback (no plugin available)
```

## Phase 1: Detect

```text
No plugin recommender available. Running manual detection only.

Manual detection summary:
- Language: Python 3.11
- Framework: FastAPI
- Package Manager: pip (pyproject.toml)
- Formatter: Ruff
- Linter: Ruff
- Type Checker: mypy
- Test Runner: pytest
- Services: none detected
- Env files: .env, .env.example
- Existing Claude config: none found
```

## Phase 2: Plan

```text
I found your stack: Python + FastAPI + Ruff + pytest.

I will install/update:

Plugins (global):
- none (declined)

Command aliases I will use:
- Recommender: manual fallback
- CLAUDE.md: manual fallback
- Commit: manual fallback

MCP servers:
- context7

Hooks:
- Ruff auto-format and auto-fix on edit
- Block writes to .env*

Skills:
- /code-review
- /write-tests
- /security-review

Subagents:
- code-reviewer (sonnet)
- test-writer (sonnet)

Permissions:
- Allow: python/pip/pytest/ruff/git read commands
- Deny: Read(.env), Read(.env.*)

What this means (simple): These automations reduce manual setup work every day.
Why I'm asking: I only proceed after you confirm the plan.
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

Updating hooks (.claude/settings.json, additive merge)...
  ✓ PostToolUse: Ruff format + fix
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

Generating CLAUDE.md manually (no plugin available)...
  ✓ CLAUDE.md created with project overview, key commands, and workflow section

Updating permissions (.claude/settings.json, additive merge)...
  ✓ Allow: python/pip/pytest/ruff/git read commands
  ✓ Deny: Read(.env), Read(.env.*)
```

Commit step:

```text
Setup is complete.
What this means (simple): I can make one clean commit for your setup files now.
Why I'm asking: This gives you a safe rollback point.

No /commit command available. To commit manually, run:
  git add .claude/ .mcp.json CLAUDE.md
  git commit -m "chore: add Claude Code setup"

Commit now? (yes/no)
```

User reply:

```text
yes
```

```text
Running manual commit:
  git add .claude/ .mcp.json CLAUDE.md
  git commit -m "chore: add Claude Code setup"
✓ Setup commit created
```

## Phase 4: Summary

```text
## Claude Code Setup Complete

Your setup is complete. Because you declined plugin installs, manual fallbacks were used for CLAUDE.md generation and the setup commit — everything works the same way.

If you want plugins later, run: /plugin install <name>

### Detected Stack
- Language: Python 3.11
- Framework: FastAPI
- Test runner: pytest
- Formatter/Linter: Ruff

### What Was Installed

#### Plugins (global)
| Plugin | Command(s) Found | What it does |
|---|---|---|
| none | N/A | Declined at consent step |

#### MCP Servers
| Server | Purpose | How to use |
|---|---|---|
| context7 | Live docs lookup | "look up FastAPI dependency injection docs" |

#### Hooks (automatic)
| Trigger | Automation |
|---|---|
| Edit/Write | Auto-format and auto-fix with Ruff |
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
- Describe what you want to build and ask Claude to help plan it.

2) Write code:
- Edit as normal. Ruff formatting and fixes run automatically.

3) Check quality:
- Run /code-review after meaningful changes.
- Run /write-tests <file-or-feature> to generate tests.
- Run /security-review before release.

4) Keep setup fresh:
- When your stack changes, paste the setup prompt again to re-run detection.
- To refresh CLAUDE.md, ask Claude: "Please update CLAUDE.md to reflect the current project."

5) Save progress:
- Use standard git: git add -A && git commit -m "your message"

Project automations explained (simple):
- Hooks: auto formatting/linting and .env protection.
- MCP servers: connected tools Claude can call.
- Skills/subagents: reusable specialist workflows Claude can invoke.

If a command does not work:
- Run /help and use the alias shown there.

To see all available /commands:
- Run /help.
```
