---
description: Verify all source URLs in TIPS.md are still reachable
---

# /verify-sources — URL Health Check

Geht durch alle Source-URLs in TIPS.md und prüft, ob sie noch erreichbar sind.

Lokales Äquivalent zur weekly-verify.md Routine, aber on-demand und interaktiv.

## Workflow

### Schritt 1 — URLs extrahieren
Lies TIPS.md. Mit Regex `\[.+?\]\((https?://[^)]+)\)` alle Source-URLs extrahieren.
Dedupe (eine URL kann mehrere Tipps haben — Threads).

### Schritt 2 — Parallel fetchen
Verwende web_fetch mit `text_content_token_limit=500` (wir wollen nur den Header, kein voller Inhalt). Wenn möglich, batche mehrere parallel.

Pro URL: klassifiziere
- ✅ OK (200, normaler Content)
- ⚠️ REDIRECT (301/302, neuer URL)
- 🚫 GONE (404, 410, oder Inhalt sagt "deleted"/"suspended")
- 🔒 PRIVATE (X-Account locked/suspended)
- ❓ UNCLEAR (Rate-Limit, Captcha, andere transiente Probleme)

### Schritt 3 — Report
Zeige Tabelle:

```
| URL | Status | Tipps |
|---|---|---|
| x.com/bcherny/status/... | ✅ OK | #01.01, #04.01, ... |
| x.com/bcherny/status/... | 🚫 GONE | #05.07 |
| x.com/bcherny/status/... | ⚠️ REDIRECT → archive.org | #11.05 |
```

### Schritt 4 — Aktion vorschlagen
Für jede problematische URL, frage:

**GONE:**
"Tipp #05.07 hat eine gelöschte Quelle. Wayback Machine prüfen? (j/n)"
- Wenn ja: web_fetch `https://web.archive.org/web/*/<original-url>` → suche neuesten Snapshot
- Wenn Snapshot gefunden: ersetze URL in TIPS.md, ergänze Beschreibung um "[archive.org-Snapshot]"
- Wenn kein Snapshot: markiere mit `[archived]` im Titel

**REDIRECT:**
"Tipp #11.05 redirected. Neue URL: <new>. Update? (j/n)"

**PRIVATE / UNCLEAR:**
Nur melden, nicht modifizieren. Manuelle Review nötig.

### Schritt 5 — Zusammenfassung
```
✅ 132 URLs geprüft
✅ 128 OK
⚠️ 2 REDIRECT → updated
🚫 1 GONE → archive.org Snapshot eingefügt
🔒 1 PRIVATE → manuelle Review
```

### Schritt 6 — Commit-Vorschlag
Wenn Änderungen: Commit-Befehl vorschlagen
```bash
git add TIPS.md
git commit -m "Verify sources: <N> URLs updated"
```

## Edge Cases

- **Rate-Limit:** Wenn web_fetch zu viele Anfragen scheitert, brich ab nach 10 Failures in Folge. Melde welche URLs nicht geprüft werden konnten.
- **Captcha-Pages:** X zeigt manchmal Captcha statt Content. Das ist kein GONE — markiere als UNCLEAR.
- **Long-form Threads:** Wenn nur die Anker-Tweet-URL down ist, aber Mirror auf threadreaderapp.com funktioniert: ersetze die URL mit der Mirror-URL.

## Performance-Hinweis

Bei 132 URLs × 2-5 Sekunden pro Fetch = 5-10 Minuten Laufzeit. Geduldig sein, oder Filter auf nur neueste 30 Tipps.

```
/verify-sources --since 2026-04-01    # nur neuere Tipps
/verify-sources --themes 04,05        # nur bestimmte Themen
```

(Hypothetische Flags — implementiere bei Bedarf via Sub-Prompt.)
