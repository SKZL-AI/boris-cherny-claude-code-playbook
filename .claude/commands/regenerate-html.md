---
description: Rebuild index.html from TIPS.md, preserving the design
---

# /regenerate-html — Rebuild Dashboard

Synchronisiert `index.html` mit `TIPS.md`. Verwende dies, nachdem `TIPS.md` durch `/add-tip`, `/scan-x` oder die Routine geändert wurde.

## Workflow

### Schritt 1 — TIPS.md parsen
Lies TIPS.md. Extrahiere:
- Alle 21 Theme-Sections (`## NN — Theme Name`)
- Alle Tipps pro Theme: ID, Titel, Difficulty, Date, Source-URL, Autor, Quote (optional), Beschreibung

### Schritt 2 — index.html im Repo öffnen
Lies die existierende `index.html`. Die Struktur ist:
- `<header>` mit Stats und Meta
- `<section class="theme-section" id="t<NN>">` für jede der 21 Themes
- Innerhalb: `<div class="tip-grid">` mit `<article class="tip" data-diff="...">` pro Tipp
- Timeline, Stages, Contested, Caveats, Footer

**Wichtig:** Das CSS und JS am Anfang/Ende des Dokuments NICHT anfassen. Nur den `<main>`-Inhalt aktualisieren.

### Schritt 3 — Diff TIPS.md vs index.html
Für jeden Tipp in TIPS.md:
- Wenn die ID in index.html existiert → updaten (Inhalt überschreiben, Position nach ID-Reihenfolge)
- Wenn die ID NICHT existiert → neues `<article>` ans Ende der entsprechenden Theme-Section anhängen
- Wenn eine ID in index.html existiert, aber NICHT in TIPS.md → markiert als `[deprecated]`, NICHT löschen (Sticky IDs)

### Schritt 4 — Article-Template
Pro Tipp ein `<article>`:

```html
<article class="tip" data-diff="<difficulty-lowercase>">
  <div class="tip-meta">
    <span class="tip-num"><TT.NN></span>
    <span class="diff diff-<difficulty-lowercase>"><Difficulty></span>
  </div>
  <h3><Titel-aus-TIPS.md></h3>
  <p><Beschreibung mit <code>inline</code> wenn Markdown-Code-Spans vorhanden.></p>
  <div class="tip-footer">
    <span><DD. MMM YYYY></span>
    <a class="tip-source" href="<URL>" target="_blank"><Source-Label> ↗</a>
  </div>
</article>
```

Source-Label-Mapping:
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
- AIEWF / no URL → Plain `<span>AIEWF Talk</span>` ohne Link

### Schritt 5 — Header / Footer aktualisieren
Im `<header>`:
- `<span><strong>NNN+</strong> Tipps</span>` → tatsächliche `total_tips` aus YAML-Tracker

Im `<footer>`:
- `NN Tipps · 21 Themen · NN Monate` → aktualisieren
- `Last full audit: YYYY-MM-DD` → aktuelles Datum

In den Stats-Cards: keine Änderung (Boris' eigene Stats sind statisch).

### Schritt 6 — Validation
Vor dem Speichern:
- Zähle `<article class="tip">` — muss `total_tips` aus TIPS.md matchen
- Prüfe ob alle 21 Themes vorhanden sind (`id="t1"` bis `id="t21"`)
- Prüfe ob keine Theme-Section leer ist (nicht wahrscheinlich, aber check)

### Schritt 7 — Datei schreiben
Schreibe die neue `index.html` an gleiche Stelle. Backup ist via git diff verfügbar.

### Schritt 8 — Visuelle Verifikation (optional)
Wenn der Nutzer ein Browser-MCP / Chrome-Extension hat: öffne `index.html` lokal und mache einen Screenshot. Vergleiche mit Erwartung.

Sonst nur kurzer Report:
```
✅ index.html regeneriert
- N Tipps in HTML (matches TIPS.md)
- 21 Theme-Sections
- Header/Footer-Counts aktualisiert
- File-Size: NNN KB
```

## Wichtig

- **Kein Auto-Commit.** Der Nutzer prüft das Diff selbst, dann committet.
- **CSS/JS unangetastet.** Wenn das Design refactored werden soll, ist das ein separater Task.
- **Sticky IDs.** Auch deprecated Tipps bleiben in index.html, nur mit `[deprecated]` Tag.
- **Bei Schema-Drift:** Wenn TIPS.md ein unerwartetes Format hat (z.B. fehlt `**Difficulty:**`), abbrechen und melden — keine raten.

## Alternative: vollständig neu bauen

Wenn der Diff-Approach zu fehleranfällig wirkt (z.B. nach großem Refactoring), kannst du auch:
1. Komplette `<main>` aus TIPS.md neu generieren
2. CSS/JS aus alter index.html behalten
3. Zusammenfügen

Das ist robuster aber langsamer und produziert größere git-diffs.
