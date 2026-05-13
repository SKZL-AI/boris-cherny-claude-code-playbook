---
description: Rebuild index.html from TIPS.md, preserving the design
---

# /regenerate-html — Rebuild Dashboard

Synchronizes `index.html` with `TIPS.md`. Use this after `TIPS.md` has been changed by `/add-tip`, `/scan-x`, or the routine.

## Workflow

### Step 1 — Parse TIPS.md
Read TIPS.md. Extract:
- All 21 theme sections (`## NN — Theme Name`)
- All tips per theme: ID, title, difficulty, date, source URL, author, quote (optional), description

### Step 2 — Open index.html in Repo
Read the existing `index.html`. The structure is:
- `<header>` with stats and meta
- `<section class="theme-section" id="t<NN>">` for each of the 21 themes
- Inside: `<div class="tip-grid">` with `<article class="tip" data-diff="...">` per tip
- Timeline, Stages, Contested, Caveats, Footer

**Important:** Do NOT touch the CSS and JS at the beginning/end of the document. Only update the `<main>` content.

### Step 3 — Diff TIPS.md vs index.html
For each tip in TIPS.md:
- If the ID exists in index.html → update (overwrite content, position by ID order)
- If the ID does NOT exist → append new `<article>` at the end of the corresponding theme section
- If an ID exists in index.html but NOT in TIPS.md → mark as `[deprecated]`, do NOT delete (sticky IDs)

### Step 4 — Article Template
One `<article>` per tip:

```html
<article class="tip" data-diff="<difficulty-lowercase>">
  <div class="tip-meta">
    <span class="tip-num"><TT.NN></span>
    <span class="diff diff-<difficulty-lowercase>"><Difficulty></span>
  </div>
  <h3><Title-from-TIPS.md></h3>
  <p><Description with <code>inline</code> if Markdown code spans are present.></p>
  <div class="tip-footer">
    <span><DD Mon YYYY></span>
    <a class="tip-source" href="<URL>" target="_blank"><Source-Label> ↗</a>
  </div>
</article>
```

Source label mapping:
- x.com/* → "X-Thread ↗"
- threadreaderapp.com/* → "X (Mirror) ↗"
- latent.space → "Latent Space ↗"
- every.to/* → "AI & I Podcast ↗"
- lennysnewsletter.com → "Lenny's Podcast ↗"
- newsletter.pragmaticengineer.com → "Pragmatic Engineer ↗"
- anthropic.com/engineering → "Anthropic Blog ↗"
- docs.claude.com → "Anthropic Docs ↗"
- threads.com → "Threads ↗"
- howborisusesclaudecode.com → "How Boris Uses ↗"
- AIEWF / no URL → Plain `<span>AIEWF Talk</span>` without link

### Step 5 — Update Header / Footer
In `<header>`:
- `<span><strong>NNN+</strong> Tips</span>` → actual `total_tips` from YAML tracker

In `<footer>`:
- `NN Tips · 21 Themes · NN Months` → update
- `Last full audit: YYYY-MM-DD` → current date

In stats cards: no changes (Boris' own stats are static).

### Step 6 — Validation
Before saving:
- Count `<article class="tip">` — must match `total_tips` from TIPS.md
- Check all 21 themes are present (`id="t1"` through `id="t21"`)
- Check no theme section is empty (unlikely, but verify)

### Step 7 — Write File
Write the new `index.html` to the same location. Backup is available via git diff.

### Step 8 — Visual Verification (optional)
If the user has a browser MCP / Chrome extension: open `index.html` locally and take a screenshot. Compare with expectation.

Otherwise just a brief report:
```
✅ index.html regenerated
- N tips in HTML (matches TIPS.md)
- 21 theme sections
- Header/footer counts updated
- File size: NNN KB
```

## Important

- **No auto-commit.** The user checks the diff themselves, then commits.
- **CSS/JS untouched.** If the design needs refactoring, that's a separate task.
- **Sticky IDs.** Even deprecated tips stay in index.html, only with `[deprecated]` tag.
- **On schema drift:** If TIPS.md has an unexpected format (e.g., missing `**Difficulty:**`), abort and report — don't guess.

## Alternative: Full Rebuild

If the diff approach seems too error-prone (e.g., after major refactoring), you can also:
1. Generate complete `<main>` from TIPS.md from scratch
2. Keep CSS/JS from old index.html
3. Merge together

This is more robust but slower and produces larger git diffs.
