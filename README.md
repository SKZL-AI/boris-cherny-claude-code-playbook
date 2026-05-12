![Tips](https://img.shields.io/badge/Tips-132-blue)
![Themes](https://img.shields.io/badge/Themes-21-green)
![Auto-Updated](https://img.shields.io/badge/Auto--Updated-2--3x%20daily-orange)
![License](https://img.shields.io/badge/License-MIT-yellow)

> **132 tips from the Head of Claude Code at Anthropic — auto-updated daily.**
> *Feed the [Implementation Guide](./IMPLEMENTATION-GUIDE.md) to Claude Code and auto-configure your project in one shot.*

# Boris Cherny Claude Code Playbook

> Eine kuratierte, deutschsprachige Sammlung aller öffentlichen Claude-Code-Tipps von **Boris Cherny** ([@bcherny](https://x.com/bcherny)), Head of Claude Code bei Anthropic — automatisch aktualisiert via Claude.ai Routines.

**[→ Visuelles Dashboard ansehen (index.html)](./index.html)** &nbsp; · &nbsp; **[→ Vollständige Tipp-Liste (TIPS.md)](./TIPS.md)** &nbsp; · &nbsp; **[→ One-Shot Setup Guide (IMPLEMENTATION-GUIDE.md)](./IMPLEMENTATION-GUIDE.md)** &nbsp; · &nbsp; **[→ Changelog](./CHANGELOG.md)**

---

## Schnellstart in 30 Sekunden

### Option 1: Alles automatisch einrichten lassen
```bash
git clone https://github.com/SKZL-AI/boris-cherny-claude-code-playbook.git
cd boris-cherny-claude-code-playbook
# Feed the implementation guide to Claude Code:
cat IMPLEMENTATION-GUIDE.md | claude -p "Execute all setup instructions for my project"
```

### Option 2: Nur lesen
Öffne [index.html](./index.html) lokal im Browser — oder lies [TIPS.md](./TIPS.md).

### Option 3: Einzelne Tipps umsetzen
Öffne [IMPLEMENTATION-GUIDE.md](./IMPLEMENTATION-GUIDE.md) und kopiere die Sections, die dich interessieren.

---

## Warum dieses Repo?

1. **Erste vollständige Sammlung** aller öffentlichen Boris-Cherny-Tipps an einem Ort — 132 Tipps, 21 Themen
2. **Automatisch aktuell** — Claude.ai Routines scannen 2–3× täglich nach neuen Tipps
3. **Sofort nutzbar** — [IMPLEMENTATION-GUIDE.md](./IMPLEMENTATION-GUIDE.md) lässt Claude Code dein Projekt in Minuten einrichten
4. **Visuelles Dashboard** — Filter, Timeline, Schwierigkeitsgrade auf einen Blick
5. **Deutsche Sprache** — Erste deutschsprachige Ressource für das Claude Code Ecosystem

---

## Worum es geht

Boris Cherny startete Claude Code im September 2024 als Side-Project bei Anthropic. Seit dem öffentlichen Launch am 24. Februar 2025 hat er regelmäßig Tipps, Workflows und Best Practices geteilt — auf X/Twitter, in Podcasts (Latent Space, Lenny's Podcast, AI & I, Pragmatic Engineer), auf Konferenzen (AI Engineer World's Fair) und im Anthropic-Engineering-Blog.

Dieses Repo bündelt diese Tipps an einer Stelle, übersetzt sie ins Deutsche, klassifiziert nach Schwierigkeitsgrad und Thema, und hält sie über automatisierte X-Scans aktuell.

**Aktuell:** 132 Tipps in 21 Themen, dokumentiert über 14 Monate.

---

## TL;DR — Boris' Setup in drei Sätzen

1. **Verifikation ist die #1-Regel:** "Give Claude a way to verify its work — it will 2–3× the quality." Wenn du nur eine Sache mitnimmst, dann diese.
2. **Parallelität ist der größte Hebel:** 5 Claudes in Terminal-Tabs + 5–10 Web-Sessions + Mobile + Worktrees. "I have dozens of Claudes running at all times."
3. **Plan-Mode → Auto-Accept:** Shift+Tab zweimal, mit Claude iterieren bis der Plan gut ist, dann durchlaufen lassen. Ein guter Plan one-shottet die Implementierung fast immer.

---

## Inhalt

- **[TIPS.md](./TIPS.md)** — Alle 132 Tipps, strukturiert nach Themen und Schwierigkeit. Source of truth für die Automatisierung.
- **[IMPLEMENTATION-GUIDE.md](./IMPLEMENTATION-GUIDE.md)** — ~70 actionable Tipps, strukturiert als ausführbare Instruktionen für Claude Code. One-shot Setup.
- **[index.html](./index.html)** — Visuelles Dashboard mit Filter, Timeline, Stages und Caveats. Lokal öffnen oder auf GitHub Pages hosten.
- **[CHANGELOG.md](./CHANGELOG.md)** — Welche Tipps wann hinzugefügt wurden.
- **[CONTRIBUTING.md](./CONTRIBUTING.md)** — Wie du selbst Tipps beisteuerst.
- **[routines/](./routines/)** — Setup-Anleitung und Prompts für Claude.ai Routines, die das Repo automatisch aktualisieren.
- **[.claude/](./.claude/)** — Slash-Commands und Subagents für die lokale Arbeit mit Claude Code.

---

## Die 21 Themen im Überblick

| # | Thema | Tipps | Boris' Kerngedanke |
|---|---|---:|---|
| 01 | Parallele Ausführung | 9 | "The single biggest productivity unlock" |
| 02 | Plan Mode | 6 | "A good plan is really important" |
| 03 | CLAUDE.md | 11 | "Anytime Claude does something wrong, we add it to the CLAUDE.md" |
| 04 | Slash Commands | 34 | Inner-Loop-Automation für tägliche Workflows |
| 05 | Subagents | 12 | Unkorrelierte Kontextfenster, nicht Anthropomorphisierung |
| 06 | Hooks | 9 | Deterministische Logik wo das Modell unzuverlässig ist |
| 07 | Permissions & Safety | 7 | Pre-allow > skip; Sandbox > danger flag |
| 08 | MCP & Integrationen | 7 | Slack, BigQuery, Sentry — Claude über das Repo hinaus |
| 09 | Modell & Effort | 9 | Opus mit Thinking für alles (Boris) |
| 10 | Verifikation | 11 | **Die #1-Regel: 2–3× Qualität durch Verifikation** |
| 11 | Long-Running & Recaps | 6 | Routines, Schedules, Stop-Hooks |
| 12 | Prompting & Specs | 6 | Delegation > Guidance |
| 13 | Customization | 6 | 37 Settings, 84 Env-Variablen |
| 14 | Headless / SDK | 10 | Claude als Unix-Utility |
| 15 | Code Review | 3 | "Reviews waren der Bottleneck" |
| 16 | Cost / ROI | 5 | "It's an ROI question, not a cost question" |
| 17 | Form-Factor | 6 | CLI, IDE, GitHub, Slack, Mobile, Web |
| 18 | Migration & Daten | 3 | Beende, was du beginnst |
| 19 | Lernen & Onboarding | 5 | Explanatory Output Style |
| 20 | Context Management | 5 | Context-Rot bei 300–400k Tokens |
| 21 | Terminal Environment | 3 | Ghostty + tmux + Voice |

---

## Staged Adoption — Boris' eigene Empfehlung

| Phase | Wann | Was machen |
|---|---|---|
| **1. Vanilla** | Woche 1 | `/init`, Plan-Mode, nicht customizen |
| **2. Compounding Knowledge** | Woche 2–3 | CLAUDE.md ausbauen, 1–2 Slash Commands |
| **3. Parallelism** | Woche 4+ | 3–5 Worktrees, PostToolUse-Hook, geteilte settings.json |
| **4. Subagents** | Monat 2+ | code-simplifier, verify-app, adversariales Review |
| **5. Autonomy** | Monat 3+ | Auto Mode, `/loop`, `/schedule`, Voice, Chrome-Extension |

Details und Übergangskriterien siehe [index.html](./index.html) oder [TIPS.md](./TIPS.md#staged-adoption).

---

## Wichtige Chronologie-Punkte

- **Sep 2024** — Boris startet Claude Code als Side-Project
- **24. Feb 2025** — Claude Code Launch als Research Preview
- **02. Jan 2026** — Canonical 13-Tipp-Thread "How I use Claude Code" (104K Likes)
- **31. Jan 2026** — 10 Team-Tipps Thread (8.5M Views)
- **29.–30. Mär 2026** — 15 versteckte Features Thread
- **16. Apr 2026** — 6 Opus 4.7 Tipps Thread
- **22. Apr 2026** — Claude Code gewinnt Webby Award

Vollständige Chronologie: siehe [index.html](./index.html) oder [CHANGELOG.md](./CHANGELOG.md).

---

## Wie dieses Repo aktuell gehalten wird

Eine **Claude.ai Routine** scannt 2–3× täglich [@bcherny auf X](https://x.com/bcherny) sowie sekundäre Quellen (Threads.net, Anthropic-Blog, Threadreader-Mirror) nach neuen Tipps. Werden neue gefunden:

1. Tipp wird in [`TIPS.md`](./TIPS.md) eingefügt (richtige Theme-Section, neue ID)
2. [`CHANGELOG.md`](./CHANGELOG.md) wird aktualisiert
3. [`index.html`](./index.html) wird via `/regenerate-html` Slash-Command synchronisiert
4. [`IMPLEMENTATION-GUIDE.md`](./IMPLEMENTATION-GUIDE.md) wird aktualisiert, falls der Tipp actionable ist
5. Commit + Push auf GitHub via GitHub-Connector

Setup-Anleitung: **[routines/setup.md](./routines/setup.md)**
Routine-Prompts: **[routines/daily-scan.md](./routines/daily-scan.md)** und **[routines/weekly-verify.md](./routines/weekly-verify.md)**

---

## Wie du das selbst nutzt

### Schnellstart als Leser

Öffne [`index.html`](./index.html) lokal im Browser — Filter nach Schwierigkeit, Sprung zu Themen, alle Quellen verlinkt.

### Schnellstart als Claude Code User

```bash
git clone https://github.com/SKZL-AI/boris-cherny-claude-code-playbook.git
# Kopiere IMPLEMENTATION-GUIDE.md in dein eigenes Projekt und führe sie aus:
cp boris-cherny-claude-code-playbook/IMPLEMENTATION-GUIDE.md mein-projekt/
cd mein-projekt
claude  # Claude Code öffnen
> Read IMPLEMENTATION-GUIDE.md and execute the setup instructions
```

### Schnellstart als Fork-Maintainer

```bash
git clone https://github.com/SKZL-AI/boris-cherny-claude-code-playbook.git
cd boris-cherny-claude-code-playbook
claude  # Claude Code öffnen
> /add-tip
```

Slash-Commands:

- `/add-tip` — Neuen Tipp strukturiert hinzufügen (interviewt dich Schritt für Schritt)
- `/scan-x` — Manueller X-Scan nach neuen Tipps
- `/verify-sources` — Alle Source-URLs prüfen
- `/regenerate-html` — `index.html` aus `TIPS.md` neu bauen

Siehe [`.claude/commands/`](./.claude/commands/) für die vollständigen Prompts.

---

## Caveats

- **Plan-Tier-gating:** Viele Features (Auto Mode, 1M-Kontext) sind Max/Team/Enterprise-only. Testen, nicht annehmen.
- **Direktionale Zahlen:** "4% aller GitHub-Commits", "200% Engineering-Produktivität" sind Boris' eigene Angaben aus Podcasts, nicht unabhängig auditiert.
- **Sekundärquellen:** Tipps zugeschrieben an Thariq, Cat Wu, Erik Schluntz u.a. aus dem Claude-Code-Team sind inkludiert, wenn Boris sie retweetet/endorsed hat.
- **Kein Inhalt** in diesem Repo stammt aus privaten oder geleakten Quellen. Alles aus öffentlichem X, Podcasts, Anthropic-Blog oder dem Threads.net-Mirror.
- **Ultrathink-Semantik** wechselte zwischen CC v1 und v2 — siehe [TIPS.md](./TIPS.md#09-modell--effort) für Details.

---

## Attribution

Alle Tipps stammen ursprünglich von **Boris Cherny** (Anthropic) und dem Claude-Code-Team. Dieses Repo ist eine inoffizielle deutschsprachige Kuration. Nicht von Anthropic affiliiert.

Primärquellen-Aggregator: [howborisusesclaudecode.com](https://howborisusesclaudecode.com) (von [@CarolinaCherry](https://x.com/CarolinaCherry)).

## Lizenz

MIT (siehe [LICENSE](./LICENSE)). Die zugrundeliegenden Tipps sind geistiges Eigentum der jeweiligen Autoren. Diese Kuration darf frei kopiert und angepasst werden, vorausgesetzt die Quellenangaben bleiben erhalten.

---

Wenn dir dieses Repo hilft, [gib ihm einen ⭐](https://github.com/SKZL-AI/boris-cherny-claude-code-playbook) — das hilft anderen, es zu finden.

---

*Maintained by [SKZL-AI](https://github.com/SKZL-AI) · Last full audit: 2026-05-13*
