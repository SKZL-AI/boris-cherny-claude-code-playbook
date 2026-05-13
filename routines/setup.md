# Setup — Claude.ai Routines for Automatic Updates

> Step-by-step guide to setting up the routines defined in [daily-scan.md](./daily-scan.md) and [weekly-verify.md](./weekly-verify.md).

## Prerequisites

- **Claude.ai Pro, Max, Team, or Enterprise.** Routines are a Research Preview (as of April 2026); availability may vary by tier.
- **GitHub account** with access to the repo (public or private, both work).
- **About 15 minutes** for the initial setup.

## Step 1 — Publish the Repo on GitHub

```bash
cd boris-cherny-claude-code-playbook
git init
git add .
git commit -m "Initial commit: Boris Cherny Claude Code Playbook"
git branch -M main
git remote add origin https://github.com/<YOUR-USER>/boris-cherny-claude-code-playbook.git
git push -u origin main
```

**Optional: Enable GitHub Pages** so the dashboard is available live at `https://<your-user>.github.io/boris-cherny-claude-code-playbook/`:

1. GitHub Repo → Settings → Pages
2. Source: Deploy from a branch
3. Branch: `main` / root
4. Save

After 1–2 minutes, the dashboard will be live.

## Step 2 — Enable Connectors in Claude.ai

Open **claude.ai → Settings → Connectors**. Enable at least:

| Connector | Purpose | Where to Find |
|---|---|---|
| **GitHub** | Read/Write access to your repo | Standard connector, OAuth |
| **Web Search** | Scan X & secondary sources | Standard connector, automatic |
| **Web Fetch** | Full content of tweet threads | Optional but recommended |

**Important for GitHub:**
- During OAuth: grant Claude access to the specific repo (not all repos).
- Permissions: Read + Write Issues, Read + Write Code.

## Step 3 — Create the First Routine (Daily Scan)

1. Claude.ai → **Routines** (in the sidebar, possibly under "Beta" or "Research Preview")
2. Click **+ New Routine**
3. Fill in the fields:

| Field | Value |
|---|---|
| **Name** | `Boris Cherny X Scan — Morning` |
| **Description** | `Scans @bcherny on X for new Claude Code tips, updates GitHub repo` |
| **Schedule** | `Cron: 0 9 * * *` (daily at 09:00 CET — Cron uses UTC: adjust for your timezone, see below) |
| **Connectors** | GitHub, Web Search, Web Fetch |
| **Prompt** | Copy the full content between the `===` markers from [daily-scan.md](./daily-scan.md) |

**Cron UTC Adjustment:**

| CET Time | UTC Cron |
|---|---|
| 09:00 CET (Winter) | `0 8 * * *` |
| 09:00 CEST (Summer) | `0 7 * * *` |
| 15:00 CET | `0 14 * * *` (W) / `0 13 * * *` (S) |
| 22:00 CET | `0 21 * * *` (W) / `0 20 * * *` (S) |

> Anthropic Routines often also accept human-readable schedules like `daily at 9am Europe/Berlin`. Try that first.

4. Click **Save & Test Run**. The first run takes 1–3 minutes.

## Step 4 — Create Two More Daily Scans

Repeat Step 3 twice:

- `Boris Cherny X Scan — Afternoon` — 15:00 CET
- `Boris Cherny X Scan — Evening` — 22:00 CET

Identical prompt, different schedules.

> Tip: If 3 scans feel like too many, skip the Afternoon routine. Morning + Evening is enough to catch 90% of posts.

## Step 5 — Create the Weekly Verify Routine

This runs once a week and checks whether all source URLs are still reachable.

| Field | Value |
|---|---|
| **Name** | `Boris Cherny Playbook — Weekly URL Verify` |
| **Schedule** | `Cron: 0 10 * * 0` (Sunday 10:00) |
| **Connectors** | GitHub, Web Fetch |
| **Prompt** | Copy the content from [weekly-verify.md](./weekly-verify.md) |

## Step 6 — Verification

After 24 hours:

1. Check the repo → Commit history. You should see at least 2–3 commits from the routine.
2. Open CHANGELOG.md. It should have entries for the current day (even if "no changes").
3. Open TIPS.md, scroll to the bottom — `last_scan_iso` should show today's date.

If all checks pass: Setup successful.

## Step 7 — Notifications (Optional)

So you get notified when new tips come in:

**Option A — GitHub Notifications:**
GitHub Repo → Watch → "Custom" → check Pushes. You will receive an email for every routine commit.

**Option B — Slack Integration:**
If you use Slack, install the GitHub App → `/github subscribe <your-user>/boris-cherny-claude-code-playbook` in a channel.

**Option C — RSS:**
GitHub automatically generates a commits RSS feed: `https://github.com/<your-user>/boris-cherny-claude-code-playbook/commits/main.atom`

## Troubleshooting

### Routine does not run / no commit
- Check the Routine Dashboard → "Run history". Which step failed?
- Most common cause: GitHub connector token expired → Reconnect.
- Second most common: Web Search rate-limited → The routine itself is fine, just wait for the next run.

### Routine commits garbage / invents tips
- Routines sometimes interpret posts too liberally. Solution: adjust the prompt — add a stricter "DO NOT INVENT" clause or explicit examples of "valid tip" vs "not a tip".
- Worst case: pause the routine, revert the problematic commit, iterate on the prompt.

### Multiple routines with identical prompts run simultaneously
- Risk: two scans process the same tweet, resulting in duplicate tips. **Solution:** The prompt checks `last_scan_anchor_tweet_id` — if Routine 1 has already set the new anchor, Routine 2 finds nothing new. This should be robust.
- If duplicates still occur: the weekly-verify routine detects and merges them.

### Auto Mode / Permission Prompts
If you enable **Auto Mode** in the routine (Max/Team/Enterprise), everything runs without approval. If not: every GitHub write triggers a permission prompt — impractical for a routine that runs 2–3 times daily.

**Recommendation:** Enable Auto Mode, but restrict `--allow-tools` to `GitHub:write_file,GitHub:commit,WebSearch,WebFetch`. No generic Bash access.

### Rollback when something incorrect was committed

```bash
git revert HEAD       # undo the last commit
git push
```

or selectively remove a tip:

```bash
# Remove the tip locally, then
git commit -am "Remove tip #XX.YY (false positive from routine)"
git push
```

On the next routine run, the false tip will NOT be re-added because `last_scan_anchor_tweet_id` has already moved past it.

## Cost Considerations

Each routine run consumes an estimated **5,000–15,000 tokens** (Web Search results + repo files + output). At 3 runs per day = ~30,000–45,000 tokens/day = ~1M tokens/month.

On Claude Max, this is within the quota. On Pro: verify it does not eat into your daily limit — otherwise reduce to 1–2 runs per day.

## When to Use Manual Instead of Automatic

There are cases where the routine is NOT the right choice:

- **Large new thread with 15+ tips at once** (like the Jan 2 or Mar 29 threads): The routine processes them one by one, but it is better to do it once manually with `/scan-x` in Claude Code locally — you have more control over theme assignment.
- **New topic area**: If a Boris post introduces an entirely new 22nd topic, the repo structure needs to be set up first — the routine will not attempt that.
- **Major refactoring**: If Anthropic launches Claude Code 3.0 and much becomes obsolete, handle it manually.

For 90% of daily updates: use the routine. For the rare big leaps: go manual.
