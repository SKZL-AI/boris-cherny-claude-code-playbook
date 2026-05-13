---
description: Add a new Boris Cherny tip to TIPS.md with full structured fields
---

# /add-tip — Interactive Tip Addition

You are in the boris-cherny-claude-code-playbook repo. The user wants to add a new tip.

## Workflow

### Step 1 — Ask for Source
Ask: "Where did you find the tip? Please provide a URL or brief description."

Possible sources:
- X/Twitter post (URL provides tweet ID)
- Podcast (which one, with timestamp if available)
- Anthropic Blog (URL)
- Conference talk (which one)
- Secondary source (newsletter, blog) — then verify original

### Step 2 — Verify Source (web_fetch)
Load the URL with web_fetch. Verify:
- Is the author @bcherny (or an Anthropic team member endorsed by Boris)?
- Is it actually a tip / workflow / best practice — not just a status update?
- Identify the date of the post

If the source doesn't fit, say so openly. No tip is fabricated.

### Step 3 — Assign Theme
21 existing themes (list in TIPS.md):
01 Parallel Execution | 02 Plan Mode | 03 CLAUDE.md | 04 Slash Commands |
05 Subagents | 06 Hooks | 07 Permissions & Safety | 08 MCP & Integrations |
09 Model & Effort | 10 Verification | 11 Long-Running & Recaps |
12 Prompting & Specs | 13 Customization | 14 Headless / SDK |
15 Code Review | 16 Cost / ROI | 17 Form-Factor | 18 Migration & Data |
19 Learning & Onboarding | 20 Context Management | 21 Terminal Environment

If none fits: ask the user whether a new theme should be created
(this also requires extending index.html, README.md, and the TOC — a larger refactoring).

### Step 4 — Assemble Fields
Create a draft with all fields, show it to the user for confirmation:

```
### #<TT.NN> — <Title>
- **Difficulty:** <Beginner|Intermediate|Advanced>
- **Date:** <YYYY-MM-DD>
- **Source:** [<Type>](<URL>)
- **Author:** @<author>
- **Quote:** "<optional verbatim, < 15 words>"

<English description, 1–3 sentences.>
```

ID assignment: check the YAML tracker at the bottom of TIPS.md under
`last_tip_id_per_theme."<TT>"` and use N+1.

Difficulty heuristic:
- Beginner: Immediately actionable, no prerequisites, no risk
- Intermediate: Setup needed (config file, hook), or tool combination
- Advanced: Multiple components, custom code, risk if applied incorrectly

### Step 5 — Get User Confirmation
Show the draft and ask: "OK like this? Should I insert it?"

For corrections: iterate. On OK: proceed to Step 6.

### Step 6 — Insert into TIPS.md
- Find the theme section (e.g., `## 04 — Slash Commands`)
- Insert before the next `---` separator line
- Update the YAML tracker at the bottom:
  - Increment `last_tip_id_per_theme."<TT>"`
  - `total_tips` +1

### Step 7 — CHANGELOG Entry
Insert at the top of CHANGELOG.md (below H1):

```
## <YYYY-MM-DD> — Manual Addition (via /add-tip)

- Added tip #<TT.NN>: <Title>
  - Source: <URL>
  - Added by: SAI
```

### Step 7b — Check IMPLEMENTATION-GUIDE.md
Check: Is this tip actionable (can Claude Code execute/configure it)?

Actionable categories:
- CLAUDE.md setup (Theme 03)
- Slash Commands (Theme 04)
- Subagents (Theme 05)
- Hooks (Theme 06)
- Permissions & Safety (Theme 07)
- MCP & Integrations (Theme 08)
- Model & Effort (Theme 09, configuration only)
- Verification (Theme 10, setup patterns only)
- Customization (Theme 13)
- Headless / SDK (Theme 14)
- Context Management (Theme 20)

If yes: Ask the user:
"This tip is actionable. Should I also add it to IMPLEMENTATION-GUIDE.md? (Recommended: yes)"

If yes:
  1. Open IMPLEMENTATION-GUIDE.md
  2. Find the matching section (1–10)
  3. Insert the tip as an executable instruction block
  4. Update the tip ID reference in Appendix D
  5. Add IMPLEMENTATION-GUIDE.md to the suggested commit file list

If no: proceed to Step 8.

### Step 8 — Ask About HTML Sync
Ask: "Should I also update index.html? (Recommended: yes, otherwise the dashboard goes out of sync.)"

If yes: run `/regenerate-html` (see regenerate-html.md).

### Step 9 — Suggest Commit
Do NOT auto-commit — the user commits themselves. But show the suggested commit command:

```bash
git add TIPS.md CHANGELOG.md index.html
git commit -m "Add tip #<TT.NN>: <Title>"
git push
```

## Important

- **No rush.** Better slow and correct than fast and wrong.
- **When in doubt, ask.** For ambiguous sources, unclear difficulty, or borderline tips — ask.
- **Don't fabricate.** If the source doesn't actually contain a tip, end the workflow and explain why.
