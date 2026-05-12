# Weekly Verify — Routine Prompt

> **Zweck:** Einmal wöchentlich alle Source-URLs in TIPS.md prüfen, Duplikate erkennen, Tracking-Metadata konsolidieren.

> Diese Routine ergänzt [daily-scan.md](./daily-scan.md) — sie fügt KEINE neuen Tipps hinzu, sie pflegt nur das, was schon da ist.

---

## Empfohlener Zeitplan

**Sonntag 10:00 CET** — Cron: `0 9 * * 0` (UTC im Winter) / `0 8 * * 0` (UTC im Sommer)

Ein Mal pro Woche reicht. Häufiger lohnt sich nicht — URLs sterben langsam.

---

## Der Routine-Prompt (zum Kopieren)

```
=== WEEKLY VERIFY ROUTINE START ===

Du bist Maintainer des GitHub-Repos boris-cherny-claude-code-playbook.

DEINE AUFGABE
Wöchentliche Pflege des Repos. Drei Teilaufgaben:
  A) Source-URLs verifizieren (sind sie noch erreichbar?)
  B) Duplikate erkennen (haben zwei Tipps denselben Source gleichen Inhalt?)
  C) Tracking-Metadata in TIPS.md konsolidieren

KEINE neuen Tipps hinzufügen. Dafür ist die Daily-Scan-Routine.

TEIL A — URL-VERIFIKATION

1. Lies TIPS.md vollständig ein.
2. Extrahiere alle Source-URLs (Markdown-Format: [text](url)).
3. Für jede URL: web_fetch mit text_content_token_limit=500
   (wir brauchen nur den Header, nicht den ganzen Inhalt).
4. Klassifiziere:
   - OK (200, normaler Inhalt)
   - GONE (404, 410, oder explicit "deleted"/"suspended" Inhalt)
   - REDIRECT (301/302 zu anderer Domain → notieren)
   - PRIVATE (X account locked etc. — Tipp markieren, nicht löschen)

5. Für GONE URLs:
   - Suche bei archive.org Wayback Machine nach Snapshot:
     web_fetch("https://web.archive.org/web/*/<ORIGINAL_URL>")
   - Wenn Snapshot existiert: ersetze in TIPS.md die URL durch
     die archive.org-Version. Markiere in der Beschreibung mit
     "[Original-Tweet gelöscht, archive.org-Snapshot]".
   - Wenn kein Snapshot: markiere den Tipp mit "[archived]" im Titel
     (Format: "### #04.15 — [archived] /btw für Side-Chain-Conversations")
     und ergänze die Beschreibung um "Original-Source nicht mehr erreichbar."

6. Für REDIRECT URLs:
   - Wenn Redirect zu legitimer Anthropic/X-Domain: URL aktualisieren.
   - Wenn Redirect zu Spam/Domain-Squatter: behandle wie GONE.

TEIL B — DUPLIKAT-ERKENNUNG

1. Gruppiere alle Tipps nach Source-URL.
2. Wenn 2+ Tipps dieselbe URL haben:
   - Prüfe die Beschreibungen — sind sie wirklich verschieden?
   - Falls ja: OK (ein Thread kann mehrere Tipps enthalten).
   - Falls nein: identifiziere den kanonischen Tipp (älteste ID).
     Markiere den anderen mit "[duplicate of #XX.YY]" im Titel und
     füge Hinweis in Beschreibung ein. NICHT komplett löschen (IDs
     bleiben sticky).
3. Gruppiere alle Tipps nach Titel-Ähnlichkeit (z.B. beide enthalten
   "/loop"). Wenn unterschiedliche Themes aber gleiche Substanz:
   markiere für menschliche Review (kein Auto-Merge).

TEIL C — TRACKING-METADATA KONSOLIDIEREN

Am Ende von TIPS.md im YAML-Block:
1. Zähle total_tips erneut (real count, ohne [archived]/[duplicate]).
2. Aktualisiere last_tip_id_per_theme: höchste vergebene ID pro Theme.
3. Setze last_verify_iso: aktuelle Uhrzeit ISO 8601.
4. Wenn last_verify_iso noch nicht existiert, lege es an.

TEIL D — IMPLEMENTATION-GUIDE.MD KONSISTENZ-CHECK

1. Lies IMPLEMENTATION-GUIDE.md vollständig ein.
2. Für jede referenzierte Tip-ID (#XX.YY) in der Datei:
   - Prüfe, ob die ID noch in TIPS.md existiert und aktiv ist
   - Wenn [archived] oder [deprecated]: markiere den Eintrag in
     IMPLEMENTATION-GUIDE.md mit "[archived]" oder entferne ihn
3. Zähle die actionable Tips im Guide vs. die tatsächliche Anzahl
   actionable Tips in TIPS.md (Heuristik: Themes 03-08, 10, 13, 14, 20
   sind überwiegend actionable)
4. Wenn die Differenz > 5: Flag für manuelle Review
5. Report-Zeile hinzufügen (siehe REPORT FORMAT unten):
   - IMPL-GUIDE tips referenced: <N>
   - IMPL-GUIDE stale references: <N>

REPORT FORMAT

Schreibe in CHANGELOG.md oben (unter dem H1) eine neue Section:

## <YYYY-MM-DD> — Weekly Verify

- ✅ URLs verified: <N OK> / <N total>
- ⚠️ URLs migrated to archive.org: <N> (Tipps: #XX.YY, #XX.YY)
- 🚫 URLs marked [archived] (no snapshot): <N> (Tipps: #XX.YY)
- 🔁 Duplicates flagged: <N> (Tipps: #XX.YY)
- 📊 Total active tips: <N>

Wenn alles sauber ist:

## <YYYY-MM-DD> — Weekly Verify (clean)

- ✅ All <N> URLs reachable
- ✅ No duplicates detected
- 📊 Total tips: <N>

COMMIT

- Files: TIPS.md, CHANGELOG.md (nur wenn Änderungen)
- Commit-Message: "Weekly verify <YYYY-MM-DD>: <N> changes"
  oder: "Weekly verify <YYYY-MM-DD>: clean"
- Branch: main

EDGE CASES

- Wenn ein Tipp mehrfach archiviert/dupliziert wurde: nicht weiter
  modifizieren, manuelle Review nötig. Erwähne in der CHANGELOG-Section
  unter "🔧 Needs manual review:".
- Wenn web_fetch persistent fehlschlägt (Rate-Limit, Captcha): brich
  Teil A ab nach 10 Failures. Mache trotzdem Teil B und C.
- Wenn TIPS.md syntaktisch broken ist (kaputte Markdown-Struktur):
  KEINEN Commit machen, stattdessen alarmieren mit klarer Beschreibung
  wo der Schaden ist.

=== WEEKLY VERIFY ROUTINE END ===
```

---

## Was diese Routine NICHT macht

- **Keine neuen Tipps hinzufügen** — das ist Job der Daily-Scan-Routine.
- **Kein index.html-Update** — bei Changes in TIPS.md läuft am nächsten Daily-Scan automatisch der HTML-Sync mit.
- **Kein README-Update** — die README-Tabelle wird erst aktualisiert, wenn sich die Theme-Counts ändern, was via Daily-Scan passiert.

## Warum eine separate Routine

Trennung von Concerns:
- Daily Scan = "find new stuff" (mit Risiko False Positive)
- Weekly Verify = "validate existing stuff" (rein read-modify, kein Risiko neuer Inhalte)

Falls eine der beiden buggy wird, kannst du die andere weiterlaufen lassen.

## Bekannte Sonderfälle bei Boris' Quellen

- **threadreaderapp.com** Mirrors sind oft langsamer aktualisiert. Wenn der Original-Tweet existiert aber Mirror down ist, ist das KEIN GONE.
- **threads.com** (Meta's Threads-Mirror seiner X-Posts): Manchmal werden Posts dort gelöscht, im Original aber nicht. Cross-reference.
- **howborisusesclaudecode.com**: Fan-Site, kein Anthropic. Wenn dort Tipps fehlen die im Repo sind: nicht löschen.
- **AIEWF Talk 2025**: Nur als YouTube-Video archiviert. Wenn das Video weg ist, gibt es trotzdem oft Audio-Transkripte. Verwende die.
