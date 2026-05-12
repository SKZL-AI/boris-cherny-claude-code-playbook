# TIPS.md — Structured Tip List

> **Source of truth.** All other artifacts (`README.md`, `index.html`) derive from this file.
> **Format:** One tip per H3 block. New tips inserted by `/add-tip` or by the Routine in `routines/daily-scan.md`.
> **Last manual audit:** 2026-05-12
> **Total tips:** 132 across 21 themes
> **Schema:** see `data/tips-schema.json`

---

## 01 — Parallele Ausführung

### #01.01 — 5 Claudes in parallelen Terminal-Tabs
- **Difficulty:** Intermediate
- **Date:** 2026-01-02 (`02. Jan 2026`)
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Tabs durchnummeriert 1–5. iTerm2 zeigt System-Notifications, sobald ein Claude Input braucht. Damit nie auf einen einzelnen Prozess warten.

### #01.02 — 5–10 weitere Claudes auf claude.ai/code
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Übergabe local↔web mit `&` oder `--teleport`. Boris startet Sessions morgens schon aus der iOS-App.

### #01.03 — 3–5 git worktrees, ein Claude pro worktree
- **Difficulty:** Advanced
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "The single biggest productivity unlock"

Team-Mitglieder nutzen Shell-Aliase `za, zb, zc` zum Springen. Manche haben einen dedizierten "Analysis-Worktree" für Logs/BigQuery. Boris persönlich nutzt stattdessen mehrere Checkouts.

### #01.04 — `claude --worktree` (oder `-w`)
- **Difficulty:** Intermediate
- **Date:** 2026-02-20
- **Source:** [X-Thread](https://x.com/bcherny/status/2025007393290272904)
- **Author:** @bcherny

Eingebaute Worktree-Isolation. Worktree benennen oder Claude benennen lassen. Mit `--tmux` startet alles in einer tmux-Session.

### #01.05 — Worktree-Mode in der Desktop-App
- **Difficulty:** Beginner
- **Date:** 2026-02-20
- **Source:** [X-Thread](https://x.com/bcherny/status/2025007393290272904)
- **Author:** @bcherny

Code-Tab → Checkbox "worktree" aktivieren. Kein Terminal nötig.

### #01.06 — Subagents mit Worktree-Isolation
- **Difficulty:** Advanced
- **Date:** 2026-02-20
- **Source:** [X-Thread](https://x.com/bcherny/status/2025007393290272904)
- **Author:** @bcherny

Claude anweisen: "use worktrees for its agents". Stark für große batched Changes und Migrationen.

### #01.07 — `isolation: worktree` im Agent-Frontmatter
- **Difficulty:** Advanced
- **Date:** 2026-02-20
- **Source:** [X-Thread](https://x.com/bcherny/status/2025007393290272904)
- **Author:** @bcherny

Custom-Subagent dauerhaft in eigenem Worktree laufen lassen. Setzen im YAML-Frontmatter der Agent-Definition.

### #01.08 — Non-git VCS via WorktreeCreate-Hook
- **Difficulty:** Advanced
- **Date:** 2026-02-20
- **Source:** [X-Thread](https://x.com/bcherny/status/2025007393290272904)
- **Author:** @bcherny

Mercurial, Perforce, SVN, Jujutsu: eigene `WorktreeCreate`- und `WorktreeRemove`-Hooks definieren.

### #01.09 — Dutzende Claudes via Worktrees
- **Difficulty:** Advanced
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny
- **Quote:** "I have dozens of Claudes running at all times"

Skaliert ab dem Punkt, an dem du dich allein durchs Tab-Switching aufhältst.

---

## 02 — Plan Mode

### #02.01 — Jeden komplexen Task im Plan-Mode starten
- **Difficulty:** Beginner
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Shift+Tab zweimal. Plan mit Claude iterieren, dann auf Auto-Accept-Edits umschalten. Claude one-shottet meistens, wenn der Plan gut ist.

### #02.02 — "A good plan is really important"
- **Difficulty:** Beginner
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny
- **Quote:** "A good plan is really important"

Denken in den Plan vorverlegen — Implementierung folgt fast immer one-shot. Front-loading reduziert Kontext-Verbrauch über die ganze Session.

### #02.03 — Bei Problemen neu planen statt drücken
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "Don't keep pushing. Switch back to plan mode and re-plan"

Wenn etwas schief läuft, frischen Kontext erzwingen.

### #02.04 — Zweiten Claude als "Staff Engineer" reviewen lassen
- **Difficulty:** Advanced
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Claude A schreibt Plan, Claude B reviewed ihn mit frischem Kontext — wie ein Senior-Review vor dem Coden.

### #02.05 — Plan-Mode auch für Verifikations-Schritte
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Nicht nur die Implementierung planen — auch "wie verifiziere ich, dass es funktioniert" gehört in den Plan.

### #02.06 — Automatische Session-Namen nach Plan-Mode
- **Difficulty:** Beginner
- **Date:** 2026-03-13
- **Source:** [X-Thread](https://x.com/bcherny/status/2032632596572811575)
- **Author:** @bcherny

Claude leitet aus der Plan-Konversation einen sprechenden Session-Namen ab. Wiedererkennbar in Parallel-Setups.

---

## 03 — CLAUDE.md

### #03.01 — Eine team-geteilte CLAUDE.md, in git eingecheckt
- **Difficulty:** Beginner
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Team trägt mehrfach pro Woche bei. Wird zur lebenden Doku der Codebase.

### #03.02 — Regel hinzufügen, sobald Claude einen Fehler macht
- **Difficulty:** Beginner
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny
- **Quote:** "Anytime we see Claude do something incorrectly we add it to the CLAUDE.md"

Compounding-Engineering im Kern.

### #03.03 — Jedes Team pflegt seine eigene CLAUDE.md
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Cross-Team-CLAUDE.md-Ownership liegt bei jedem einzelnen Team. Lokales Wissen bleibt lokal.

### #03.04 — @.claude in PR-Kommentaren taggen
- **Difficulty:** Advanced
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Boris' Version von Dan Shippers "Compounding Engineering". Installiert via `/install-github-action`.

### #03.05 — "Update your CLAUDE.md so you don't make that mistake again"
- **Difficulty:** Beginner
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "Update your CLAUDE.md so you don't make that mistake again"

End-of-Correction-Prompt: lässt Claude die Regel für sich selbst schreiben.

### #03.06 — CLAUDE.md gnadenlos kürzen über die Zeit
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

"Keep iterating until Claude's mistake rate measurably drops." Pruning ist genauso wichtig wie Hinzufügen.

### #03.07 — Notes-Verzeichnis pro Task, von CLAUDE.md referenziert
- **Difficulty:** Advanced
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Ein Engineer pflegt ein Notes-Verzeichnis pro Task, wird nach jedem PR aktualisiert. CLAUDE.md verweist darauf.

### #03.08 — CLAUDE.md-Varianten je nach Scope
- **Difficulty:** Intermediate
- **Date:** 2025-06-15
- **Source:** AIEWF Talk 2025
- **Author:** @bcherny

`CLAUDE.md` (Projekt, in git), `CLAUDE.local.md` (gitignored, persönlich), `~/.claude/CLAUDE.md` (global), per Unterordner `a/b/CLAUDE.md` für Monorepos.

### #03.09 — Memory ist nur eine Markdown-Datei
- **Difficulty:** Beginner
- **Date:** 2025-05-07
- **Source:** [Latent Space Podcast](https://www.latent.space/p/claude-code)
- **Author:** @bcherny
- **Quote:** "It's a file that has some stuff. And it's auto-read into context"

Simpler als jeder Vector-Store.

### #03.10 — `#` voranstellen zum Merken
- **Difficulty:** Beginner
- **Date:** 2025-06-15
- **Source:** AIEWF Talk 2025
- **Author:** @bcherny

"Add to Claude's memory by prepending # to something you want Claude Code to remember." Claude fragt nach Memory-Location (Projekt/User).

### #03.11 — Auto-Memory + Auto-Dream
- **Difficulty:** Advanced
- **Date:** 2026-03-25
- **Source:** [X (RT)](https://x.com/bcherny/status/2036959638646866021)
- **Author:** @thariq (RT @bcherny)

Auto-Memory speichert Preferences/Korrekturen automatisch. Auto-Dream ist ein Subagent, der past Sessions periodisch reviewt und konsolidiert (REM-Sleep-Metapher).

---

## 04 — Slash Commands

### #04.01 — Slash Commands für jeden Inner-Loop-Workflow
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Stored in `.claude/commands/`, in git eingecheckt. Claude selbst kann sie auch nutzen.

### #04.02 — `/commit-push-pr` dutzendfach pro Tag
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Inline-Bash für vorab-berechneten `git status` — vermeidet Model-Hin-und-Her.

### #04.03 — `/feature-dev` als Schritt-für-Schritt-Guide
- **Difficulty:** Intermediate
- **Date:** 2025-11-15
- **Source:** [AI & I Podcast](https://every.to/podcast/how-to-use-claude-code-like-the-people-who-built-it)
- **Author:** @bcherny

"First ask me what exactly I want, build the specification, build a detailed plan, then a to-do list, walk through step-by-step."

### #04.04 — `/commit` — der grundlegendste Command
- **Difficulty:** Beginner
- **Date:** 2025-11-15
- **Source:** [AI & I Podcast](https://every.to/podcast/how-to-use-claude-code-like-the-people-who-built-it)
- **Author:** @bcherny

Meist-genutztes Slash-Command bei Anthropic. Auto-runs save+push ohne Permission-Prompts.

### #04.05 — `/code-review` auf jedem PR
- **Difficulty:** Intermediate
- **Date:** 2025-11-15
- **Source:** [AI & I Podcast](https://every.to/podcast/how-to-use-claude-code-like-the-people-who-built-it)
- **Author:** @bcherny

Mensch approved den Merge, Claude macht den ersten Sweep. Standard im Anthropic-Team.

### #04.06 — Slash Commands sind Prompts, keine Tools
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny
- **Quote:** "Slash commands are actually just like prompts"

Wichtig fürs mentale Modell.

### #04.07 — Lokale Commands vor MCP für simple Cases
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

"If you just want something really simple and local… just use local commands for that." MCP nur, wenn nötig.

### #04.08 — `/init` generiert Starter-CLAUDE.md
- **Difficulty:** Beginner
- **Date:** 2025-04-18
- **Source:** [Anthropic Blog](https://www.anthropic.com/engineering/claude-code-best-practices)
- **Author:** @bcherny

Analysiert Codebase, erkennt Build-Systeme, Tests, Code-Patterns. Erster Schritt in neuem Projekt.

### #04.09 — `/techdebt` findet duplizierten Code
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Am Ende jeder Session laufen lassen. Community-Liebling unter den Custom-Commands.

### #04.10 — Context-Dump Slash Command
- **Difficulty:** Advanced
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Synct 7 Tage Slack + GDrive + Asana + GitHub in einen Prompt.

### #04.11 — `/simplify` (built-in skill)
- **Difficulty:** Intermediate
- **Date:** 2026-02-27
- **Source:** [X-Thread](https://x.com/bcherny/status/2027534984534544489)
- **Author:** @bcherny

Parallele Agents verbessern Code-Qualität und erzwingen CLAUDE.md-Compliance. Usage: "make this change then run /simplify".

### #04.12 — `/batch` (built-in skill)
- **Difficulty:** Advanced
- **Date:** 2026-02-27
- **Source:** [X-Thread](https://x.com/bcherny/status/2027534984534544489)
- **Author:** @bcherny

Interviewt dich, fächert dann zu dutzenden/hunderten/tausenden Worktree-Agents auf. Beispiel: "/batch migrate src/ from Solid to React".

### #04.13 — `/loop` für wiederkehrende lokale Tasks (bis 3 Tage)
- **Difficulty:** Advanced
- **Date:** 2026-03-07
- **Source:** [X-Thread](https://x.com/bcherny/status/2030193932404150413)
- **Author:** @bcherny

Boris' Setup: `/loop 5m /babysit`, `/loop 30m /slack-feedback`, `/loop /post-merge-sweeper`, `/loop 1h /pr-pruner`.

### #04.14 — `/schedule` für Cloud-basierte Recurring Jobs
- **Difficulty:** Advanced
- **Date:** 2026-03-23
- **Source:** [X (RT)](https://x.com/bcherny/status/2036555259997462541)
- **Author:** @noah-z (RT @bcherny)

Überlebt einen geschlossenen Laptop. Anthropic-Team nutzt es für auto CI-failure-resolution, Docs-Updates.

### #04.15 — `/btw` für Side-Chain-Conversations
- **Difficulty:** Beginner
- **Date:** 2026-03-10
- **Source:** [X-Thread](https://x.com/bcherny/status/2031506296697131352)
- **Author:** @bcherny
- **Quote:** "I use this all the time to answer quick questions while the agent works"

Single-Turn, keine Tool-Calls, voller Kontext. Von Erik Schluntz als Side-Project gebaut.

### #04.16 — `/branch` + `--resume <id> --fork-session`
- **Difficulty:** Intermediate
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Existierende Session in eine branched Conversation forken. Spart Re-Kontextualisierung.

### #04.17 — `/effort` setzt Reasoning-Level
- **Difficulty:** Intermediate
- **Date:** 2026-03-13
- **Source:** [X-Thread](https://x.com/bcherny/status/2032632596572811575)
- **Author:** @bcherny

low / medium / high / xhigh / max. Boris nutzt xhigh für die meisten Tasks, max für die härtesten. Max gilt nur für die aktuelle Session, andere Levels sind sticky.

### #04.18 — `/focus` Mode (CLI)
- **Difficulty:** Intermediate
- **Date:** 2026-04-16
- **Source:** [X-Thread](https://x.com/bcherny/status/2044847848035156457)
- **Author:** @bcherny
- **Quote:** "I generally trust the model to run the right commands and edits"

Versteckt Zwischenarbeit, zeigt nur Endresultat.

### #04.19 — `/go` — Composite Skill
- **Difficulty:** Advanced
- **Date:** 2026-04-16
- **Source:** [X-Thread](https://x.com/bcherny/status/2044847848035156457)
- **Author:** @bcherny
- **Quote:** "Many of my prompts look like 'Claude do blah blah /go'"

Claude testet end-to-end (Bash, Browser oder Computer Use) → führt `/simplify` aus → öffnet einen PR.

### #04.20 — `/fewer-permission-prompts` Skill
- **Difficulty:** Intermediate
- **Date:** 2026-04-16
- **Source:** [X-Thread](https://x.com/bcherny/status/2044847848035156457)
- **Author:** @bcherny

Scannt Session-History nach safe-but-prompted Commands; empfiehlt Allowlist-Erweiterung.

### #04.21 — `/voice` aktiviert Voice-Dictation
- **Difficulty:** Beginner
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny
- **Quote:** "I do most of my coding by speaking to Claude, rather than typing"

Space-Bar im CLI halten, Voice-Button im Desktop, iOS-Dictation.

### #04.22 — `/color` zum Color-Coden von Sessions
- **Difficulty:** Beginner
- **Date:** 2026-03-13
- **Source:** [X-Thread](https://x.com/bcherny/status/2032632602629386348)
- **Author:** @bcherny

Leichter, parallele Sessions auseinanderzuhalten.

### #04.23 — `/statusline`
- **Difficulty:** Intermediate
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021700784019452195)
- **Author:** @bcherny

Zeigt Context-%, Git-Branch, Model, Cost. Jeder im Team hat seine eigene Statusline.

### #04.24 — `/keybindings`
- **Difficulty:** Advanced
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021700883873165435)
- **Author:** @bcherny

Jedes Key-Binding ist customizable, Settings live-reload. Stored in `~/.claude/keybindings.json`.

### #04.25 — `/sandbox` für Open-Source-Sandbox
- **Difficulty:** Advanced
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021700506465579443)
- **Author:** @bcherny

File- und Network-Isolation. Modi: BashTool auto-allow, BashTool mit Prompts, off.

### #04.26 — `/plugin` zum Marketplace-Browsen
- **Difficulty:** Intermediate
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021699862522364149)
- **Author:** @bcherny

LSPs, MCPs, Skills, Agents, Hooks. Companies können eigenen Marketplace hosten.

### #04.27 — `/agents` zum Erstellen von Custom Agents
- **Difficulty:** Intermediate
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021700144039903699)
- **Author:** @bcherny

Markdown-Dateien in `.claude/agents/` ablegen. Frontmatter konfiguriert Tools/Model/System-Prompt.

### #04.28 — `/terminal-setup` für Shift+Enter Newlines
- **Difficulty:** Beginner
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021699859359883608)
- **Author:** @bcherny

Für IDE-Terminal, Apple Terminal, Warp, Alacritty.

### #04.29 — `/vim` für Vim-Mode-Editing
- **Difficulty:** Beginner
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021699859359883608)
- **Author:** @bcherny

Ein-Zeilen-Setup. Für Vim-User selbstverständlich.

### #04.30 — `/teleport`
- **Difficulty:** Intermediate
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Holt eine Cloud-Session runter ins lokale Terminal (`claude --teleport`).

### #04.31 — `/remote-control`
- **Difficulty:** Intermediate
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Steuert eine lokale Session von jedem Device aus. Boris hat "Enable Remote Control for all sessions" in `/config`.

### #04.32 — `/compact <hint>` statt `/clear` mid-task
- **Difficulty:** Intermediate
- **Date:** 2026-04-15
- **Source:** [X (RT Thariq)](https://x.com/bcherny/status/2044548257058328723)
- **Author:** @thariq (RT @bcherny)

`/compact` ist lossy LLM-Summary, hält Momentum. `/clear` + Briefing ist hand-geschriebener Kontext. Regel: neuer Task = clear, related = compact.

### #04.33 — `/rewind` (oder double-Esc) statt Korrektur
- **Difficulty:** Intermediate
- **Date:** 2026-04-15
- **Source:** [X (RT Thariq)](https://x.com/bcherny/status/2044548257058328723)
- **Author:** @thariq (RT @bcherny)

Kontext nicht mit failed attempts + Korrekturen verschmutzen — rewind und re-prompten mit dem Gelernten.

### #04.34 — "Summarize from here" vor dem Rewind
- **Difficulty:** Advanced
- **Date:** 2026-04-15
- **Source:** [X (RT Thariq)](https://x.com/bcherny/status/2044548257058328723)
- **Author:** @thariq (RT @bcherny)

Claude eine Handoff-Message an sein zukünftiges Selbst schreiben lassen. Maximiert kontinuierliches Lernen über Rewinds hinweg.

---

## 05 — Subagents

### #05.01 — Subagents = Automation für PR-Workflows
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Stored in `.claude/agents/`. Wiederverwendbar im Team.

### #05.02 — `code-simplifier` Agent
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Cleant Code nach Claude's Arbeit. Boris' Standard nach jeder Implementierung.

### #05.03 — `verify-app` Agent
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Detaillierte Instruktionen für End-to-End-Testing. Verifikationsschritt als wiederverwendbarer Baustein.

### #05.04 — "use subagents" anhängen für mehr Compute
- **Difficulty:** Beginner
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Ein-Wort-Eskalation an jeden Prompt. Wirft mehr Compute auf das Problem.

### #05.05 — Tasks an Subagents auslagern für sauberen Hauptkontext
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Hält das Window für wichtige Arbeit frei. Recherche-Heavy-Aufgaben sind perfekt dafür.

### #05.06 — 5 parallele Exploration-Agents auf neuer Codebase
- **Difficulty:** Advanced
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

"Use 5 subagents to explore the codebase" — läuft parallel. Schnellster Weg zum Verständnis.

### #05.07 — Permission-Requests an Opus-Subagent via Hook
- **Difficulty:** Advanced
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Hook scannt auf Prompt-Injection-Attacks, auto-approved die safen. Reduziert UI-Reibung massiv.

### #05.08 — Adversariales Subagent-Pattern für Code Review
- **Difficulty:** Advanced
- **Date:** 2025-11-15
- **Source:** [AI & I Podcast](https://every.to/podcast/how-to-use-claude-code-like-the-people-who-built-it)
- **Author:** @bcherny

Boris spawnt Subagents für Style/History/Bugs als ersten Pass — dann 5 weitere Subagents, die Löcher in die ersten Findings poken, um False Positives zu eliminieren.

### #05.09 — Subagents = unkorrelierte Kontextfenster
- **Difficulty:** Advanced
- **Date:** 2025-11-15
- **Source:** [AI & I Podcast](https://every.to/podcast/how-to-use-claude-code-like-the-people-who-built-it)
- **Author:** @bcherny

Der Wert ist nicht Anthropomorphisierung — sondern zwei Kontextfenster, die nichts voneinander wissen.

### #05.10 — Custom `--agent` Flag
- **Difficulty:** Intermediate
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

`claude --agent=ReadOnly`. Agent .md-Frontmatter setzt Name, Color, Tools, Model, System-Prompt.

### #05.11 — Default-Agent setzen
- **Difficulty:** Advanced
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021700144039903699)
- **Author:** @bcherny

`"agent"`-Feld in settings.json oder `--agent`-Flag. Team-spezifische Defaults durchsetzen.

### #05.12 — Parallele Subagents für Plan-Research
- **Difficulty:** Advanced
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny
- **Quote:** "Research three separate ideas. Do it in parallel. Use three agents"

---

## 06 — Hooks

### #06.01 — PostToolUse Hook für Auto-Formatting
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Matcher `"Write|Edit"`, runs `bun run format || true`. Claude formatiert ~90% korrekt, Hook fängt die 10% ab.

### #06.02 — SessionStart Hook
- **Difficulty:** Advanced
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Lädt dynamisch Kontext, wann immer Claude startet.

### #06.03 — PreToolUse Hook
- **Difficulty:** Advanced
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Loggt jeden Bash-Command. Audit-Trail für sensible Repos.

### #06.04 — PermissionRequest Hook
- **Difficulty:** Advanced
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Routet Approval-Prompts nach WhatsApp/Slack/SMS.

### #06.05 — Stop Hook hält Claude am Laufen
- **Difficulty:** Advanced
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Poke Claude, wenn er stoppt. Kann einen Agent kicken oder per Prompt entscheiden, ob weitergemacht wird.

### #06.06 — Agent Stop Hook für lange Verifikation
- **Difficulty:** Advanced
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Deterministischer als Claude zu bitten, sich selbst zu verifizieren.

### #06.07 — PostCompact Hook
- **Difficulty:** Advanced
- **Date:** 2026-03-13
- **Source:** [X-Thread](https://x.com/bcherny/status/2032632602629386348)
- **Author:** @bcherny

Feuert nach Kontext-Kompression. Nützlich für Re-Injection kritischer Instruktionen.

### #06.08 — WorktreeCreate / WorktreeRemove Hooks
- **Difficulty:** Advanced
- **Date:** 2026-02-20
- **Source:** [X-Thread](https://x.com/bcherny/status/2025007393290272904)
- **Author:** @bcherny

Für non-git VCS. Worktree-Logik selbst definieren.

### #06.09 — Ralph-Wiggum Plugin für lange Tasks
- **Difficulty:** Advanced
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @geoffreyhuntley (endorsed by @bcherny)

Community-Plugin für unattended Cooking. Für mehrtägige Runs.

---

## 07 — Permissions & Safety

### #07.01 — Kein `--dangerously-skip-permissions` für Normal-Arbeit
- **Difficulty:** Beginner
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Stattdessen `/permissions` nutzen, um sichere Commands vorab zu allowen.

### #07.02 — `.claude/settings.json` mit Team teilen
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Pre-allowed Perms in git einchecken. Onboarding wird zur Ein-Befehl-Sache.

### #07.03 — Wildcard-Syntax für Permissions
- **Difficulty:** Intermediate
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021700332292911228)
- **Author:** @bcherny

`"Bash(bun run *)"`, `"Edit(/docs/**)"`. Praktisch für ganze Tool-Familien.

### #07.04 — Auto Mode (Opus 4.7)
- **Difficulty:** Intermediate
- **Date:** 2026-04-16
- **Source:** [X-Thread](https://x.com/bcherny/status/2044847848035156457)
- **Author:** @bcherny

Model-basierter Classifier auto-approved sichere Permission-Prompts. Shift+Tab cycelt: Ask → Plan → Auto.

### #07.05 — `--permission-mode=dontAsk` in Sandboxes
- **Difficulty:** Advanced
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Boris nutzt das nur in Sandboxes für lange Runs.

### #07.06 — Open-Source-Sandbox-Runtime aktivieren
- **Difficulty:** Advanced
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021700506465579443)
- **Author:** @bcherny

Reduziert Prompts ohne `--dangerously-skip`.

### #07.07 — Permission-System: Innenleben
- **Difficulty:** Intermediate
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021700332292911228)
- **Author:** @bcherny
- **Quote:** "Combo of prompt-injection detection, static analysis, sandboxing, and human oversight"

---

## 08 — MCP & Integrationen

### #08.01 — Slack MCP, eingecheckt in `.mcp.json`
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Mit Team geteilt. Claude sucht und postet selbstständig.

### #08.02 — `bq` CLI für BigQuery
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "I haven't written a line of SQL in 6+ months"

### #08.03 — Sentry für Error-Logs
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Zieht Error-Logs automatisch in Claude. Bug-Triage ohne Context-Switching.

### #08.04 — Slack-Bug-Thread reinpasten → "fix"
- **Difficulty:** Beginner
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Zero Context-Switching.

### #08.05 — Claude auf Docker-Logs ansetzen
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Überraschend stark im Troubleshooting verteilter Systeme.

### #08.06 — Slack MCP für tägliche Summaries
- **Difficulty:** Intermediate
- **Date:** 2026-03-07
- **Source:** [X-Thread](https://x.com/bcherny/status/2030193932404150413)
- **Author:** @bcherny

`/loop every morning use the Slack MCP to give me a summary of top posts I was tagged in`.

### #08.07 — iMessage als Claude-Code-Channel
- **Difficulty:** Beginner
- **Date:** 2026-03-25
- **Source:** [X-Thread](https://x.com/bcherny/status/2036959638646866021)
- **Author:** @bcherny

`/plugin install imessage@claude-plugins-official`. Claude von jedem Apple-Gerät via SMS texten.

---

## 09 — Modell & Effort

### #09.01 — Opus 4.5 mit Thinking für alles
- **Difficulty:** Beginner
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny
- **Quote:** "Almost always faster in the end"

Weniger Steuerung nötig, besser im Tool-Use.

### #09.02 — Opus 4.6 1M als Default für Max/Team/Enterprise
- **Difficulty:** Intermediate
- **Date:** 2026-03-13
- **Source:** [X-Thread](https://x.com/bcherny/status/2032514807388123255)
- **Author:** @bcherny

Pro/Sonnet-User opt-in via `/extra-usage`.

### #09.03 — Opus 4.7 nutzt adaptives Thinking
- **Difficulty:** Intermediate
- **Date:** 2026-04-16
- **Source:** [X-Thread](https://x.com/bcherny/status/2044847848035156457)
- **Author:** @bcherny

Modell entscheidet selbst, wann Thinking sinnvoll ist. Keine festen Budgets mehr.

### #09.04 — "Think carefully and step-by-step" pusht Thinking
- **Difficulty:** Beginner
- **Date:** 2026-04-16
- **Source:** [X-Thread](https://x.com/bcherny/status/2044847848035156457)
- **Author:** @bcherny

Oder "Prioritize responding quickly", um Tokens zu sparen.

### #09.05 — Ultrathink-Triggerwörter (Legacy)
- **Difficulty:** Intermediate
- **Date:** 2025-04-18
- **Source:** [Anthropic Blog](https://www.anthropic.com/engineering/claude-code-best-practices)
- **Author:** @bcherny

think < think hard < think harder < ultrathink. In CC v2 ersetzt durch `/effort`, ultrathink bleibt highlighted.

### #09.06 — Opus 4.7: kürzere Antworten, weniger Auto-Tool-Use
- **Difficulty:** Intermediate
- **Date:** 2026-04-16
- **Source:** [Anthropic Docs](https://docs.claude.com)
- **Author:** @bcherny

Wenn du Länge/Stil willst, explizit sagen. Für Refactor across 40 files: explizit Subagents anfordern.

### #09.07 — 4.7's höhere Treue zu "don't nitpick"
- **Difficulty:** Advanced
- **Date:** 2026-04-16
- **Source:** [Anthropic Docs](https://docs.claude.com)
- **Author:** @bcherny

Code-Review-Harnesses für ältere Modelle sehen evtl. niedrigeren Recall — keine Regression.

### #09.08 — Default war Sonnet, Model ist überridable
- **Difficulty:** Beginner
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

"We default to Sonnet for most everything… you can override the model if you want."

### #09.09 — Plan/Think-Instruktionen direkt schreiben
- **Difficulty:** Beginner
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny
- **Quote:** "If you want Claude to think, just tell it to think"

---

## 10 — Verifikation

### #10.01 — Verifikation = 2–3× Qualität
- **Difficulty:** Beginner
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny
- **Quote:** "Will 2–3x the quality of the final result"

Der wichtigste einzelne Tipp im ganzen Setup.

### #10.02 — Boris' claude.ai/code Change-Verifikation
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny
- **Quote:** "Claude tests every single change I land to claude.ai/code"

Claude öffnet Chrome-Extension, testet jeden UI-Change, iteriert bis UX gut ist.

### #10.03 — Verifikation variiert je Domain
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Bash, Test-Suite, Simulator, Browser, Computer-Use. Investiere in deren Robustheit.

### #10.04 — Backend = Server/Service end-to-end laufen lassen
- **Difficulty:** Intermediate
- **Date:** 2026-04-16
- **Source:** [X-Thread](https://x.com/bcherny/status/2044847848035156457)
- **Author:** @bcherny

Stelle sicher, dass Claude deinen Service starten kann.

### #10.05 — Frontend = Chromium-Extension
- **Difficulty:** Intermediate
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Boris nutzt sie für jeden Web-Code-Change. Zuverlässiger als andere Browser-MCPs.

### #10.06 — Desktop-Apps = Computer Use
- **Difficulty:** Advanced
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Desktop-App bündelt automatic Server-Start + eingebautes Browser-Testing.

### #10.07 — "Grill me on these changes"-Pattern
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "Don't make a PR until I pass your test"

### #10.08 — "Prove to me this works"
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Lass Claude Verhalten zwischen main und deinem Branch diffen.

### #10.09 — Nach mittelmäßigem Fix
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "Scrap this and implement the elegant solution"

### #10.10 — Code → Screenshot → Iterate
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

Zeig Claude einen Mock, lass es Puppeteer nutzen zum Vergleichen und Iterieren.

### #10.11 — Fehler früh erkennen
- **Difficulty:** Beginner
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny
- **Quote:** "Better to identify that earlier and correct it earlier"

---

## 11 — Long-Running & Recaps

### #11.01 — (a) Background-Agent zur Selbst-Verifikation
- **Difficulty:** Intermediate
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Claude prompten, Background-Agent zu spawnen wenn fertig.

### #11.02 — (b) Agent Stop Hook für deterministische Verifikation
- **Difficulty:** Advanced
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Zuverlässiger als (a). Code statt Modell trifft die Entscheidung.

### #11.03 — (c) Ralph-Wiggum Plugin
- **Difficulty:** Advanced
- **Date:** 2026-01-02
- **Source:** [X-Thread](https://x.com/bcherny/status/2007179832300581177)
- **Author:** @bcherny

Community-Pattern für sehr lange Runs.

### #11.04 — Recaps für lange Sessions
- **Difficulty:** Beginner
- **Date:** 2026-04-16
- **Source:** [X-Thread](https://x.com/bcherny/status/2044847848035156457)
- **Author:** @bcherny

Kurze Summary über Done + Next. Deaktivierbar in `/config`.

### #11.05 — Routines (Research Preview)
- **Difficulty:** Advanced
- **Date:** 2026-04-14
- **Source:** [X](https://x.com/bcherny)
- **Author:** @bcherny

Schedule-, GitHub-Event- und API-Trigger. Läuft auf Anthropic-Infra.

### #11.06 — Cross-Session-Continuity-Workaround
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

"Write down the state of this session into this text doc… in your new session, tell Claude to read from that doc."

---

## 12 — Prompting & Specs

### #12.01 — Delegation > Guidance (Opus 4.7)
- **Difficulty:** Intermediate
- **Date:** 2026-04-16
- **Source:** [X (Cat Wu)](https://x.com/bcherny)
- **Author:** @catwu (endorsed by @bcherny)
- **Quote:** "Treat it like an engineer you're delegating to, not a pair programmer"

### #12.02 — Full Task Context Upfront
- **Difficulty:** Intermediate
- **Date:** 2026-04-16
- **Source:** [X (Cat Wu)](https://x.com/bcherny)
- **Author:** @catwu (endorsed by @bcherny)

Goal + Constraints + Acceptance-Criteria — alle drei im ersten Turn.

### #12.03 — Detaillierte Specs, weniger Ambiguität
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "The more specific you are, the better the output"

### #12.04 — Prototyp > PRD
- **Difficulty:** Advanced
- **Date:** 2026-02-19
- **Source:** [Pragmatic Engineer](https://newsletter.pragmaticengineer.com/p/building-claude-code-with-boris-cherny)
- **Author:** @bcherny

"There's just no way we could have shipped this if we started with static mocks and Figma or if we started with a PRD."

### #12.05 — Nicht micromanagen, wie Claude einen Bug fixt
- **Difficulty:** Beginner
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "Paste the bug, say 'fix.' Don't micromanage how"

### #12.06 — Prototypen statt Design-Dokumente
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

"Ask Claude Code to prototype three versions of it. Try the feature and see which one I like better."

---

## 13 — Customization

### #13.01 — Spinner-Verbs customizen
- **Difficulty:** Beginner
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021701145023197516)
- **Author:** @bcherny

Star-Trek-themed Beispiel. settings.json in Source Control einchecken.

### #13.02 — Output-Styles: Explanatory / Learning / Custom
- **Difficulty:** Intermediate
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021701379409273093)
- **Author:** @bcherny

Claude erklärt Frameworks; coacht dich durch Changes hindurch.

### #13.03 — 37 Settings + 84 Environment-Variablen
- **Difficulty:** Advanced
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021701636075458648)
- **Author:** @bcherny

`"env"`-Feld in settings.json nutzen, um Wrapper-Scripts zu vermeiden.

### #13.04 — Claude antwortet in deiner Sprache
- **Difficulty:** Beginner
- **Date:** 2026-01-07
- **Source:** [X-Thread](https://x.com/bcherny/status/2009072293826453669)
- **Author:** @bcherny

Japanese, Spanish, German — beliebige Sprache konfigurierbar.

### #13.05 — settings.json in git einchecken
- **Difficulty:** Intermediate
- **Date:** 2026-02-11
- **Source:** [X-Thread](https://x.com/bcherny/status/2021701145023197516)
- **Author:** @bcherny

Team profitiert von Customizations. Support für Enterprise-weite Policies.

### #13.06 — NO_FLICKER Mode
- **Difficulty:** Intermediate
- **Date:** 2026-04-01
- **Source:** [X-Thread](https://x.com/bcherny/status/2037038538718667103)
- **Author:** @bcherny

Experimentelles Renderer: kein Flicker/Jump, Mouse-Support. `CLAUDE_CODE_NO_FLICKER=1 claude`.

---

## 14 — Headless / SDK

### #14.01 — `claude -p` für non-interactive Mode
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

Prompt in Quotes übergeben. Pipeline-friendly.

### #14.02 — Best für read-only Tests
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny
- **Quote:** "Where it works really well"

### #14.03 — Small Start, dann skalieren
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

"Start small… test on one test… iterate on your prompt. Then scale to 10."

### #14.04 — Pre-Commit Hook mit `-p`
- **Difficulty:** Advanced
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

"Just add a line: `claude -p` and whatever instruction you have." Unter ~5 Sek halten.

### #14.05 — `--allow-tools` zum Scopen von Permissions
- **Difficulty:** Advanced
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

Spezifische Tools für Batch-Operationen lockdownen.

### #14.06 — `--bare` Flag für 10× SDK-Startup
- **Difficulty:** Advanced
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Skippt Search nach lokaler CLAUDE.md/Settings/MCPs.

### #14.07 — `--add-dir` (oder `/add-dir`)
- **Difficulty:** Intermediate
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

Gibt Claude Zugriff auf zusätzliche Repos.

### #14.08 — `--name "<session>"`
- **Difficulty:** Beginner
- **Date:** 2026-03-13
- **Source:** [X-Thread](https://x.com/bcherny/status/2032632602629386348)
- **Author:** @bcherny

Human-readable Session-Namen für parallele Arbeit.

### #14.09 — `claude` ist Unix-Utility, kein Chatbot
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

"Cat the CSV, pipe it into claude."

### #14.10 — Stack: React Ink + Commander.js + Bun
- **Difficulty:** Intermediate
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

Für eigene CLI-Tools übertragbar.

---

## 15 — Code Review

### #15.01 — Automatic PR Review durch ein Agent-Team
- **Difficulty:** Beginner
- **Date:** 2026-03-09
- **Source:** [X-Thread](https://x.com/bcherny/status/2031089411820228645)
- **Author:** @bcherny

Jeder Agent fokussiert auf andere Concerns (Logic, Security, Performance), postet Inline-Kommentare.

### #15.02 — Reviews waren der Bottleneck
- **Difficulty:** Beginner
- **Date:** 2026-03-09
- **Source:** [X-Thread](https://x.com/bcherny/status/2031089411820228645)
- **Author:** @bcherny
- **Quote:** "Code output per engineer is up 200% this year"

### #15.03 — Boris nutzte es wochenlang vor Launch
- **Difficulty:** Beginner
- **Date:** 2026-03-09
- **Source:** [X-Thread](https://x.com/bcherny/status/2031089411820228645)
- **Author:** @bcherny
- **Quote:** "It catches real bugs I wouldn't have noticed otherwise"

---

## 16 — Cost / ROI

### #16.01 — ROI-Frage, keine Cost-Frage
- **Difficulty:** Beginner
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny
- **Quote:** "An engineer 50, 70% more productive — that's worth a lot"

### #16.02 — ~$6/Tag pro aktivem User
- **Difficulty:** Beginner
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @catwu

### #16.03 — Manche Anthropic-Engineers > $1.000/Monat
- **Difficulty:** Beginner
- **Date:** 2025-11-15
- **Source:** [AI & I Podcast](https://every.to/podcast/how-to-use-claude-code-like-the-people-who-built-it)
- **Author:** @bcherny

Hauptsächlich für Code-Migrationen.

### #16.04 — Teams unter-funden, Tokens unlimited geben
- **Difficulty:** Beginner
- **Date:** 2026-02-19
- **Source:** [Lenny's Podcast](https://www.lennysnewsletter.com/p/head-of-claude-code-what-happens)
- **Author:** @bcherny
- **Quote:** "Start by giving engineers as many tokens as possible"

### #16.05 — 1-Stunden Prompt Cache
- **Difficulty:** Advanced
- **Date:** 2026-04-13
- **Source:** [X-Thread](https://x.com/bcherny/status/2043715713551212834)
- **Author:** @bcherny

Massive Kosten-Reduktion für wiederholte Multi-Turn-Agent-Arbeit.

---

## 17 — Form-Factor & Workflow

### #17.01 — Claude Code hat eine Mobile-App
- **Difficulty:** Beginner
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny

iOS und Android. Boris schreibt viel Code aus der iOS-App.

### #17.02 — Dispatch — Secure Remote Control
- **Difficulty:** Advanced
- **Date:** 2026-03-29
- **Source:** [X-Thread](https://x.com/bcherny/status/2038454336355999749)
- **Author:** @bcherny
- **Quote:** "When I'm not coding, I'm dispatching"

Nutzt MCPs/Browser/Computer mit deinen Permissions.

### #17.03 — VS Code / JetBrains / Cursor Extension
- **Difficulty:** Beginner
- **Date:** 2025-04-18
- **Source:** [Anthropic Docs](https://docs.claude.com)
- **Author:** @bcherny

Empfohlen für IDE-Nutzer: Inline-Diffs, @-Mentions, Plan-Review.

### #17.04 — GitHub-App / Slack-App / Web
- **Difficulty:** Beginner
- **Date:** 2026-04-15
- **Source:** [Threads](https://www.threads.com/@boris_cherny)
- **Author:** @bcherny

"Every engineer is different and you can use Claude Code the way you want."

### #17.05 — 4 Modi der Claude-Code-Nutzung
- **Difficulty:** Beginner
- **Date:** 2025-06-15
- **Source:** AIEWF Talk 2025
- **Author:** @bcherny

Terminal / IDE-Extension / GitHub-App / SDK als Unix-Utility.

### #17.06 — Workflow zum Task anpassen
- **Difficulty:** Intermediate
- **Date:** 2025-06-15
- **Source:** AIEWF Talk 2025
- **Author:** @bcherny

(explore › plan › confirm › code › commit) vs (tests › commit › code › iterate) vs (code › screenshot › iterate).

---

## 18 — Migration & Daten

### #18.01 — Migrationen immer zu Ende führen
- **Difficulty:** Advanced
- **Date:** 2026-02-19
- **Source:** [Pragmatic Engineer](https://newsletter.pragmaticengineer.com/p/building-claude-code-with-boris-cherny)
- **Author:** @bcherny
- **Quote:** "When you start a migration, finish the migration"

Partiell-migrierte Codebases verwirren Menschen und Modelle.

### #18.02 — `/batch` ist das Migration-Tool
- **Difficulty:** Advanced
- **Date:** 2026-02-27
- **Source:** [X-Thread](https://x.com/bcherny/status/2027534984534544489)
- **Author:** @bcherny

Interaktiv planen, dann zu dutzenden Worktree-Agents auffächern.

### #18.03 — BigQuery-Skill in Codebase einchecken
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Ganzes Team nutzt es für Analytics direkt aus Claude Code.

---

## 19 — Lernen & Onboarding

### #19.01 — Explanatory / Learning Output Style
- **Difficulty:** Beginner
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Claude erklärt das *Warum* hinter Changes.

### #19.02 — Visual HTML-Presentation generieren
- **Difficulty:** Beginner
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "Surprisingly good slides!"

### #19.03 — ASCII-Diagramme erfragen
- **Difficulty:** Beginner
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Von neuen Protokollen, Codebases, Architekturen.

### #19.04 — Spaced-Repetition-Learning-Skill
- **Difficulty:** Advanced
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Du erklärst dein Verständnis, Claude stellt Follow-up-Fragen.

### #19.05 — Onboarding-Workflow bei Anthropic
- **Difficulty:** Beginner
- **Date:** 2025-04-18
- **Source:** [Anthropic Blog](https://www.anthropic.com/engineering/claude-code-best-practices)
- **Author:** @bcherny

Neue Engineers nutzen Claude Code, um Codebases zu navigieren.

---

## 20 — Context Management

### #20.01 — Auto-Compact-Threshold absenken
- **Difficulty:** Advanced
- **Date:** 2026-04-15
- **Source:** [X (RT Thariq)](https://x.com/bcherny/status/2044548257058328723)
- **Author:** @thariq (RT @bcherny)

`CLAUDE_CODE_AUTO_COMPACT_WINDOW=400000 claude`, um Context-Rot im 1M-Modell zu umgehen.

### #20.02 — Context-Rot startet bei 300–400k Tokens
- **Difficulty:** Advanced
- **Date:** 2026-04-15
- **Source:** [X (RT Thariq)](https://x.com/bcherny/status/2044548257058328723)
- **Author:** @thariq (RT @bcherny)

Lass intelligenz-sensitive Sessions nicht darüber hinaus driften.

### #20.03 — "Dumb Zone" bei ~40% Kontext
- **Difficulty:** Advanced
- **Date:** 2026-04-15
- **Source:** [X (RT Thariq)](https://x.com/bcherny/status/2044548257058328723)
- **Author:** @thariq (RT @bcherny)

Newcomers: unter 40% halten. Erfahrene: unter 30%; 60% nur bei simplen Tasks.

### #20.04 — Jeder Turn ist ein Branching-Point
- **Difficulty:** Advanced
- **Date:** 2026-04-15
- **Source:** [X (RT Thariq)](https://x.com/bcherny/status/2044548257058328723)
- **Author:** @thariq (RT @bcherny)

Pick Continue / `/rewind` / `/clear` / `/compact` / Subagent.

### #20.05 — Agentic Search > RAG
- **Difficulty:** Advanced
- **Date:** 2025-05-07
- **Source:** [Latent Space](https://www.latent.space/p/claude-code)
- **Author:** @bcherny

"Just using regular code searching, you know, glob, grep." Umgeht Indexing/Sync/Security-Probleme.

---

## 21 — Terminal Environment

### #21.01 — Ghostty Terminal
- **Difficulty:** Beginner
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Team-Liebling: synchronized Rendering, 24-bit Color, Unicode.

### #21.02 — tmux für ein Tab pro Task
- **Difficulty:** Intermediate
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny

Terminal-Tabs nach Color-Coden und Namen organisieren.

### #21.03 — Voice-Dictation (fn x2 auf macOS)
- **Difficulty:** Beginner
- **Date:** 2026-01-31
- **Source:** [X-Thread](https://x.com/bcherny/status/2017742741636321619)
- **Author:** @bcherny
- **Quote:** "You speak 3x faster than you type"

---

## Tracking Metadata

<!-- Automation reads from here. Do not delete. -->

```yaml
last_scan_iso: "2026-05-12T20:00:00Z"
last_scan_anchor_tweet_id: "2044847848035156457"
last_tip_id_per_theme:
  "01": 9
  "02": 6
  "03": 11
  "04": 34
  "05": 12
  "06": 9
  "07": 7
  "08": 7
  "09": 9
  "10": 11
  "11": 6
  "12": 6
  "13": 6
  "14": 10
  "15": 3
  "16": 5
  "17": 6
  "18": 3
  "19": 5
  "20": 5
  "21": 3
total_tips: 132
```

<!-- End tracking metadata -->
