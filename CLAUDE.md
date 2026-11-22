# AI Automation Bootcamp (TCF): Desktop-Vorlage (Claude Code + n8n)

Diese Datei lädt Claude Code beim Öffnen des Projekts automatisch. Sie enthält die Arbeitsweise, die Bootcamp-Regeln und die wichtigsten n8n-Konventionen. **Einrichtung noch nicht erledigt?** Dann zuerst das Runbook in [README.md](README.md) abarbeiten.

## Worum geht es?
Das **AI Automation Bootcamp** ist ein Bootcamp der **Tourismus+Congress GmbH Frankfurt am Main (TCF)** in Kooperation mit **buildbar_**: 30.11. bis 03.12.2026 in Frankfurt am Main, Trainer Friedemann Schütz. Die Teilnehmenden sind Mitarbeitende der TCF. **Jede:r arbeitet am eigenen Vorhaben** aus dem eigenen Berufsalltag, im **eigenen n8n-Konto in one.intelligence**.

Am Ende hat jede Person:
1. eine **erste funktionierende Workflow-Lösung** in der eigenen n8n,
2. ein **eigenes Code-Repository** (privat, auf dem eigenen GitHub-Konto),
3. einen **klaren nächsten Schritt** für das eigene Vorhaben.

**Das Projekt läuft nach dem Bootcamp weiter**, die Person baut danach selbst weiter.

Ablauf: **Tag 1** einrichten, Vorhaben klären (Skills `idee-klaeren` und `grill-me`) und eine erste Version bauen. **Tag 2** eigene Daten und Systeme anbinden. **Tag 3** verlässlich machen. **Tag 4** ein zweites Vorhaben im Chat von one.intelligence, dann Vorstellung und Übergabe.

**Desktop-Variante:** Claude Code läuft lokal auf dem Rechner der Person. n8n ist über den MCP-Server `n8n-mcp` angebunden, der per `npx` lokal startet (stdio). Adresse und API-Schlüssel des eigenen n8n-Kontos stehen in der eigenen `.mcp.json`. Diese Datei ist gitignored und gelangt nie ins Repository.

## Arbeitsweise (so verhältst du dich)
- **Zielgruppe:** Mitarbeitende der TCF (Tourismus und Kongresse in Frankfurt am Main), oft mit wenig oder keiner Code-Erfahrung. Erkläre in **einfacher Sprache**, ohne unerklärten Fachjargon, in der du-Form.
- **Ein Vorhaben pro Person, passend für vier Tage.** Lieber ein Ablauf, der wirklich läuft, als drei halbfertige.
- **Erst die Idee klären:** Ist die Person unsicher, beschreibt sie ihr Vorhaben vage oder geht es direkt nach der Einrichtung los, nutze **zuerst** den Skill `idee-klaeren` (freundliches Interview, Ergebnis: Prozess-Steckbrief). Biete das aktiv an. Hat jemand einen **fertigen Plan** und will ihn prüfen lassen („grill mich“), nimm den Skill `grill-me`, aber **nur auf ausdrücklichen Wunsch**.
- **Zugänge beim Planen mitdenken:** Was das Vorhaben braucht (KI über one.intelligence, Tabellen, Datenbank, Postfach oder andere Systeme des Hauses), steht unter [Was im Setup dabei ist](#was-im-setup-dabei-ist-beim-planen-mitdenken). Fehlt ein Zugang oder eine Freigabe, früh sagen und bis dahin mit Beispieldaten bauen.
- **Themen-Skills nutzen:** Passt das Vorhaben zu einem Bootcamp-Thema, lies vor dem Planen den passenden Skill (siehe [Themen-Skills](#themen-skills)).
- **Freigaben früh prüfen:** Braucht das Vorhaben Postfach, Kalender, Teams oder ein Google-Konto, kläre das am Tag 1 **vor dem Bauen** (siehe [Freigaben früh prüfen](#freigaben-früh-prüfen-microsoft-365-und-google)).
- **Sei proaktiv:** Führe den Standard-Prozess **selbstständig** durch. Frag nicht für jeden Schritt um Erlaubnis.
- **Nach jedem Workflow automatisch (ohne Nachfrage):** validieren, mit **Testdaten testen** (Skill `n8n-testdaten`), mit **Sticky Notes dokumentieren** (Skill `n8n-dokumentation`), **Security-Check** (Skill `n8n-security-audit`). Ist der Workflow fertig, zusätzlich einen kurzen **Prüfbericht** (Skill `n8n-pruefbericht`).
- **Silent Execution:** Werkzeuge ohne Zwischenkommentar ausführen, danach **kurz und verständlich** berichten, was gebaut, getestet und dokumentiert wurde.
- **Frontend zeigen = DU startest es:** Will die Person ihre App ansehen, übernimm das selbst: falls nötig `npm install`, dann `npm run dev` **im Hintergrund** starten und die URL **`http://localhost:3000`** nennen bzw. die Vorschau öffnen. Die Person tippt keine Befehle. Läuft der Server schon, nenn einfach die URL.
- **Event-Infos (Agenda, Zeiten, Ort, Ansprechpersonen, Vorhaben):** Lies **https://tcf.buildbar.de/claude.md** per WebFetch (reines Markdown, aktuell, ohne Zugangsdaten) und antworte daraus. Weitere Seiten: Event-Seite https://tcf.buildbar.de, Vorhaben https://tcf.buildbar.de/vorhaben, Grundlagen https://tcf.buildbar.de/grundlagen, Anleitung Desktop https://tcf.buildbar.de/starten/desktop.
- **Zugangsdaten** für die Supabase des Bootcamps und das **Bootcamp-Passwort** (für das Veröffentlichen) stehen nur im Zugangsbereich **https://tcf.buildbar.de/#zugang**. Den öffnet die Person selbst im Browser. Den n8n-API-Schlüssel legt sie in ihrem eigenen n8n-Konto an.
- **Vorrang:** Beschreibt ein Skill einen anderen Hosting-Weg oder einen fremden Account, gelten im Bootcamp die Abläufe in dieser Datei.

## n8n-Zugang
- **Eure n8n in one.intelligence**, der Plattform, die die TCF für alle Mitarbeitenden nutzt. Jede Person arbeitet in ihrem **eigenen Konto**. Adresse und API-Schlüssel stehen in der lokalen `.mcp.json` (`N8N_API_URL`, `N8N_API_KEY`). Die Workflows bleiben dort, auch nach dem Bootcamp.
- **Eigenes Kürzel:** Workflows, Data Tables, Webhook- und Formularpfade beginnen mit dem Kürzel der Person (z. B. Workflow `mk_anfragen-sortieren`, Pfad `mk-anfragen`). Webhook-Pfade gelten für die ganze n8n-Instanz, auch für andere Häuser in one.intelligence. Ein Pfad darf nur einmal aktiv sein, sonst lässt sich der Workflow nicht aktivieren. In Skills und Beispiel-Workflows steht dafür `kuerzel`, `<kürzel>` oder `DEIN-KUERZEL` (Beispiel `mk`): Dort überall das Kürzel der Person einsetzen.
- **Importe und Vorlagen** bekommen dasselbe Kürzel: Beispiele aus `examples/workflows/` und Vorlagen aus `n8n_deploy_template` (Parameter `name`) sofort umbenennen (z. B. `mk: hello-webhook`) und Webhook- und Formularpfade ändern (z. B. `mk-hello`), bevor du aktivierst.
- **Gesperrt:** Workflows löschen, Zugänge verwalten, Ordner löschen oder verschieben, Versionen und Ausführungen löschen sowie Data Tables löschen oder umbauen sind in der `.mcp.json` abgeschaltet (`DISABLED_TOOLS`, `DISABLED_TOOL_OPERATIONS`), weil es echte Konten sind. Will die Person etwas löschen, macht sie das selbst im n8n-Editor. Diese Zeilen nicht aus der `.mcp.json` entfernen.
- **Zugänge (Credentials) legt die Person selbst im n8n-Editor an**, nie im Chat. Du baust den Node ohne Zugang, legst den Workflow an und erklärst in einfachen Worten: „Öffne in n8n den Workflow „…“, klick doppelt auf den Node „…“, wähle oben bei „Credential to connect with“ deinen Zugang aus oder lege mit „Create new credential“ einen an, und speichere.“
- **Verbindung ändern:** URL und Key stehen in `.mcp.json`. Meldet die n8n, dass der Schlüssel ungültig oder abgelaufen ist (401), legt die Person in n8n einen neuen an (Einstellungen, „n8n API“, lange Laufzeit) und schreibt ihn dir in den Chat; du trägst ihn in `.mcp.json` ein, danach startet sie die App neu. Den Key nie ausgeben, nie in andere Dateien schreiben, nie committen.
- **Workflows ohne Webhook testen:** Steht in `.mcp.json` ein gültiger `N8N_MCP_ACCESS_TOKEN`, kann `n8n_test_workflow` auch Workflows mit Zeitplan oder manuellem Trigger starten. Ohne ihn antwortet es mit `Workflow cannot be triggered externally`. Das ist kein Fehler im Workflow: Dann bittest du die Person, den Workflow im n8n-Editor mit **Execute workflow** zu starten, und siehst danach unter **Executions** nach.
- Zeitgesteuerte Workflows nicht im Minutentakt laufen lassen und nach dem Testen wieder deaktivieren, wenn sie nicht dauerhaft laufen sollen.

## KI-Zugang (one.intelligence)
KI-Schritte laufen über **one.intelligence**, mit dem eigenen Zugang der Person. So bleiben die Daten in der Plattform, die die TCF freigegeben hat, und die Workflows laufen nach dem Bootcamp ohne fremde Schlüssel weiter.
- **Node:** „one.intelligence Chat Model“, `"type": "CUSTOM.lmChatOneIntelligence"`, `"typeVersion": 1`, `"parameters": {"model": "claude-sonnet-5-5"}`. Er hängt über `ai_languageModel` an einem „Basic LLM Chain“ (`@n8n/n8n-nodes-langchain.chainLlm`, typeVersion 1.7) oder einem „AI Agent“ (`@n8n/n8n-nodes-langchain.agent`).
- **Modelle:** Welche das Konto anbietet, zeigt die Auswahl im Node. Wo vorhanden: `claude-sonnet-5-5` als Standard, `claude-haiku-5-5` für einfache, schnelle Aufgaben. Ein Modell mit `local/` im Namen läuft auf den Servern von one.intelligence, wenn Daten die Plattform nicht verlassen sollen.
- **Zugang:** vom Typ `oneIntelligenceApi`, legt die Person selbst an. Den API-Schlüssel dafür bekommt sie in one.intelligence unter Einstellungen, Konto, API-Schlüssel. Er gehört nur in n8n, nie in den Chat, in Code oder ins Repository.
- **Nodes mit `CUSTOM.` im Typ** baut one.intelligence selbst. n8n-mcp kennt sie nicht: `get_node` findet sie nicht, und `n8n_validate_workflow` meldet sie als unbekannt. Das ist hier normal. Ob so ein Node arbeitet, zeigt der Testlauf. Ersetze ihn nie wegen dieser Meldung durch einen anderen Node.
- **Rechnen und Vergleichen macht n8n, nie die KI.** Die KI liest, sortiert, fasst zusammen und schreibt Entwürfe.

## Was im Setup dabei ist (beim Planen mitdenken)

Im TCF-Setup gibt es keine gemeinsamen Zugänge zu bezahlten Datendiensten. **Denk mit, was eure n8n und das Bootcamp-Setup mitbringen, und schlag es vor, wenn das Vorhaben es braucht.**

| Wenn das Vorhaben … | dann | Achtung |
|---|---|---|
| Texte verstehen, sortieren, zusammenfassen oder Entwürfe schreiben soll | **KI über one.intelligence** (siehe oben) | Normalfall für alles mit KI |
| eine Tabelle braucht | **Data Tables** in n8n | eigenes Kürzel im Namen |
| eine App mit Login, Datei-Upload oder eigener Datenbank braucht | **Supabase des Bootcamps** | Schlüssel im Zugangsbereich, keine sensiblen Daten |
| eine Seite oder ein Formular für Menschen braucht | **n8n-Formular** oder eine kleine **App** (lokal, öffentlich über `deploy.tcf.buildbar.de`) | |
| **offene Daten** abruft (Wetter, Feiertage, Statistik, OpenStreetMap) | nichts nötig, HTTP-Request-Node | |
| Infos von **einfachen Websites** braucht | HTTP Request liest die Seite, die KI zieht die Angaben heraus | Nutzungsbedingungen der Seite beachten |
| **Mails verschicken** soll | Mail-Zugang des Hauses (Outlook) nach Freigabe der IT | siehe [Mailversand](#mailversand) |

**Nicht dabei** sind Dienste, die je Abfrage abrechnen: Google-Einträge von Betrieben, Seiten mit Bot-Schutz oder viel JavaScript, Sprache zu Text, eine große Wissensbasis mit Vektorsuche. Braucht ein Vorhaben so etwas, im Steckbrief festhalten, welcher Dienst, wer das Konto anlegt und bezahlt und wie oft der Ablauf für wie viele Einträge läuft. Bis das geklärt ist, mit Beispieldaten bauen.

## Freigaben früh prüfen (Microsoft 365 und Google)
Viele Vorhaben scheitern nicht an n8n, sondern an fehlenden Freigaben. Kläre das deshalb **am Tag 1 im Steckbrief, bevor gebaut wird**, mit dem Skill `m365-google-freigaben`. Fehlt der Skill, nutze die Fakten in diesem Abschnitt.
- **Outlook-Postfach und Kalender (Microsoft 365):** In Standard-Tenants (von Microsoft empfohlene Consent-Policy) braucht der Zugriff eine **Admin-Freigabe** der IT.
- **Teams (Teams-Node, Teams-Transkripte):** braucht **immer** eine Admin-Freigabe (Admin-Consent).
- **IMAP mit Passwort** ist bei Exchange Online abgeschaltet und daher kein Ausweg.
- **Google (Gmail, Kalender, Drive, Sheets, Slides):** Auf einer selbst betriebenen n8n (dazu zählt eure n8n in one.intelligence) braucht es eine **eigene OAuth-App**. Steht sie im Status „Testing“, laufen die Refresh-Tokens **nach 7 Tagen** ab.
- **Bis die Freigabe da ist:** mit Beispieldaten, Datei-Upload oder n8n-Formular bauen, sodass später nur die Anbindung getauscht wird. Offene Freigaben kommen als nächster Schritt in die README.

## Themen-Skills
Für die sechs Bootcamp-Themen gibt es eigene Skills. Lies den passenden Skill, sobald ein Vorhaben in die Richtung geht:

| Thema | Skill |
|-------|-------|
| Meetingnotizen strukturieren | `meetingnotizen` |
| E-Mail-Anfragen sortieren und Antwortentwürfe vorbereiten | `mail-triage-entwuerfe` |
| Wiederkehrende Berichte erstellen | `bericht-zeitgesteuert` |
| Terminfindung und Koordination erleichtern | `terminkoordination` |
| Daten analysieren und visualisieren | `daten-visualisieren` |
| Präsentationen effizienter erstellen | `praesentation` |
| Freigaben für Microsoft 365 und Google klären | `m365-google-freigaben` |

Zu jedem Thema gibt es einen importierbaren Beispiel-Workflow unter `examples/workflows/` (der Skill nennt die Datei). Beim Import Namen und Pfade mit dem Kürzel der Person versehen (siehe [n8n-Zugang](#n8n-zugang)). Die Vorhaben der Gruppe stehen nach dem Kick-off auf https://tcf.buildbar.de/vorhaben.

Gut zu wissen: n8n hat **keinen PowerPoint-Node**. Für Folien gibt es den **Google Slides Node** (u. a. Replace Text in einer Vorlage).

## Workflow-Erstellung: Standard-Prozess
Diesen Ablauf führst du **automatisch** durch (Schritte 6 bis 9 und 11 ohne Extra-Aufforderung):

1. `tools_documentation()`: Best Practices laden
2. `search_templates({query: "..."})`: passende Vorlage prüfen
3. Passt eine Vorlage: `n8n_deploy_template({templateId, name: "<Kürzel>: <Titel>"})`, **Autor nennen**. Danach Webhook- und Formularpfade mit dem Kürzel versehen.
4. Sonst: `search_nodes()` → `get_node({detail: "standard"})` → `n8n_create_workflow()`
5. Iterativ erweitern: `n8n_update_partial_workflow({id, intent, operations})`
6. Validieren: `n8n_validate_workflow({id})` → `n8n_autofix_workflow({id})`
7. Testdaten generieren und **in der Instanz testen**. Das fängt Laufzeitfehler, die der statische Validator nicht sieht (Skill `n8n-testdaten`)
8. **Workflow dokumentieren** mit Sticky Notes (Skill `n8n-dokumentation`)
9. Security-Checkliste (Skill `n8n-security-audit`)
10. Aktivieren: `n8n_update_partial_workflow({operations: [{type: "activateWorkflow"}]})`
11. **Prüfbericht** erstellen, sobald der Workflow fertig ist (Skill `n8n-pruefbericht`)

## Kritische Konventionen

### nodeType-Formate (je nach Tool unterschiedlich!)
| Tool-Kategorie | Format | Beispiel |
|---------------|--------|----------|
| Search/Validate | `nodes-base.*` | `nodes-base.slack` |
| Workflow-Tools | `n8n-nodes-base.*` | `n8n-nodes-base.slack` |
| AI/LangChain | `@n8n/n8n-nodes-langchain.*` | `@n8n/n8n-nodes-langchain.agent` |

### Webhook-Datenstruktur
Webhook-Daten liegen unter `.body`:
```
FALSCH:  {{$json.email}}
RICHTIG: {{$json.body.email}}
```

### Expression-Syntax
- Expressions immer mit `{{}}`: `{{$json.field}}`
- In **Code Nodes KEIN** `{{}}`: `$json.field`
- Node-Namen mit Leerzeichen in Quotes: `{{$node["HTTP Request"].json.data}}`
- Node-Namen sind case-sensitive

### IF-Node Multi-Output Routing (KRITISCH!)
IF-Nodes haben zwei Outputs. `branch` setzen, sonst landen beide Connections am selben Output:
```json
{type: "addConnection", source: "If", target: "True Handler", sourcePort: "main", targetPort: "main", branch: "true"}
{type: "addConnection", source: "If", target: "False Handler", sourcePort: "main", targetPort: "main", branch: "false"}
```
Switch-Node: `case: 0`, `case: 1`, …

### addConnection-Syntax (vier separate String-Parameter!)
```json
{ "type": "addConnection", "source": "Webhook", "target": "Slack", "sourcePort": "main", "targetPort": "main" }
```
`removeConnection` hat dasselbe Format.

### AI-Workflow-Connections
Für LangChain/AI-Nodes `sourceOutput` nutzen: `ai_languageModel`, `ai_tool`, `ai_memory`, `ai_embedding`, `ai_vectorStore`, `ai_outputParser`, `ai_document`, `ai_textSplitter`.

⚠️ **AI-Tool-Node-Namen:** Der Name eines als Tool verbundenen Nodes (`ai_tool`) wird zum **Funktionsnamen fürs LLM**. Daher **nur Buchstaben, Ziffern und Unterstriche** (kein Leerzeichen, Bindestrich, keine Klammer, kein Umlaut, nicht mit Ziffer beginnen). Beispiel: `hello_webhook_aufrufen`, nicht „hello-webhook aufrufen“.

⚠️ **AI-Sub-Nodes haben kein „Execute“:** Tool-, Modell- und Memory-Nodes laufen **nur, wenn der Agent sie aufruft**. Den Workflow über den **Chat** starten, **nicht** einen Sub-Node einzeln per „Test step“ ausführen (sonst Fehler „has a supplyData method but no execute method“).

⚠️ **HTTP-Tool für Agents:** den **regulären HTTP Request als Tool** verwenden (`n8n-nodes-base.httpRequestTool`, v4.x) mit `$fromAI('feld','Beschreibung','string')` für Werte, die das LLM füllt. **Nicht** den Legacy-Node `@n8n/n8n-nodes-langchain.toolHttpRequest` (v1.1, deprecated). Fast jeder Standard-Node kann als Tool an den Agent gehängt werden.

### Ein grüner Lauf ist kein Beweis

Die teuersten Fehler in n8n melden **keinen Fehler**. Der Ablauf läuft durch, ist
grün, und das Ergebnis ist trotzdem falsch. Beim Vorabbau der Beispiel-Workflows
waren das **neun von dreizehn** gefundenen Stolperstellen.

**Deshalb nach jedem Abruf prüfen, ob das ERWARTETE Ergebnis da ist**, nicht ob der
Aufruf funktioniert hat:

```javascript
const zeilen = $input.all();
if (zeilen.length < ERWARTET) {
  throw new Error('Nur ' + zeilen.length + ' statt ' + ERWARTET + '. Nicht weiterarbeiten.');
}
```

Diese fünf kosten sonst je eine halbe Stunde Suche (alle am 19.09.2026 gemessen):

| Wo | Was still passiert |
|---|---|
| **HTTP-Node, Query-Parameter** | Ein Parameter lässt sich **nicht mehrfach** senden. Wer `parameters=a`, `parameters=b` einzeln anlegt, sendet nur den letzten. Als Komma-Liste schreiben: `parameters=a,b` |
| **Datei-Upload** | n8n hängt einen **Index** an den Feldnamen: hochgeladen als `datei`, angekommen als `datei0`. Und die Endung wird aus dem **MIME-Typ** geraten, nicht aus dem Namen — `report.xlsx` kann als `bin` ankommen |
| **PDF einlesen** | Ein **eingescanntes** PDF hat keine Textebene. `extractFromFile` liefert einen leeren String, ohne zu scheitern. Auf Mindestlänge prüfen |
| **Leeres Ergebnis** | **0 Items stoppen die ganze Kette.** Ein korrekt leeres Ergebnis (etwa: kein Feiertag in dieser Woche) sieht dann aus wie ein Absturz. `alwaysOutputData` setzen |
| **Zählfelder von APIs** | Felder wie `total_rows` meinen oft den **Gesamtbestand**, nicht die Treffer der Abfrage. Nie als Trefferzahl lesen, immer die Liste selbst zählen |

**Und für Logik, die man prüfen kann:** erst ausserhalb von n8n testen, dann
einbauen. n8n speichert kaputten Code stillschweigend, der Fehler kommt zur
Laufzeit — und vor Publikum ist das der schlechteste Zeitpunkt.

### Mailversand

Mails gehen nur über einen **eigenen Mail-Zugang der Person**, etwa das Postfach des Hauses (Outlook), und nur an die Person selbst oder ihr Team, mit deren Einverständnis. Für Outlook braucht es in Microsoft-365-Organisationen meist eine **Freigabe der IT** (Skill `m365-google-freigaben`). Einen gemeinsamen Mailversand gibt es im Bootcamp nicht. Die Empfänger stehen fest im Workflow (Set-Node), nie aus einer Eingabe einer Oberfläche.

**Ohne Mail-Zugang geht es auch:** Ergebnis in eine Data Table schreiben oder den Webhook die fertige Liste zurückgeben lassen und im Frontend anzeigen. Für Berichte, die jemand prüfen soll, bevor sie rausgehen, eignet sich ein Outlook-**Entwurf** (`resource: "draft"`), sobald die Freigabe da ist.

## Best Practices

### Do
- **Template-First:** immer Templates prüfen, bevor von Scratch gebaut wird
- **Explicit Parameters:** ALLE Parameter explizit setzen (Default-Werte sind die häufigste Fehlerquelle)
- Workflows **iterativ** bauen, `intent` bei Updates angeben
- Nach signifikanten Änderungen validieren, Validation-Profil `runtime`
- Batch-Operationen in **einem** `n8n_update_partial_workflow`-Call
- `includeExamples: true` für echte Konfigurationsbeispiele
- **Zahlen aus der Quelle:** Kennzahlen, Summen und Diagrammwerte rechnet n8n aus den echten Daten, nicht die KI

### Don't
- nodeType-Prefix vergessen
- Validation vor Aktivierung überspringen
- Expression-Syntax in Code Nodes verwenden
- **Code Nodes nutzen, wenn Standard-Nodes verfügbar sind** (Code ist der letzte Ausweg)
- Workflows, Zugänge oder Tabellen anderer Personen anfassen

## Datenbank
Meistens braucht es keine externe Datenbank:
- **n8n Data Tables** (Standard, in eurer n8n eingebaut, per MCP `n8n_manage_datatable`): für Daten, die zu einem Workflow gehören. Mit eigenem Kürzel im Namen. Der Speicher gilt für die ganze n8n, deshalb keine großen Datenmengen und keine Dateien hinein.
- **TCF-Supabase:** Postgres mit Login und Datei-Uploads. Project-URL, `anon`-Key und `service_role`-Key stehen im Zugangsbereich https://tcf.buildbar.de/#zugang. Der **`service_role`-Key nur serverseitig** als Credential in n8n, **nie** im Frontend, in `env` für den Deploy oder im Repository. Das Frontend nutzt höchstens den `anon`-Key, und nur mit Row Level Security auf den Tabellen. Alle Teilnehmenden nutzen dieselben Keys: eigene Tabellen mit **eigenem Präfix**, keine sensiblen oder personenbezogenen Daten.

Details: `docs/datenbank.md`.

## App öffentlich veröffentlichen (EU-Adresse, ohne Hosting-Account)
Lokal zeigst du die App auf `http://localhost:3000`. Will die Person eine **öffentliche Adresse** („stell mein Frontend online“, „veröffentliche meine App“), gehst **du** so vor. Die Person tippt keine Befehle.

**Voraussetzungen:** GitHub-CLI angemeldet (`gh auth status`, sonst `gh auth login` mit Browser-Login durch die Person). Das Projekt liegt im **eigenen privaten Repository** (siehe [Dein Repository zum Mitnehmen](#dein-repository-zum-mitnehmen-ergebnis-regel)). `npm run build` im Frontend-Ordner ist grün. Das **Bootcamp-Passwort** (dasselbe wie für den Zugangsbereich https://tcf.buildbar.de/#zugang) schreibt dir die Person in den Chat. Schreib es nie in eine Datei.

1. Aktuellen Stand committen und pushen: `git push`. Vorher mit `git remote get-url origin` prüfen, dass `origin` auf das eigene private Repository zeigt und nicht auf die Vorlage `freddy-schuetz/tcf-ai-automation-bootcamp`. Zeigt es noch auf die Vorlage, zuerst das eigene Repository anlegen (siehe [Dein Repository zum Mitnehmen](#dein-repository-zum-mitnehmen-ergebnis-regel), Schritt 6).
2. Deploy vorbereiten:
   ```bash
   curl -s -X POST https://deploy.tcf.buildbar.de/prepare -d repo=<owner>/<name> --data-urlencode password=<BOOTCAMP-PASSWORT>
   ```
   Antwort: `deployId` und `public_key`.
3. Den Public Key als **read-only Deploy-Key** ans private Repository hängen (die Person bestätigt den Aufruf per Klick):
   ```bash
   gh api repos/<owner>/<name>/keys -f title=buildbar-deploy -f key='<public_key>' -F read_only=true
   ```
4. Veröffentlichen:
   ```bash
   curl -s -X POST https://deploy.tcf.buildbar.de/publish -d deployId=<deployId> -d base_dir=/frontend-starter --data-urlencode password=<BOOTCAMP-PASSWORT> --data-urlencode env=$'NEXT_PUBLIC_N8N_BASE=https://EURE-N8N-ADRESSE\nNEXT_PUBLIC_SUPABASE_URL=...'
   ```
   Antwort: die URL, z. B. `https://app-xxxx.tcf.buildbar.de`. **Der erste Build dauert einige Minuten.**
5. **Spätere Änderungen veröffentlichen — dieselbe Adresse:** committen, pushen, dann
   ```bash
   curl -s -X POST https://deploy.tcf.buildbar.de/update -d repo=<owner>/<name> --data-urlencode password=<BOOTCAMP-PASSWORT>
   ```
   ⚠️ **Nie ein zweites Mal `/prepare` + `/publish` für dasselbe Repository.** Das legt eine **zweite App unter neuer Adresse** an, während die alte mit dem alten Stand weiterläuft — und genau dann wirkt es so, als ginge das Veröffentlichen nicht mehr. `/prepare` antwortet bei einem bekannten Repository deshalb mit `existing: true` und der bestehenden Adresse.
6. **Antwortet die Adresse nach ein paar Minuten weiter mit 503 oder „no available server“:** nicht raten, nachsehen.
   ```bash
   curl -s -X POST https://deploy.tcf.buildbar.de/status -d repo=<owner>/<name> --data-urlencode password=<BOOTCAMP-PASSWORT>
   ```
   Antwort: `status` (`finished` oder `failed`), `commit` und bei einem Fehlschlag `fehlerzeilen` aus dem Build-Protokoll auf dem Server. Ein `failed` liegt fast immer am eigenen Stand (fehlende Abhängigkeit, Typfehler, fehlende Env-Variable) — sag der Person, was dort steht, statt ein Serverproblem zu vermuten.
7. **Einmalig einrichten, danach genügt `git push`:** Die Antwort von `/publish` und `/update` enthält unter `webhook.einmal_ausfuehren` eine fertige `gh`-Zeile. Führ sie einmal aus (die Person bestätigt per Klick). Danach stösst jeder Push auf `main` die Veröffentlichung selbst an, Schritt 5 entfällt.

- `base_dir` ist der Frontend-Ordner im Repository (Standard `/frontend-starter`). `env` enthält eine Zeile `KEY=VALUE` je Variable.
- ⚠️ **`NEXT_PUBLIC_*`-Werte landen im Browser-Code** und sind damit öffentlich: nur n8n-Adresse, Supabase-URL und Supabase-`anon`-Key. **Nie** in `env` oder ins Repository: `service_role`-Key, KI-Schlüssel, n8n-API-Key, Bootcamp-Passwort.
- ⚠️ **KI-Chat im Frontend-Starter bleibt aus:** `frontend-starter/app/api/chat/route.ts` hat **keinen Login** und braucht einen eigenen Anbieter-Schlüssel. Im TCF-Bootcamp gibt es dafür keinen Schlüssel, und ein offener Chat auf einer öffentlichen Adresse wäre für jede Person nutzbar, die sie kennt. Deshalb beim Veröffentlichen **weder `ANTHROPIC_API_KEY` noch `CHAT_ENABLED=true`** in `env`. KI läuft im Bootcamp über **n8n** mit dem Node von one.intelligence; die App ruft dafür nur einen Webhook auf.

## Dein Repository zum Mitnehmen (Ergebnis-Regel)
Am Ende des Bootcamps liegt **alles** im **eigenen privaten GitHub-Repository** der Person. Das ist Teil des Ergebnisses, nicht optional. Lege das Repository **früh** an (spätestens, sobald der erste Workflow läuft), pushe nach jedem Meilenstein und räume es am Tag 4 gemeinsam mit der Person auf. Die Person tippt keine Befehle.

1. **GitHub-Login:** `gh auth status`. Nicht angemeldet: `gh auth login` starten, die Person bestätigt im Browser. Fehlt `gh`: Windows `winget install --id GitHub.cli`, macOS `brew install gh`, danach App neu starten.
2. **Workflows exportieren:** Jeden Workflow der Person mit `n8n_get_workflow({id, mode: "full"})` holen und als JSON unter `workflows/<kurzer-name>.json` speichern. Vor dem Speichern nur `name`, `nodes`, `connections` und `settings` behalten. `pinData`, `id`, `versionId`, `activeVersionId`, `shared`, `meta` und `tags` entfernen, bei `credentials` in den Nodes nur den Namen lassen und die `id` löschen. Keys oder Passwörter in Parametern ebenfalls entfernen. Beim Import in eine andere n8n werden Credentials ohnehin neu zugeordnet.
3. **README schreiben:** Ersetze den Vorlagen-Text in `README.md` durch eine README zum eigenen Vorhaben: welches Problem es löst, welche Workflows es gibt (Dateien unter `workflows/`), welche Credentials und Freigaben nötig sind, wie man die Workflows in eine andere n8n importiert, aktueller Stand und Grenzen und zum Schluss **„Nächster Schritt“**: ein konkreter Schritt (z. B. „IT um Admin-Freigabe für das Postfach bitten“). Der Prüfbericht darf als `docs/pruefbericht.md` dazu.
4. **Vor dem Commit prüfen:** `git status`. `.mcp.json`, `.env.local` und `backup/` dürfen nicht auftauchen (sind gitignored). Keine Keys, keine Passwörter, keine echten personenbezogenen Daten im Repository.
5. **Commit:** `git add -A` und `git commit -m "<kurze Beschreibung>"`. Fragt git nach Name und E-Mail, frag die Person und setze beides mit `git config user.name` und `git config user.email` nur für dieses Repository.
6. **Privates Repository anlegen und pushen:** Der Klon zeigt noch auf die öffentliche Vorlage. Deshalb zuerst `git remote rename origin vorlage`, dann:
   ```bash
   gh repo create ai-automation-bootcamp --private --source=. --remote=origin --push
   ```
   Ist der Name schon vergeben (z. B. weil die Person auch den Browser-Weg genutzt hat), frag nach einem anderen Namen. Danach reicht `git push`.
7. **Link nennen** und kurz zeigen, wo Workflows und README liegen.

## Sicherheit
1. **API-Keys niemals** in Workflow-Parametern: n8n **Credentials** nutzen!
2. Security-Checkliste vor Aktivierung (Skill `n8n-security-audit`)
3. Keine personenbezogenen Daten in Node-Namen, Sticky Notes, Testdaten oder im Repository; in der gemeinsamen Bootcamp-Supabase nur Test- oder Beispieldaten. Sensible Daten des Hauses nie in den Chat kopieren, zum Bauen Beispieldaten in derselben Struktur nehmen
4. `.mcp.json`, `.env*`, `.codex/config.toml` und `opencode.json` bleiben lokal (gitignored). Nie committen, nie ausgeben.
5. Kein offener KI-Chat auf einer öffentlichen Adresse (siehe Abschnitt zum Veröffentlichen)
6. **Lizenz:** Die Dokument-Skills von Anthropic (pptx, docx, xlsx aus `anthropics/skills`) sind proprietär lizenziert. **Nicht** kopieren, nicht nachbauen, nichts daraus ableiten.
7. Workflow-Änderungen werden automatisch nach `backup/` gesichert (Hook, lokal, gitignored)

## Geladene Skills
**Am Anfang (Tag 1):** `idee-klaeren` klärt Idee und Prozess und macht daraus einen Bau-Auftrag (Steckbrief), Ideen-Menü in `docs/tourismus-ideen.md` · `grill-me` ist der Härtetest für einen **fertigen** Plan, **nur auf ausdrücklichen Wunsch** („grill mich“) · `m365-google-freigaben` prüft früh, welche Freigaben das Vorhaben braucht.
**Themen:** `meetingnotizen`, `mail-triage-entwuerfe`, `bericht-zeitgesteuert`, `terminkoordination`, `daten-visualisieren`, `praesentation`
**n8n:** `n8n-mcp-tools-expert`, `n8n-workflow-patterns`, `n8n-node-configuration`, `n8n-expression-syntax`, `n8n-validation-expert`, `n8n-code-javascript`, `n8n-code-python` (von czlonkowski/n8n-skills) · `n8n-testdaten`, `n8n-dokumentation`, `n8n-security-audit`, `n8n-pruefbericht`
**Frontend/Backend (optional):** `frontend-build`, `frontend-scaffold`, `backend-fastapi`, lauffähige Beispiele in `frontend-starter/` und `backend-example/`.
