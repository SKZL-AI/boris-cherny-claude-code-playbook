# Changelog

All content changes to the repo are documented here — manual edits, routine scans, and verification runs.

Newest entries first.

---

## 2026-05-24 — Routine Scan (no changes)
- Scanned 6 sources (x.com/bcherny, threadreaderapp.com/user/bcherny, howborisusesclaudecode.com, threads.com/@boris_cherny, bcherny Claude Code 2026, boris cherny claude code announcement May 24 2026), no new tips since anchor `2056755719941062919`
- All discovered tweet IDs ≤ anchor `2056755719941062919`; no @bcherny posts after scan cutoff
- Scan completed. Anchor unchanged: `2056755719941062919`

---

## 2026-05-23 — Routine Scan (no changes)
- Scanned 6 sources (x.com/bcherny, threadreaderapp.com/user/bcherny, howborisusesclaudecode.com, threads.com/@boris_cherny, simonwillison.net code-w-claude-2026, bcherny Claude Code May 2026), no new tips since anchor `2056755719941062919`
- No Boris tweet IDs higher than current anchor detected; "Code with Claude" London event (May 19–21) already captured in previous scans
- Scan completed. Anchor unchanged: `2056755719941062919`

---

## 2026-05-22 — Routine Scan (no changes)
- Scanned 6 sources (x.com/bcherny, threadreaderapp.com/user/bcherny, howborisusesclaudecode.com, threads.com/@boris_cherny, simonwillison.net code-w-claude-2026, bcherny Claude Code tip May 2026), no new tips since anchor `2056755719941062919`
- All discovered tweet IDs ≤ anchor `2056755719941062919`; no posts from Boris Cherny after last scan cutoff
- Scan completed. Anchor unchanged: `2056755719941062919`

---

## 2026-05-22 — Routine Scan (no changes)
- Scanned 8 sources (x.com/bcherny, threadreaderapp.com/user/bcherny, howborisusesclaudecode.com, simonwillison.net code-w-claude-2026, MIT Technology Review, Lenny's Newsletter, bcherny Claude Code tip May 2026, threads.com/@boris_cherny), no new tips since anchor `2056755719941062919`
- No Boris tweet IDs higher than current anchor detected across all sources (~36h since last scan)
- Scan completed. Anchor unchanged: `2056755719941062919`

---

## 2026-05-21 — Routine Scan (no changes)
- Scanned 6 sources (x.com/bcherny, threadreaderapp.com/user/bcherny, howborisusesclaudecode.com, simonwillison.net code-w-claude-2026, MIT Technology Review May 21, bcherny Claude Code tip May 2026), no new tips since anchor `2056755719941062919`
- No Boris tweet IDs higher than current anchor detected across all sources
- All found tweet IDs ≤ anchor; Code Review / /btw / /simplify / /batch / Routines / Auto-Dream already captured in prior scans
- Scan completed. Anchor unchanged: `2056755719941062919`

---

## 2026-05-21 — Routine Scan (no changes)
- Scanned 8 sources (x.com/bcherny, threadreaderapp.com/user/bcherny, howborisusesclaudecode.com, borischerny.com, Code with Claude Extended London recap, InfoQ code-with-claude, simonwillison.net live blog, bcherny Claude Code tip May 2026), no new tips since anchor `2056755719941062919`
- No Boris tweet IDs higher than current anchor detected across all sources
- Scan completed. Anchor unchanged: `2056755719941062919`

---

## 2026-05-20 — Manual Scan (no changes)
- Scanned 6 sources (x.com/bcherny, threadreaderapp.com, howborisusesclaudecode.com, Code w/ Claude 2026 conference, CNBC May 20 interview, Claude Code changelog), no new tips since anchor `2056755719941062919`
- Conference keynote (May 19, London) referenced Agent View, /goal, and Routines — all launched in Week 20 (May 11–15) and already captured in prior scans; no new Boris X posts found
- No Boris tweet IDs higher than current anchor detected across all sources
- Scan completed. Anchor unchanged: `2056755719941062919`

---

## 2026-05-20 — Routine Scan (no changes)
- Scanned 6 sources (x.com/bcherny, threadreaderapp, howborisusesclaudecode.com, medium, venturebeat, pasqualepillitteri.it), no new tips since anchor `2044847848035156457`
- 4 posts found after last anchor: event greetings (Code with Claude London), stickers promo, and one pure RT (@ClaudeDevs /radio) — none meet tip criteria
- Managed Agents features (Dreaming, Outcomes, Multiagent Orchestration) announced at Code with Claude London via official Anthropic blog, not Boris's personal X — excluded per sourcing rules
- Scan completed. New anchor: `2056755719941062919`

---

## 2026-05-13 — Implementation Guide + GitHub Launch

- 🆕 **IMPLEMENTATION-GUIDE.md** created: ~70 actionable tips from TIPS.md as executable Claude Code instructions. 10 sections: CLAUDE.md Setup, Settings & Permissions, Slash Commands, Hooks, Subagents, MCP Integrations, Verification, Headless/SDK, Context Management, Automation. Plus 4 appendices (Env Vars, Settings Template, Checklist, Tip ID Reference). Language: English.
- 📝 **README.md** overhauled: Tip count fixed to 132, badges (Tips/Themes/Auto-Updated/License), English 2-line hook, 30-second quick-start (3 options), "Why This Repo?" section, IMPLEMENTATION-GUIDE.md in table of contents, star CTA at bottom, GitHub URLs updated to SKZL-AI.
- 📝 **CLAUDE.md** expanded: IMPLEMENTATION-GUIDE.md added to file structure, Rule 7 added (sync actionable tips to IMPLEMENTATION-GUIDE.md).
- 🤖 **Routines updated:**
  - `routines/daily-scan.md`: STEP 8b added — IMPLEMENTATION-GUIDE.md sync (when new tip is actionable, auto-add to guide)
  - `routines/weekly-verify.md`: PART D added — IMPLEMENTATION-GUIDE.md consistency check (validate tip IDs, flag stale references)
  - `.claude/commands/add-tip.md`: Step 7b added — actionable check on manual tip addition with offer to also add to IMPLEMENTATION-GUIDE.md
- 🚀 **GitHub Launch:** Public repo at github.com/SKZL-AI/boris-cherny-claude-code-playbook, topics, GitHub Pages, description.
- 🌐 **Full English translation:** All files translated from German to English for international accessibility.

---

## 2026-05-12 — Initial Release

- 🎉 **Repo created** with 132 tips across 21 themes
- 📁 Structure: `TIPS.md` (Source of Truth), `README.md` (GitHub front page), `index.html` (Dashboard), `routines/` (Automation), `.claude/` (Slash Commands & Subagents)
- 🤖 Automation set up:
  - `routines/daily-scan.md` — 2–3x daily X scan
  - `routines/weekly-verify.md` — Weekly URL health check
  - `.claude/commands/add-tip.md` — Manual tip addition
  - `.claude/commands/scan-x.md` — Manual X scan
  - `.claude/commands/verify-sources.md` — Local URL check
  - `.claude/commands/regenerate-html.md` — Rebuild HTML from TIPS.md
  - `.claude/agents/tip-scout.md` — Subagent for X scanning
- 📊 Initial tracking metadata set in TIPS.md:
  - `last_scan_iso: 2026-05-12T20:00:00Z`
  - `total_tips: 132`

### Initial Tip Distribution

| Theme | Tips |
|---|---:|
| 01 Parallel Execution | 9 |
| 02 Plan Mode | 6 |
| 03 CLAUDE.md | 11 |
| 04 Slash Commands | 34 |
| 05 Subagents | 12 |
| 06 Hooks | 9 |
| 07 Permissions & Safety | 7 |
| 08 MCP & Integrations | 7 |
| 09 Model & Effort | 9 |
| 10 Verification | 11 |
| 11 Long-Running & Recaps | 6 |
| 12 Prompting & Specs | 6 |
| 13 Customization | 6 |
| 14 Headless / SDK | 10 |
| 15 Code Review | 3 |
| 16 Cost / ROI | 5 |
| 17 Form Factor | 6 |
| 18 Migration & Data | 3 |
| 19 Learning & Onboarding | 5 |
| 20 Context Management | 5 |
| 21 Terminal Environment | 3 |
| **Total** | **132** |

### Primary Sources for Initial Research

- [@bcherny on X](https://x.com/bcherny) — Main channel
- [howborisusesclaudecode.com](https://howborisusesclaudecode.com) (Fan aggregator)
- [Latent Space Podcast](https://www.latent.space/p/claude-code) (May 2025)
- [Lenny's Podcast](https://www.lennysnewsletter.com/p/head-of-claude-code-what-happens) (Feb 2026)
- [AI & I Podcast](https://every.to/podcast/how-to-use-claude-code-like-the-people-who-built-it) (Nov 2025)
- [Pragmatic Engineer Newsletter](https://newsletter.pragmaticengineer.com/p/building-claude-code-with-boris-cherny) (Feb 2026)
- [Anthropic Engineering Blog](https://www.anthropic.com/engineering/claude-code-best-practices) (Apr 2025)
- AI Engineer World's Fair Keynote (Jun 2025)

### Notes

- Tip IDs are **sticky** from this point forward. Even deprecated tips keep their ID and are only marked with `[deprecated]` in the title.
- The next verify routine (Sunday) will check URL health — expecting 100% OK at initial release.
- The first daily scan routine runs the day after deployment; should return "no new tips" if nothing posted in the last 24h.

---

*Format convention for future entries: see `routines/daily-scan.md` and `routines/weekly-verify.md`.*
