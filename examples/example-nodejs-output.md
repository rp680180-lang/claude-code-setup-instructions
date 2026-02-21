# Example Output: Node.js / Next.js / TypeScript Project

This shows what the wizard produces for a typical Next.js project with TypeScript, Prettier, ESLint, Jest, Playwright, and a GitHub repo.

---

## Phase 1: Detection Results

```
Detected:
- Language: Node.js (TypeScript)
- Framework: Next.js 14 (React)
- Package Manager: npm
- Formatter: Prettier
- Linter: ESLint
- Test Runner: Jest + Playwright
- CSS: Tailwind CSS
- ORM: Prisma (PostgreSQL)
- Services: GitHub, Vercel
- Env files: .env.local, .env.example
- Existing Claude config: None
```

## Phase 2: Plan

```
I'll install the following for your Node.js / Next.js / TypeScript project:

MCP Servers:
  ✓ context7 — live documentation lookups for React, Next.js, Prisma, etc.
  ✓ playwright — browser testing and UI automation
  ✓ github — GitHub issues, PRs, and Actions integration

Hooks:
  ✓ PostToolUse: auto-format with Prettier on every file edit
  ✓ PostToolUse: auto-lint with ESLint on every file edit
  ✓ PreToolUse: block writes to .env* files

Skills:
  ✓ /code-review — review code for bugs, quality, and React best practices
  ✓ /write-tests — generate Jest unit tests or Playwright E2E tests
  ✓ /security-review — check for XSS, injection, auth issues

Subagents:
  ✓ code-reviewer (sonnet) — proactive code quality review
  ✓ test-writer (sonnet) — test generation with Jest/Playwright

Other:
  ✓ CLAUDE.md — project instructions (commands, structure, conventions)
  ✓ Permissions — auto-allow npm/npx/git commands, protect .env files

Shall I proceed with this installation?
```

## Phase 3: Installation Log

```
Installing MCP servers...
  ✓ context7 added (project scope)
  ✓ playwright added (project scope)
  ✓ github added (project scope)

Creating hooks...
  ✓ PostToolUse: Prettier auto-format on Edit|Write|MultiEdit
  ✓ PostToolUse: ESLint auto-fix on Edit|Write|MultiEdit
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
  ✓ CLAUDE.md created (48 lines)

Configuring permissions...
  ✓ Allow: npm run *, npx *, node *, git diff/log/status
  ✓ Deny: Read(.env), Read(.env.*), Read(.env.local)
```

## Phase 4: Summary

```
## Claude Code Setup Complete

### Detected Stack
- **Language**: TypeScript (Node.js 20)
- **Framework**: Next.js 14 (App Router)
- **Test Runner**: Jest (unit) + Playwright (E2E)
- **Formatter**: Prettier
- **Linter**: ESLint

### What Was Installed

#### MCP Servers
| Server | Purpose | How to use |
|--------|---------|------------|
| context7 | Live docs for any library | "look up the Next.js App Router docs" |
| playwright | Browser automation & testing | "test the login page in the browser" |
| github | GitHub integration | "show me open PRs" or "create an issue" |

#### Hooks (run automatically)
| Trigger | What happens |
|---------|-------------|
| Every file edit | Auto-formats with Prettier |
| Every file edit | Auto-fixes ESLint issues |
| Write to .env* | Blocked — use .env.example instead |

#### Skills
| Command | What it does |
|---------|-------------|
| /code-review | Reviews code for bugs, React anti-patterns, and quality |
| /write-tests src/app/api/users/route.ts | Generates Jest tests for the specified file |
| /security-review | Scans for XSS, injection, and auth vulnerabilities |

#### Subagents (Claude delegates to these automatically)
| Agent | Purpose |
|-------|---------|
| code-reviewer | Reviews code changes after edits (sonnet) |
| test-writer | Generates tests when asked (sonnet) |

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
- Your code is auto-formatted and linted on every edit — no action needed
- Type `/code-review` after making changes for a quality check
- Type `/security-review` before deploying for a security scan
- Type `/write-tests src/components/Button.tsx` to generate tests
- Commit `.claude/` and `.mcp.json` to share this setup with your team
- Edit `CLAUDE.md` to add any project-specific instructions Claude should know
```
