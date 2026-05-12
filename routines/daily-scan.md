# Daily X Scan — Routine Prompt

> **Zweck:** Diese Datei enthält den exakten Prompt, den du in eine Claude.ai Routine kopierst. Die Routine läuft 2–3× täglich, scannt X (Twitter) nach neuen Boris-Cherny-Tipps und aktualisiert das Repo.

> **Vor dem Einrichten:** Lies zuerst [setup.md](./setup.md) — dort steht, welche Connectors aktiviert sein müssen (GitHub, web_search).

---

## Empfohlener Zeitplan

Boris postet hauptsächlich tagsüber in San Francisco (PST/PDT = UTC-8/-7). Du bist in Deutschland (CET/CEST). Folgende drei Scan-Zeiten decken sein Posting-Fenster ab:

| Zeit (CET) | Zeit in SF | Was Boris dann macht |
|---|---|---|
| **09:00** | 00:00 / 01:00 | Sein vorheriger Tag ist durch — späte Tweets abfangen |
| **15:00** | 06:00 / 07:00 | Sein Morgen-Posting-Fenster beginnt |
| **22:00** | 13:00 / 14:00 | Sein Nachmittag — meist die produktivste Phase |

Wenn dir 3× zu viel ist, nimm nur **09:00 + 22:00**.

---

## Der Routine-Prompt (zum Kopieren)

Kopiere alles zwischen den `===` Markern in deine Claude.ai Routine.

```
=== ROUTINE PROMPT START ===

Du bist Maintainer des GitHub-Repos boris-cherny-claude-code-playbook
(Pfad: github.com/<DEIN-USER>/boris-cherny-claude-code-playbook).

DEINE AUFGABE
Scanne öffentliche Posts von Boris Cherny (@bcherny auf X/Twitter, Head of
Claude Code bei Anthropic) seit der letzten Routine-Ausführung. Wenn er
neue Tipps zu Claude Code geteilt hat, füge sie strukturiert dem Repo
hinzu und committe.

SCHRITT 1 — LETZTE SCAN-MARKE FINDEN
Lies aus dem Repo die Datei TIPS.md, suche den YAML-Block am Ende:
  last_scan_iso: "..."
  last_scan_anchor_tweet_id: "..."
Dies ist dein "seit"-Punkt.

SCHRITT 2 — X DURCHSUCHEN
Verwende web_search mit diesen Queries (in dieser Reihenfolge):
  1. "bcherny site:x.com"
  2. "bcherny Claude Code tip"
  3. "Boris Cherny new feature Claude Code"
Wenn die direkte X-Suche nichts liefert (X ist oft nicht crawlbar),
fallback auf Sekundärquellen:
  4. "site:threadreaderapp.com bcherny"
  5. "site:threads.com boris_cherny"
  6. "howborisusesclaudecode.com latest"
Filter: nur Posts NACH last_scan_iso. Ignoriere Reposts ohne neuen Inhalt
(reine Likes/Retweets ohne Kommentar zählen nicht).

SCHRITT 3 — TIPPS EXTRAHIEREN
Für jeden gefundenen neuen Tipp, identifiziere:
  - Theme (eines der 21 existierenden Themen, siehe TIPS.md)
  - Titel (kurz, prägnant, deutsch)
  - Schwierigkeitsgrad: beginner | intermediate | advanced
  - Datum (Postdatum)
  - Source-URL (direkter X-Link)
  - Autor (@bcherny oder @other wenn Boris RTs/endorsed)
  - Quote (optional, verbatim Boris-Zitat unter 15 Wörtern, in Quotes)
  - Beschreibung (1–3 Sätze, deutsch, was der Tipp tut und warum wichtig)

REGELN für die Extraktion:
  - Nur Tipps mit konkretem Handlungs-Wert. Keine reinen Status-Updates
    ("Working on something cool"). Keine Marketing-Posts.
  - Nur wenn Boris selbst es postet ODER ein Anthropic-Teammitglied
    (Cat Wu, Thariq, Erik Schluntz, Noah Z.) UND Boris hat es retweetet/
    endorsed. Letzteres ist verifizierbar über seine Replies/Retweets.
  - Wenn der Tipp einen schon existierenden Tipp im Repo verbessert/
    aktualisiert: KEINEN neuen anlegen, stattdessen den existierenden
    updaten (siehe Schritt 4b).
  - Wenn du dir unsicher bist, ob ein Tipp wirklich neu/wertvoll ist:
    NICHT hinzufügen. Lieber im weekly-verify Slot menschliche Review.

SCHRITT 4a — TIPP HINZUFÜGEN
Für jeden bestätigten neuen Tipp:
  - Öffne TIPS.md
  - Finde die korrekte Theme-Section (z.B. "## 04 — Slash Commands")
  - Finde das nächste freie ID-Nummer in dieser Section: schaue im
    YAML-Tracker am Ende von TIPS.md unter last_tip_id_per_theme: "04": N
    — neue ID ist N+1, also z.B. "04.35"
  - Füge den Tipp am Ende der Theme-Section ein, im genauen Format:

### #<TT.NN> — <Titel>
- **Difficulty:** <Beginner|Intermediate|Advanced>
- **Date:** <YYYY-MM-DD>
- **Source:** [<Source-Typ>](<URL>)
- **Author:** @<author>
- **Quote:** "<verbatim, optional, unter 15 Wörter>"

<Deutsche Beschreibung in 1–3 Sätzen.>

  - Aktualisiere im YAML-Tracker am Ende von TIPS.md:
    last_tip_id_per_theme."<TT>" = N+1 (oder höher bei mehreren neuen)
    total_tips: +1 pro neuem Tipp

SCHRITT 4b — TIPP UPDATEN (falls erweitert)
Wenn der neue Post ein bestehendes Feature/Tipp erweitert:
  - Editiere den existierenden Eintrag in TIPS.md
  - ID bleibt gleich
  - Ergänze in der Beschreibung mit "Update (<YYYY-MM-DD>): <was neu ist>"

SCHRITT 5 — TRACKING-METADATA UPDATEN
Am Ende von TIPS.md, im YAML-Block:
  - last_scan_iso: aktuelle Uhrzeit in ISO 8601, z.B. "2026-05-12T22:00:00Z"
  - last_scan_anchor_tweet_id: ID des neuesten gefundenen Posts
    (auch wenn keine neuen Tipps daraus extrahiert wurden — wichtig für
    die nächste Routine, um nicht denselben Post erneut zu verarbeiten)

SCHRITT 6 — CHANGELOG.MD AKTUALISIEREN
Öffne CHANGELOG.md, füge oben (unter dem H1) eine neue Section ein:

## <YYYY-MM-DD> — Routine Scan

- ➕ Added tip #<TT.NN>: <Titel> (Source: <URL-Domain>)
- 📝 Updated tip #<TT.NN>: <was geändert>
- 🔍 Scan completed. Anchor: <tweet-id>

Wenn KEINE neuen Tipps gefunden wurden, schreibe stattdessen nur:

## <YYYY-MM-DD> — Routine Scan (no changes)

- 🔍 Scanned <N> sources, no new tips since <last_anchor>

SCHRITT 7 — INDEX.HTML SYNCHRONISIEREN
Wenn Schritt 4a/4b Änderungen gemacht hat:
  - Öffne index.html
  - Für JEDEN neuen Tipp in TIPS.md, finde die entsprechende
    <section class="theme-section" id="t<NN>"> in index.html
  - Füge ein neues <article class="tip" data-diff="<difficulty>"> Element
    ans Ende der <div class="tip-grid"> in dieser Section ein
  - Format des Artikels (genau nachbauen, Pattern aus existierenden Tipps):

<article class="tip" data-diff="<difficulty>">
  <div class="tip-meta">
    <span class="tip-num"><TT.NN></span>
    <span class="diff diff-<difficulty>"><Difficulty></span>
  </div>
  <h3><Titel></h3>
  <p><Beschreibung. <code>code</code> für inline-Code.></p>
  <div class="tip-footer">
    <span><DD. MMM YYYY></span>
    <a class="tip-source" href="<URL>" target="_blank">Source ↗</a>
  </div>
</article>

  - Aktualisiere im <header> die Zahl "87+ Tipps" auf die neue Gesamtzahl
  - Aktualisiere im <footer> "Last full audit" auf aktuelles Datum

SCHRITT 8 — README.MD TABELLE UPDATEN
In README.md, in der "Die 21 Themen im Überblick"-Tabelle, aktualisiere
die Tipp-Anzahl der betroffenen Theme(s).

SCHRITT 8b — IMPLEMENTATION-GUIDE.MD SYNC
Wenn der neue Tipp in eine der folgenden Kategorien fällt:
  - CLAUDE.md-Konfiguration (Theme 03)
  - Slash Commands (Theme 04, neuer Command oder neues Pattern)
  - Subagents (Theme 05, neuer Agent oder Pattern)
  - Hooks (Theme 06, neuer Hook-Typ oder Pattern)
  - Permissions & Safety (Theme 07, neue Einstellung)
  - MCP & Integrationen (Theme 08, neue Integration)
  - Modell & Effort (Theme 09, neue Konfiguration)
  - Verifikation (Theme 10, neues Verification-Pattern)
  - Customization (Theme 13, neue Einstellung)
  - Headless / SDK (Theme 14, neuer CLI-Flag oder Pattern)
  - Context Management (Theme 20, neue Strategie)

Dann:
  1. Öffne IMPLEMENTATION-GUIDE.md
  2. Finde die passende Section (1-10 oder Appendix)
  3. Füge den neuen Tipp als ausführbaren Instruktionsblock ein
     (Imperativ-Modus: "Create...", "Add...", "Configure...")
  4. Aktualisiere die Tip-ID-Referenz in Appendix D
  5. Füge IMPLEMENTATION-GUIDE.md zur Commit-Files-Liste hinzu

Wenn der Tipp NICHT actionable ist (z.B. Philosophie, ROI, Form-Factor,
persönliche Präferenz, Terminal-Environment): IMPLEMENTATION-GUIDE.md
NICHT ändern.

SCHRITT 9 — COMMIT & PUSH
Verwende den GitHub-Connector:
  - Branch: main
  - Commit-Message-Format:
    - Bei neuen Tipps: "Add <N> tip(s) from <YYYY-MM-DD> scan"
    - Bei Updates: "Update tip(s) from <YYYY-MM-DD> scan"
    - Bei nichts gefunden: "Routine scan <YYYY-MM-DD> (no changes)"
  - Files to commit: TIPS.md, CHANGELOG.md, index.html, README.md
    (nur die tatsächlich geänderten)

SCHRITT 10 — KURZE ZUSAMMENFASSUNG
Schreibe an SAI (mich) eine knappe Statusmeldung:
  - Wie viele Tipps gefunden
  - Welche IDs hinzugefügt
  - Direkter Link zum Commit
  - Wenn nichts gefunden: einfach "No new tips since <last>. Scan OK."

EDGE CASES — DAS NICHT TUN
  - NICHT erfinden. Wenn du keine echten neuen Posts findest, ist das OK.
    Schreibe ehrlich "no new tips".
  - NICHT Tipps aus älteren als last_scan_iso noch einmal hinzufügen.
  - NICHT Tipps anderer Personen hinzufügen, außer Boris hat sie
    explizit endorsed.
  - NICHT Code direkt nach index.html commiten ohne entsprechende
    TIPS.md-Aktualisierung — TIPS.md ist Source of Truth.
  - NICHT die YAML-Tracking-Metadata am Ende von TIPS.md löschen.
  - NICHT auf eine andere Branch committen als main.
  - NICHT bei rate-limit-errors oder zugriffs-problemen am GitHub-Connector
    silent failen — explizit melden und ohne Commit beenden.

WENN UNKLAR
Schreibe mir lieber eine Frage als zu raten:
  - "Ich habe einen Post gefunden, der nach einem Tipp klingt, aber
    Boris hat ihn nur geliked (nicht retweetet). Soll ich ihn aufnehmen?"
  - "Tipp #04.32 könnte durch diesen neuen Post obsolet sein. Update
    oder neuer Eintrag?"

Bei vollständig erfolgreichem Run: keine Frage nötig.

=== ROUTINE PROMPT END ===
```

---

## Wie das Setup verifiziert wird

Nach dem ersten Run prüfst du:

1. ✅ CHANGELOG.md hat einen neuen Eintrag für heute
2. ✅ TIPS.md `last_scan_iso` ist aktualisiert
3. ✅ Git-Log zeigt einen Commit der Routine
4. ✅ index.html zeigt im Footer das neue Datum

Wenn ja: Routine läuft. Wenn nein: siehe [Troubleshooting in setup.md](./setup.md#troubleshooting).

---

## Anpassungen für deinen Use-Case

Falls du das Repo unter einem anderen Pfad hast, ersetze im Prompt:
- `github.com/<DEIN-USER>/boris-cherny-claude-code-playbook` → dein tatsächlicher Pfad

Falls du andere Sekundärquellen mit-scannen willst, erweitere Schritt 2 um:
- `site:newsletter.pragmaticengineer.com bcherny`
- `site:every.to "Boris Cherny"`
- `site:latent.space "Boris Cherny"`

Falls du das Repo nicht-öffentlich willst: Routine braucht trotzdem write-access via GitHub-Connector. Privates Repo ist OK.

---

## Was passiert bei Fehlern

Claude.ai Routines retryen bei transienten Fehlern automatisch. Bei permanenten Fehlern (Connector-Token expired, Branch protection, Schema-Drift) wirst du benachrichtigt.

**Manuell debuggen:** Du kannst die Routine jederzeit "manuell triggern" über das Routine-Dashboard, mit denselben Prompt aber als one-shot.

**Notfall-Stop:** Routine im Dashboard pausieren. Die letzten Commits bleiben, nichts wird gerolled back.
