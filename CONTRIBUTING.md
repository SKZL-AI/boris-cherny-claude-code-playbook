# Contributing

Thank you for your interest! This repo grows primarily through automated Claude.ai Routines, but manual contributions are welcome.

## What you can contribute

### 1. A new tip that the routine missed

If you find a public Boris Cherny tip that is not yet in the repo:

1. Fork the repo
2. Open with Claude Code: `cd boris-cherny-claude-code-playbook && claude`
3. Run `/add-tip` — the Slash Command walks you through a structured interview
4. Submit a Pull Request with the source URL in the description

**Criteria for inclusion:**
- Source must be publicly verifiable (X, podcast, blog, conference recording)
- Author: @bcherny or a Claude Code team member endorsed by Boris
- Concretely actionable, not pure marketing/status updates

### 2. Correction of an existing tip

If a tip is factually incorrect, a source URL is dead, or the wording is off:

1. Fork
2. Edit `TIPS.md` directly
3. **Important:** Do NOT change the ID. Even deprecated tips keep their ID.
4. Update `index.html` via `/regenerate-html` or manually
5. Submit a Pull Request with a justification

### 3. Wording improvements

If you can think of better English phrasing — go ahead. Verbatim Boris quotes stay in their original English wording.

### 4. New theme

If a Boris tip introduces a 22nd theme (e.g., "Voice Workflows"):

1. Open an Issue with the proposal: theme name, rationale, 2-3 example tips
2. Wait for discussion
3. Upon approval: submit a PR with changes to `TIPS.md`, `README.md` (table), `index.html` (TOC + new `<section>`)

## Pull Request checklist

- [ ] Source URL of the tip included in the PR description
- [ ] Tip ID follows the format `TT.NN` (theme number . sequential number)
- [ ] Difficulty is `beginner` | `intermediate` | `advanced` (no other values)
- [ ] Date in `YYYY-MM-DD` format in TIPS.md, `DD. MMM YYYY` in the display
- [ ] English verbatim quotes in quotation marks, under 15 words
- [ ] English description 1-3 sentences, no marketing speak
- [ ] CHANGELOG entry added at the top of `CHANGELOG.md`
- [ ] `index.html` is in sync with `TIPS.md` (`/regenerate-html` has been run)

## What we do NOT accept

- Tips from private sources (leaked Slack screenshots, internal Anthropic documents)
- Tips from other people, even if they work with Boris — unless Boris has explicitly retweeted/endorsed them
- AI-generated tips that "sound like Boris" but are not from him
- Your own best practices that have no Boris origin (create your own repo for those)

## Style guide

- **English prose**, technical terms (Worktree, Subagent, Hook, Slash Command) in `code` formatting where appropriate
- **Concise, no filler.** Boris is direct; the repo should be too.
- **Code snippets in backticks**: `inline` for commands, ```` ``` ```` for blocks
- **No emojis in tip text** (except in the CHANGELOG where they serve a structural purpose)
- **Source links with `↗` suffix** in HTML, plain Markdown links in TIPS.md

## Contacting the maintainer

Owner of this repo: SAKIZLI.AI (Furkan Sakizli).

- Issues: for questions, bug reports, theme proposals
- Direct: via the profile of [@sakizli](https://github.com/sakizli) on GitHub

For questions about Claude Code itself: not this repo, but [Anthropic Docs](https://docs.claude.com) or [Anthropic Support](https://support.claude.com).

## Code of Conduct

- Be respectful. Argue about content, not about people.
- If someone interprets a tip differently — discuss it in the PR, not in subtext.
- English is the primary language for Issues/PRs.
