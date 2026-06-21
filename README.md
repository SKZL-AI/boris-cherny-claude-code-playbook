![Tips](https://img.shields.io/badge/Tips-144-blue)
![Themes](https://img.shields.io/badge/Themes-21-green)
![Auto-Updated](https://img.shields.io/badge/Auto--Updated-2--3x%20daily-orange)
![License](https://img.shields.io/badge/License-MIT-yellow)

> **144 tips from the Head of Claude Code at Anthropic — auto-updated daily.**
> *Feed the [Implementation Guide](./IMPLEMENTATION-GUIDE.md) to Claude Code and auto-configure your project in one shot.*

# Boris Cherny Claude Code Playbook

> A curated collection of all public Claude Code tips by **Boris Cherny** ([@bcherny](https://x.com/bcherny)), Head of Claude Code at Anthropic — automatically updated via Claude.ai Routines.

**[View Visual Dashboard (index.html)](./index.html)** &nbsp; · &nbsp; **[Full Tip List (TIPS.md)](./TIPS.md)** &nbsp; · &nbsp; **[One-Shot Setup Guide (IMPLEMENTATION-GUIDE.md)](./IMPLEMENTATION-GUIDE.md)** &nbsp; · &nbsp; **[Changelog](./CHANGELOG.md)**

---

## Quick Start in 30 Seconds

### Option 1: Auto-configure everything
```bash
git clone https://github.com/SKZL-AI/boris-cherny-claude-code-playbook.git
cd boris-cherny-claude-code-playbook
# Feed the implementation guide to Claude Code:
cat IMPLEMENTATION-GUIDE.md | claude -p "Execute all setup instructions for my project"
```

### Option 2: Just read
Open [index.html](./index.html) locally in your browser — or read [TIPS.md](./TIPS.md).

### Option 3: Cherry-pick individual tips
Open [IMPLEMENTATION-GUIDE.md](./IMPLEMENTATION-GUIDE.md) and copy the sections you need.

---

## Why This Repo?

1. **First complete collection** of all public Boris Cherny tips in one place — 144 tips, 21 themes
2. **Automatically up-to-date** — Claude.ai Routines scan for new tips 2–3x daily
3. **Instantly actionable** — [IMPLEMENTATION-GUIDE.md](./IMPLEMENTATION-GUIDE.md) lets Claude Code configure your project in minutes
4. **Visual dashboard** — Filters, timeline, difficulty levels at a glance
5. **Structured & searchable** — Every tip tagged by theme, difficulty, date, and source

---

## What This Is About

Boris Cherny started Claude Code in September 2024 as a side project at Anthropic. Since the public launch on February 24, 2025, he has regularly shared tips, workflows, and best practices — on X/Twitter, in podcasts (Latent Space, Lenny's Podcast, AI & I, Pragmatic Engineer), at conferences (AI Engineer World's Fair), and on the Anthropic Engineering Blog.

This repo collects those tips in one place, classifies them by difficulty and theme, and keeps them current through automated X scans.

**Current:** 144 tips across 21 themes, documented over 14 months.

---

## TL;DR — Boris' Setup in Three Sentences

1. **Verification is the #1 rule:** "Give Claude a way to verify its work — it will 2–3x the quality." If you take away only one thing, make it this.
2. **Parallelism is the biggest lever:** 5 Claudes in terminal tabs + 5–10 web sessions + mobile + worktrees. "I have dozens of Claudes running at all times."
3. **Plan Mode → Auto-Accept:** Shift+Tab twice, iterate the plan with Claude, then let it run. A good plan one-shots the implementation almost every time.

---

## Contents

- **[TIPS.md](./TIPS.md)** — All 144 tips, structured by theme and difficulty. Source of truth for automation.
- **[IMPLEMENTATION-GUIDE.md](./IMPLEMENTATION-GUIDE.md)** — ~70 actionable tips structured as executable instructions for Claude Code. One-shot setup.
- **[index.html](./index.html)** — Visual dashboard with filters, timeline, stages, and caveats. Open locally or host on GitHub Pages.
- **[CHANGELOG.md](./CHANGELOG.md)** — Which tips were added when.
- **[CONTRIBUTING.md](./CONTRIBUTING.md)** — How to contribute tips.
- **[routines/](./routines/)** — Setup guide and prompts for Claude.ai Routines that auto-update the repo.
- **[.claude/](./.claude/)** — Slash commands and subagents for local work with Claude Code.

---

## All 21 Themes at a Glance

| # | Theme | Tips | Boris' Core Insight |
|---|---|---:|---|
| 01 | Parallel Execution | 9 | "The single biggest productivity unlock" |
| 02 | Plan Mode | 6 | "A good plan is really important" |
| 03 | CLAUDE.md | 11 | "Anytime Claude does something wrong, we add it to the CLAUDE.md" |
| 04 | Slash Commands | 34 | Inner-loop automation for daily workflows |
| 05 | Subagents | 12 | Uncorrelated context windows, not anthropomorphization |
| 06 | Hooks | 9 | Deterministic logic where the model is unreliable |
| 07 | Permissions & Safety | 7 | Pre-allow > skip; Sandbox > danger flag |
| 08 | MCP & Integrations | 7 | Slack, BigQuery, Sentry — Claude beyond the repo |
| 09 | Model & Effort | 9 | Opus with Thinking for everything (Boris) |
| 10 | Verification | 11 | **The #1 rule: 2–3x quality through verification** |
| 11 | Long-Running & Recaps | 6 | Routines, Schedules, Stop Hooks |
| 12 | Prompting & Specs | 6 | Delegation > Guidance |
| 13 | Customization | 6 | 37 settings, 84 env variables |
| 14 | Headless / SDK | 10 | Claude as a Unix utility |
| 15 | Code Review | 3 | "Reviews were the bottleneck" |
| 16 | Cost / ROI | 5 | "It's an ROI question, not a cost question" |
| 17 | Form Factor | 8 | CLI, IDE, GitHub, Slack, Mobile, Web |
| 18 | Migration & Data | 3 | Finish what you start |
| 19 | Learning & Onboarding | 5 | Explanatory Output Style |
| 20 | Context Management | 5 | Context rot at 300–400k tokens |
| 21 | Terminal Environment | 3 | Ghostty + tmux + Voice |

---

## Staged Adoption — Boris' Own Recommendation

| Phase | When | What to Do |
|---|---|---|
| **1. Vanilla** | Week 1 | `/init`, Plan Mode, no customization |
| **2. Compounding Knowledge** | Week 2–3 | Build CLAUDE.md, 1–2 slash commands |
| **3. Parallelism** | Week 4+ | 3–5 worktrees, PostToolUse hook, shared settings.json |
| **4. Subagents** | Month 2+ | code-simplifier, verify-app, adversarial review |
| **5. Autonomy** | Month 3+ | Auto Mode, `/loop`, `/schedule`, Voice, Chrome Extension |

Details and graduation criteria in [index.html](./index.html) or [TIPS.md](./TIPS.md).

---

## Key Timeline

- **Sep 2024** — Boris starts Claude Code as a side project
- **Feb 24, 2025** — Claude Code public launch (Research Preview)
- **Jan 2, 2026** — Canonical 13-tip thread "How I use Claude Code" (104K likes)
- **Jan 31, 2026** — 10 team tips thread (8.5M views)
- **Mar 29–30, 2026** — 15 hidden features thread
- **Apr 16, 2026** — 6 Opus 4.7 tips thread
- **Apr 22, 2026** — Claude Code wins Webby Award

Full timeline in [index.html](./index.html) or [CHANGELOG.md](./CHANGELOG.md).

---

## How This Repo Stays Current

A **Claude.ai Routine** scans [@bcherny on X](https://x.com/bcherny) and secondary sources (Threads.net, Anthropic Blog, Threadreader mirrors) 2–3x daily for new tips. When new ones are found:

1. Tip is inserted into [`TIPS.md`](./TIPS.md) (correct theme section, new ID)
2. [`CHANGELOG.md`](./CHANGELOG.md) is updated
3. [`index.html`](./index.html) is synced via `/regenerate-html` slash command
4. [`IMPLEMENTATION-GUIDE.md`](./IMPLEMENTATION-GUIDE.md) is updated if the tip is actionable
5. Commit + push to GitHub via GitHub Connector

Setup guide: **[routines/setup.md](./routines/setup.md)**
Routine prompts: **[routines/daily-scan.md](./routines/daily-scan.md)** and **[routines/weekly-verify.md](./routines/weekly-verify.md)**

---

## How to Use This

### As a Reader

Open [`index.html`](./index.html) locally in your browser — filter by difficulty, jump to themes, all sources linked.

### As a Claude Code User

```bash
git clone https://github.com/SKZL-AI/boris-cherny-claude-code-playbook.git
# Copy IMPLEMENTATION-GUIDE.md into your own project and run it:
cp boris-cherny-claude-code-playbook/IMPLEMENTATION-GUIDE.md my-project/
cd my-project
claude  # Open Claude Code
> Read IMPLEMENTATION-GUIDE.md and execute the setup instructions
```

### As a Fork Maintainer

```bash
git clone https://github.com/SKZL-AI/boris-cherny-claude-code-playbook.git
cd boris-cherny-claude-code-playbook
claude  # Open Claude Code
> /add-tip
```

Slash Commands:

- `/add-tip` — Add a new tip interactively (walks you through step by step)
- `/scan-x` — Manual X scan for new tips
- `/verify-sources` — Check all source URLs
- `/regenerate-html` — Rebuild `index.html` from `TIPS.md`

See [`.claude/commands/`](./.claude/commands/) for full prompt definitions.

---

## Caveats

- **Plan-tier gating:** Many features (Auto Mode, 1M context) are Max/Team/Enterprise only. Test, don't assume.
- **Directional numbers:** "4% of all GitHub commits", "200% engineering productivity" are Boris' own claims from podcasts, not independently audited.
- **Secondary sources:** Tips attributed to Thariq, Cat Wu, Erik Schluntz, and other Claude Code team members are included only when Boris retweeted/endorsed them.
- **No content** in this repo comes from private or leaked sources. Everything from public X, podcasts, Anthropic Blog, or Threads.net mirrors.
- **Ultrathink semantics** changed between CC v1 and v2 — see [TIPS.md](./TIPS.md) for details.

---

## Attribution

All tips originate from **Boris Cherny** (Anthropic) and the Claude Code team. This repo is an unofficial curation. Not affiliated with Anthropic.

Primary source aggregator: [howborisusesclaudecode.com](https://howborisusesclaudecode.com) (by [@CarolinaCherry](https://x.com/CarolinaCherry)).

## License

MIT (see [LICENSE](./LICENSE)). The underlying tips are intellectual property of their respective authors. This curation may be freely copied and adapted, provided source attributions are retained.

---

If this repo helps you, [give it a star](https://github.com/SKZL-AI/boris-cherny-claude-code-playbook) — it helps others find it.

---

*Maintained by [SKZL-AI](https://github.com/SKZL-AI) · Last full audit: 2026-06-02*
