---
description: Manually scan X for new Boris Cherny posts since last scan
---

# /scan-x — Manual X Scan

Manueller Trigger des X-Scans, wenn du nicht auf die nächste Routine warten willst (z.B. nach einem großen Anthropic-Event).

## Workflow

### Schritt 1 — last_scan_iso lesen
Öffne TIPS.md, finde am Ende den YAML-Block:
```yaml
last_scan_iso: "..."
last_scan_anchor_tweet_id: "..."
```
Das ist der Cut-off.

### Schritt 2 — Multi-Query X-Suche
Verwende web_search mit folgenden Queries nacheinander:
1. `bcherny site:x.com`
2. `bcherny Claude Code`
3. `Boris Cherny Anthropic tip`
4. `site:threadreaderapp.com bcherny`
5. `site:threads.com boris_cherny`
6. `howborisusesclaudecode latest tips`

Für jede Query: filtere Ergebnisse nach Datum > `last_scan_iso`.

### Schritt 3 — Kandidaten aggregieren
Gruppiere die gefundenen Posts. Pro Post:
- Tweet-ID (oder Äquivalent)
- Datum
- Vollständiger Text (web_fetch wenn nötig)
- Klassifizierung: "tip" | "status" | "marketing" | "RT-no-comment"

Nur "tip"-Klassifizierte sind weiterzu verarbeiten.

### Schritt 4 — Präsentation an den Nutzer
Zeige eine kompakte Tabelle:

```
Gefunden seit <last_scan_iso>:

| # | Datum | Titel-Vorschlag | Theme-Vorschlag | Diff | Quelle |
|---|---|---|---|---|---|
| 1 | 2026-05-XX | ... | 04 Slash Commands | Int | x.com/... |
| 2 | ... | ... | ... | ... | ... |
```

Frage: "Welche soll ich aufnehmen? (1,2,3 / alle / keine)"

### Schritt 5 — Für ausgewählte Tipps: Add-Workflow
Für jeden ausgewählten Kandidaten: führe den `/add-tip`-Workflow ab Schritt 4 aus
(Felder vorschlagen → Bestätigung → einfügen → CHANGELOG).

### Schritt 6 — Tracking-Metadata
Am Ende des Scans (auch wenn keine Tipps aufgenommen wurden):
- Aktualisiere `last_scan_iso` auf jetzt
- Aktualisiere `last_scan_anchor_tweet_id` auf den NEUESTEN gefundenen Post
  (nicht nur die aufgenommenen — sonst wird er bei nächster Routine erneut gefunden)

### Schritt 7 — HTML-Sync
Wenn Tipps aufgenommen: `/regenerate-html` anbieten.

## Unterschied zu Daily-Scan-Routine

| | Routine (daily-scan.md) | Slash Command (/scan-x) |
|---|---|---|
| Läuft | 2–3× täglich automatisch | Wenn du es triggerst |
| Bestätigung | Auto-commit | Manueller Step pro Tipp |
| Risiko | Kann False Positive einfügen | Du siehst alles vorher |
| Wann nutzen | Normalbetrieb | Nach großen Threads, Events |

## Edge Cases

- Wenn die Routine schon heute gelaufen ist und ich nochmal scanne: gleiche Ergebnisse möglich, da `last_scan_iso` schon "weiter" ist. Das ist OK — es wird einfach "no new tips" zurückgeben.
- Wenn ich einen Tipp manuell vor der Routine adde: die Routine sieht ihn nicht doppelt, weil der Tweet-Anker schon notiert ist (sobald ich `last_scan_anchor_tweet_id` setze).
