# AI Automation Bootcamp: Desktop-Vorlage (Claude Code + n8n)

Die Projektvorlage für das **AI Automation Bootcamp** der **Tourismus+Congress GmbH Frankfurt am Main (TCF)** in Kooperation mit **buildbar_** (30.11. bis 03.12.2026 in Frankfurt am Main). Gemacht für **Mitarbeitende der TCF mit wenig oder keiner Code-Erfahrung**: Du beschreibst ein Vorhaben aus deinem Berufsalltag, **Claude baut** die Automatisierung in **n8n** und bei Bedarf eine kleine Web-Oberfläche. Jede:r arbeitet am eigenen Vorhaben.

**Was du mitnimmst:** eine erste funktionierende Workflow-Lösung, ein eigenes Code-Repository, das dir gehört, und einen klaren nächsten Schritt für deine Organisation.

Diese Vorlage ist für die **Desktop-App** (Claude Code läuft auf deinem Rechner, mit lokaler Vorschau). Darfst du nichts installieren? Dann nimm den **Browser-Weg**: https://tcf.buildbar.de/starten/web

- Event-Seite und Agenda: https://tcf.buildbar.de
- Zugangsdaten (mit Passwort): https://tcf.buildbar.de/#zugang
- Anleitung Desktop: https://tcf.buildbar.de/starten/desktop
- Vorhaben: https://tcf.buildbar.de/vorhaben · Grundlagen: https://tcf.buildbar.de/grundlagen

> 📝 **Vor dem Bootcamp:** [Zugangs-Checkliste](docs/zugangs-checkliste.md): Claude-Plan, GitHub, dein Konto in eurer n8n in one.intelligence, Freigaben und Beispieldaten. Kein Technik-Wissen nötig, offene Punkte klären wir im Kick-off.
>
> 📄 **Zum ersten Mal hier?** [Anleitung Desktop](https://tcf.buildbar.de/starten/desktop): von der Installation über den n8n-Zugang bis zum ersten laufenden Workflow, in einfacher Sprache.

> 🧭 **Idee noch unklar?** Sag **„Hilf mir, meine Idee zu klären.“** Claude stellt dir ein paar einfache Fragen und macht daraus einen Bau-Plan.

---

## ✨ Einrichten in 1 Satz

Öffne in der **Claude Desktop-App** den Bereich **Code**, wähle einen leeren Ordner und schreib:

> **„Richte mir https://github.com/freddy-schuetz/tcf-ai-automation-bootcamp ein.“**

Claude prüft die Voraussetzungen, lädt die Vorlage herunter, richtet sie ein und fragt dich nur nach deinem **n8n-API-Schlüssel**. Die Adresse eurer n8n steht schon drin.

**Das brauchst du vorher:**
- Die **Claude Desktop-App** ([Download](https://claude.com/download)) und einen **bezahlten Claude-Plan** (Pro, Max, Team oder Enterprise). Ohne ihn ist der Code-Bereich gesperrt. Gebaut wird im Bereich **Code**, Cowork eignet sich dafür nicht.
- ⚠️ **Windows: Git UND Node.js vorher installieren.** Lokale Sessions starten nur, wenn Git vorhanden ist, und Node.js braucht der n8n-MCP-Server. [Git für Windows](https://git-scm.com/downloads/win) und [Node.js (LTS)](https://nodejs.org) mit den Standard-Einstellungen installieren, danach die App einmal neu starten. Auf dem Mac ist Git meist schon dabei.
- Dein **Konto in eurer n8n in one.intelligence** und einen **API-Schlüssel** daraus (Einstellungen, „n8n API“, „Create API Key“, mit **langer Laufzeit**).
- Ein kostenloses **[GitHub](https://github.com)-Konto**: Dein Projekt landet am Ende in deinem eigenen privaten Repository.

> 🧩 **Du nutzt Codex, OpenCode oder einen anderen Agent statt Claude Code?** Setup in **[AGENTS.md](AGENTS.md)**.

---

## 🤖 Setup-Anleitung für Claude (Agent-Runbook)

> 💡 *Diesen Abschnitt liest **Claude** beim Einrichten. Als Teilnehmer:in kannst du ihn überspringen.*

*Wenn dich jemand bittet, dieses Repository einzurichten („Richte mir https://github.com/freddy-schuetz/tcf-ai-automation-bootcamp ein.“), arbeite diese Schritte ab. Ziel: ein Satz, danach läuft alles. Die Person tippt keine Befehle. Schreib einfach und in der du-Form.*

1. **Voraussetzungen prüfen:**
   - `git --version`, `node --version` (Node 20 oder neuer) und `npx --version`. Node.js und `npx` braucht der n8n-MCP-Server.
   - `gh --version` (GitHub-CLI, später für das eigene Repository und das Veröffentlichen).
   - **Windows:** Git **und** Node.js sollten vorab installiert sein. Läuft diese Session lokal, ist Git zwangsläufig vorhanden. Fehlt Node.js, biete an: `winget install --silent --accept-package-agreements --accept-source-agreements OpenJS.NodeJS.LTS` (die Person bestätigt die Windows-Sicherheitsabfrage) oder die Person installiert es selbst von https://nodejs.org. Fehlt `gh`: `winget install --id GitHub.cli`.
   - **macOS:** `brew install node gh` (ohne Homebrew: Node.js von https://nodejs.org, GitHub-CLI von https://cli.github.com).
   - **Linux:** Paketmanager, z. B. `sudo apt install -y git nodejs npm`.
   - Nach einer Installation ist das Programm oft erst nach einem **Neustart der App** im PATH. Kommt „not found“, bitte die Person, die App neu zu starten, dann hier weitermachen.
2. **Klonen:**
   - Ist der geöffnete Ordner leer, direkt hinein klonen: `git clone https://github.com/freddy-schuetz/tcf-ai-automation-bootcamp .`
   - Sonst in einen Unterordner klonen (`git clone https://github.com/freddy-schuetz/tcf-ai-automation-bootcamp`) und der Person sagen, dass sie nach dem Neustart genau den Ordner `tcf-ai-automation-bootcamp` im Code-Bereich öffnet. Nur dort werden `CLAUDE.md`, Skills und n8n-Verbindung geladen.
3. **MCP-Konfiguration anlegen:** `.mcp.json` als Kopie von `.mcp.json.example` erzeugen (`cp .mcp.json.example .mcp.json`). Mit `git check-ignore .mcp.json` bestätigen, dass sie ignoriert wird.
4. **n8n-Zugang** in `.mcp.json`:
   - **Adresse:** steht schon in `.mcp.json` (`N8N_API_URL` = `https://n8n.oi.destination.one`). Nur ändern, wenn die n8n der Person eine andere Adresse hat.
   - **API-Schlüssel:** legt die Person in n8n an (Einstellungen, „n8n API“, „Create API Key“), mit **langer Laufzeit**, damit das Projekt auch nach dem Bootcamp verbunden bleibt.
   - **`N8N_MCP_ACCESS_TOKEN` (optional):** Ohne ihn kann Claude Workflows **ohne** Webhook (also alle mit Zeitplan) nicht selbst starten, die Person startet sie dann im n8n-Editor. Bietet eure n8n unter Einstellungen den Punkt „Instance-level MCP“, erzeugt die Person dort einen Token. Sonst die Zeile aus `.mcp.json` löschen.
   - **`DISABLED_TOOLS` und `DISABLED_TOOL_OPERATIONS` stehen lassen.** Sie sperren Löschen und Umbauen über Claude, weil es ein echtes Konto ist.
   - URL mit `https://` und **ohne** Schrägstrich am Ende. Den Key darf die Person dir in den Chat schreiben. Er bleibt nur in der lokalen `.mcp.json`: **nie ausgeben, nie in andere Dateien schreiben, nie committen.**
5. **(Optional) Frontend-Abhängigkeiten**, falls eine Oberfläche gewünscht ist: im Ordner `frontend-starter` `npm install`.
6. **Neustart:** Bitte die Person, die App neu zu starten (bzw. das Projekt neu zu öffnen), damit der n8n-MCP-Server und die Skills geladen werden. Hat sie in einen Unterordner geklont, öffnet sie jetzt diesen Ordner.
7. **Verbindung prüfen:** `n8n_health_check` muss OK liefern, danach zur Kontrolle `n8n_list_workflows`.
   - Fehler bei der Verbindung: URL prüfen (Tippfehler, `https://`, kein Schrägstrich am Ende).
   - Fehler bei der Anmeldung (401): Key unvollständig oder falsch. Neuen Key eintragen, App neu starten.
   - Webhook-Pfade gelten für die ganze n8n in one.intelligence: eigene Pfade immer mit Kürzel (Regeln in `CLAUDE.md`).
8. **Fertig melden** und den Start anbieten: „Sollen wir gemeinsam schauen, was du bauen willst? Sag einfach: Hilf mir, meine Idee zu klären.“ Anregungen: https://tcf.buildbar.de/vorhaben und `docs/tourismus-ideen.md`. Braucht die Idee Postfach, Kalender, Teams oder Google, die Freigaben gleich am Anfang prüfen (Skill `m365-google-freigaben`).

---

## 🔑 n8n-Zugang

**Eure n8n in one.intelligence:** Du arbeitest in deinem eigenen Konto. Adresse (`https://n8n.oi.destination.one`, schon eingetragen) und API-Schlüssel stehen in deiner lokalen `.mcp.json`. Den Schlüssel legst du in n8n unter **Einstellungen, n8n API, Create API Key** an, mit langer Laufzeit. Workflows, Tabellen und Webhook-Pfade bekommen dein Kürzel (z. B. `mk-anfragen`), weil Pfade für die ganze n8n gelten.

**Optional, der MCP-Token:** `N8N_MCP_ACCESS_TOKEN` in derselben `.mcp.json` schaltet frei, dass Claude Workflows **ohne Webhook** starten kann, also alle zeitgesteuerten. Ohne ihn startest du solche Workflows im n8n-Editor selbst.

**KI in n8n:** läuft über one.intelligence. Den Zugang vom Typ „one.intelligence“ legst du einmal selbst in deinem n8n-Konto an, den Schlüssel dafür gibt es in one.intelligence unter Einstellungen, Konto, API-Schlüssel. Er gehört nie ins Repository.

---

## 🛠️ Manuelles Setup (statt der 1-Satz-Variante)

```bash
git clone https://github.com/freddy-schuetz/tcf-ai-automation-bootcamp
cd tcf-ai-automation-bootcamp
cp .mcp.json.example .mcp.json        # dann N8N_API_KEY eintragen
```
Den Ordner in Claude Code öffnen. Der n8n-MCP-Server (`npx n8n-mcp`) und alle Skills laden automatisch. Verbindung mit „Prüfe die n8n-Verbindung.“ testen.

---

## 📦 Was ist drin?

### Die Skills: das Wissen, das Claude automatisch nutzt
Skills sind Spickzettel, die Claude **von selbst** heranzieht, sobald sie zum Thema passen. Du musst sie nicht aufrufen.

**Tag 1: Vorhaben planen**
- `idee-klaeren`: macht aus einer vagen oder schwer beschreibbaren Idee einen klaren Bau-Plan (inkl. Ideen-Menü).
- `grill-me`: nur auf Zuruf („grill mich“), klopft deinen **fertigen** Plan Frage für Frage ab, bevor gebaut wird.
- `m365-google-freigaben`: prüft früh, ob dein Vorhaben eine Freigabe deiner IT braucht (Postfach, Kalender, Teams, Google).

**Die sechs Bootcamp-Themen**
- `meetingnotizen`: Mitschriften und Transkripte in Beschlüsse und Aufgaben verwandeln.
- `mail-triage-entwuerfe`: E-Mail-Anfragen sortieren und Antwortentwürfe vorbereiten.
- `bericht-zeitgesteuert`: wiederkehrende Berichte automatisch erstellen und verschicken.
- `terminkoordination`: Terminfindung und Abstimmung mit vielen Beteiligten.
- `daten-visualisieren`: Excel- oder CSV-Daten auswerten und als Diagramm aufbereiten.
- `praesentation`: Folien aus Kennzahlen und Stichpunkten befüllen.

**Workflows richtig bauen** (von [czlonkowski](https://github.com/czlonkowski/n8n-skills)):
- `n8n-mcp-tools-expert`: wie man die n8n-Werkzeuge richtig bedient.
- `n8n-workflow-patterns`: bewährte Baumuster (Webhook, API-Aufruf, Datenbank, KI-Agent, Zeitplan).
- `n8n-node-configuration`: wie man einen einzelnen Baustein (Node) korrekt einstellt.
- `n8n-expression-syntax`: die `{{ }}`-Ausdrücke, mit denen Daten durch den Workflow fließen.
- `n8n-validation-expert`: findet Fehler im Workflow und erklärt sie.
- `n8n-code-javascript` / `n8n-code-python`: falls mal eigener Code in einem Node nötig ist.

**Qualität sichern und verständlich machen:**
- `n8n-testdaten`: erzeugt Testfälle und probiert den Workflow durch.
- `n8n-dokumentation`: schreibt **Sticky Notes in einfacher Sprache** in den Workflow.
- `n8n-security-audit`: Sicherheits-Check vor dem Aktivieren (keine offenen Keys, abgesicherte Webhooks …).
- `n8n-pruefbericht`: kurzer, verständlicher Bericht zum fertigen Workflow.

**Optional: eigene Oberfläche oder eigenes Backend**
- `frontend-build` / `frontend-scaffold`: Web-Apps mit Next.js (Formulare, Dashboards, Tabellen, Karten …), angebunden an n8n, FastAPI oder KI-Streaming.
- `backend-fastapi`: eigenes Python-Backend, wenn n8n für schwere Rechen- oder Datenlogik nicht reicht.

### Die Dateien und Ordner
| Pfad | Was es ist |
|------|-----------|
| `CLAUDE.md` | Die Spielregeln für Claude (lädt automatisch): Workflows korrekt bauen, testen, dokumentieren, veröffentlichen und ins eigene Repository bringen. |
| `.mcp.json.example` | Vorlage für die Verbindung zu deiner n8n. Die echte `.mcp.json` mit deinem Key bleibt lokal. |
| `examples/workflows/` | Importierbare Lern-Beispiele mit Sticky-Notes-Erklärung: `n8n-grundlagen.json`, `ai-agent-grundlagen.json`, `ai-agent-datatable.json`, `ai-agent-tool-webhook.json`, `hello-webhook.json`, `datatable-alle-zeilen.json`, dazu je ein Beispiel pro Bootcamp-Thema. |
| `workflows/` | Hier landen am Ende **deine** Workflows als JSON (legt Claude an). |
| `frontend-starter/` | Lauffähige Web-App: Formular → n8n-Webhook, plus optionaler KI-Chat. |
| `backend-example/` | Lauffähiges FastAPI-Backend (`/health` und Beispiel-Endpoint). |
| `docs/datenbank.md` | Welche Datenbank wann (n8n Data Tables, Supabase, SQLite). |
| `docs/zugangs-checkliste.md` | Vorbereitung: was vor Tag 1 geklärt sein sollte. |
| `docs/tourismus-ideen.md` | Ideen-Menü mit konkreten Tourismus-Anwendungsfällen. |

---

## 🧪 Dein erster Workflow

**Noch unsicher?** Sag zuerst **„Hilf mir, meine Idee zu klären.“** Weißt du schon, was du willst, beschreib es direkt, z. B.:
> „Bau mir einen Workflow: Ein Webhook empfängt einen Namen und antwortet mit einer freundlichen Begrüßung.“

Claude baut den Workflow und **validiert, testet mit Beispieldaten, dokumentiert ihn mit Sticky Notes und macht einen Sicherheits-Check**, ohne dass du extra darum bitten musst. Am Ende berichtet Claude verständlich, was passiert ist.

**Lieber erst lernen?** Importiere die Beispiele in n8n (Workflows, Import from File). Alle erklären sich per Sticky Notes:
- `examples/workflows/n8n-grundlagen.json`: Grundlogik, Trigger-Arten und die wichtigsten Bausteine.
- `examples/workflows/ai-agent-grundlagen.json`: ein KI-Agent mit Sprachmodell (Claude), Memory und Tool.
- `examples/workflows/ai-agent-datatable.json`: Chat → KI-Agent → Ergebnis in eine n8n Data Table.
- `examples/workflows/ai-agent-tool-webhook.json`: der KI-Agent ruft per Tool den `hello-webhook` auf.
- `examples/workflows/hello-webhook.json`: Mini-Workflow zum Ausprobieren.
- `examples/workflows/datatable-alle-zeilen.json`: holt **alle** Zeilen einer Data Table. Die Data-Table-Node liefert nämlich still nur 50, ohne Fehlermeldung.

Zu den sechs Bootcamp-Themen gibt es je ein Beispiel, das der passende Themen-Skill als Startpunkt nutzt: `meetingnotizen-aufgaben.json`, `mail-triage-entwuerfe.json`, `bericht-woechentlich.json`, `terminumfrage.json`, `csv-auswertung-diagramm.json`, `folien-google-slides.json`.

> ⚠️ **Eigenes Kürzel:** nach dem Import den Workflow-Namen mit deinem Kürzel beginnen (z. B. `mk: hello-webhook`) und den Webhook-Pfad ändern (z. B. `mk-hello`). Webhook-Pfade gelten für die ganze n8n in one.intelligence, sonst kollidieren sie, wenn mehrere dasselbe Beispiel importieren. Oder sag Claude: „Importiere das Beispiel hello-webhook mit meinem Kürzel.“

---

## 🎨 Optional: Oberfläche und Veröffentlichen

Die Skills `frontend-build` und `frontend-scaffold` befähigen Claude, Next.js-Oberflächen zu bauen: Formulare, Dashboards, Tabellen, Diagramme, Karten. Sag z. B. *„Bau mir ein Dashboard, das die Ergebnisse aus meinem Workflow anzeigt.“*

### 👀 Lokal ansehen
Sag **„Starte mein Frontend.“** Claude installiert alles und startet die App auf deinem Rechner. Du bekommst einen Link wie `http://localhost:3000`. Das reicht zum Bauen, Testen und für eine Demo am eigenen Bildschirm.

### 🌍 Öffentlich teilen (EU-Adresse, ohne Hosting-Account)
Sag **„Stell mein Frontend online.“** Claude veröffentlicht die Oberfläche über den buildbar-Deploy-Dienst (`deploy.tcf.buildbar.de`) auf EU-Infrastruktur, z. B. unter `https://app-xxxx.tcf.buildbar.de`. Der erste Build dauert ein paar Minuten.

Dafür nötig: dein **GitHub-Konto** mit einmaligem Login über die GitHub-CLI (`gh auth login`, Claude führt dich durch) und einmal das **Bootcamp-Passwort** aus dem Zugangsbereich. Deine Keys kommen nie ins Repository.

> ⚠️ **KI-Chat bleibt aus:** Der optionale KI-Chat (`frontend-starter/app/api/chat/route.ts`) hat keinen Login und braucht einen eigenen Anthropic-Schlüssel. Im TCF-Bootcamp gibt es dafür keinen, KI läuft über n8n mit one.intelligence. Wer eine App mit Chat-Schlüssel veröffentlicht, gibt den Schlüssel jeder Person frei, die die Adresse kennt.

---

## 💾 Dein Repository zum Mitnehmen

Alles, was du baust, liegt am Ende in **deinem eigenen privaten GitHub-Repository**. Es gehört dir und bleibt nach dem Bootcamp bei dir. Sag **„Lade mein Projekt in mein privates GitHub-Repository.“** Claude
- legt das private Repository an (`gh repo create --private`) und lädt alles hoch,
- speichert deine Workflows als JSON unter `workflows/`, damit du sie in jede n8n importieren kannst,
- schreibt eine README zu deinem Vorhaben mit dem **nächsten Schritt** für deine Organisation.

Am besten legt Claude das Repository früh an und lädt nach jedem Meilenstein hoch. Am Tag 4 räumt ihr es gemeinsam auf.

---

## 🗄️ Brauche ich eine Datenbank?

Meistens nicht. Faustregel:
- **Daten im n8n-Workflow** → **n8n Data Tables** (in jeder n8n eingebaut).
- **Login, Datei-Uploads, eigene App-Datenbank** → **TCF-Supabase** (Zugangsdaten im Zugangsbereich).

Details: **[docs/datenbank.md](docs/datenbank.md)**.

---

## ⚠️ Sicherheit
- **Niemals** API-Keys (n8n, one.intelligence, Supabase `service_role`) oder das Bootcamp-Passwort ins Repository. `.mcp.json` und `.env*` stehen in `.gitignore`.
- Keys gehören nur in `.mcp.json` (lokal) bzw. in n8n-Credentials.
- Zum Bauen Beispieldaten nehmen: keine echten personenbezogenen oder vertraulichen Daten im Chat, im Repository oder in der gemeinsamen Supabase.

## 👤 Gebaut von
**Friedemann Schütz**, Trainer des Bootcamps: (KI-)Automatisierung, KI-Agenten, Frontends, Infrastruktur, Datenmanagement und Prozessoptimierung (n8n Ambassador). Beratung, Umsetzung, Workshops und Schulungen.
→ **[friedemann-schuetz.de](https://friedemann-schuetz.de)** · [KI-Check](https://ki-check.friedemann-schuetz.de) · [LinkedIn](https://www.linkedin.com/in/friedemann-schuetz)

## 📄 Lizenz und Dank
MIT (siehe `LICENSE`).

Mit großem Dank an:
- **[Romuald Członkowski / czlonkowski](https://github.com/czlonkowski)** für die gebündelten n8n-Kern-Skills und den **n8n-MCP-Server**, auf dem das Ganze läuft.
- **[snipKI](https://snipki.de)** für Grundlage und Idee dieser Vorlage.

Details in `ATTRIBUTION.md`.
