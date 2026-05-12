# Changelog

Alle inhaltlichen Änderungen am Repo werden hier dokumentiert — manuelle Edits, Routine-Scans und Verifikations-Runs.

Neueste Einträge oben.

---

## 2026-05-13 — Implementation Guide + GitHub Launch

- 🆕 **IMPLEMENTATION-GUIDE.md** erstellt: ~70 actionable Tipps aus TIPS.md als ausführbare Claude Code Instruktionen. 10 Sections: CLAUDE.md Setup, Settings & Permissions, Slash Commands, Hooks, Subagents, MCP Integrations, Verification, Headless/SDK, Context Management, Automation. Plus 4 Appendices (Env Vars, Settings Template, Checklist, Tip-ID-Referenz). Sprache: Englisch (für maximale Reichweite).
- 📝 **README.md** überarbeitet: Tip-Count auf 132 korrigiert, Badges (Tips/Themes/Auto-Updated/License), englischer 2-Zeilen-Hook oben, 30-Sekunden-Schnellstart (3 Optionen), "Warum dieses Repo?" Section, IMPLEMENTATION-GUIDE.md in Inhaltsverzeichnis, Star-CTA am Ende, GitHub-URLs auf SKZL-AI aktualisiert.
- 📝 **CLAUDE.md** erweitert: IMPLEMENTATION-GUIDE.md in Dateistruktur eingefügt, Regel 7 hinzugefügt (actionable Tips auch in IMPLEMENTATION-GUIDE.md einpflegen).
- 🤖 **Routinen aktualisiert:**
  - `routines/daily-scan.md`: SCHRITT 8b hinzugefügt — IMPLEMENTATION-GUIDE.md Sync (wenn neuer Tipp actionable, automatisch in Guide einpflegen)
  - `routines/weekly-verify.md`: TEIL D hinzugefügt — IMPLEMENTATION-GUIDE.md Konsistenz-Check (Tip-IDs validieren, Stale-References flaggen)
  - `.claude/commands/add-tip.md`: Schritt 7b hinzugefügt — Actionable-Check bei manueller Tipp-Ergänzung mit Angebot, Tipp auch in IMPLEMENTATION-GUIDE.md aufzunehmen
- 🚀 **GitHub Launch:** Öffentliches Repo unter github.com/SKZL-AI/boris-cherny-claude-code-playbook, Topics, GitHub Pages, Description.

---

## 2026-05-12 — Initial Release

- 🎉 **Repo erstellt** mit 132 Tipps über 21 Themen
- 📁 Struktur: `TIPS.md` (Source of Truth), `README.md` (GitHub-Front), `index.html` (Dashboard), `routines/` (Automation), `.claude/` (Slash Commands & Subagents)
- 🤖 Automation eingerichtet:
  - `routines/daily-scan.md` — 2–3× tägliches X-Scan
  - `routines/weekly-verify.md` — Sonntäglicher URL-Health-Check
  - `.claude/commands/add-tip.md` — Manueller Tipp-Add
  - `.claude/commands/scan-x.md` — Manueller X-Scan
  - `.claude/commands/verify-sources.md` — Lokaler URL-Check
  - `.claude/commands/regenerate-html.md` — HTML aus TIPS.md neu bauen
  - `.claude/agents/tip-scout.md` — Subagent für X-Scanning
- 📊 Erste Tracking-Metadata in TIPS.md gesetzt:
  - `last_scan_iso: 2026-05-12T20:00:00Z`
  - `total_tips: 132`

### Initial Tip Distribution

| Theme | Tipps |
|---|---:|
| 01 Parallele Ausführung | 9 |
| 02 Plan Mode | 6 |
| 03 CLAUDE.md | 11 |
| 04 Slash Commands | 34 |
| 05 Subagents | 12 |
| 06 Hooks | 9 |
| 07 Permissions & Safety | 7 |
| 08 MCP & Integrationen | 7 |
| 09 Modell & Effort | 9 |
| 10 Verifikation | 11 |
| 11 Long-Running & Recaps | 6 |
| 12 Prompting & Specs | 6 |
| 13 Customization | 6 |
| 14 Headless / SDK | 10 |
| 15 Code Review | 3 |
| 16 Cost / ROI | 5 |
| 17 Form-Factor | 6 |
| 18 Migration & Daten | 3 |
| 19 Lernen & Onboarding | 5 |
| 20 Context Management | 5 |
| 21 Terminal Environment | 3 |
| **Σ** | **132** |

### Primärquellen für die initiale Recherche

- [@bcherny auf X](https://x.com/bcherny) — Hauptkanal
- [howborisusesclaudecode.com](https://howborisusesclaudecode.com) (Fan-Aggregator)
- [Latent Space Podcast](https://www.latent.space/p/claude-code) (Mai 2025)
- [Lenny's Podcast](https://www.lennysnewsletter.com/p/head-of-claude-code-what-happens) (Feb 2026)
- [AI & I Podcast](https://every.to/podcast/how-to-use-claude-code-like-the-people-who-built-it) (Nov 2025)
- [Pragmatic Engineer Newsletter](https://newsletter.pragmaticengineer.com/p/building-claude-code-with-boris-cherny) (Feb 2026)
- [Anthropic Engineering Blog](https://www.anthropic.com/engineering/claude-code-best-practices) (Apr 2025)
- AI Engineer World's Fair Keynote (Jun 2025)

### Notes

- Tipp-IDs sind **sticky** ab diesem Punkt. Auch deprecated Tipps behalten ihre ID, werden nur mit `[deprecated]` im Titel markiert.
- Die nächste Verify-Routine (Sonntag) wird URL-Health überprüfen — erwartet 100% OK bei Initial-Release.
- Erste Daily-Scan-Routine läuft am Tag nach Deployment, dürfte "no new tips" returnen, wenn nichts in den letzten 24h.

---

*Format-Konvention für künftige Einträge: siehe `routines/daily-scan.md` und `routines/weekly-verify.md`.*
