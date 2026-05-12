# Setup — Claude.ai Routines für automatische Updates

> Schritt-für-Schritt-Anleitung, um die in [daily-scan.md](./daily-scan.md) und [weekly-verify.md](./weekly-verify.md) definierten Routinen einzurichten.

## Voraussetzungen

- **Claude.ai Pro, Max, Team oder Enterprise.** Routines sind ein Research Preview (Stand April 2026), Verfügbarkeit kann je nach Tier variieren.
- **GitHub-Account** mit dem Repo (öffentlich oder privat, beides geht).
- **Etwa 15 Minuten** für das initiale Setup.

## Schritt 1 — Repo auf GitHub veröffentlichen

```bash
cd boris-cherny-claude-code-playbook
git init
git add .
git commit -m "Initial commit: Boris Cherny Claude Code Playbook"
git branch -M main
git remote add origin https://github.com/<DEIN-USER>/boris-cherny-claude-code-playbook.git
git push -u origin main
```

**Optional: GitHub Pages aktivieren**, damit das Dashboard live unter `https://<dein-user>.github.io/boris-cherny-claude-code-playbook/` erreichbar wird:

1. GitHub-Repo → Settings → Pages
2. Source: Deploy from a branch
3. Branch: `main` / root
4. Save

Nach 1–2 Minuten ist das Dashboard live.

## Schritt 2 — Connectors in Claude.ai aktivieren

Öffne **claude.ai → Settings → Connectors**. Aktiviere mindestens:

| Connector | Wozu | Wo zu finden |
|---|---|---|
| **GitHub** | Read/Write auf dein Repo | Standard-Connector, OAuth |
| **Web Search** | X & Sekundärquellen scannen | Standard-Connector, automatisch |
| **Web Fetch** | Voller Inhalt von Tweet-Threads | Optional aber empfohlen |

**Wichtig bei GitHub:**
- Bei OAuth: gib Claude Zugriff auf das spezifische Repo (nicht alle Repos).
- Berechtigungen: Read + Write Issues, Read + Write Code.

## Schritt 3 — Erste Routine anlegen (Daily Scan)

1. Claude.ai → **Routines** (im Sidebar, ggf. unter "Beta" oder "Research Preview")
2. **+ New Routine** klicken
3. Felder ausfüllen:

| Feld | Wert |
|---|---|
| **Name** | `Boris Cherny X Scan — Morning` |
| **Description** | `Scans @bcherny on X for new Claude Code tips, updates GitHub repo` |
| **Schedule** | `Cron: 0 9 * * *` (täglich 09:00 CET — Cron-UTC: passe an deine Zeitzone an, siehe unten) |
| **Connectors** | GitHub, Web Search, Web Fetch |
| **Prompt** | Kompletten Inhalt zwischen den `===` Markern aus [daily-scan.md](./daily-scan.md) reinkopieren |

**Cron-UTC-Anpassung:**

| CET-Zeit | UTC-Cron |
|---|---|
| 09:00 CET (Winter) | `0 8 * * *` |
| 09:00 CEST (Sommer) | `0 7 * * *` |
| 15:00 CET | `0 14 * * *` (W) / `0 13 * * *` (S) |
| 22:00 CET | `0 21 * * *` (W) / `0 20 * * *` (S) |

> Anthropic-Routines akzeptieren oft auch lesbare Schedules wie `daily at 9am Europe/Berlin`. Probiere zuerst das.

4. **Save & Test Run** klicken. Erster Run dauert 1–3 Minuten.

## Schritt 4 — Zwei weitere Daily-Scans anlegen

Wiederhole Schritt 3 zweimal:

- `Boris Cherny X Scan — Afternoon` — 15:00 CET
- `Boris Cherny X Scan — Evening` — 22:00 CET

Identischer Prompt, andere Schedules.

> Tipp: Wenn dir 3 Scans zu viel sind, lass das Afternoon-Routine weg. Morning + Evening reicht für 90% der Posts.

## Schritt 5 — Weekly Verify Routine anlegen

Diese läuft einmal pro Woche und prüft, ob alle Source-URLs noch erreichbar sind.

| Feld | Wert |
|---|---|
| **Name** | `Boris Cherny Playbook — Weekly URL Verify` |
| **Schedule** | `Cron: 0 10 * * 0` (Sonntag 10:00) |
| **Connectors** | GitHub, Web Fetch |
| **Prompt** | Inhalt aus [weekly-verify.md](./weekly-verify.md) reinkopieren |

## Schritt 6 — Verifikation

Nach 24h:

1. Schaue ins Repo → Commits-History. Du solltest mindestens 2–3 Commits von der Routine sehen.
2. Öffne CHANGELOG.md. Sollte tagesaktuelle Einträge haben (auch wenn "no changes").
3. Öffne TIPS.md, scroll nach unten — `last_scan_iso` sollte heute sein.

Wenn ja: ✅ Setup erfolgreich.

## Schritt 7 — Notifications (optional)

Damit du merkst, wenn neue Tipps reinkommen:

**Option A — GitHub-Notifications:**
GitHub-Repo → Watch → "Custom" → ✓ Pushes. Du bekommst eine E-Mail bei jedem Routine-Commit.

**Option B — Slack-Integration:**
Wenn du Slack hast, GitHub-App → `/github subscribe <dein-user>/boris-cherny-claude-code-playbook` in einem Channel.

**Option C — RSS:**
GitHub generiert automatisch einen Commits-RSS-Feed: `https://github.com/<dein-user>/boris-cherny-claude-code-playbook/commits/main.atom`

## Troubleshooting

### Routine läuft nicht / kein Commit
- Prüfe das Routine-Dashboard → "Run history". Welcher Schritt failed?
- Häufigste Ursache: GitHub-Connector-Token abgelaufen → Reconnecten.
- Zweithäufigste: Web Search rate-limited → Routine selbst ist OK, einfach nächsten Run abwarten.

### Routine commitet Müll / erfindet Tipps
- Routinen interpretieren manchmal Posts großzügig. Lösung: Prompt anpassen — schärfere "DO NOT INVENT"-Klausel oder explizite Beispiele für "valid tip" vs "not a tip".
- Im Worst Case: Routine pausieren, problematischen Commit revert'en, Prompt iterieren.

### Mehrere Routines mit identischem Prompt laufen synchron
- Risiko: zwei Scans am selben Tweet, doppelte Tipps. **Lösung:** Der Prompt prüft `last_scan_anchor_tweet_id` — wenn Routine 1 schon den neuen Anker gesetzt hat, findet Routine 2 nichts Neues. Sollte robust sein.
- Wenn doch Duplikate entstehen: weekly-verify Routine erkennt und merged sie.

### Auto Mode / Permission-Prompts
Wenn du **Auto Mode** in der Routine aktivierst (Max/Team/Enterprise), läuft alles ohne Approval. Wenn nicht: jeder GitHub-Write triggert einen Permission-Prompt — bei einer 2–3× täglich laufenden Routine unpraktisch.

**Empfehlung:** Auto Mode an, aber `--allow-tools` auf `GitHub:write_file,GitHub:commit,WebSearch,WebFetch` beschränken. Kein generischer Bash-Zugriff.

### Rollback wenn etwas Schiefes commitet wurde

```bash
git revert HEAD       # letzten Commit rückgängig machen
git push
```

oder gezielt einen Tipp wieder rausnehmen:

```bash
# Lokal Tipp entfernen, dann
git commit -am "Remove tip #XX.YY (false positive from routine)"
git push
```

Beim nächsten Routine-Run wird der falsche Tipp NICHT wieder hinzugefügt, weil `last_scan_anchor_tweet_id` schon weiter ist.

## Kosten-Einordnung

Pro Routine-Run werden geschätzt **5.000–15.000 Tokens** verbraucht (Web-Search-Ergebnisse + Repo-Files + Output). Bei 3× täglich = ~30.000–45.000 Tokens/Tag = ~1M Tokens/Monat.

Auf Claude Max ist das im Rahmen der Quota. Auf Pro: prüfen, dass es nicht das tägliche Limit auffrisst — sonst auf 1–2× täglich reduzieren.

## Wann manuell statt automatisch

Es gibt Fälle, in denen die Routine NICHT die richtige Wahl ist:

- **Großer neuer Thread mit 15+ Tipps gleichzeitig** (wie der 02. Jan oder 29. Mär Threads): Routine arbeitet die einzeln ab, aber besser einmal manuell mit `/scan-x` im Claude Code lokal — du hast mehr Kontrolle über die Theme-Zuordnung.
- **Neuer Themenbereich**: Wenn ein Boris-Post ein völlig neues 22. Thema einführt, muss erst die Struktur im Repo angelegt werden — Routine traut sich das nicht.
- **Major Refactoring**: Wenn Anthropic Claude Code 3.0 launcht und vieles obsolet wird, manuell.

Für 90% der Daily-Updates: Routine. Für die seltenen großen Sprünge: manuell.
