# Daily X Scan — Routine Prompt

> **Purpose:** This file contains the exact prompt you copy into a Claude.ai Routine. The routine runs 2-3 times daily, scans X (Twitter) for new Boris Cherny tips, and updates the repo.

> **Before setting up:** First read [setup.md](./setup.md) — it explains which connectors must be enabled (GitHub, web_search).

---

## Recommended Schedule

Boris mainly posts during daytime in San Francisco (PST/PDT = UTC-8/-7). You are in Germany (CET/CEST). The following three scan times cover his posting window:

| Time (CET) | Time in SF | What Boris is typically doing |
|---|---|---|
| **09:00** | 00:00 / 01:00 | His previous day is over — catch late tweets |
| **15:00** | 06:00 / 07:00 | His morning posting window begins |
| **22:00** | 13:00 / 14:00 | His afternoon — usually the most productive phase |

If 3 times is too many, just use **09:00 + 22:00**.

---

## The Routine Prompt (for copying)

Copy everything between the `===` markers into your Claude.ai Routine.

```
=== ROUTINE PROMPT START ===

You are the maintainer of the GitHub repo boris-cherny-claude-code-playbook
(path: github.com/<YOUR-USER>/boris-cherny-claude-code-playbook).

YOUR TASK
Scan public posts by Boris Cherny (@bcherny on X/Twitter, Head of
Claude Code at Anthropic) since the last routine execution. If he
has shared new Claude Code tips, add them to the repo in a structured
format and commit.

STEP 1 — FIND LAST SCAN MARKER
Read the file TIPS.md from the repo, find the YAML block at the end:
  last_scan_iso: "..."
  last_scan_anchor_tweet_id: "..."
This is your "since" point.

STEP 2 — SEARCH X
Use web_search with these queries (in this order):
  1. "bcherny site:x.com"
  2. "bcherny Claude Code tip"
  3. "Boris Cherny new feature Claude Code"
If the direct X search returns nothing (X is often not crawlable),
fall back to secondary sources:
  4. "site:threadreaderapp.com bcherny"
  5. "site:threads.com boris_cherny"
  6. "howborisusesclaudecode.com latest"
Filter: only posts AFTER last_scan_iso. Ignore reposts without new content
(pure likes/retweets without commentary do not count).

STEP 3 — EXTRACT TIPS
For each new tip found, identify:
  - Theme (one of the 21 existing themes, see TIPS.md)
  - Title (short, concise, in English)
  - Difficulty level: beginner | intermediate | advanced
  - Date (post date)
  - Source URL (direct X link)
  - Author (@bcherny or @other if Boris RTs/endorsed)
  - Quote (optional, verbatim Boris quote under 15 words, in quotes)
  - Description (1-3 sentences, in English, what the tip does and why it matters)

RULES for extraction:
  - Only tips with concrete actionable value. No pure status updates
    ("Working on something cool"). No marketing posts.
  - Only if Boris himself posts it OR an Anthropic team member
    (Cat Wu, Thariq, Erik Schluntz, Noah Z.) AND Boris has retweeted/
    endorsed it. The latter is verifiable via his replies/retweets.
  - If the tip improves/updates an already existing tip in the repo:
    DO NOT create a new one, instead update the existing one
    (see Step 4b).
  - If you are unsure whether a tip is truly new/valuable:
    DO NOT add it. Better to leave it for human review in the
    weekly-verify slot.

STEP 4a — ADD TIP
For each confirmed new tip:
  - Open TIPS.md
  - Find the correct theme section (e.g. "## 04 — Slash Commands")
  - Find the next free ID number in this section: look in the
    YAML tracker at the end of TIPS.md under last_tip_id_per_theme: "04": N
    — new ID is N+1, e.g. "04.35"
  - Insert the tip at the end of the theme section, in the exact format:

### #<TT.NN> — <Title>
- **Difficulty:** <Beginner|Intermediate|Advanced>
- **Date:** <YYYY-MM-DD>
- **Source:** [<Source-Type>](<URL>)
- **Author:** @<author>
- **Quote:** "<verbatim, optional, under 15 words>"

<English description in 1-3 sentences.>

  - Update in the YAML tracker at the end of TIPS.md:
    last_tip_id_per_theme."<TT>" = N+1 (or higher if multiple new ones)
    total_tips: +1 per new tip

STEP 4b — UPDATE TIP (if extended)
If the new post extends an existing feature/tip:
  - Edit the existing entry in TIPS.md
  - ID stays the same
  - Add to the description with "Update (<YYYY-MM-DD>): <what is new>"

STEP 5 — UPDATE TRACKING METADATA
At the end of TIPS.md, in the YAML block:
  - last_scan_iso: current time in ISO 8601, e.g. "2026-05-12T22:00:00Z"
  - last_scan_anchor_tweet_id: ID of the newest post found
    (even if no new tips were extracted from it — important for
    the next routine, to avoid reprocessing the same post)

STEP 6 — UPDATE CHANGELOG.MD
Open CHANGELOG.md, insert a new section at the top (under the H1):

## <YYYY-MM-DD> — Routine Scan

- Added tip #<TT.NN>: <Title> (Source: <URL-Domain>)
- Updated tip #<TT.NN>: <what changed>
- Scan completed. Anchor: <tweet-id>

If NO new tips were found, write only:

## <YYYY-MM-DD> — Routine Scan (no changes)

- Scanned <N> sources, no new tips since <last_anchor>

STEP 7 — SYNC INDEX.HTML
If Step 4a/4b made changes:
  - Open index.html
  - For EACH new tip in TIPS.md, find the corresponding
    <section class="theme-section" id="t<NN>"> in index.html
  - Add a new <article class="tip" data-diff="<difficulty>"> element
    at the end of the <div class="tip-grid"> in that section
  - Article format (replicate exactly, pattern from existing tips):

<article class="tip" data-diff="<difficulty>">
  <div class="tip-meta">
    <span class="tip-num"><TT.NN></span>
    <span class="diff diff-<difficulty>"><Difficulty></span>
  </div>
  <h3><Title></h3>
  <p><Description. <code>code</code> for inline code.></p>
  <div class="tip-footer">
    <span><DD. MMM YYYY></span>
    <a class="tip-source" href="<URL>" target="_blank">Source ↗</a>
  </div>
</article>

  - Update in the <header> the number "87+ Tips" to the new total
  - Update in the <footer> "Last full audit" to the current date

STEP 8 — UPDATE README.MD TABLE
In README.md, in the "The 21 Themes at a Glance" table, update
the tip count for the affected theme(s).

STEP 8b — SYNC IMPLEMENTATION-GUIDE.MD
If the new tip falls into one of the following categories:
  - CLAUDE.md configuration (Theme 03)
  - Slash Commands (Theme 04, new command or new pattern)
  - Subagents (Theme 05, new agent or pattern)
  - Hooks (Theme 06, new hook type or pattern)
  - Permissions & Safety (Theme 07, new setting)
  - MCP & Integrations (Theme 08, new integration)
  - Model & Effort (Theme 09, new configuration)
  - Verification (Theme 10, new verification pattern)
  - Customization (Theme 13, new setting)
  - Headless / SDK (Theme 14, new CLI flag or pattern)
  - Context Management (Theme 20, new strategy)

Then:
  1. Open IMPLEMENTATION-GUIDE.md
  2. Find the appropriate section (1-10 or Appendix)
  3. Insert the new tip as an executable instruction block
     (imperative mode: "Create...", "Add...", "Configure...")
  4. Update the tip ID reference in Appendix D
  5. Add IMPLEMENTATION-GUIDE.md to the commit file list

If the tip is NOT actionable (e.g. philosophy, ROI, form factor,
personal preference, terminal environment): DO NOT modify
IMPLEMENTATION-GUIDE.md.

STEP 9 — COMMIT & PUSH
Use the GitHub connector:
  - Branch: main
  - Commit message format:
    - For new tips: "Add <N> tip(s) from <YYYY-MM-DD> scan"
    - For updates: "Update tip(s) from <YYYY-MM-DD> scan"
    - For nothing found: "Routine scan <YYYY-MM-DD> (no changes)"
  - Files to commit: TIPS.md, CHANGELOG.md, index.html, README.md
    (only those actually changed)

STEP 10 — BRIEF SUMMARY
Write a brief status message to SAI (me):
  - How many tips found
  - Which IDs added
  - Direct link to the commit
  - If nothing found: simply "No new tips since <last>. Scan OK."

EDGE CASES — DO NOT DO THIS
  - DO NOT fabricate. If you find no real new posts, that is OK.
    Honestly write "no new tips".
  - DO NOT add tips from before last_scan_iso again.
  - DO NOT add tips from other people unless Boris has explicitly
    endorsed them.
  - DO NOT commit code directly to index.html without a corresponding
    TIPS.md update — TIPS.md is the source of truth.
  - DO NOT delete the YAML tracking metadata at the end of TIPS.md.
  - DO NOT commit to any branch other than main.
  - DO NOT silently fail on rate-limit errors or access problems with
    the GitHub connector — report explicitly and finish without committing.

WHEN UNCLEAR
Ask me a question rather than guessing:
  - "I found a post that sounds like a tip, but Boris only liked it
    (did not retweet). Should I include it?"
  - "Tip #04.32 might be made obsolete by this new post. Update
    or new entry?"

On a fully successful run: no question needed.

=== ROUTINE PROMPT END ===
```

---

## How to Verify the Setup

After the first run, check:

1. CHANGELOG.md has a new entry for today
2. TIPS.md `last_scan_iso` is updated
3. Git log shows a commit from the routine
4. index.html shows the new date in the footer

If yes: the routine is working. If not: see [Troubleshooting in setup.md](./setup.md#troubleshooting).

---

## Customization for Your Use Case

If your repo is at a different path, replace in the prompt:
- `github.com/<YOUR-USER>/boris-cherny-claude-code-playbook` with your actual path

If you want to scan additional secondary sources, extend Step 2 with:
- `site:newsletter.pragmaticengineer.com bcherny`
- `site:every.to "Boris Cherny"`
- `site:latent.space "Boris Cherny"`

If you want the repo to be private: the routine still needs write access via the GitHub connector. A private repo is fine.

---

## What Happens on Errors

Claude.ai Routines automatically retry on transient errors. For permanent errors (connector token expired, branch protection, schema drift) you will be notified.

**Manual debugging:** You can "manually trigger" the routine at any time via the Routine Dashboard, using the same prompt but as a one-shot.

**Emergency stop:** Pause the routine in the Dashboard. The latest commits remain; nothing is rolled back.
