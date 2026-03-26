# Lab 1: Eine Todo-Anwendung mit Bob erstellen

## Überblick

In diesem Lab lernen Sie, wie Sie Bobs KI-gestützte Funktionen nutzen, um eine vollständige Full-Stack-Todo-Anwendung von Grund auf zu erstellen. Sie werden Bobs verschiedene Modi, Auto-Genehmigungen und literarisches Programmieren kennenlernen.

**Dauer**: 45 Minuten
**Schwierigkeitsgrad**: Anfänger bis Fortgeschrittene

## Was Sie erstellen werden

Eine Full-Stack-Todo-Anwendung mit:
- **Backend**: Python Flask REST API mit SQLite-Datenbank
- **Frontend**: Moderne JavaScript Single-Page-Anwendung
- **Funktionen**: Erstellen, Lesen, Aktualisieren und Löschen von Todos

## Lernziele

Am Ende dieses Labs werden Sie:
- ✅ Bobs drei Modi verstehen (Architect, Code, Ask)
- ✅ Auto-Approvals für schnelle Entwicklung nutzen
- ✅ Literate Coding Techniken anwenden
- ✅ Eine vollständige Full-Stack-Anwendung erstellen

## Voraussetzungen

Stellen Sie vor dem Start sicher, dass Sie Folgendes haben:
- [ ] Python 3.8+ installiert
- [ ] Node.js 14+ installiert (für npm)
- [ ] Git installiert und konfiguriert
- [ ] Bob installiert und läuft
- [ ] Texteditor oder IDE geöffnet

Falls Sie die Einrichtung noch nicht abgeschlossen haben, siehe [prerequisites.md](../prerequisites.md).

## Lab-Struktur

```
Lab 1 Zeitplan (40 Minuten)
├── Schritt 1: Einführung & Planung (5 Min.)
├── Schritt 2: Backend-Entwicklung (15 Min.)
├── Schritt 3: Frontend-Entwicklung (15 Min.)
└── Schritt 4: Testen & Verifizierung (5 Min.)
```

---

## Schritt 1: Einführung in Bob-Modi (5 Minuten)

### Bobs Modi verstehen

Bob hat drei verschiedene Modi, die jeweils für unterschiedliche Aufgaben optimiert sind:

> **🎯 Bob-Differenzierungsmerkmal: [Anpassbare Modi](../bob-differentiators.md#1--extensible-architecture)**
> Bobs Modussystem ist eines seiner Hauptunterscheidungsmerkmale. Im Gegensatz zu anderen KI-Assistenten ermöglicht Bob die Erstellung benutzerdefinierter Modi, die auf die spezifischen Workflows Ihres Teams zugeschnitten sind. Die drei integrierten Modi, die Sie in diesem Lab verwenden werden, sind nur der Anfang – Sie können spezialisierte Modi für Code-Review, Dokumentation, Architekturdesign und mehr erstellen. Mehr dazu in [Lab 6](../lab6/README.md).

#### 🎯 Plan-Modus
**Wann zu verwenden**: Planung, Design, Strategieentwicklung
- Projektstrukturen erstellen
- API-Endpunkte entwerfen
- Datenbankschemata planen
- Architekturentscheidungen treffen

#### 💻 Code-Modus
**Wann zu verwenden**: Code schreiben, ändern, refaktorieren
- Funktionen implementieren
- Dateien erstellen
- Bestehenden Code ändern
- Fehler beheben

#### ❓ Ask-Modus
**Wann zu verwenden**: Lernen, verstehen, Hilfe erhalten
- Code-Konzepte erklären
- Dokumentation abrufen
- Fehler verstehen
- Best Practices lernen

### Zwischen Modi wechseln

In Bobs Benutzeroberfläche:
1. Suchen Sie nach dem Modus-Selektor (normalerweise oben)
2. Klicken Sie, um verfügbare Modi anzuzeigen
3. Wählen Sie den benötigten Modus aus
4. Bob passt sein Verhalten entsprechend an

### Ihre erste Aufgabe: Projektplanung

**Wechseln Sie in den Plan-Modus** und fragen Sie Bob:

```
Ich möchte eine Todo-Anwendung mit einem Python Flask-Backend und JavaScript-Frontend erstellen.
Bitte helfen Sie mir bei der Planung:
1. Projektverzeichnisstruktur
2. Benötigte API-Endpunkte
3. Datenbankschema
4. Empfehlungen für den Technologie-Stack
```

**Bobs interaktiver Ansatz:**

Bevor Bob einen Plan bereitstellt, wird er klärende Fragen stellen, um Ihre Anforderungen besser zu verstehen. Dies ist ein wichtiges Unterscheidungsmerkmal – Bob lässt Sie den Prozess steuern und macht dabei hilfreiche Vorschläge.

Bob könnte fragen:
- "Wie komplex soll die Anwendung sein?"
- "Welche Datenbank bevorzugen Sie (SQLite, PostgreSQL, MySQL)?"
- "Benötigen Sie Benutzerauthentifizierung?"
- "Sollen wir zusätzliche Funktionen wie Kategorien oder Prioritäten einbeziehen?"

**Für dieses Lab antworten Sie mit grundlegenden Anforderungen:**
- Einfache/grundlegende Komplexität
- SQLite-Datenbank (keine Installation erforderlich)
- Keine Benutzerauthentifizierung
- Nur grundlegende CRUD-Operationen

Dieser kollaborative Ansatz stellt sicher, dass Bob genau das erstellt, was Sie benötigen, nicht was er annimmt, dass Sie wollen.

**Erwartete Antwort von Bob:**

Nach Ihren Klarstellungen sollte Bob Folgendes bereitstellen:
- Verzeichnisstruktur mit backend/- und frontend/-Ordnern
- REST-API-Endpunkte (GET, POST, PUT, DELETE)
- Datenbankschema für Todos (id, title, description, completed, created_at)
- Empfehlungen für Flask, SQLite, CORS usw.

**💡 Tipp**: Machen Sie sich Notizen zu Bobs Empfehlungen. Sie werden diesen Plan in den nächsten Schritten verwenden.

---

## Schritt 2: Backend-Entwicklung mit Code-Modus (15 Minuten)

Jetzt erstellen wir das Flask-Backend mit Bobs Code-Modus.

### 2.1: In den Code-Modus wechseln

Wechseln Sie von Architect zu Code-Modus in Bobs Benutzeroberfläche.

### 2.2: Backend-Struktur erstellen

**Eingabeaufforderung für Bob:**

```
Erstelle ein Flask-Backend für die Todo-App mit folgenden Dateien:
1. app.py - Haupt-Flask-Anwendung mit aktiviertem CORS
2. models.py - SQLAlchemy Todo-Modell
3. database.py - Datenbankinitialisierung
4. requirements.txt - Python-Abhängigkeiten

Das Todo-Modell sollte haben: id, title, description, completed (boolean), created_at (timestamp)
```

**Was Bob erstellen wird:**

Bob sollte diese Dateien im `backend/`-Verzeichnis generieren. Überprüfen Sie jede Datei, während Bob sie erstellt.

### 2.3: Auto-Genehmigungen verstehen

**Auto-Genehmigungen** ermöglichen es Bob, mehrere Änderungen vorzunehmen, ohne jedes Mal um Bestätigung zu bitten.

Um Auto-Genehmigungen zu aktivieren:
1. Suchen Sie nach Auto-Genehmigungs-Einstellungen in Bob
2. Für diese Sitzung aktivieren
3. Bob wird nun mehrere Dateien schnell erstellen

**⚠️ Wichtig**: Überprüfen Sie die Dateien, nachdem Bob sie erstellt hat, um sicherzustellen, dass sie Ihren Anforderungen entsprechen.

### 2.4: REST-API-Endpunkte implementieren

**Eingabeaufforderung für Bob:**

```
Implementiere die folgenden REST-API-Endpunkte in app.py:
- GET /api/todos - Alle Todos auflisten
- POST /api/todos - Ein neues Todo erstellen
- PUT /api/todos/<id> - Ein Todo aktualisieren
- DELETE /api/todos/<id> - Ein Todo löschen

Füge ordnungsgemäße Fehlerbehandlung und JSON-Antworten hinzu.
```

### 2.5: Generierten Code überprüfen

Bob sollte etwas Ähnliches wie diese Struktur erstellt haben:

**app.py** (Hauptabschnitte):
```python
from flask import Flask, request, jsonify
from flask_cors import CORS
from models import Todo
from database import db, init_db

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///todos.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
CORS(app)

init_db(app)

@app.route('/api/todos', methods=['GET'])
def get_todos():
    todos = Todo.query.all()
    return jsonify([todo.to_dict() for todo in todos])

@app.route('/api/todos', methods=['POST'])
def create_todo():
    data = request.get_json()
    todo = Todo(
        title=data.get('title'),
        description=data.get('description', ''),
        completed=False
    )
    db.session.add(todo)
    db.session.commit()
    return jsonify(todo.to_dict()), 201

# Weitere Endpunkte...
```

### 2.6: Unit-Testfälle erstellen und ausführen

**Eingabeaufforderung für Bob:**

```bash
Erstelle Unit-Testfälle für jeden der API-Endpunkte und stelle mindestens 90% Code-Abdeckung sicher.
```

### 2.7: Backend-Setup testen

**Wichtig:** Verwenden Sie immer eine virtuelle Umgebung, um Projektabhängigkeiten zu isolieren.

Erstellen Sie eine virtuelle Umgebung und installieren Sie Abhängigkeiten:

```bash
# Zum Backend-Verzeichnis navigieren
cd backend

# Virtuelle Umgebung erstellen
python3 -m venv venv

# Virtuelle Umgebung aktivieren
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Abhängigkeiten installieren
pip install -r requirements.txt

# Anwendung ausführen
python app.py
```

**Warum eine virtuelle Umgebung verwenden?**
- Isoliert Projektabhängigkeiten von System-Python-Paketen
- Verhindert Versionskonflikte zwischen verschiedenen Projekten
- Erleichtert die Reproduktion der exakten Umgebung auf anderen Maschinen
- Hält Ihre System-Python-Installation sauber

**Hinweis:** Denken Sie daran, die virtuelle Umgebung jedes Mal zu aktivieren, wenn Sie am Projekt arbeiten. Sie wissen, dass sie aktiviert ist, wenn Sie `(venv)` in Ihrer Terminal-Eingabeaufforderung sehen.

Alternativ können Sie Bob bitten, das für Sie zu tun.

**Eingabeaufforderung für Bob:**

```bash
Führe die Backend-Anwendung aus und teste sie mit 1 Beispiel-Curl-Befehl pro API-Endpunkt.
```

Der Server sollte auf `http://localhost:5000` starten

**✅ Checkpoint**: Backend läuft ohne Fehler.

---

## Schritt 3: Frontend-Entwicklung (15 Minuten)

Jetzt erstellen wir die Benutzeroberfläche mit JavaScript.

### 3.1: Frontend-Struktur erstellen

**Eingabeaufforderung für Bob (noch im Code-Modus):**

```
Erstelle ein Frontend für die Todo-App mit:
1. index.html - Haupt-HTML-Struktur mit sauberem, modernem Design
2. styles.css - Responsive CSS-Styling
3. app.js - JavaScript für API-Interaktionen

Füge hinzu:
- Eingabefeld für neue Todos
- Liste zur Anzeige von Todos
- Schaltflächen für Abschließen- und Löschen-Aktionen
- Responsives Design für Mobilgeräte und Desktop
```

### 3.2: Literate Coding verstehen

**Literate Coding** bedeutet, Code zu schreiben, der sich durch Kommentare und klare Struktur selbst erklärt.

**Eingabeaufforderung für Bob:**

```
Verwende in app.js Literate Coding, um zu erklären:
- Wie die API-Aufrufe funktionieren
- Warum wir async/await verwenden
- Wie die Fehlerbehandlung implementiert ist
- Den Zweck jeder Funktion

Füge detaillierte Kommentare hinzu, die einem Anfänger helfen würden, den Code zu verstehen.
```

### 3.3: Frontend-Code überprüfen

Bob sollte Dateien ähnlich wie diese erstellen:

**app.js** (mit Literate Coding):
```javascript
/**
 * Todo-Anwendung - Frontend JavaScript
 * 
 * Diese Datei behandelt alle Interaktionen zwischen der Benutzeroberfläche
 * und der Flask-Backend-API. Wir verwenden moderne JavaScript-Funktionen
 * wie async/await für saubereren asynchronen Code.
 */

// API-Basis-URL - zeigt auf unser Flask-Backend
const API_URL = 'http://localhost:5000/api/todos';

/**
 * Ruft alle Todos von der Backend-API ab
 * 
 * Diese Funktion demonstriert das async/await-Muster:
 * - 'async'-Schlüsselwort ermöglicht die Verwendung von 'await' innerhalb
 * - 'await' pausiert die Ausführung, bis das Promise aufgelöst ist
 * - Dies lässt asynchronen Code synchron aussehen und ist leichter zu lesen
 * 
 * @returns {Promise<void>}
 */
async function fetchTodos() {
    try {
        // GET-Anfrage an Backend senden
        const response = await fetch(API_URL);
        
        // JSON-Antwort parsen
        const todos = await response.json();
        
        // UI mit abgerufenen Todos aktualisieren
        displayTodos(todos);
    } catch (error) {
        // Fehler behandeln (Netzwerkprobleme, Serverfehler usw.)
        console.error('Fehler beim Abrufen von Todos:', error);
        showError('Todos konnten nicht geladen werden. Bitte versuchen Sie es erneut.');
    }
}

/**
 * Erstellt ein neues Todo-Element
 * 
 * Diese Funktion zeigt, wie man eine POST-Anfrage mit JSON-Daten sendet.
 * Wir verwenden die Fetch-API, die Promises zurückgibt, was sie perfekt
 * für async/await-Syntax macht.
 * 
 * @param {string} title - Der Todo-Titel
 * @param {string} description - Die Todo-Beschreibung
 */
async function createTodo(title, description) {
    try {
        const response = await fetch(API_URL, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({ title, description })
        });
        
        if (response.ok) {
            // Todo-Liste aktualisieren
            await fetchTodos();
            // Eingabeformular leeren
            clearForm();
        }
    } catch (error) {
        console.error('Fehler beim Erstellen von Todo:', error);
        showError('Todo konnte nicht erstellt werden. Bitte versuchen Sie es erneut.');
    }
}

// Weitere Funktionen mit detaillierten Erklärungen...
```

### 3.4: Frontend testen

Öffnen Sie `frontend/index.html` in Ihrem Browser:

```bash
# Vom lab1-Verzeichnis aus
cd frontend

# Im Standard-Browser öffnen
# Windows:
start index.html
# macOS:
open index.html
# Linux:
xdg-open index.html
```

**✅ Checkpoint**: Frontend lädt und zeigt die UI an.

---

## Schritt 4: Testen & Verifizierung (5 Minuten)

Lassen Sie uns die vollständige Anwendung End-to-End testen.

### 4.1: Backend starten

```bash
# Zum Backend-Verzeichnis navigieren
cd backend

# Virtuelle Umgebung aktivieren (falls noch nicht aktiviert)
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Anwendung ausführen
python app.py
```

Server sollte auf `http://localhost:5000` laufen

**💡 Tipp:** Sie wissen, dass die virtuelle Umgebung aktiviert ist, wenn Sie `(venv)` am Anfang Ihrer Terminal-Eingabeaufforderung sehen.

### 4.2: Frontend öffnen

Öffnen Sie `frontend/index.html` in Ihrem Browser.

### 4.3: CRUD-Operationen testen

**Ein Todo erstellen:**
1. Geben Sie einen Titel ein: "Bob lernen"
2. Geben Sie eine Beschreibung ein: "Alle drei Labs abschließen"
3. Klicken Sie auf "Add Todo"
4. ✅ Todo erscheint in der Liste

**Als abgeschlossen markieren:**
1. Klicken Sie auf die Schaltfläche "Complete" bei einem Todo
2. ✅ Todo wird als abgeschlossen angezeigt (durchgestrichen oder mit Häkchen)

**Ein Todo löschen:**
1. Klicken Sie auf die Schaltfläche "Delete" bei einem Todo
2. ✅ Todo wird aus der Liste entfernt

**Seite aktualisieren:**
1. Browser aktualisieren
2. ✅ Todos bleiben erhalten (in Datenbank gespeichert)

### 4.4: Browser-Konsole überprüfen

Öffnen Sie die Browser-Entwicklertools (F12):
- ✅ Keine JavaScript-Fehler
- ✅ API-Aufrufe erfolgreich (200-Statuscodes)
- ✅ Daten sind ordnungsgemäß formatiert

### 4.5: Datenbank verifizieren

```bash
# Im Backend-Verzeichnis
python
>>> from app import app, db
>>> from models import Todo
>>> with app.app_context():
...     todos = Todo.query.all()
...     for todo in todos:
...         print(f"{todo.id}: {todo.title}")
```

✅ Todos sind in der Datenbank gespeichert

---

## Herzlichen Glückwunsch! 🎉

Sie haben Lab 1 erfolgreich abgeschlossen! Sie haben gelernt:

- ✅ Bobs Architect-Modus für die Planung zu verwenden
- ✅ Bobs Code-Modus für die Implementierung zu verwenden
- ✅ Auto-Genehmigungen zu aktivieren und zu verwenden
- ✅ Prinzipien des literarischen Programmierens anzuwenden
- ✅ Eine vollständige Full-Stack-Anwendung zu erstellen

## Was Sie erstellt haben

```
bob-todo-app/
├── backend/
│   ├── app.py              # Flask REST API
│   ├── models.py           # Datenbankmodelle
│   ├── database.py         # DB-Initialisierung
│   ├── requirements.txt    # Abhängigkeiten
│   └── todos.db           # SQLite-Datenbank
├── frontend/
│   ├── index.html         # UI-Struktur
│   ├── styles.css         # Styling
│   └── app.js             # Frontend-Logik
└── .gitignore             # Git-Ignore-Regeln
```

## Wichtige Erkenntnisse

### Bobs Modi
- **Architect**: Perfekt für Planung und Designentscheidungen
- **Code**: Am besten für Implementierung und Dateierstellung
- **Ask**: Großartig zum Lernen und Verstehen
- **Benutzerdefinierte Modi**: Erstellen Sie Ihre eigenen spezialisierten Modi ([Mehr erfahren](../bob-differentiators.md#customizable-modes))

### Auto-Approvals
- Beschleunigt die Entwicklung erheblich
- Nützlich zum Erstellen mehrerer zusammenhängender Dateien
- Überprüfen Sie immer den generierten Code

### Literate Coding
- Macht Code selbstdokumentierend
- Hilft Teammitgliedern, Ihren Code zu verstehen
- Nützlich zum Lernen und Lehren


> **💡 Hinter den Kulissen: Intelligente Ressourcenoptimierung**
> Während Sie diese App erstellt haben, hat Bob automatisch das richtige KI-Modell für jede Aufgabe ausgewählt – leistungsstarke Modelle für komplexe Architekturentscheidungen und leichtere Modelle für einfache Dateioperationen. Diese [automatische Modellauswahl](../bob-differentiators.md#automatic-model-selection) optimiert sowohl Qualität als auch Kosten, ohne dass Sie darüber nachdenken müssen. Sie können bis zu 60% der KI-Kosten einsparen und gleichzeitig hervorragende Ergebnisse erzielen!

## Nächste Schritte

### Ihre App verbessern
Probieren Sie diese Verbesserungen aus:
1. Todo-Kategorien oder Tags hinzufügen
2. Fälligkeitsdaten implementieren
3. Benutzerauthentifizierung hinzufügen
4. Ein Prioritätssystem erstellen
5. Such- und Filterfunktionalität hinzufügen

### Weiterlernen
- **[Lab 2: Sicherheitsanalyse →](../lab2/README.md)** - Lernen Sie, Sicherheitslücken zu identifizieren und zu beheben
- **[Lab 3: Code-Übersetzung →](../lab3/README.md)** - Code zwischen Sprachen übersetzen

## Fehlerbehebung

### Backend-Probleme

**Problem**: `ModuleNotFoundError: No module named 'flask'`
```bash
# Stellen Sie sicher, dass die virtuelle Umgebung aktiviert ist
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Abhängigkeiten installieren
pip install -r requirements.txt
```

**Problem**: `Address already in use`
```bash
# Prozess beenden, der Port 5000 verwendet
# Windows:
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# macOS/Linux:
lsof -ti:5000 | xargs kill -9
```

**Problem**: Datenbankfehler
```bash
# Datenbank löschen und neu erstellen
rm todos.db
python
>>> from app import app, db
>>> with app.app_context():
...     db.create_all()
```

### Frontend-Probleme

**Problem**: CORS-Fehler in der Browser-Konsole
- Stellen Sie sicher, dass Flask-CORS installiert ist: `pip install flask-cors`
- Überprüfen Sie, ob CORS in `app.py` aktiviert ist
- Überprüfen Sie, ob das Backend auf Port 5000 läuft

**Problem**: API-Aufrufe schlagen fehl
- Überprüfen Sie, ob das Backend läuft
- Überprüfen Sie, ob API_URL in `app.js` mit der Backend-URL übereinstimmt
- Öffnen Sie die Browser-Entwicklertools und überprüfen Sie die Registerkarte "Network"

**Problem**: Todos bleiben nicht erhalten
- Überprüfen Sie die Browser-Konsole auf Fehler
- Überprüfen Sie, ob die Datenbankdatei existiert
- Testen Sie API-Endpunkte direkt mit curl oder Postman

## Zusätzliche Ressourcen

- [Flask-Dokumentation](https://flask.palletsprojects.com/)
- [JavaScript Fetch API](https://developer.mozilla.org/de/docs/Web/API/Fetch_API)
- [SQLAlchemy-Dokumentation](https://docs.sqlalchemy.org/)
- [Bob-Dokumentation](https://ibm.biz/bob-doc)

## Glossar / Glossary

| Englischer Begriff | Deutscher Begriff | Erklärung |
|-------------------|-------------------|-----------|
| Todo | Aufgabe | Eine zu erledigende Aufgabe |
| Backend | Backend / Server-Seite | Serverseitige Anwendungslogik |
| Frontend | Frontend / Client-Seite | Benutzeroberfläche im Browser |
| API | API / Schnittstelle | Application Programming Interface |
| Endpoint | Endpunkt | URL, unter der die API erreichbar ist |
| CRUD | CRUD | Create, Read, Update, Delete (Erstellen, Lesen, Aktualisieren, Löschen) |
| Database | Datenbank | Strukturierte Datenspeicherung |
| Repository | Repository / Code-Ablage | Versionskontrollierte Code-Speicherung |
| Commit | Commit / Änderungssatz | Gespeicherter Satz von Code-Änderungen |
| Mode | Modus | Bobs Betriebsmodus (Plan/Code/Ask) |
| Virtual Environment | Virtuelle Umgebung | Isolierte Python-Umgebung für Projektabhängigkeiten |

## Feedback

Wie war dieses Lab? Wir würden gerne Ihre Gedanken hören:
- Was hat gut funktioniert?
- Was war verwirrend?
- Verbesserungsvorschläge?
- Welche zusätzlichen Themen möchten Sie behandelt sehen?

---

**Bereit für die nächste Herausforderung?** → [Lab 2 starten: Sicherheitsanalyse](../lab2/README.md)

**Zuletzt aktualisiert: Februar 2026**