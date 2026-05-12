# CLAUDE.md — Project Instructions

> This file gives Claude Code context about how to work in this repository. It is automatically read at session start.

## What this repo is

A curated, German-language collection of all public Claude Code tips by **Boris Cherny** (Head of Claude Code at Anthropic). Maintained semi-automatically via Claude.ai Routines and Claude Code slash commands.

## File structure (source of truth)

```
.
├── README.md              # Human-facing GitHub front page (narrative)
├── TIPS.md                # ★ SOURCE OF TRUTH ★ — all tips, structured
├── index.html             # Visual dashboard (regenerated from TIPS.md)
├── CHANGELOG.md           # Append-only log of additions/changes
├── IMPLEMENTATION-GUIDE.md # Actionable tips for Claude Code auto-setup (English)
├── CONTRIBUTING.md        # How others contribute
├── data/
│   └── tips-schema.json   # JSON schema for tip entries
├── routines/
│   ├── setup.md           # How to configure Claude.ai Routines
│   ├── daily-scan.md      # Routine prompt for 2–3× daily X scan
│   └── weekly-verify.md   # Routine prompt for weekly URL verification
└── .claude/
    ├── commands/          # Slash commands (add-tip, scan-x, etc.)
    └── agents/            # Subagents (tip-scout)
```

## Critical rules

1. **TIPS.md is the source of truth.** Never edit `index.html` directly to add content — always update `TIPS.md` first, then regenerate via `/regenerate-html`.
2. **Tip IDs are sticky.** Once a tip has ID `04.15`, it keeps that ID forever, even if reordered. New tips get the next free ID in their theme (e.g., `04.35`).
3. **German prose, English source quotes preserved.** All descriptions in German. Verbatim quotes from Boris stay in English, in quotation marks, under 15 words.
4. **Every tip must have a verifiable source URL.** No tips from private sources, leaks, or unverified secondary repostings. If the original X-post is deleted, mark the tip with `[archived]` and link a Wayback Machine snapshot if available.
5. **Difficulty levels are: `beginner`, `intermediate`, `advanced`.** No others.
6. **Dates use `DD. MMM YYYY` format in German** (e.g., `02. Jan 2026`), and `YYYY-MM-DD` in the structured fields for sortability.
7. **IMPLEMENTATION-GUIDE.md tracks actionable tips only.** When adding a tip that Claude Code can execute (settings, commands, hooks, agents, MCP, permissions), also add it to `IMPLEMENTATION-GUIDE.md` in the appropriate section. Non-actionable tips (philosophy, workflow habits, cost/ROI) stay only in `TIPS.md`.

## Tip entry format in TIPS.md

```markdown
### #04.35 — `<short-title>`
- **Difficulty:** Intermediate
- **Theme:** Slash Commands
- **Date:** 2026-05-12 (`12. Mai 2026`)
- **Source:** [X-Thread](https://x.com/bcherny/status/XXXXXXXXXXXXXX)
- **Author:** @bcherny *(or @other if reposted/endorsed by bcherny)*
- **Quote:** "verbatim under 15 words"

DE-Beschreibung: 1–3 Sätze, was der Tipp macht und warum er wichtig ist. Code-Beispiele in `inline code` falls relevant.
```

## Slash commands available

- `/add-tip` — Interactive: walks through fields, validates, inserts into correct theme section in TIPS.md, appends CHANGELOG entry.
- `/scan-x` — Searches X for new bcherny posts since `LAST_SCAN` (stored in CHANGELOG). Returns candidates for human review.
- `/verify-sources` — Crawls all source URLs in TIPS.md, flags 404s or hijacked domains.
- `/regenerate-html` — Rebuilds `index.html` from `TIPS.md`. Preserves the existing design.

See `.claude/commands/` for full prompt definitions.

## Workflow conventions

- **Branch:** Always work on `main`. This is a low-velocity content repo, no PR review needed for new tips (Routine commits directly).
- **Commit messages:** `Add tip #XX.YY: <short-title>` or `Update CHANGELOG / Regenerate HTML`.
- **No code formatting hooks.** This is a content repo.
- **Plan mode is overkill for single-tip additions.** Use it for bulk operations (e.g., reorganizing themes).

## What NOT to do

- ❌ Don't invent tips. If you can't verify it from a source URL, don't add it.
- ❌ Don't paraphrase Boris's quotes into German. Keep the English verbatim.
- ❌ Don't change tip IDs. Even if a tip is deprecated, leave the ID and mark `[deprecated]` in the title.
- ❌ Don't edit `index.html` to add tips. Use `/regenerate-html`.
- ❌ Don't translate technical terms that have no good German equivalent (Worktree, Subagent, Slash Command, Hook). Use the English term in italics.

## When in doubt

Read the most recent entries in [CHANGELOG.md](./CHANGELOG.md) to see what kind of changes happen here. Read 2–3 existing entries in [TIPS.md](./TIPS.md) to match the prose style.

If something is genuinely ambiguous, ask the user via `ask_user_input_v0` or in plain conversation — don't guess.
