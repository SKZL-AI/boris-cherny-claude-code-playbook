---
description: Add a new Boris Cherny tip to TIPS.md with full structured fields
---

# /add-tip — Interactive Tip Addition

Du bist im boris-cherny-claude-code-playbook Repo. Der Nutzer möchte einen neuen Tipp hinzufügen.

## Workflow

### Schritt 1 — Quelle erfragen
Frage: "Wo hast du den Tipp gefunden? Bitte URL oder kurze Beschreibung."

Mögliche Quellen:
- X/Twitter Post (URL gibt Tweet-ID)
- Podcast (welcher, ggf. mit Timestamp)
- Anthropic Blog (URL)
- Konferenz-Talk (welcher)
- Sekundärquelle (Newsletter, Blog) — dann original verify

### Schritt 2 — Quelle prüfen (web_fetch)
Lade die URL mit web_fetch. Verifiziere:
- Ist der Autor @bcherny (oder Anthropic-Team-Member endorsed von Boris)?
- Ist das wirklich ein Tipp / Workflow / Best Practice — kein reines Status-Update?
- Datum des Posts identifizieren

Wenn die Quelle nicht passt, sage es offen. Kein Tipp wird erfunden.

### Schritt 3 — Theme zuordnen
21 existierende Themen (Liste in TIPS.md):
01 Parallele Ausführung | 02 Plan Mode | 03 CLAUDE.md | 04 Slash Commands |
05 Subagents | 06 Hooks | 07 Permissions & Safety | 08 MCP & Integrationen |
09 Modell & Effort | 10 Verifikation | 11 Long-Running & Recaps |
12 Prompting & Specs | 13 Customization | 14 Headless / SDK |
15 Code Review | 16 Cost / ROI | 17 Form-Factor | 18 Migration & Daten |
19 Lernen & Onboarding | 20 Context Management | 21 Terminal Environment

Wenn keines passt: frage den Nutzer, ob ein neues Theme angelegt werden soll
(dann muss auch index.html, README.md, und der TOC erweitert werden — größeres Refactoring).

### Schritt 4 — Felder zusammenstellen
Erstelle einen Vorschlag mit allen Feldern, zeige ihn dem Nutzer zur Bestätigung:

```
### #<TT.NN> — <Titel>
- **Difficulty:** <Beginner|Intermediate|Advanced>
- **Date:** <YYYY-MM-DD>
- **Source:** [<Type>](<URL>)
- **Author:** @<author>
- **Quote:** "<optional verbatim, < 15 words>"

<Deutsche Beschreibung, 1–3 Sätze.>
```

ID-Vergabe: schaue im YAML-Tracker am Ende von TIPS.md unter
`last_tip_id_per_theme."<TT>"` und nimm N+1.

Schwierigkeits-Heuristik:
- Beginner: Sofort umsetzbar, ohne Vorkenntnisse, kein Risiko
- Intermediate: Setup nötig (Config-File, Hook), oder Tool-Kombination
- Advanced: Mehrere Components, Custom-Code, Risiko bei falscher Anwendung

### Schritt 5 — Nutzer-Bestätigung einholen
Zeige den Entwurf und frage: "OK so? Soll ich einfügen?"

Bei Korrekturen: iteriere. Bei OK: weiter zu Schritt 6.

### Schritt 6 — TIPS.md einfügen
- Theme-Section finden (z.B. `## 04 — Slash Commands`)
- Vor der nächsten `---` Trennlinie einfügen
- YAML-Tracker am Ende aktualisieren:
  - `last_tip_id_per_theme."<TT>"` erhöhen
  - `total_tips` +1

### Schritt 7 — CHANGELOG-Eintrag
Oben in CHANGELOG.md (unter H1) einfügen:

```
## <YYYY-MM-DD> — Manual Addition (via /add-tip)

- ➕ Added tip #<TT.NN>: <Titel>
  - Source: <URL>
  - Added by: SAI
```

### Schritt 7b — IMPLEMENTATION-GUIDE.md prüfen
Prüfe: Ist dieser Tipp actionable (kann Claude Code ihn ausführen/konfigurieren)?

Actionable-Kategorien:
- CLAUDE.md-Setup (Theme 03)
- Slash Commands (Theme 04)
- Subagents (Theme 05)
- Hooks (Theme 06)
- Permissions & Safety (Theme 07)
- MCP & Integrationen (Theme 08)
- Modell & Effort (Theme 09, nur Konfiguration)
- Verifikation (Theme 10, nur Setup-Patterns)
- Customization (Theme 13)
- Headless / SDK (Theme 14)
- Context Management (Theme 20)

Wenn ja: Frage den Nutzer:
"Dieser Tipp ist actionable. Soll ich ihn auch in IMPLEMENTATION-GUIDE.md einpflegen? (Empfohlen: ja)"

Bei Ja:
  1. Öffne IMPLEMENTATION-GUIDE.md
  2. Finde die passende Section (1–10)
  3. Füge den Tipp als ausführbaren Instruktionsblock ein
  4. Aktualisiere die Tip-ID-Referenz in Appendix D
  5. Füge IMPLEMENTATION-GUIDE.md zur Commit-Vorschlag-Liste hinzu

Bei Nein: weiter zu Schritt 8.

### Schritt 8 — Frage nach HTML-Sync
Frage: "Soll ich auch index.html aktualisieren? (Empfohlen ja, sonst läuft das Dashboard out of sync.)"

Bei Ja: führe `/regenerate-html` aus (siehe regenerate-html.md).

### Schritt 9 — Commit-Vorschlag
Mache KEINEN automatischen Commit — der Nutzer kommittet selbst. Aber zeige den vorgeschlagenen Commit-Befehl:

```bash
git add TIPS.md CHANGELOG.md index.html
git commit -m "Add tip #<TT.NN>: <Titel>"
git push
```

## Wichtig

- **Keine Eile.** Lieber langsam und korrekt als schnell und falsch.
- **Im Zweifel nachfragen.** Bei mehrdeutigen Quellen, unklarer Difficulty, oder grenzwertigen Tipps — frage.
- **Nichts erfinden.** Wenn die Quelle nicht wirklich einen Tipp enthält, beende den Workflow und erkläre warum.
