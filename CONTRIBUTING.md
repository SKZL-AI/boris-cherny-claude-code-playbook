# Contributing

Vielen Dank fürs Interesse! Dieses Repo wächst primär automatisiert via Claude.ai Routines, aber manuelle Beiträge sind willkommen.

## Was du beitragen kannst

### 1. Neuer Tipp, den die Routine übersehen hat

Wenn du einen öffentlichen Boris-Cherny-Tipp findest, der noch nicht im Repo ist:

1. Fork das Repo
2. Öffne mit Claude Code: `cd boris-cherny-claude-code-playbook && claude`
3. Führe `/add-tip` aus — der Slash-Command interviewt dich strukturiert
4. Pull Request mit Source-URL in der Beschreibung

**Kriterien für Aufnahme:**
- Quelle muss öffentlich verifizierbar sein (X, Podcast, Blog, Konferenz-Aufnahme)
- Autor: @bcherny oder Claude-Code-Team-Member endorsed von Boris
- Konkret handlungs-relevant, kein reines Marketing/Status

### 2. Korrektur eines existierenden Tipps

Wenn ein Tipp inhaltlich falsch ist, Source-URL tot, oder Übersetzung holprig:

1. Fork
2. Editiere `TIPS.md` direkt
3. **Wichtig:** ID NICHT ändern. Auch deprecated Tipps behalten ihre ID.
4. Aktualisiere `index.html` via `/regenerate-html` oder manuell
5. Pull Request mit Begründung

### 3. Übersetzungsverbesserungen

Wenn dir bessere deutsche Formulierungen einfallen — gerne. Verbatim-Boris-Zitate bleiben aber Englisch.

### 4. Neues Theme

Sollte ein Boris-Tipp ein 22. Thema einführen (z.B. "Voice-Workflows"):

1. Issue eröffnen mit dem Proposal: Theme-Name, Begründung, 2–3 Beispiel-Tipps
2. Diskussion abwarten
3. Bei Approval: PR mit Änderungen in `TIPS.md`, `README.md` (Tabelle), `index.html` (TOC + neue `<section>`)

## Pull-Request-Checkliste

- [ ] Source-URL des Tipps in der PR-Beschreibung
- [ ] Tipp-ID folgt dem Format `TT.NN` (Theme-Number . laufende Nummer)
- [ ] Difficulty ist `beginner` | `intermediate` | `advanced` (keine anderen Werte)
- [ ] Datum im Format `YYYY-MM-DD` in TIPS.md, `DD. MMM YYYY` in der Anzeige
- [ ] Englische Verbatim-Zitate in Anführungszeichen, unter 15 Wörter
- [ ] Deutsche Beschreibung 1–3 Sätze, kein Marketing-Speak
- [ ] CHANGELOG-Eintrag in `CHANGELOG.md` oben hinzugefügt
- [ ] `index.html` ist synchron mit `TIPS.md` (`/regenerate-html` gelaufen)

## Was wir NICHT akzeptieren

- Tipps aus privaten Quellen (geleakte Slack-Screenshots, interne Anthropic-Dokumente)
- Tipps anderer Personen, auch wenn die mit Boris zusammen arbeiten — außer Boris hat sie explizit retweetet/endorsed
- KI-generierte Tipps, die "klingen wie Boris" aber nicht von ihm sind
- Eigene Best-Practices, die kein Boris-Ursprung haben (mach dafür dein eigenes Repo)

## Stil-Guide

- **Deutsche Prosa**, technische Begriffe (Worktree, Subagent, Hook, Slash Command) auf Englisch in *kursiv* oder code-formatiert
- **Knapp, kein Filler**. Boris ist direkt; das Repo sollte es auch sein.
- **Code-Snippets in Backticks**: `inline` für Befehle, ```` ``` ```` für Blocks
- **Keine Emojis im Tipp-Text** (außer im CHANGELOG wo sie strukturierend sind)
- **Source-Links mit `↗`-Suffix** im HTML, plain Markdown-Links in TIPS.md

## Mit dem Maintainer Kontakt aufnehmen

Owner dieses Repos: SAKIZLI.AI (Furkan Sakizli).

- Issues: für Fragen, Bug-Reports, Theme-Proposals
- Direct: über das Profil von [@sakizli](https://github.com/sakizli) auf GitHub

Für inhaltliche Fragen zu Claude Code selbst: nicht dieses Repo, sondern [Anthropic Docs](https://docs.claude.com) oder [Anthropic Support](https://support.claude.com).

## Code of Conduct

- Sei respektvoll. Streite über Inhalte, nicht über Personen.
- Wenn jemand einen Tipp anders interpretiert — diskutiere im PR, nicht im Subtext.
- Englisch und Deutsch sind beide OK in Issues/PRs.
