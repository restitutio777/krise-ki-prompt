# Hormuz Briefing — Prio-Finder Integration

## Dateien

| Datei | Zweck |
|---|---|
| `api/claude.js` | Vercel Serverless Function — leitet Anfragen sicher an Anthropic weiter |
| `prio-widget.html` | Der fertige Widget-Code zum Einbetten in die bestehende Seite |
| `vercel.json` | Vercel-Konfiguration (Timeout 30s) |

---

## Schritt 1 — API-Key als Umgebungsvariable setzen

Im Vercel Dashboard:
**Settings → Environment Variables → Add**

```
Name:   ANTHROPIC_API_KEY
Value:  sk-ant-...
Scope:  Production, Preview
```

→ Danach **Redeploy** auslösen.

---

## Schritt 2 — Serverless Function einfügen

`api/claude.js` in das Root-Verzeichnis Ihres Repos kopieren.

Der Endpunkt ist dann automatisch unter `/api/claude` erreichbar.

---

## Schritt 3 — Widget in die bestehende Seite einbetten

Den Inhalt von `prio-widget.html` an der gewünschten Stelle in Ihrer Seite einfügen — z.B. nach dem Zeitachsen-Abschnitt:

```html
<!-- Bestehender Inhalt ... -->
<section id="timeline">...</section>

<!-- Widget hier einfügen: -->
<!-- Inhalt von prio-widget.html -->
<section id="prio-finder" style="margin: 4rem 0;">
  ...
</section>

<!-- Weiterer Inhalt ... -->
```

Mit einem Anker-Link können Sie direkt auf den Finder verlinken:
```html
<a href="#prio-finder">Meine persönlichen Prioritäten →</a>
```

---

## Kosten

- Claude Sonnet: ca. ~0,003 $ pro Aufruf (Input ~500 Token + Output ~300 Token)
- Bei 1.000 Aufrufen/Tag ≈ 3 $/Tag

---

## Optional — Rate Limiting

Um Missbrauch zu verhindern, kann in `api/claude.js` ein einfaches IP-basiertes Rate Limit ergänzt werden. Alternativ: Vercel's eingebaute Edge-Middleware nutzen.
