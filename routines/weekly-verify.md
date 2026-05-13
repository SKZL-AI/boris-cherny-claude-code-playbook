# Weekly Verify — Routine Prompt

> **Purpose:** Once a week, check all source URLs in TIPS.md, detect duplicates, and consolidate tracking metadata.

> This routine complements [daily-scan.md](./daily-scan.md) — it does NOT add new tips; it only maintains what is already there.

---

## Recommended Schedule

**Sunday 10:00 CET** — Cron: `0 9 * * 0` (UTC in winter) / `0 8 * * 0` (UTC in summer)

Once per week is sufficient. Running it more often is not worthwhile — URLs die slowly.

---

## The Routine Prompt (Copy-Paste Ready)

```
=== WEEKLY VERIFY ROUTINE START ===

You are the maintainer of the GitHub repo boris-cherny-claude-code-playbook.

YOUR TASK
Weekly maintenance of the repo. Three subtasks:
  A) Verify source URLs (are they still reachable?)
  B) Detect duplicates (do two tips share the same source or identical content?)
  C) Consolidate tracking metadata in TIPS.md

Do NOT add new tips. That is the job of the Daily Scan routine.

PART A — URL VERIFICATION

1. Read TIPS.md in its entirety.
2. Extract all source URLs (Markdown format: [text](url)).
3. For each URL: web_fetch with text_content_token_limit=500
   (we only need the header, not the full content).
4. Classify:
   - OK (200, normal content)
   - GONE (404, 410, or explicit "deleted"/"suspended" content)
   - REDIRECT (301/302 to a different domain → note it)
   - PRIVATE (X account locked etc. — mark the tip, do not delete it)

5. For GONE URLs:
   - Search archive.org Wayback Machine for a snapshot:
     web_fetch("https://web.archive.org/web/*/<ORIGINAL_URL>")
   - If a snapshot exists: replace the URL in TIPS.md with
     the archive.org version. Add a note in the description:
     "[Original tweet deleted, archive.org snapshot]".
   - If no snapshot exists: mark the tip with "[archived]" in the title
     (Format: "### #04.15 — [archived] /btw for side-chain conversations")
     and add "Original source no longer available." to the description.

6. For REDIRECT URLs:
   - If redirecting to a legitimate Anthropic/X domain: update the URL.
   - If redirecting to spam/domain squatter: treat as GONE.

PART B — DUPLICATE DETECTION

1. Group all tips by source URL.
2. If 2+ tips share the same URL:
   - Check the descriptions — are they truly different?
   - If yes: OK (a single thread can contain multiple tips).
   - If no: identify the canonical tip (oldest ID).
     Mark the other with "[duplicate of #XX.YY]" in the title and
     add a note in the description. Do NOT delete entirely (IDs
     remain sticky).
3. Group all tips by title similarity (e.g., both contain
   "/loop"). If different themes but same substance:
   flag for human review (no auto-merge).

PART C — CONSOLIDATE TRACKING METADATA

At the end of TIPS.md in the YAML block:
1. Recount total_tips (real count, excluding [archived]/[duplicate]).
2. Update last_tip_id_per_theme: highest assigned ID per theme.
3. Set last_verify_iso: current time in ISO 8601.
4. If last_verify_iso does not yet exist, create it.

PART D — IMPLEMENTATION-GUIDE.MD CONSISTENCY CHECK

1. Read IMPLEMENTATION-GUIDE.md in its entirety.
2. For each referenced tip ID (#XX.YY) in the file:
   - Check whether the ID still exists in TIPS.md and is active
   - If [archived] or [deprecated]: mark the entry in
     IMPLEMENTATION-GUIDE.md with "[archived]" or remove it
3. Count the actionable tips in the guide vs. the actual number of
   actionable tips in TIPS.md (heuristic: themes 03-08, 10, 13, 14, 20
   are predominantly actionable)
4. If the difference is > 5: flag for manual review
5. Add a report line (see REPORT FORMAT below):
   - IMPL-GUIDE tips referenced: <N>
   - IMPL-GUIDE stale references: <N>

REPORT FORMAT

Write a new section at the top of CHANGELOG.md (below the H1):

## <YYYY-MM-DD> — Weekly Verify

- ✅ URLs verified: <N OK> / <N total>
- ⚠️ URLs migrated to archive.org: <N> (Tips: #XX.YY, #XX.YY)
- 🚫 URLs marked [archived] (no snapshot): <N> (Tips: #XX.YY)
- 🔁 Duplicates flagged: <N> (Tips: #XX.YY)
- 📊 Total active tips: <N>

If everything is clean:

## <YYYY-MM-DD> — Weekly Verify (clean)

- ✅ All <N> URLs reachable
- ✅ No duplicates detected
- 📊 Total tips: <N>

COMMIT

- Files: TIPS.md, CHANGELOG.md (only if changes were made)
- Commit message: "Weekly verify <YYYY-MM-DD>: <N> changes"
  or: "Weekly verify <YYYY-MM-DD>: clean"
- Branch: main

EDGE CASES

- If a tip has been archived/duplicated multiple times: do not
  modify further, manual review required. Mention it in the CHANGELOG
  section under "🔧 Needs manual review:".
- If web_fetch persistently fails (rate limit, captcha): abort
  Part A after 10 failures. Still proceed with Parts B and C.
- If TIPS.md is syntactically broken (corrupted Markdown structure):
  do NOT commit. Instead, alert with a clear description of
  where the damage is.

=== WEEKLY VERIFY ROUTINE END ===
```

---

## What This Routine Does NOT Do

- **Does not add new tips** — that is the job of the Daily Scan routine.
- **Does not update index.html** — when there are changes in TIPS.md, the HTML sync runs automatically during the next Daily Scan.
- **Does not update the README** — the README table is only updated when theme counts change, which happens via Daily Scan.

## Why a Separate Routine

Separation of concerns:
- Daily Scan = "find new stuff" (with risk of false positives)
- Weekly Verify = "validate existing stuff" (purely read-modify, no risk of new content)

If one of the two becomes buggy, you can keep the other one running.

## Known Special Cases for Boris's Sources

- **threadreaderapp.com** mirrors are often updated more slowly. If the original tweet exists but the mirror is down, that is NOT a GONE case.
- **threads.com** (Meta's Threads mirror of his X posts): Sometimes posts are deleted there but not in the original. Cross-reference.
- **howborisusesclaudecode.com**: Fan site, not Anthropic. If tips are missing there that exist in the repo: do not delete.
- **AIEWF Talk 2025**: Only archived as a YouTube video. If the video is gone, there are often still audio transcripts available. Use those.
