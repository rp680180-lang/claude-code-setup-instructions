# Example Output: Project With Existing Claude Config

This example shows what happens when you run the wizard on a project that already has some Claude Code setup. The wizard merges additively — it never overwrites or removes your existing configuration.

Stack used in this example: Node.js / Express / TypeScript with partial existing Claude setup (`.claude/settings.json` and `.mcp.json` already present, no `CLAUDE.md` yet).

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
- commit-commands — needed for clean setup commits

(claude-code-setup, claude-md-management already installed — no action needed)

What this means (simple): Only one tool needs to be added globally.
Why I'm asking: Plugin installation is a global change.
Approve global plugin installs? (yes/no)
```

User reply:

```text
yes
```

```text
Installing missing plugins:
- /plugin install commit-commands

No action needed from you here; I will run that install.

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
- Language: Node.js (TypeScript)
- Framework: Express
- Package Manager: npm
- Formatter: Prettier
- Linter: ESLint
- Test Runner: Jest
- Env files: .env, .env.example

Existing Claude config found (will merge, additive only):
  .claude/settings.json — has 2 existing hooks, 3 existing permissions
  .mcp.json — has context7 already configured
  No CLAUDE.md found — will create
  No .claude/skills/ found — will create
  No .claude/agents/ found — will create
```

## Phase 2: Plan

```text
I found your stack: Node.js + TypeScript + Express + Prettier + Jest.

I will install/update (existing config preserved throughout):

Plugins (global):
- commit-commands — commit workflow (others already installed)

Command aliases I will use:
- Recommender: /claude-automation-recommender
- CLAUDE.md: /claude-md-improver
- Commit: /commit

MCP servers:
- context7 — already present, will skip
- (no additional servers detected for this stack)

Hooks:
- Prettier auto-format on edit — will add (not in existing config)
- ESLint auto-fix on edit — will add (not in existing config)
- Block writes to .env* — already present in existing config, will skip

Skills:
- /code-review (new)
- /write-tests (new)
- /security-review (new)

Subagents:
- code-reviewer (sonnet) (new)
- test-writer (sonnet) (new)

Permissions:
- npm/node/npx/git read allows — some already present, will merge missing only
- Deny: Read(.env), Read(.env.*) — already present, will skip

What this means (simple): I will only add what's missing. Nothing existing will be removed or changed.
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
  → context7 already present — skipped

Updating hooks (.claude/settings.json, additive merge)...
  → .env protection hook already present — skipped
  ✓ PostToolUse: Prettier (added)
  ✓ PostToolUse: ESLint (added)
  (existing 2 hooks preserved unchanged)

Updating skills (additive)...
  ✓ .claude/skills/code-review/SKILL.md (created)
  ✓ .claude/skills/write-tests/SKILL.md (created)
  ✓ .claude/skills/security-review/SKILL.md (created)

Updating subagents (additive)...
  ✓ .claude/agents/code-reviewer.md (created)
  ✓ .claude/agents/test-writer.md (created)

Generating CLAUDE.md with plugin command: /claude-md-improver
  ✓ CLAUDE.md created (no previous file — full generation)

Updating permissions (.claude/settings.json, additive merge)...
  → Deny: Read(.env) already present — skipped
  → Deny: Read(.env.*) already present — skipped
  ✓ Allow: npm/npx commands (added)
  ✓ Allow: node/ts-node commands (added)
  (existing 3 permissions preserved unchanged)
```

Commit step:

```text
Setup is complete.
What this means (simple): I can make one clean commit for your setup files now.
Why I'm asking: This gives you a safe rollback point.
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

Your existing Claude configuration was preserved. Only missing items were added.

### Detected Stack
- Language: TypeScript (Node.js)
- Framework: Express
- Test runner: Jest
- Formatter/Linter: Prettier + ESLint

### What Was Updated

#### Plugins (global)
| Plugin | Command(s) Found | What it does |
|---|---|---|
| claude-code-setup | /claude-automation-recommender | Re-analyze setup recommendations |
| commit-commands | /commit | Smart commit workflow (newly installed) |
| claude-md-management | /claude-md-improver | Generate/refresh CLAUDE.md |

#### MCP Servers
| Server | Purpose | Status |
|---|---|---|
| context7 | Live docs lookup | Already present — no change |

#### Hooks (automatic)
| Trigger | Automation | Status |
|---|---|---|
| Edit/Write | Auto-format with Prettier | Added |
| Edit/Write | Auto-fix ESLint | Added |
| Write .env* | Blocked to protect secrets | Already present — no change |

#### Skills and Subagents
| Item | Purpose | Status |
|---|---|---|
| /code-review | Review quality and bugs | Created |
| /write-tests | Generate tests for a file/feature | Created |
| /security-review | Scan common vulnerabilities | Created |
| code-reviewer | Delegated quality reviewer | Created |
| test-writer | Delegated test generator | Created |

#### Files Created/Updated
- .claude/settings.json (merged — existing entries preserved)
- .claude/skills/* (created)
- .claude/agents/* (created)
- .mcp.json (no change — context7 already present)
- CLAUDE.md (created)

### Beginner Workflow Card

1) Start work:
- Use /feature-dev when building something new.

2) Write code:
- Edit as normal. Formatting and linting run automatically.

3) Check quality:
- Run /code-review after meaningful changes.
- Run /write-tests <file-or-feature> to generate tests.
- Run /security-review before release.

4) Keep setup fresh:
- Run /claude-automation-recommender when stack/tools change.
- Run /claude-md-improver to refresh project instructions.

5) Save progress:
- Use /commit for a clean commit.

Project automations explained (simple):
- Hooks: auto formatting/linting and .env protection.
- MCP servers: connected tools Claude can call.
- Skills/subagents: reusable specialist workflows Claude can invoke.

If a command does not work:
- Run /help and use the alias shown there.

To see all available /commands:
- Run /help.
```
