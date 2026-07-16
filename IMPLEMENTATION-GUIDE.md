# Boris' Tips — Claude Code Implementation Guide

> **What this is:** ~70 actionable tips from Boris Cherny (Head of Claude Code, Anthropic) structured as executable instructions for Claude Code. Feed this file to Claude Code and it will auto-configure your project.
>
> **What this is NOT:** A reference document. For the full 147-tip collection (including philosophy, workflow habits, and team practices), see [TIPS.md](./TIPS.md).
>
> **Source:** All tips originate from Boris Cherny's public posts on X, podcasts, conferences, and the Anthropic blog. Tip IDs reference [TIPS.md](./TIPS.md) for full context and source URLs.

---

## How to Use This File

### Option A: One-Shot Auto-Setup (Recommended)
```bash
cat IMPLEMENTATION-GUIDE.md | claude -p "Execute all setup instructions in this document for my current project. Skip sections that don't apply. Ask me before creating files."
```

### Option B: Feed into an Active Session
```
Open Claude Code in your project, then paste:
> Read IMPLEMENTATION-GUIDE.md and execute the setup instructions section by section. Ask me before each section whether to proceed.
```

### Option C: Cherry-Pick Sections
Copy individual sections below into Claude Code as needed. Each section is self-contained.

### Staged Adoption (Boris' Recommendation)
Don't implement everything at once. Follow this order:
1. **Week 1:** Section 1 (CLAUDE.md) + Section 2 (Settings)
2. **Week 2–3:** Section 3 (Slash Commands) + Section 7 (Verification)
3. **Week 4+:** Section 4 (Hooks) + Section 5 (Subagents)
4. **Month 2+:** Section 6 (MCP) + Section 8 (Headless) + Section 9–10

---

## Section 1: CLAUDE.md Setup

*Implements tips: #03.01, #03.02, #03.05, #03.07, #03.08, #03.09, #03.10, #03.12*

CLAUDE.md is Claude Code's project memory — automatically read at session start. Boris calls it "compounding engineering": every mistake Claude makes becomes a rule that prevents future mistakes.

### 1.1 Create Project CLAUDE.md

If `CLAUDE.md` does not exist in the project root, create it with this starter template. If it exists, review and merge relevant sections.

```markdown
# CLAUDE.md

## Project Overview
<!-- Describe what this project does in 1-2 sentences -->

## Tech Stack
<!-- List languages, frameworks, key dependencies -->

## Build & Test
<!-- Commands Claude needs to run -->
- Build: `npm run build` (or your build command)
- Test: `npm test`
- Lint: `npm run lint`
- Dev server: `npm run dev`

## Code Conventions
<!-- Rules Claude should follow -->
- Use TypeScript strict mode
- Prefer named exports over default exports
- Write tests for all new functions

## Known Gotchas
<!-- Add rules here whenever Claude makes a mistake -->
<!-- Example: "Always use path.join() instead of string concatenation for file paths" -->
<!-- Example: "The auth middleware must be applied before route handlers" -->

## Project Structure
<!-- Key directories and their purpose -->
```

After initial creation, run `/init` to let Claude analyze your codebase and enrich the file automatically.

### 1.2 Create Personal CLAUDE.local.md

Create `CLAUDE.local.md` in the project root (this file is gitignored — personal preferences only).

```markdown
# CLAUDE.local.md — Personal Settings

## My Preferences
- Respond in English (or your preferred language)
- Use concise output, no verbose explanations unless asked
- When fixing bugs: show the diff, not the whole file

## My Environment
- OS: (your OS)
- Editor: (your editor)
- Terminal: (your terminal)
```

Ensure `.gitignore` includes `CLAUDE.local.md`.

### 1.3 Create Global CLAUDE.md

Create `~/.claude/CLAUDE.md` for settings that apply to ALL your projects.

```markdown
# Global Claude Code Settings

## Universal Rules
- Always run tests after making changes
- Never commit directly to main without asking
- Use conventional commit messages (feat:, fix:, chore:, etc.)
- When unsure, ask — don't guess
```

### 1.4 Error-Correction Workflow

After Claude makes a mistake, tell it:

> "Update your CLAUDE.md so you don't make that mistake again."

Claude will write the rule itself. This is Boris' core "compounding engineering" pattern — over time, CLAUDE.md accumulates project-specific knowledge that prevents recurring errors.

### 1.5 Notes Directory for Complex Tasks

For large projects, create a `notes/` directory referenced from CLAUDE.md:

```markdown
<!-- Add to CLAUDE.md -->
## Task Notes
See `notes/` directory for per-task context files. Read the relevant note before starting work on that area.
```

Create `notes/` and add `.md` files per task/feature area as needed.

### 1.6 Memory via `#` Prefix

In any Claude Code session, prepend `#` to something you want Claude to remember:

```
# Always use the v2 API endpoint, not v1
```

Claude will ask whether to save to project memory (CLAUDE.md) or user memory (~/.claude/CLAUDE.md).

### 1.7 Write REVIEW.md and Skills as Team Automation Infrastructure

Encode domain knowledge that previously lived in reviewer heads as agent-readable artifacts. Create a `REVIEW.md` at the project root:

```markdown
# REVIEW.md

## Code Review Criteria
<!-- What every PR must satisfy before merge -->
- All new API endpoints must include rate limiting
- React components must use design-system tokens, not raw CSS values
- DB queries must go through the repository layer, not direct ORM calls

## Architecture Decisions
<!-- Brief ADRs — link to full docs if needed -->
- Use React Query for server state, Zustand for UI state
- Prefer composition over inheritance in component design

## Common Rejections
<!-- Patterns that get PRs sent back — so Claude avoids them -->
- Do not use console.log in production code
- Do not import from sibling directories — use index barrels
```

Reference it from CLAUDE.md:

```markdown
## Review Standards
See REVIEW.md for the code review checklist agents must follow before opening a PR.
```

Also invest in Skills (`.claude/commands/`) that encode repeated workflows. The goal: an agent cloned fresh into your repo can do meaningful work without any additional context from you. (#03.12)

---

## Section 2: Settings & Permissions

*Implements tips: #07.01, #07.02, #07.03, #07.04, #13.01, #13.03, #13.05, #13.06, #20.01*

### 2.1 Create Team-Shared Settings

Create `.claude/settings.json` in the project root. This file is checked into git so the whole team benefits.

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run *)",
      "Bash(npx *)",
      "Bash(node *)",
      "Bash(git status)",
      "Bash(git diff *)",
      "Bash(git log *)",
      "Bash(git add *)",
      "Bash(git commit *)",
      "Bash(git push *)",
      "Bash(git checkout *)",
      "Bash(git branch *)",
      "Bash(ls *)",
      "Bash(cat *)",
      "Bash(find *)",
      "Bash(grep *)",
      "Bash(mkdir *)",
      "Bash(cp *)",
      "Bash(mv *)",
      "Read(*)",
      "Write(*)",
      "Edit(*)"
    ]
  }
}
```

Adapt the `Bash(...)` patterns to your project's tool chain:
- **Python projects:** Add `"Bash(python *)"`, `"Bash(pip *)"`, `"Bash(pytest *)"`, `"Bash(ruff *)"`
- **Go projects:** Add `"Bash(go *)"`, `"Bash(make *)"`
- **Rust projects:** Add `"Bash(cargo *)"`, `"Bash(rustfmt *)"`

Boris' rule: **Use `/permissions` to pre-allow safe commands instead of `--dangerously-skip-permissions`**.

### 2.2 Wildcard Permission Patterns

Use wildcards to allow entire tool families (#07.03):

```json
"Bash(bun run *)"      // All bun scripts
"Edit(/docs/**)"        // Edit anything in docs/
"Bash(docker compose *)" // All docker compose commands
```

### 2.3 Environment Variables

Set these in your shell profile (`.bashrc`, `.zshrc`, etc.) or in `.claude/settings.json` under `"env"`:

```json
{
  "env": {
    "CLAUDE_CODE_AUTO_COMPACT_WINDOW": "400000",
    "CLAUDE_CODE_NO_FLICKER": "1"
  }
}
```

| Variable | Value | Why (Boris' Tip) |
|----------|-------|-------------------|
| `CLAUDE_CODE_AUTO_COMPACT_WINDOW` | `400000` | Prevents context rot at 300-400k tokens (#20.01) |
| `CLAUDE_CODE_NO_FLICKER` | `1` | Experimental renderer with no flicker/jump, mouse support (#13.06) |

### 2.4 Spinner Customization (Optional Fun)

Add to `.claude/settings.json` (#13.01):

```json
{
  "spinner": {
    "verbs": ["Analyzing", "Computing", "Synthesizing", "Reasoning", "Investigating"]
  }
}
```

### 2.5 Git-Check the Settings

```bash
git add .claude/settings.json
git commit -m "chore: add team-shared Claude Code settings"
```

The team now shares permissions, env vars, and customizations. New members get the full setup on first `claude` session.

---

## Section 3: Slash Commands

*Implements tips: #04.01, #04.02, #04.03, #04.04, #04.05, #04.09, #04.10, #04.15, #04.17, #04.23, #04.35*

Slash commands are markdown files in `.claude/commands/`. They are prompts, not tools — Claude reads them as instructions. Check them into git for team sharing.

### 3.1 `/commit` — The Most-Used Command at Anthropic

Create `.claude/commands/commit.md`:

```markdown
---
description: Commit current changes with a descriptive message
---

Look at the current git diff (staged and unstaged). Write a concise, conventional commit message that describes what changed and why. Then:

1. Stage all relevant files
2. Commit with the message
3. Show the commit hash

Do NOT push unless I explicitly say "and push".
```

### 3.2 `/commit-push-pr` — Boris' Daily Driver

Create `.claude/commands/commit-push-pr.md`:

```markdown
---
description: Commit, push, and create a PR in one shot
---

1. Run `git status` and `git diff --stat` to understand current changes
2. Write a conventional commit message (feat/fix/chore/refactor)
3. Stage and commit
4. Push to the current branch (create remote branch if needed)
5. Create a PR with:
   - Title matching the commit message
   - Body summarizing the changes (bullet points)
   - Link to any related issues mentioned in the diff

Show me the PR URL when done.
```

### 3.3 `/feature-dev` — Step-by-Step Feature Development

Create `.claude/commands/feature-dev.md`:

```markdown
---
description: Guided feature development from spec to PR
---

Walk me through building a new feature step by step:

1. **Ask** what exactly I want to build (requirements, constraints, edge cases)
2. **Build a specification** from my answers
3. **Create a detailed plan** (files to create/modify, architecture decisions)
4. **Show me a TODO list** and get my approval
5. **Implement step by step**, showing progress after each step
6. **Run tests** after implementation
7. **Ask if I want to commit and create a PR**

Do NOT skip the planning phase. Boris says: "A good plan is really important."
```

### 3.4 `/code-review` — PR Review Command

Create `.claude/commands/code-review.md`:

```markdown
---
description: Review current changes like a senior engineer
---

Review the current git diff (or PR if a URL is provided). Check for:

1. **Logic errors** — Will this code do what it's supposed to?
2. **Edge cases** — What inputs/states could break this?
3. **Security** — Any injection, auth, or data exposure risks?
4. **Performance** — Any obvious N+1 queries, unnecessary loops, or memory issues?
5. **Style** — Does it match the project's conventions (see CLAUDE.md)?
6. **Tests** — Are the changes adequately tested?

For each issue found:
- Severity: 🔴 Critical / 🟡 Suggestion / 🟢 Nitpick
- File and line number
- What's wrong and how to fix it

Be honest. If the code is good, say so briefly.
```

### 3.5 `/techdebt` — End-of-Session Debt Scanner

Create `.claude/commands/techdebt.md`:

```markdown
---
description: Scan for technical debt in recently changed files
---

Look at files changed in the last 5 commits. For each, check for:

- Duplicated code (copy-paste across files)
- TODO/FIXME/HACK comments that should be addressed
- Functions longer than 50 lines
- Unused imports or dead code
- Missing error handling
- Missing or outdated tests

Report as a prioritized list. Don't fix anything — just report.
```

### 3.6 `/btw` — Side-Chain Quick Question

Create `.claude/commands/btw.md`:

```markdown
---
description: Quick question without interrupting current work
---

Answer this quick question using your current context. Do NOT use any tools — just answer from what you already know about this codebase.

$ARGUMENTS
```

This is Boris' most-used pattern: "I use this all the time to answer quick questions while the agent works." Single-turn, no tool calls, full context.

### 3.7 `/effort` — Set Reasoning Level

Use the built-in `/effort` command to set reasoning depth:
- `low` — Quick answers, minimal thinking
- `medium` — Default balanced mode
- `high` — Deeper analysis
- `xhigh` — Boris' default for most tasks
- `max` — Hardest problems only (resets after session)

Boris uses `xhigh` for most work and `max` for the hardest problems.

### 3.8 `/statusline` — Context & Cost Display

Use the built-in `/statusline` command to show:
- Context window usage (%)
- Current git branch
- Active model
- Session cost

Boris says every team member has their own statusline configuration.

### 3.9 `/checkup` — Claude Code Health Maintenance

Run the built-in `/checkup` command periodically to keep your setup healthy. It will:

1. Remove unused skills, MCPs, and plugins (saves context window space)
2. Deduplicate your local `CLAUDE.md` against the committed version
3. Split an oversized root `CLAUDE.md` into nested per-folder files and skills
4. Disable slow hooks that are blocking performance
5. Update Claude Code to the latest version
6. Enable auto mode by default
7. Pre-approve frequently denied read-only commands

Every proposed change is shown and confirmed before being applied. Run after major project changes or when you notice Claude Code feeling sluggish.

---

## Section 4: Hooks

*Implements tips: #06.01, #06.02, #06.03, #06.05, #06.06, #06.07*

Hooks are deterministic triggers that run before/after Claude uses tools. They're configured in `.claude/settings.json`. Boris uses them where "the model is unreliable" — formatting, logging, verification.

### 4.1 PostToolUse: Auto-Format on Write/Edit

Add to `.claude/settings.json`:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "command": "npx prettier --write $CLAUDE_FILE_PATH || true"
      }
    ]
  }
}
```

Adapt the formatter to your stack:
- **Python:** `"command": "ruff format $CLAUDE_FILE_PATH || true"`
- **Go:** `"command": "gofmt -w $CLAUDE_FILE_PATH || true"`
- **Rust:** `"command": "rustfmt $CLAUDE_FILE_PATH || true"`

Boris says Claude formats ~90% correctly — the hook catches the remaining 10%.

### 4.2 SessionStart: Load Dynamic Context

```json
{
  "hooks": {
    "SessionStart": [
      {
        "command": "echo 'Current branch:' && git branch --show-current && echo 'Recent commits:' && git log --oneline -5"
      }
    ]
  }
}
```

This injects fresh context whenever Claude starts — branch info, recent commits, anything your workflow needs.

### 4.3 PreToolUse: Bash Command Logging

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "command": "echo \"$(date -Iseconds) CLAUDE_BASH: $CLAUDE_COMMAND\" >> .claude/audit.log"
      }
    ]
  }
}
```

Creates an audit trail of every bash command Claude runs. Essential for sensitive repos.

### 4.4 Stop Hook: Keep Claude Running

```json
{
  "hooks": {
    "Stop": [
      {
        "command": "echo 'Claude stopped. Checking if work is complete...' && npm test 2>&1 | tail -5"
      }
    ]
  }
}
```

When Claude stops, the hook runs your test suite. If tests fail, Claude sees the output and can decide to continue.

### 4.5 PostCompact: Re-Inject Critical Instructions

```json
{
  "hooks": {
    "PostCompact": [
      {
        "command": "cat CLAUDE.md"
      }
    ]
  }
}
```

After context compression, critical instructions from CLAUDE.md may be lost. This hook re-injects them. Boris calls this essential for long-running sessions.

### 4.6 Agent Stop: Deterministic Verification

```json
{
  "hooks": {
    "AgentStop": [
      {
        "command": "npm test && npm run lint && npm run build"
      }
    ]
  }
}
```

More reliable than asking Claude to verify itself. Code, not the model, makes the pass/fail decision.

---

## Section 5: Subagents

*Implements tips: #05.01, #05.02, #05.03, #05.08, #05.10, #05.11*

Subagents are parallel Claude instances with isolated context windows. Boris: "The value is uncorrelated context windows, not anthropomorphization." Store them in `.claude/agents/`.

### 5.1 Code Simplifier Agent

Create `.claude/agents/code-simplifier.md`:

```markdown
---
name: code-simplifier
description: Simplify and clean code after implementation
tools:
  - Read
  - Write
  - Edit
  - Bash
  - Grep
  - Glob
---

You are a code simplifier. Your job is to review recent changes and make them simpler, more readable, and more maintainable.

## Rules
1. Read CLAUDE.md first for project conventions
2. Look at files changed in the last commit (or staged changes)
3. For each file, simplify:
   - Remove dead code and unused imports
   - Reduce function complexity (extract helpers if function > 40 lines)
   - Simplify conditional logic
   - Improve variable names for clarity
4. Run the project's test suite after changes
5. Do NOT change behavior — only simplify implementation
6. If tests fail, revert your changes to that file

Be aggressive about simplification but conservative about behavior changes.
```

### 5.2 Verify App Agent

Create `.claude/agents/verify-app.md`:

```markdown
---
name: verify-app
description: End-to-end verification of the application
tools:
  - Bash
  - Read
  - Grep
  - Glob
---

You are a verification agent. Your job is to verify the application works correctly end-to-end.

## Steps
1. Read CLAUDE.md for build/test commands
2. Run the full test suite
3. Start the dev server (if applicable) and verify it responds
4. Check for TypeScript/linting errors
5. Verify the build completes without errors
6. Report a summary: PASS (all green) or FAIL (with details)

## Output Format
```
VERIFICATION REPORT
===================
Tests:     PASS/FAIL (X passed, Y failed)
Lint:      PASS/FAIL
Build:     PASS/FAIL
Server:    PASS/FAIL (responds on port XXXX)
===================
OVERALL:   PASS/FAIL
```

If any step fails, provide the error output and suggest a fix.
```

### 5.3 Adversarial Reviewer Agent

Create `.claude/agents/adversarial-reviewer.md`:

```markdown
---
name: adversarial-reviewer
description: Find holes and weaknesses in code changes
tools:
  - Read
  - Grep
  - Glob
  - Bash
---

You are an adversarial code reviewer. Your job is to find problems that a normal reviewer would miss.

## Approach
1. Read the recent changes (git diff HEAD~1)
2. For each change, actively try to break it:
   - What inputs would cause unexpected behavior?
   - What race conditions are possible?
   - What happens under load/scale?
   - What security implications exist?
   - What happens if external services are down?
3. Check if error handling covers all failure modes
4. Verify that tests actually test the important paths (not just happy path)

## Output
List each finding with:
- **Severity:** Critical / High / Medium / Low
- **Location:** File:line
- **Attack vector:** How this could go wrong
- **Recommendation:** How to fix it

Be skeptical. Assume the code is wrong until proven otherwise. Boris uses this pattern with 5 agents reviewing, then 5 more agents poking holes in the first findings.
```

### 5.4 Using Subagents

Once agents are defined, use them:

```
# Run a specific agent
claude --agent=code-simplifier

# Ask Claude to use subagents on the fly
"Review this PR. Use subagents."

# Parallel exploration of a new codebase
"Use 5 subagents to explore the codebase and summarize the architecture"
```

### 5.5 Set a Default Agent

In `.claude/settings.json`, set a team-wide default agent (#05.11):

```json
{
  "agent": "verify-app"
}
```

Or use per-session: `claude --agent=code-simplifier`

---

## Section 6: MCP Integrations

*Implements tips: #08.01, #08.06, #08.07*

MCP (Model Context Protocol) connects Claude to external services. Configure in `.mcp.json` at project root.

### 6.1 Slack MCP

Create `.mcp.json` (replace with your team's Slack token):

```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-slack"],
      "env": {
        "SLACK_BOT_TOKEN": "$SLACK_BOT_TOKEN"
      }
    }
  }
}
```

Set the env var: `export SLACK_BOT_TOKEN="xoxb-your-token-here"`

Boris uses this for:
- Searching Slack threads from Claude Code
- Posting status updates
- Daily summaries: `/loop every morning use the Slack MCP to give me a summary of top posts I was tagged in`

### 6.2 BigQuery via CLI

No MCP needed — Boris uses the `bq` CLI directly:

```
# In CLAUDE.md, add:
## Data Queries
Use `bq query --use_legacy_sql=false` for BigQuery. Project: your-gcp-project.
```

Boris: "I haven't written a line of SQL in 6+ months."

### 6.3 Sentry for Error Tracking

```json
{
  "mcpServers": {
    "sentry": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-sentry"],
      "env": {
        "SENTRY_AUTH_TOKEN": "$SENTRY_AUTH_TOKEN",
        "SENTRY_ORG": "your-org",
        "SENTRY_PROJECT": "your-project"
      }
    }
  }
}
```

Claude pulls error logs automatically. Bug triage without context-switching.

---

## Section 7: Verification Setup

*Implements tips: #10.01, #10.02, #10.03, #10.04, #10.05, #10.07, #10.08*

**This is Boris' #1 rule: "Give Claude a way to verify its work — it will 2-3x the quality of the final result."**

### 7.1 Add Verification Instructions to CLAUDE.md

Append to your `CLAUDE.md`:

```markdown
## Verification
After making changes, ALWAYS verify by:
1. Running the test suite: `npm test`
2. Running the linter: `npm run lint`
3. Building the project: `npm run build`
4. If frontend: open in browser and visually verify
5. If API: test the endpoint with curl

Do NOT submit a PR until all verifications pass.
```

### 7.2 Domain-Specific Verification

Choose verification tools based on your domain:

| Domain | Verification Method | Boris' Approach |
|--------|-------------------|-----------------|
| **Backend** | Start server, hit endpoints | "Make sure Claude can start your service" |
| **Frontend** | Chromium extension, screenshots | Boris uses this for every web UI change |
| **CLI tools** | Run with test inputs | `echo "test" \| my-tool --flag` |
| **Libraries** | Unit + integration tests | Full test suite on every change |
| **Desktop** | Computer Use | Built-in browser testing in desktop app |

### 7.3 Verification Prompt Patterns

Use these patterns in your prompts:

```
# "Grill me" pattern (#10.07)
"Grill me on these changes. Don't make a PR until I pass your test."

# "Prove it" pattern (#10.08)
"Prove to me this works. Diff the behavior between main and this branch."

# "Scrap and redo" pattern (#10.09)
"Scrap this and implement the elegant solution."

# Screenshot iteration (#10.10)
"Take a screenshot, compare it to the mock, and iterate until they match."
```

### 7.4 The `/go` Composite Pattern

Boris' workflow for most changes:

```
"Make [change]. Then verify end-to-end (run tests, start server, check the endpoint). Then run /simplify. Then create a PR."
```

This chains implementation → verification → cleanup → delivery in one prompt.

---

## Section 8: Headless / SDK Patterns

*Implements tips: #14.01, #14.04, #14.05, #14.06, #14.09*

Claude Code is a Unix utility, not a chatbot. Boris: "Cat the CSV, pipe it into claude."

### 8.1 Non-Interactive Mode (`claude -p`)

```bash
# Simple prompt
claude -p "Explain what this function does" < src/utils.ts

# Pipe data
cat data.csv | claude -p "Analyze this CSV and find anomalies"

# Generate code
claude -p "Write a Python script that converts JSON to CSV" > convert.py

# Code review in CI
git diff HEAD~1 | claude -p "Review this diff for bugs and security issues"
```

### 8.2 Pre-Commit Hook

Add to `.git/hooks/pre-commit` (or use husky/lint-staged):

```bash
#!/bin/bash
# Quick Claude check on staged changes (keep under 5 seconds)
git diff --cached --diff-filter=ACM | claude -p "Check for obvious bugs, security issues, or leaked secrets. Reply PASS or FAIL with reason." --bare
```

Make executable: `chmod +x .git/hooks/pre-commit`

The `--bare` flag skips loading CLAUDE.md/settings/MCPs for faster startup (10x speedup, #14.06).

### 8.3 Scoping Permissions for Batch Operations

```bash
# Only allow read operations
claude -p "Analyze the codebase architecture" --allow-tools "Read,Grep,Glob"

# Allow specific bash commands
claude -p "Run all tests" --allow-tools "Bash(npm test)"
```

### 8.4 Pipeline Examples

```bash
# Aggregate context from multiple sources
(cat README.md; echo "---"; git log --oneline -20) | claude -p "Summarize project state"

# Batch processing
for file in src/*.ts; do
  claude -p "Add JSDoc comments to all exported functions" --bare < "$file" > "${file}.documented"
done

# CI/CD integration
claude -p "$(cat <<EOF
Review the test results below. If there are failures, explain the root cause.
$(npm test 2>&1)
EOF
)"
```

---

## Section 9: Context Management

*Implements tips: #20.01, #20.02, #20.03, #20.04*

### 9.1 Auto-Compact Threshold

Set in your environment (already configured in Section 2.3 if using settings.json):

```bash
export CLAUDE_CODE_AUTO_COMPACT_WINDOW=400000
```

Boris (via Thariq): Context rot starts at 300-400k tokens. The 1M context window doesn't mean you should use all of it.

### 9.2 Context Usage Guidelines

| Context % | What Boris' Team Does |
|-----------|----------------------|
| 0-30% | Sweet spot for complex work |
| 30-40% | OK for experienced users |
| 40-60% | Only for simple, repetitive tasks |
| 60%+ | Performance degrades — `/compact` or `/clear` |

### 9.3 Decision Tree: `/compact` vs `/clear`

```
Is this a continuation of the same task?
  ├── Yes → /compact <hint about what to keep>
  └── No → /clear, then brief the new context manually

Is the context polluted with failed attempts?
  ├── Yes → /rewind to before the failure, re-prompt
  └── No → continue normally
```

Boris (via Thariq): "Each turn is a branching point. Pick: Continue / `/rewind` / `/clear` / `/compact` / Subagent."

### 9.4 Compact Hints

When compacting, give Claude a hint about what to preserve:

```
/compact Keep the database migration plan and the API endpoint structure. Forget the debugging attempts.
```

---

## Section 10: Automation & Long-Running Tasks

*Implements tips: #11.01, #11.02, #11.05, #11.06, #04.13, #04.14*

### 10.1 `/loop` for Recurring Local Tasks

```bash
# Monitor and fix (Boris' setup)
/loop 5m /babysit          # Check if anything needs attention every 5 min
/loop 30m /slack-feedback   # Summarize Slack every 30 min
/loop 1h /pr-pruner         # Close stale PRs hourly
```

`/loop` runs locally until you stop it or close the terminal. Max duration ~3 days.

### 10.2 `/schedule` for Cloud-Based Jobs

```bash
/schedule "every morning at 9am" "Check for CI failures and auto-fix if possible"
/schedule "on PR merge to main" "Run full test suite and update docs if needed"
```

`/schedule` runs on Anthropic infrastructure — survives laptop close. Available on Team/Enterprise plans.

### 10.3 Cross-Session Continuity

When ending a long session, tell Claude:

```
"Write down the state of this session into a handoff.md file. Include: what was done, what's pending, key decisions made, and current blockers."
```

In the next session:

```
"Read handoff.md and continue where the previous session left off."
```

This is Boris' workaround for cross-session memory before Routines existed. Still useful for complex multi-day tasks.

### 10.4 Background Verification Agent

After completing a feature, tell Claude:

```
"Spawn a background agent to run the full test suite and report results. Continue with the next task in the foreground."
```

The background agent runs verification while you keep working. Boris calls this the most practical long-running pattern.

---

## Appendix A: All Recommended Environment Variables

```bash
# Context management
export CLAUDE_CODE_AUTO_COMPACT_WINDOW=400000  # Prevent context rot (#20.01)

# Rendering
export CLAUDE_CODE_NO_FLICKER=1                # Stable renderer (#13.06)

# Model (optional — these can also be set via /effort)
# export ANTHROPIC_MODEL=claude-opus-4-20250901  # Force Opus model
```

---

## Appendix B: Complete `.claude/settings.json` Template

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run *)",
      "Bash(npx *)",
      "Bash(node *)",
      "Bash(git *)",
      "Bash(ls *)",
      "Bash(cat *)",
      "Bash(find *)",
      "Bash(grep *)",
      "Bash(mkdir *)",
      "Bash(cp *)",
      "Bash(mv *)",
      "Read(*)",
      "Write(*)",
      "Edit(*)"
    ]
  },
  "env": {
    "CLAUDE_CODE_AUTO_COMPACT_WINDOW": "400000",
    "CLAUDE_CODE_NO_FLICKER": "1"
  },
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "command": "npx prettier --write $CLAUDE_FILE_PATH || true"
      }
    ],
    "PostCompact": [
      {
        "command": "cat CLAUDE.md"
      }
    ]
  }
}
```

---

## Appendix C: Quick-Start Checklist

After running this guide, verify:

- [ ] `CLAUDE.md` exists in project root with project-specific rules
- [ ] `CLAUDE.local.md` exists and is gitignored
- [ ] `~/.claude/CLAUDE.md` exists with global settings
- [ ] `.claude/settings.json` exists with permissions and hooks
- [ ] `.claude/settings.json` is committed to git
- [ ] `.claude/commands/` has at least: `commit.md`, `code-review.md`
- [ ] `.claude/agents/` has at least: `code-simplifier.md`, `verify-app.md`
- [ ] PostToolUse hook auto-formats on save
- [ ] PostCompact hook re-injects CLAUDE.md
- [ ] `CLAUDE_CODE_AUTO_COMPACT_WINDOW` is set to 400000
- [ ] Verification instructions are in CLAUDE.md
- [ ] Team members can `git pull` and get the full setup immediately

---

## Appendix D: Tip ID Reference

Every instruction in this guide traces back to a specific Boris Cherny tip in [TIPS.md](./TIPS.md). Here is the complete mapping:

| Section | Tip IDs Implemented |
|---------|-------------------|
| 1. CLAUDE.md Setup | #03.01, #03.02, #03.05, #03.07, #03.08, #03.09, #03.10 |
| 2. Settings & Permissions | #07.01, #07.02, #07.03, #07.04, #13.01, #13.03, #13.05, #13.06, #20.01 |
| 3. Slash Commands | #04.01, #04.02, #04.03, #04.04, #04.05, #04.09, #04.10, #04.15, #04.17, #04.23, #04.35 |
| 4. Hooks | #06.01, #06.02, #06.03, #06.05, #06.06, #06.07 |
| 5. Subagents | #05.01, #05.02, #05.03, #05.08, #05.10, #05.11 |
| 6. MCP Integrations | #08.01, #08.06, #08.07 |
| 7. Verification | #10.01, #10.02, #10.03, #10.04, #10.05, #10.07, #10.08 |
| 8. Headless / SDK | #14.01, #14.04, #14.05, #14.06, #14.09 |
| 9. Context Management | #20.01, #20.02, #20.03, #20.04 |
| 10. Automation | #11.01, #11.02, #11.05, #11.06, #04.13, #04.14 |
| **Total** | **~70 tips implemented** |

---

*Generated from [TIPS.md](./TIPS.md) (147 tips, 21 themes) · Version 1.0 · 2026-07-09*
*Part of the [Boris Cherny Claude Code Playbook](https://github.com/SKZL-AI/boris-cherny-claude-code-playbook)*
