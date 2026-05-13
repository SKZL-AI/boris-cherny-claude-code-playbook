---
description: Verify all source URLs in TIPS.md are still reachable
---

# /verify-sources — URL Health Check

Goes through all source URLs in TIPS.md and checks whether they are still reachable.

Local equivalent of the weekly-verify.md routine, but on-demand and interactive.

## Workflow

### Step 1 — Extract URLs
Read TIPS.md. Extract all source URLs using regex `\[.+?\]\((https?://[^)]+)\)`.
Dedupe (one URL can cover multiple tips — threads).

### Step 2 — Fetch in Parallel
Use web_fetch with `text_content_token_limit=500` (we only want the header, not the full content). If possible, batch multiple in parallel.

Per URL: classify
- ✅ OK (200, normal content)
- ⚠️ REDIRECT (301/302, new URL)
- 🚫 GONE (404, 410, or content says "deleted"/"suspended")
- 🔒 PRIVATE (X account locked/suspended)
- ❓ UNCLEAR (rate limit, captcha, other transient issues)

### Step 3 — Report
Show table:

```
| URL | Status | Tips |
|---|---|---|
| x.com/bcherny/status/... | ✅ OK | #01.01, #04.01, ... |
| x.com/bcherny/status/... | 🚫 GONE | #05.07 |
| x.com/bcherny/status/... | ⚠️ REDIRECT → archive.org | #11.05 |
```

### Step 4 — Suggest Actions
For each problematic URL, ask:

**GONE:**
"Tip #05.07 has a deleted source. Check Wayback Machine? (y/n)"
- If yes: web_fetch `https://web.archive.org/web/*/<original-url>` → find latest snapshot
- If snapshot found: replace URL in TIPS.md, add "[archive.org snapshot]" to description
- If no snapshot: mark with `[archived]` in the title

**REDIRECT:**
"Tip #11.05 redirected. New URL: <new>. Update? (y/n)"

**PRIVATE / UNCLEAR:**
Report only, don't modify. Manual review needed.

### Step 5 — Summary
```
✅ 132 URLs checked
✅ 128 OK
⚠️ 2 REDIRECT → updated
🚫 1 GONE → archive.org snapshot inserted
🔒 1 PRIVATE → manual review
```

### Step 6 — Suggest Commit
If changes were made: suggest commit command
```bash
git add TIPS.md
git commit -m "Verify sources: <N> URLs updated"
```

## Edge Cases

- **Rate limit:** If web_fetch fails too many requests, abort after 10 consecutive failures. Report which URLs could not be checked.
- **Captcha pages:** X sometimes shows captcha instead of content. That's not GONE — mark as UNCLEAR.
- **Long-form threads:** If only the anchor tweet URL is down, but a mirror on threadreaderapp.com works: replace the URL with the mirror URL.

## Performance Note

At 132 URLs × 2–5 seconds per fetch = 5–10 minutes runtime. Be patient, or filter to only the newest 30 tips.

```
/verify-sources --since 2026-04-01    # only newer tips
/verify-sources --themes 04,05        # only specific themes
```

(Hypothetical flags — implement on demand via sub-prompt.)
