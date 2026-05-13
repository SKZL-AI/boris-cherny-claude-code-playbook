---
description: Manually scan X for new Boris Cherny posts since last scan
---

# /scan-x — Manual X Scan

Manual trigger of the X scan when you don't want to wait for the next routine (e.g., after a major Anthropic event).

## Workflow

### Step 1 — Read last_scan_iso
Open TIPS.md, find the YAML block at the bottom:
```yaml
last_scan_iso: "..."
last_scan_anchor_tweet_id: "..."
```
That's the cut-off.

### Step 2 — Multi-Query X Search
Use web_search with the following queries in sequence:
1. `bcherny site:x.com`
2. `bcherny Claude Code`
3. `Boris Cherny Anthropic tip`
4. `site:threadreaderapp.com bcherny`
5. `site:threads.com boris_cherny`
6. `howborisusesclaudecode latest tips`

For each query: filter results by date > `last_scan_iso`.

### Step 3 — Aggregate Candidates
Group the found posts. Per post:
- Tweet ID (or equivalent)
- Date
- Full text (web_fetch if needed)
- Classification: "tip" | "status" | "marketing" | "RT-no-comment"

Only "tip"-classified entries move forward.

### Step 4 — Present to User
Show a compact table:

```
Found since <last_scan_iso>:

| # | Date | Suggested Title | Suggested Theme | Diff | Source |
|---|---|---|---|---|---|
| 1 | 2026-05-XX | ... | 04 Slash Commands | Int | x.com/... |
| 2 | ... | ... | ... | ... | ... |
```

Ask: "Which ones should I add? (1,2,3 / all / none)"

### Step 5 — For Selected Tips: Add Workflow
For each selected candidate: run the `/add-tip` workflow starting from Step 4
(suggest fields → confirmation → insert → CHANGELOG).

### Step 6 — Update Tracking Metadata
At the end of the scan (even if no tips were added):
- Update `last_scan_iso` to now
- Update `last_scan_anchor_tweet_id` to the NEWEST found post
  (not just the added ones — otherwise it would be found again in the next routine)

### Step 7 — HTML Sync
If tips were added: offer `/regenerate-html`.

## Difference from Daily Scan Routine

| | Routine (daily-scan.md) | Slash Command (/scan-x) |
|---|---|---|
| Runs | 2–3× daily automatically | When you trigger it |
| Confirmation | Auto-commit | Manual step per tip |
| Risk | May insert false positives | You see everything first |
| When to use | Normal operation | After major threads, events |

## Edge Cases

- If the routine already ran today and I scan again: same results possible, since `last_scan_iso` is already "ahead." That's OK — it will simply return "no new tips."
- If I add a tip manually before the routine: the routine won't see it as a duplicate, because the tweet anchor is already recorded (once I set `last_scan_anchor_tweet_id`).
