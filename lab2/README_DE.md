# Lab 2: Sicherheitsanalyse & Code-Korrekturen

## Überblick

In diesem Lab verwenden Sie Bob, um bestehenden Code zu analysieren, Sicherheitslücken zu identifizieren und Korrekturen zu implementieren. Sie lernen, häufige Sicherheitsprobleme wie SQL-Injection, XSS und hartcodierte Geheimnisse zu erkennen und dann Bobs verschiedene Modi zu verwenden, um diese zu beheben.

> **🔍 Bob-Differenzierungsmerkmal: [Bob Findings](../bob-differentiators.md#3--bob-findings-automated-analysis-engine)**
> Dieses Lab zeigt Bob Findings, Bobs automatisierte Sicherheits- und Code-Qualitätsanalyse-Engine. Im Gegensatz zu einfachen Lintern bietet Bob Findings kontinuierliche, proaktive Analysen mit spezifischen Sanierungsempfehlungen, Schweregradsbewertungen und Code-Beispielen. Es ist, als hätten Sie einen Sicherheitsexperten, der Ihren Code in Echtzeit überprüft!

**Dauer**: 45 Minuten
**Schwierigkeitsgrad**: Fortgeschrittene

## Was Sie analysieren werden

Eine anfällige Todo-Anwendung mit absichtlichen Sicherheitslücken:
- **SQL-Injection**-Schwachstellen in Datenbankabfragen
- **Cross-Site Scripting (XSS)** im Frontend-Code
- **Hartcodierte Geheimnisse** und Anmeldedaten
- **Fehlende Eingabevalidierung**
- **Unsichere Fehlerbehandlung**

## Lernziele

Am Ende dieses Labs werden Sie:
- ✅ Ask-Modus verwenden, um bestehende Codebasen zu verstehen
- ✅ Architect-Modus verwenden, um Fehler zu identifizieren und Korrekturen zu planen
- ✅ SQL-Injection-Schwachstellen erkennen
- ✅ XSS-Angriffsvektoren identifizieren
- ✅ Hartcodierte Geheimnisse und Anmeldedaten finden
- ✅ Sicherheitskorrekturen mit Code-Modus implementieren
- ✅ Sichere Codierungspraktiken anwenden

## Voraussetzungen

Stellen Sie vor dem Start sicher, dass Sie Folgendes haben:
- [ ] Lab 1 abgeschlossen (oder vertraut mit Flask und JavaScript)
- [ ] Python 3.8+ installiert
- [ ] Bob installiert und läuft
- [ ] Verständnis grundlegender Web-Sicherheitskonzepte

## Lab-Struktur

```
Lab 2 Zeitplan (45 Minuten)
├── Schritt 1: Code-Exploration (10 Min.)
├── Schritt 2: Fehleridentifikation (10 Min.)
├── Schritt 3: Sicherheitsanalyse (15 Min.)
└── Schritt 4: Implementierung von Korrekturen (10 Min.)
```

---

## Schritt 1: Code-Exploration mit Ask-Modus (10 Minuten)

### Die anfällige Codebasis verstehen

Das Verzeichnis `vulnerable-app/` enthält eine Todo-Anwendung mit absichtlichen Sicherheitsproblemen. Lassen Sie uns Bobs Ask-Modus verwenden, um die Code-Struktur zu verstehen.

### 1.1: In den Ask-Modus wechseln

Öffnen Sie Bob und wechseln Sie in den **Ask-Modus** (❓).

### 1.2: Das Backend erkunden

**Eingabeaufforderung für Bob:**

```
Bitte analysiere den Code in lab2/vulnerable-app/backend/ und erkläre:
1. Was ist die Gesamtstruktur der Anwendung?
2. Wie werden Datenbankabfragen konstruiert?
3. Wie wird Benutzereingabe behandelt?
4. Welche Sicherheitsmaßnahmen sind vorhanden?
```

**Worauf Sie achten sollten:**

Bob sollte identifizieren:
- Flask-Anwendung mit REST-API-Endpunkten
- Direkte String-Verkettung in SQL-Abfragen ⚠️
- Hartcodierte Datenbank-Anmeldedaten ⚠️
- Fehlende Eingabevalidierung ⚠️

### 1.3: Das Frontend erkunden

**Eingabeaufforderung für Bob:**

```
Analysiere den Frontend-Code in lab2/vulnerable-app/frontend/ und erkläre:
1. Wie wird Benutzereingabe in der UI angezeigt?
2. Gibt es DOM-Manipulationsmethoden, die riskant sein könnten?
3. Wie werden Daten von der API gerendert?
```

**Worauf Sie achten sollten:**

Bob sollte identifizieren:
- Verwendung von `innerHTML` zum Rendern von Benutzerinhalten ⚠️
- Keine Eingabebereinigung ⚠️
- Direkte Einfügung von Benutzerdaten in das DOM ⚠️

### 1.4: Nach spezifischen Funktionen fragen

**Eingabeaufforderung für Bob:**

```
Erkläre die Funktion search_todos() in app.py. 
Was macht sie und gibt es Sicherheitsbedenken?
```

**Erwartete Antwort:**

Bob sollte erklären, dass die Funktion String-Formatierung verwendet, um SQL-Abfragen zu erstellen, was anfällig für SQL-Injection-Angriffe ist.

**💡 Wichtige Erkenntnis**: Der Ask-Modus ist perfekt, um unbekannten Code zu verstehen und Erklärungen zu erhalten, wie Dinge funktionieren.

---

## Schritt 2: Fehleridentifikation mit Plan-Modus (10 Minuten)

Jetzt verwenden wir den Architect-Modus, um systematisch alle Probleme zu identifizieren.

### 2.1: In den Plan-Modus wechseln

Wechseln Sie von Ask zu **Plan-Modus** (🎯).

### 2.2: Sicherheitsanalyse anfordern

> **💡 Bob Findings verwenden**
> Bob Findings kann Ihren Code automatisch auf Sicherheitslücken, Code-Qualitätsprobleme und Compliance-Verstöße scannen. Die Analyse, die Sie gleich anfordern werden, demonstriert Bobs [Sicherheitslücken-Erkennungsfähigkeiten](../bob-differentiators.md#security-vulnerability-detection), die über einfache statische Analysen hinausgehen und kontextbewusste Empfehlungen bieten.

**Eingabeaufforderung für Bob:**

```
Analysiere die Codebasis in lab2/vulnerable-app/ auf Sicherheitslücken.
Erstelle einen umfassenden Bericht mit:
1. Liste aller gefundenen Sicherheitsprobleme
2. Schweregradsbewertung für jedes Problem (Kritisch/Hoch/Mittel/Niedrig)
3. Potenzielle Auswirkungen jeder Schwachstelle
4. Empfohlene Korrektur für jedes Problem
5. Prioritätsreihenfolge für Korrekturen
```

**Erwartete Ausgabe:**

Bob sollte eine strukturierte Analyse wie diese bereitstellen:

```
SICHERHEITSANALYSEBERICHT
=========================

KRITISCHE PROBLEME:
1. Hartcodierte Datenbank-Anmeldedaten (config.py)
   - Auswirkung: Vollständiger Datenbankzugriff, wenn Code offengelegt wird
   - Korrektur: Umgebungsvariablen verwenden
   - Priorität: 1

2. SQL-Injection (app.py, search_todos-Funktion)
   - Auswirkung: Unbefugter Datenzugriff, Datenmanipulation
   - Korrektur: Parametrisierte Abfragen verwenden
   - Priorität: 1

HOHE PROBLEME:
3. Cross-Site Scripting (app.js, displayTodo-Funktion)
   - Auswirkung: Script-Injection, Session-Hijacking
   - Korrektur: textContent statt innerHTML verwenden
   - Priorität: 2

MITTLERE PROBLEME:
4. Fehlende Eingabevalidierung
   - Auswirkung: Ungültige Daten in der Datenbank
   - Korrektur: Validierungs-Middleware hinzufügen
   - Priorität: 3
```

### 2.3: Korrekturplan erstellen

**Eingabeaufforderung für Bob:**

```
Erstelle basierend auf der Sicherheitsanalyse einen detaillierten Plan zur Behebung dieser Probleme.
Füge hinzu:
1. Reihenfolge der Korrekturen (kritischste zuerst)
2. Dateien, die geändert werden müssen
3. Spezifische erforderliche Code-Änderungen
4. Teststrategie
```

**Bobs Antwort:**

Bob wird eine detaillierte TODO-Liste mit allen erforderlichen Korrekturen erstellen. Dies demonstriert Bobs Fähigkeit, komplexe Probleme in umsetzbare Schritte zu zerlegen.

**⚠️ Wichtig**: Überprüfen Sie die TODO-Liste, die Bob erstellt, aber **implementieren Sie die Korrekturen noch nicht**. Wir werden jeden Schwachstellentyp im nächsten Schritt detailliert untersuchen, bevor wir Änderungen vornehmen. Dies stellt sicher, dass Sie verstehen, was Sie korrigieren und warum.

**💡 Wichtige Erkenntnis**: Der Plan-Modus zeichnet sich durch Analyse, Planung und die Erstellung strukturierter Ansätze für Probleme aus. Die TODO-Liste dient als Ihr Fahrplan für die Implementierungsphase.

---

## Schritt 3: Tiefgehende Analyse der Sicherheitslücken (15 Minuten) - Optional

Dieser Schritt bietet eine detaillierte Erklärung jedes Schwachstellentyps. Wenn Sie bereits mit diesen Sicherheitskonzepten vertraut sind, können Sie zu [Schritt 4: Implementierung von Korrekturen](#schritt-4-implementierung-von-korrekturen-mit-code-modus-10-minuten) springen.

**Was Sie in dieser Tiefenanalyse lernen werden:**
- Wie SQL-Injection-Angriffe funktionieren
- Wie XSS-Schwachstellen ausgenutzt werden können
- Warum hartcodierte Geheimnisse gefährlich sind
- Best Practices für sichere Codierung

Lassen Sie uns jeden Schwachstellentyp im Detail untersuchen.

### 3.1: SQL-Injection-Schwachstelle

**Ort**: `vulnerable-app/backend/app.py`

**Anfälliger Code:**
```python
@app.route('/api/todos/search', methods=['GET'])
def search_todos():
    query = request.args.get('q')
    # ANFÄLLIG: Direkte String-Formatierung in SQL
    sql = f"SELECT * FROM todos WHERE title LIKE '%{query}%'"
    results = db.session.execute(sql)
    return jsonify([dict(row) for row in results])
```

**Das Problem:**

Ein Angreifer könnte eine bösartige Abfrage wie diese senden:
```
?q='; DROP TABLE todos; --
```

Dies würde zu folgendem führen:
```sql
SELECT * FROM todos WHERE title LIKE '%'; DROP TABLE todos; --%'
```

**Eingabeaufforderung für Bob (Ask-Modus):**

```
Erkläre, wie die SQL-Injection-Schwachstelle in search_todos() funktioniert.
Gib ein Beispiel für eine bösartige Abfrage und welchen Schaden sie anrichten könnte.
```

**Die Korrektur:**

Verwenden Sie parametrisierte Abfragen:
```python
@app.route('/api/todos/search', methods=['GET'])
def search_todos():
    query = request.args.get('q')
    # SICHER: Parametrisierte Abfrage
    results = Todo.query.filter(Todo.title.like(f'%{query}%')).all()
    return jsonify([todo.to_dict() for todo in results])
```

### 3.2: Cross-Site Scripting (XSS)-Schwachstelle

**Ort**: `vulnerable-app/frontend/app.js`

**Anfälliger Code:**
```javascript
function displayTodo(todo) {
    const todoElement = document.createElement('div');
    // ANFÄLLIG: innerHTML mit Benutzerinhalten
    todoElement.innerHTML = `
        <h3>${todo.title}</h3>
        <p>${todo.description}</p>
    `;
    document.getElementById('todo-list').appendChild(todoElement);
}
```

**Das Problem:**

Ein Angreifer könnte ein Todo mit folgendem Titel erstellen:
```html
<img src=x onerror="alert('XSS-Angriff!')">
```

Dieses Skript würde ausgeführt, wenn das Todo angezeigt wird.

**Eingabeaufforderung für Bob (Ask-Modus):**

```
Erkläre die XSS-Schwachstelle in der displayTodo()-Funktion.
Zeige mir ein Beispiel für eine bösartige Payload und wie sie ausgeführt würde.
```

**Die Korrektur:**

Verwenden Sie `textContent` statt `innerHTML`:
```javascript
function displayTodo(todo) {
    const todoElement = document.createElement('div');
    const title = document.createElement('h3');
    const description = document.createElement('p');
    
    // SICHER: textContent verhindert Script-Ausführung
    title.textContent = todo.title;
    description.textContent = todo.description;
    
    todoElement.appendChild(title);
    todoElement.appendChild(description);
    document.getElementById('todo-list').appendChild(todoElement);
}
```

### 3.3: Hartcodierte Geheimnisse-Schwachstelle

**Ort**: `vulnerable-app/backend/config.py`

**Anfälliger Code:**
```python
# ANFÄLLIG: Hartcodierte Anmeldedaten
DATABASE_URL = "postgresql://admin:SuperSecret123@localhost/todos"
API_KEY = "sk_live_abc123xyz789"
SECRET_KEY = "my-secret-key-12345"
```

**Das Problem:**

- Anmeldedaten sind im Quellcode sichtbar
- Jeder mit Code-Zugriff hat vollen Systemzugriff
- Anmeldedaten können nicht ohne Code-Änderungen geändert werden
- Verschiedene Umgebungen verwenden dieselben Anmeldedaten

**Eingabeaufforderung für Bob (Ask-Modus):**

```
Warum sind hartcodierte Geheimnisse ein Sicherheitsrisiko?
Was sind die Best Practices für die Verwaltung von Geheimnissen in Anwendungen?
```

**Die Korrektur:**

Verwenden Sie Umgebungsvariablen:
```python
import os
from dotenv import load_dotenv

load_dotenv()

# SICHER: Aus Umgebung laden
DATABASE_URL = os.getenv('DATABASE_URL')
API_KEY = os.getenv('API_KEY')
SECRET_KEY = os.getenv('SECRET_KEY')

# Validieren, dass Geheimnisse geladen wurden
if not all([DATABASE_URL, API_KEY, SECRET_KEY]):
    raise ValueError("Fehlende erforderliche Umgebungsvariablen")
```

Erstellen Sie eine `.env`-Datei (niemals committen!):
```
DATABASE_URL=postgresql://admin:SuperSecret123@localhost/todos
API_KEY=sk_live_abc123xyz789
SECRET_KEY=my-secret-key-12345
```

### 3.4: Schwachstellen testen

**⚠️ WARNUNG**: Testen Sie nur auf Ihren eigenen Systemen!

**SQL-Injection testen:**
```bash
# Versuchen Sie, SQL zu injizieren
curl "http://localhost:5000/api/todos/search?q=test'%20OR%20'1'='1"
```

**XSS testen:**
```bash
# Todo mit Skript erstellen
curl -X POST http://localhost:5000/api/todos \
  -H "Content-Type: application/json" \
  -d '{"title":"<script>alert(\"XSS\")</script>","description":"test"}'
```

---

## Schritt 4: Implementierung von Korrekturen mit Code-Modus (10 Minuten)

Jetzt beheben wir alle Schwachstellen mit Bobs Code-Modus.

### 4.1: In den Code-Modus wechseln

Wechseln Sie zu **Code-Modus** (💻).

### 4.2: SQL-Injection beheben

**Eingabeaufforderung für Bob:**

```
Behebe die SQL-Injection-Schwachstelle in vulnerable-app/backend/app.py.
Ersetze die String-Formatierung durch parametrisierte Abfragen mit SQLAlchemy.
```

Bob sollte die Funktion `search_todos()` ändern, um sichere Abfragen zu verwenden.

### 4.3: XSS-Schwachstelle beheben

**Eingabeaufforderung für Bob:**

```
Behebe die XSS-Schwachstelle in vulnerable-app/frontend/app.js.
Ersetze die innerHTML-Verwendung durch sichere DOM-Manipulation mit textContent.
Aktualisiere alle Funktionen, die benutzergenerierte Inhalte anzeigen.
```

### 4.4: Hartcodierte Geheimnisse beheben

**Eingabeaufforderung für Bob:**

```
Behebe die hartcodierten Geheimnisse in vulnerable-app/backend/config.py.
1. Verschiebe Geheimnisse in Umgebungsvariablen
2. Erstelle eine .env.example-Datei mit Platzhalterwerten
3. Füge python-dotenv zu requirements.txt hinzu
4. Aktualisiere den Code, um aus der Umgebung zu laden
```

### 4.5: Eingabevalidierung hinzufügen

**Eingabeaufforderung für Bob:**

```
Füge Eingabevalidierung zum Todo-Erstellungs-Endpunkt hinzu.
Validiere:
- Titel ist erforderlich und nicht leer
- Titellänge liegt zwischen 1 und 200 Zeichen
- Beschreibungslänge ist weniger als 1000 Zeichen
Gib angemessene Fehlermeldungen für ungültige Eingaben zurück.
```

### 4.6: Korrekturen verifizieren

**Wichtig**: Bob hat die Korrekturen direkt an den Dateien in `lab2/vulnerable-app/` vorgenommen (nicht in einem separaten Lösungsordner). Der anfällige Code wurde durch sicheren Code ersetzt.

Führen Sie die Anwendung aus und testen Sie die Korrekturen:

```bash
# Backend starten (aus dem vulnerable-app-Verzeichnis, wo Korrekturen angewendet wurden)
cd lab2/vulnerable-app/backend
python -m venv venv
source venv/bin/activate  # oder venv\Scripts\activate unter Windows
pip install -r requirements.txt
python app.py # kann mit AirPlay auf dem Mac in Konflikt geraten, führen Sie in diesem Fall stattdessen Folgendes aus:
FLASK_RUN_PORT=8080 flask run

# Frontend öffnen (aus dem vulnerable-app-Verzeichnis)
cd ../frontend
# index.html im Browser öffnen
```

**Sicherheit testen:**
1. SQL-Injection versuchen - sollte sicher fehlschlagen (keine Daten durchgesickert)
2. XSS-Payload versuchen - sollte als Klartext angezeigt werden (nicht ausführen)
3. Überprüfen Sie, dass keine Geheimnisse im Code sind (verifizieren Sie, dass config.py Umgebungsvariablen verwendet)
4. Eingabevalidierung testen (versuchen Sie leeren Titel, zu langen Titel usw.)

**Vorher/Nachher vergleichen:**
Wenn Sie den ursprünglichen anfälligen Code sehen möchten, überprüfen Sie das Verzeichnis `lab2/solution/`, das Referenzimplementierungen der Korrekturen enthält.

---

## Herzlichen Glückwunsch! 🎉

Sie haben Lab 2 erfolgreich abgeschlossen! Sie haben gelernt:

- ✅ Ask-Modus zu verwenden, um bestehenden Code zu verstehen
- ✅ Architect-Modus für Sicherheitsanalysen zu verwenden
- ✅ SQL-Injection-Schwachstellen zu identifizieren
- ✅ XSS-Angriffsvektoren zu erkennen
- ✅ Hartcodierte Geheimnisse zu finden und zu beheben
- ✅ Sichere Codierungspraktiken zu implementieren
- ✅ Code-Modus zu verwenden, um Sicherheitsprobleme zu beheben

> **🎯 Bob Findings in Aktion**
> In diesem Lab haben Sie Bobs [automatisierte Sicherheitsanalysefähigkeiten](../bob-differentiators.md#security-vulnerability-detection) erlebt. Bob Findings überwacht Ihren Code kontinuierlich auf Schwachstellen und bietet umsetzbare Sanierungsanleitungen. Dieser proaktive Ansatz hilft Ihnen, Sicherheitsprobleme zu erkennen, bevor sie in die Produktion gelangen, wodurch Risiken und technische Schulden reduziert werden.

## Gelernte Sicherheits-Best-Practices

### 1. SQL-Injection-Prävention
- ✅ Immer parametrisierte Abfragen verwenden
- ✅ Niemals Benutzereingaben in SQL verketten
- ✅ ORM-Funktionen verwenden (wie SQLAlchemy)
- ✅ Eingaben validieren und bereinigen

### 2. XSS-Prävention
- ✅ `textContent` statt `innerHTML` verwenden
- ✅ Benutzereingaben vor der Anzeige bereinigen
- ✅ Content Security Policy-Header verwenden
- ✅ Ausgabe ordnungsgemäß codieren

### 3. Geheimnisse-Verwaltung
- ✅ Niemals Anmeldedaten hartcodieren
- ✅ Umgebungsvariablen verwenden
- ✅ Geheimnisse-Verwaltungsdienste verwenden
- ✅ Geheimnisse regelmäßig rotieren
- ✅ Niemals Geheimnisse in die Versionskontrolle committen

### 4. Eingabevalidierung
- ✅ Alle Benutzereingaben validieren
- ✅ Whitelist-Validierung verwenden
- ✅ Angemessene Längenbeschränkungen festlegen
- ✅ Klare Fehlermeldungen zurückgeben

## Vergleich: Vorher und Nachher

### Vorher (Anfällig)
```python
# SQL-Injection-Risiko
sql = f"SELECT * FROM todos WHERE title LIKE '%{query}%'"

# Hartcodierte Geheimnisse
DATABASE_URL = "postgresql://admin:password@localhost/db"

# XSS-Risiko
element.innerHTML = `<h3>${userInput}</h3>`
```

### Nachher (Sicher)
```python
# Sichere parametrisierte Abfrage
results = Todo.query.filter(Todo.title.like(f'%{query}%')).all()

# Umgebungsvariablen
DATABASE_URL = os.getenv('DATABASE_URL')

# Sichere DOM-Manipulation
element.textContent = userInput
```

## Zusätzliche Sicherheitsressourcen

### OWASP Top 10
1. Injection
2. Broken Authentication
3. Sensitive Data Exposure
4. XML External Entities (XXE)
5. Broken Access Control
6. Security Misconfiguration
7. Cross-Site Scripting (XSS)
8. Insecure Deserialization
9. Using Components with Known Vulnerabilities
10. Insufficient Logging & Monitoring

### Empfohlene Lektüre
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)
- [Flask Security Best Practices](https://flask.palletsprojects.com/en/latest/security/)
- [JavaScript Security Best Practices](https://developer.mozilla.org/de/docs/Web/Security)

## Nächste Schritte

### Weiterlernen
- **[Lab 3: Code-Übersetzung →](../lab3/README.md)** - Lernen Sie, Code zwischen Sprachen zu übersetzen

### Mehr üben
Versuchen Sie, diese zusätzlichen Schwachstellen zu finden und zu beheben:
1. **CSRF** - CSRF-Schutz hinzufügen
2. **Authentifizierung** - Benutzerauthentifizierung implementieren
3. **Autorisierung** - Rollenbasierte Zugriffskontrolle hinzufügen
4. **Rate Limiting** - Brute-Force-Angriffe verhindern
5. **HTTPS** - Sichere Verbindungen erzwingen

## Fehlerbehebung

### Backend-Probleme

**Problem**: Import-Fehler nach Behebung von Geheimnissen
```bash
# python-dotenv installieren
pip install python-dotenv
```

**Problem**: Umgebungsvariablen werden nicht geladen
```bash
# Überprüfen Sie, ob .env-Datei existiert
ls -la .env

# .env-Format überprüfen (keine Leerzeichen um =)
DATABASE_URL=wert
```

### Frontend-Probleme

**Problem**: XSS funktioniert nach Korrektur immer noch
- Überprüfen Sie, dass Sie `textContent` und nicht `innerHTML` verwenden
- Überprüfen Sie alle Benutzereingabe-Anzeigepunkte
- Browser-Cache leeren

### Test-Probleme

**Problem**: SQL-Injection kann nicht getestet werden
- Stellen Sie sicher, dass Sie zuerst die anfällige Version testen
- Überprüfen Sie, ob das Backend läuft
- Überprüfen Sie, ob die Endpunkt-URL korrekt ist

## Feedback

Wie war dieses Lab? Wir würden gerne hören:
- Haben Sie alle Schwachstellen gefunden?
- Waren die Erklärungen klar?
- Welche anderen Sicherheitsthemen interessieren Sie?

---

**Bereit für die nächste Herausforderung?** → [Lab 3 starten: Code-Übersetzung](../lab3/README.md)

*Zuletzt aktualisiert: Dezember 2025*