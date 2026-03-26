# Lab 4: BobShell und Kommandozeilen-Nutzung

## Überblick

In diesem Lab lernen Sie, wie Sie Bobs Kommandozeilen-Schnittstelle (BobShell) verwenden, um Entwicklungsaufgaben zu automatisieren, Bob in CI/CD-Pipelines zu integrieren und leistungsstarke Automatisierungsskripte zu erstellen. BobShell ermöglicht es Ihnen, Bobs KI-Fähigkeiten in Skripten, Build-Prozessen und automatisierten Workflows zu nutzen.

> **🧠 Bob-Differenzierungsmerkmal: [Intelligente Ressourcenoptimierung](../bob-differentiators.md#2--intelligent-resource-optimization)**
> BobShell nutzt Bobs [automatische Modellauswahl](../bob-differentiators.md#automatic-model-selection), um jeden Befehl zu optimieren. Einfache Aufgaben wie Code-Formatierung verwenden leichtere Modelle für Geschwindigkeit, während komplexe Analysen Frontier-Klasse-Modelle für Genauigkeit verwenden. Dies geschieht automatisch im Hintergrund und reduziert die Kosten um bis zu 60%, während die Qualität erhalten bleibt.

**Dauer:** 45-60 Minuten
**Schwierigkeitsgrad:** Fortgeschrittene
**Voraussetzungen:** Abschluss der Labs 1-3, grundlegende Kommandozeilen-Kenntnisse

## Lernziele

Am Ende dieses Labs werden Sie in der Lage sein:

1. BobShell für interaktive und nicht-interaktive Befehlsausführung zu verwenden
2. Automatisierungsskripte zu erstellen, die Bobs KI-Fähigkeiten nutzen
3. Bob in CI/CD-Pipelines zu integrieren
4. Bob für Code-Generierung, Analyse und Refactoring über CLI zu verwenden
5. Automatisierte Code-Reviews und Qualitätsprüfungen zu implementieren
6. Benutzerdefinierte Workflows zu erstellen, die Bob mit anderen CLI-Tools kombinieren

## Was ist BobShell?

BobShell ist Bobs Kommandozeilen-Schnittstelle, die Folgendes bietet:

- **Interaktiver Modus**: Direkt mit Bob im Terminal chatten
- **Nicht-interaktiver Modus**: Einzelne Befehle für Automatisierung ausführen
- **Skript-Integration**: Bob in Shell-Skripten und Automatisierungs-Workflows verwenden
- **CI/CD-Integration**: Bob in Build- und Deployment-Pipelines einbinden
- **Batch-Verarbeitung**: Mehrere Dateien oder Aufgaben nacheinander verarbeiten

## Lab-Struktur

```
lab4/
├── README.md                 # Diese Datei
├── examples/                 # Beispielbefehle und Anwendungsfälle
│   ├── basic-commands.md     # Grundlegende BobShell-Befehle
│   ├── code-generation.md    # Code-Generierungsbeispiele
│   └── analysis-examples.md  # Code-Analysebeispiele
├── scripts/                  # Automatisierungsskripte
│   ├── code-review.sh        # Automatisiertes Code-Review-Skript
│   ├── refactor-batch.sh     # Batch-Refactoring-Skript
│   └── generate-docs.sh      # Dokumentationsgenerierungs-Skript
└── ci-cd/                    # CI/CD-Integrationsbeispiele
    ├── github-actions.yml    # GitHub Actions Workflow
    ├── gitlab-ci.yml         # GitLab CI Konfiguration
    └── jenkins-pipeline.txt  # Jenkins Pipeline Beispiel
```

## Teil 1: Erste Schritte mit BobShell

### Schritt 1.1: BobShell installieren und verifizieren

**⚠️ Wichtig für Windows-Benutzer:**

BobShell wird unter Windows nicht automatisch mit Bob installiert. Sie müssen es separat installieren, indem Sie der offiziellen Installationsanleitung folgen:

👉 **[BobShell-Installationsanleitung](https://internal.bob.ibm.com/docs/shell/install-and-setup)**

**📚 Hinweis:** Öffentliche Bob-Dokumentation ist verfügbar unter: **https://ibm.biz/bob-doc**

**Für alle Benutzer**, überprüfen Sie, dass BobShell installiert und zugänglich ist:

```bash
# BobShell-Version prüfen
bob --version

# Hilfeinformationen anzeigen
bob --help
```

**Erwartete Ausgabe:**
```
Bob CLI v1.x.x
Usage: bob [options] [command]
...
```

**Wenn Sie "command not found" oder einen ähnlichen Fehler sehen:**
- Windows-Benutzer: Folgen Sie der [Installationsanleitung](https://internal.bob.ibm.com/docs/shell/install-and-setup), um BobShell zu installieren
- macOS/Linux-Benutzer: Überprüfen Sie, ob Bob installiert ist und die Shell-Komponente aktiviert ist
- Überprüfen Sie, dass BobShell in Ihrem System-PATH ist

**Was passiert:**
- Das `--version`-Flag zeigt die installierte Version von BobShell an
- Das `--help`-Flag zeigt alle verfügbaren Befehle und Optionen
- Dies bestätigt, dass BobShell ordnungsgemäß installiert ist und in Ihrem PATH liegt

### Schritt 1.2: Interaktiver Modus

Starten Sie Bob im interaktiven Modus, um direkt vom Terminal aus zu chatten:

```bash
# Interaktive BobShell-Sitzung starten
bob
```

**Was passiert:**
- Einfaches Eingeben von `bob` startet eine interaktive BobShell-Sitzung
- Sie sehen eine Eingabeaufforderung, wo Sie direkt mit Bob chatten können
- Alle Fähigkeiten von Bob sind über natürlichsprachliche Befehle verfügbar

**Probieren Sie diese Befehle im interaktiven Modus aus:**

```
# Bob bitten, ein Konzept zu erklären
> Erkläre, was ein Closure in JavaScript ist

# Code-Generierung anfordern
> Erstelle eine Python-Funktion zur Berechnung von Fibonacci-Zahlen

# Um Code-Review bitten
> Überprüfe diesen Code: [Code hier einfügen]
```

Um den interaktiven Modus zu verlassen, drücken Sie zweimal `Ctrl+C`.

**📚 Mehr erfahren:** Siehe die [BobShell Interactive Mode Dokumentation](https://internal.bob.ibm.com/docs/shell/start-bobshell-interactive) für zusätzliche Funktionen und Optionen.

**Was passiert:**
- Der interaktive Modus bietet eine konversationelle Schnittstelle im Terminal
- Sie können Fragen stellen, Code anfordern und Erklärungen erhalten
- Perfekt für schnelle Abfragen ohne Öffnen der vollständigen IDE
- Sitzungsverlauf wird während der Konversation beibehalten

### Schritt 1.3: Nicht-interaktiver Modus

Führen Sie einzelne Befehle aus, ohne in den interaktiven Modus zu wechseln. Lassen Sie uns zuerst eine einfache Testdatei erstellen:

```bash
# Eine einfache Python-Datei zum Arbeiten erstellen
echo 'def add(a, b):
    return a + b

def multiply(x, y):
    return x * y' > calculator.py
```

Probieren Sie nun diese nicht-interaktiven Befehle aus:

```bash
# Code in einer Datei erklären
bob "Erkläre, was die Datei calculator.py macht"

# Um Code-Review bitten
bob "Überprüfe calculator.py und schlage Verbesserungen vor"

# Neuen Code generieren
bob "Erstelle eine Python-Funktion, die die Fakultät einer Zahl berechnet" --yolo --hide-intermediary-output > factorial.py

# Eine schnelle Frage stellen
bob "Was ist der Unterschied zwischen einer Liste und einem Tupel in Python?"
```

**Was passiert:**
- Der nicht-interaktive Modus führt einen einzelnen Befehl aus und beendet sich
- Verwenden Sie einfach `bob "Ihre Eingabeaufforderung"` für einmalige Befehle
- Für Befehle, die explizite Genehmigung zum Aufrufen bestimmter Tools bei Bob erfordern, müssen Sie das --yolo-Argument für die automatische Genehmigung hinzufügen
- Perfekt für Automatisierung und Skripting
- Ergebnisse werden an stdout ausgegeben für einfache Erfassung
- Kann mit anderen CLI-Tools über Pipes verkettet werden

### Schritt 1.4: Ausgabeumleitung verstehen

Bei Verwendung der Ausgabeumleitung (`>`) mit BobShell müssen Sie verstehen, wie Bob seine Ausgabe behandelt, um saubere Code-Dateien zu erhalten.

**⚠️ Wichtig: Verhalten der Ausgabeumleitung**

Standardmäßig wird bei Umleitung von Bobs Ausgabe in eine Datei **Bobs Denkprozess und Zwischenausgabe zusammen mit dem generierten Code in die Datei aufgenommen**. Um nur den Code zu erhalten:

**Option 1: Das `--hide-intermediary-output`-Flag verwenden**
```bash
# Code mit sauberer Ausgabe generieren
bob "Erstelle eine Python-Funktion, die die Fakultät einer Zahl berechnet" --yolo --hide-intermediary-output > factorial.py
```

**Option 2: Dateischreibanweisung in die Eingabeaufforderung aufnehmen**
```bash
# Bob bitten, direkt in die Datei zu schreiben
bob "Erstelle eine Python-Funktion, die die Fakultät einer Zahl berechnet und schreibe sie in factorial.py" --yolo
```

**Was ohne diese Ansätze enthalten ist:**
- Bobs Denkprozess
- Tool-Verwendungsnachrichten
- Status-Updates
- Der generierte Code

**Was Sie mit diesen Ansätzen erhalten:**
- Nur den sauberen, generierten Code
- Keine Zwischennachrichten
- Sofort verwendbare Dateien

**Beispielvergleich:**

```bash
# ❌ Dies enthält Bobs Denken in der Datei
bob "Erstelle eine Sortierfunktion" --yolo > sort.py

# ✅ Dies erstellt eine saubere Code-Datei
bob "Erstelle eine Sortierfunktion" --yolo --hide-intermediary-output > sort.py

# ✅ Dies erstellt auch eine saubere Code-Datei
bob "Erstelle eine Sortierfunktion und schreibe sie in sort.py" --yolo
```

**💡 Best Practice:** Verwenden Sie immer `--hide-intermediary-output` bei Umleitung in Dateien, oder bitten Sie Bob explizit, in die Datei zu schreiben.

### Schritt 1.5: Sitzungsfortsetzung verwenden

Bob speichert Ihre interaktiven Sitzungen automatisch, sodass Sie frühere Konversationen fortsetzen und dort weitermachen können, wo Sie aufgehört haben.

**Sitzungen fortsetzen:**

```bash
# Verfügbare Sitzungen auflisten
bob --list-sessions

# Die letzte Sitzung fortsetzen
bob --resume latest

# Eine bestimmte Sitzung nach Index fortsetzen
bob --resume 5
```

**Sitzungsfortsetzung in Ihrem Workflow verwenden:**

Bob speichert Ihren Konversationsverlauf automatisch, sodass Sie zu früherer Arbeit zurückkehren können:

```
# Neue Sitzung starten
bob

# An Ihrem Code arbeiten
> Überprüfe calculator.py und schlage Verbesserungen vor

# Bob gibt Vorschläge...

# Sitzung beenden (zweimal Ctrl+C)

# Später dieselbe Sitzung fortsetzen
bob --resume latest

# Von dort weitermachen, wo Sie aufgehört haben
> Lass uns diese Vorschläge jetzt implementieren
```

**Wie Sitzungsfortsetzung funktioniert:**

- Bob speichert alle interaktiven Sitzungen automatisch
- Jede Sitzung wird indiziert und kann mit `--list-sessions` aufgelistet werden
- Verwenden Sie `--resume latest`, um Ihre neueste Arbeit fortzusetzen
- Verwenden Sie `--resume <index>`, um zu einer bestimmten Sitzung zurückzukehren
- Sitzungsverlauf enthält den gesamten Konversationskontext

**Sitzungen verwalten:**

```bash
# Alle verfügbaren Sitzungen auflisten
bob --list-sessions

# Eine bestimmte Sitzung löschen
bob --delete-session 3

# Fortsetzen und weiterarbeiten
bob --resume latest
```

**Wann Sitzungsfortsetzung verwenden:**

1. **Arbeit fortsetzen:** Nach einer Pause dort weitermachen, wo Sie aufgehört haben
2. **Kontexterhaltung:** Konversationskontext über Sitzungen hinweg beibehalten
3. **Mehrere Projekte:** Zwischen verschiedenen Projektsitzungen wechseln
4. **Lernen und Experimentieren:** Zu früheren Erkundungen zurückkehren

**Beispiel-Workflow:**

```bash
# Mit einem Feature beginnen
bob
> Analysiere myapp.js auf Leistungsprobleme
# Bob identifiziert mehrere Probleme
> Schlage Optimierungen für die Datenbankabfragen vor
# Sitzung beenden

# Später fortsetzen
bob --resume latest
> Lass uns diese Datenbankoptimierungen jetzt implementieren
# Bob erinnert sich an die vorherige Analyse und fährt fort
```

**💡 Tipp:** Verwenden Sie `--resume latest`, wenn Sie Ihre neueste Arbeit fortsetzen möchten, oder `--list-sessions`, um alle verfügbaren Sitzungen zu sehen und eine bestimmte auszuwählen.

## Teil 2: Code-Generierung über CLI

### Schritt 2.1: Einzelne Dateien generieren

Verwenden Sie Bob, um vollständige Code-Dateien von der Kommandozeile aus mit natürlichsprachlichen Eingabeaufforderungen zu generieren:

```bash
# Eine Python-Klasse generieren (mit --hide-intermediary-output für saubere Ausgabe)
bob "Erstelle eine Python-Klasse zur Verwaltung eines Warenkorbs mit Methoden zum Hinzufügen, Entfernen und Berechnen der Gesamtsumme" --yolo --hide-intermediary-output > cart.py

# Eine React-Komponente generieren (Bob bitten, in Datei zu schreiben)
bob "Erstelle eine React-Komponente für eine Benutzerprofilkarte mit Avatar, Name und Bio und schreibe sie in UserProfile.jsx" --yolo

# Eine Testdatei generieren (mit --hide-intermediary-output)
bob "Erstelle Unit-Tests für die Datei cart.py mit pytest" --yolo --hide-intermediary-output > test_cart.py
```

**Was passiert:**
- Verwenden Sie natürliche Sprache, um zu beschreiben, welchen Code Sie möchten
- Verwenden Sie das `--hide-intermediary-output`-Flag mit `>`-Umleitung für saubere Code-Dateien
- Oder fügen Sie "schreibe es in [Dateiname]" in Ihre Eingabeaufforderung ein, damit Bob direkt schreibt
- Bob analysiert die Anfrage und generiert geeigneten, funktionierenden Code
- Seien Sie spezifisch über Sprache, Framework und Anforderungen in Ihrer Eingabeaufforderung

### Schritt 2.2: Mehrere verwandte Dateien generieren

Für komplexe Projekte mit mehreren Dateien beschreiben Sie die vollständige Struktur:

```bash
# Ein vollständiges API-Modul generieren
bob "Erstelle eine vollständige REST-API für eine Todo-Anwendung in Python mit Routen, Modellen und Datenbank-Setup. Stelle alle notwendigen Dateien bereit."

# Frontend-Komponenten generieren
bob "Erstelle eine Reihe von React-Komponenten für ein Dashboard: Header, Sidebar, MainContent und Footer. Stelle jede Komponente in einem separaten Code-Block bereit."
```

**Was passiert:**
- Beschreiben Sie die vollständige Projektstruktur in Ihrer Eingabeaufforderung
- Bob wird mehrere Code-Blöcke oder Dateien bereitstellen
- Sie können jeden Teil separat speichern oder Bob bitten, sie zu organisieren
- Fügen Sie Details zur Dateiorganisation in Ihre Eingabeaufforderung ein

**💡 Tipp:** Für Multi-Datei-Projekte können Sie Bob bitten, zuerst eine Dateistruktur bereitzustellen und dann jede Datei einzeln zu generieren.

### Schritt 2.3: Gespeicherte Eingabeaufforderungen für Konsistenz verwenden

Speichern Sie häufige Eingabeaufforderungen für wiederholte Verwendung:

```bash
# Eine Eingabeaufforderungsdatei für konsistente API-Generierung erstellen
cat > api-prompt.txt << 'EOF'
Erstelle einen REST-API-Endpunkt mit:
- Anforderungsvalidierung
- Fehlerbehandlung
- Antwortformatierung
- Ordnungsgemäßen HTTP-Statuscodes
EOF

# Die gespeicherte Eingabeaufforderung mit spezifischen Details verwenden (mit sauberer Ausgabe)
bob "$(cat api-prompt.txt) Erstelle einen POST-Endpunkt unter /api/users zum Erstellen neuer Benutzer" --yolo --hide-intermediary-output > user-endpoint.js

# Oder mit zusätzlichem Kontext kombinieren (Bob bitten, in Datei zu schreiben)
bob "$(cat api-prompt.txt) Erstelle einen GET-Endpunkt unter /api/products zum Auflisten von Produkten mit Paginierung und schreibe ihn in products-endpoint.js" --yolo
```

**Was passiert:**
- Speichern Sie häufige Anforderungen in Textdateien
- Kombinieren Sie gespeicherte Eingabeaufforderungen mit spezifischen Details
- Gewährleistet Konsistenz in Ihrer Codebasis
- Reduziert Wiederholungen in Ihren Eingabeaufforderungen

## Teil 3: Code-Analyse und Review - Beispiel-Anwendungsfälle

**📝 Hinweis:** Dieser Abschnitt demonstriert Beispiel-Eingabeaufforderungen, die zeigen, wie BobShell für Code-Analyse und Review in echten Projekten verwendet werden kann. Dies sind Referenzbeispiele, keine Befehle, die als Teil dieses Labs ausgeführt werden sollen.

### Schritt 3.1: Beispiele für Code-Qualitätsanalyse

BobShell kann Code auf Qualitätsprobleme mit natürlichsprachlichen Eingabeaufforderungen analysieren. Hier sind Beispiel-Eingabeaufforderungen, die Sie in Ihren Projekten verwenden könnten:

```bash
# Beispiel: Eine einzelne Datei analysieren
bob "Analysiere die Code-Qualität, Leistung und Sicherheit von ./src/app.js"

# Beispiel: Gesamtes Verzeichnis analysieren und als JSON speichern
bob "Analysiere alle Dateien in ./src rekursiv und stelle einen detaillierten Bericht bereit" > analysis-report.json

# Beispiel: Spezifische Metriken erhalten
bob "Analysiere ./src und stelle Metriken zu Komplexität, Wartbarkeit und Testabdeckung bereit"
```

**Wie diese funktionieren:**
- Verwenden Sie natürliche Sprache, um zu beschreiben, was Bob analysieren soll
- Seien Sie spezifisch über Aspekte: Qualität, Leistung, Sicherheit usw.
- Erwähnen Sie, ob Sie rekursive Verzeichnisanalyse möchten
- Verwenden Sie Ausgabeumleitung (`>`), um Ergebnisse in Dateien zu speichern

### Schritt 3.2: Beispiele für automatisierte Code-Reviews

BobShell kann umfassende Code-Reviews mit konversationellen Eingabeaufforderungen durchführen. Beispiel-Eingabeaufforderungen:

```bash
# Beispiel: Änderungen in einem Branch überprüfen
bob "Überprüfe die Code-Änderungen zwischen main und feature-branch"

# Beispiel: Spezifische Dateien mit Style Guide überprüfen
bob "Überprüfe die React-Komponenten in ./src/components nach dem Airbnb Style Guide"

# Beispiel: Review mit spezifischem Fokus
bob "Überprüfe ./src auf Code-Qualitätsprobleme und stelle Vorschläge im Markdown-Format bereit" > review-report.md
```

**Wie diese funktionieren:**
- Beschreiben Sie, welchen Code Sie überprüfen lassen möchten (Dateien, Verzeichnisse, Git-Änderungen)
- Geben Sie Style Guides oder Standards an (Airbnb, Google usw.)
- Erwähnen Sie spezifische Schwerpunktbereiche (Sicherheit, Leistung, Best Practices)
- Verwenden Sie Ausgabeumleitung, um Review-Berichte zu speichern

### Schritt 3.3: Beispiele für Sicherheitsanalyse

BobShell kann Code auf Sicherheitslücken mit natürlicher Sprache scannen. Beispiel-Eingabeaufforderungen:

```bash
# Beispiel: Sicherheitsscan mit Schweregrad-Fokus
bob "Scanne ./src auf hohe und kritische Sicherheitslücken"

# Beispiel: Nach spezifischen Schwachstellen suchen
bob "Überprüfe ./src auf SQL-Injection, XSS und offengelegte Geheimnisse"

# Beispiel: Sicherheitsbericht generieren
bob "Führe eine umfassende Sicherheitsanalyse von ./src durch und generiere einen HTML-Bericht" > security-report.html
```

**Wie diese funktionieren:**
- Bitten Sie Bob, auf Sicherheitsprobleme zu scannen oder zu analysieren
- Geben Sie Schweregrade (hoch, kritisch) oder Schwachstellentypen an
- Fordern Sie spezifische Ausgabeformate an (HTML, Markdown, JSON)
- Ähnlich wie Schwachstellen, die Sie in Lab 2 behoben haben

**💡 Wann diese Eingabeaufforderungen verwenden:**
- Während Code-Reviews vor dem Zusammenführen von Pull Requests
- Als Teil von CI/CD-Pipelines für automatisierte Qualitätsprüfungen
- Bei der Prüfung bestehender Codebasen auf Sicherheitsprobleme
- Zur Generierung von Compliance- und Sicherheitsberichten

## Teil 4: Automatisierungsskripte

### Schritt 4.1: Automatisiertes Code-Review-Skript

Lassen Sie uns das automatisierte Code-Review-Skript untersuchen:

**Datei: `scripts/code-review.sh`**

Dieses Skript führt automatisierte Code-Reviews auf geänderten Dateien durch. Siehe das vollständige Skript in der Datei für Details zur Implementierung.

**Verwendung:**
```bash
# Änderungen gegen main-Branch überprüfen
./scripts/code-review.sh

# Änderungen gegen anderen Branch überprüfen
./scripts/code-review.sh develop
```

**Was passiert:**
- Skript identifiziert alle geänderten Code-Dateien mit git diff
- Jede Datei wird einzeln von Bob überprüft
- Reviews werden als Markdown-Dateien mit Zeitstempeln gespeichert
- Ein Zusammenfassungsbericht aggregiert alle Ergebnisse
- Perfekt für Pre-Commit- oder Pre-Merge-Prüfungen

### Schritt 4.2: Batch-Refactoring-Skript

**Datei: [`scripts/refactor-batch.sh`](scripts/refactor-batch.sh)**

Dieses Skript refaktoriert mehrere Dateien sicher basierend auf angegebenen Kriterien unter Verwendung von Bobs natürlichsprachlicher Schnittstelle.

**Funktionen:**
- Automatische Backup-Erstellung vor Refactoring
- Mehrere Refactoring-Typen: modernize, optimize, cleanup, security
- Verarbeitet mehrere Dateien im Batch
- Detaillierte Protokollierung und Fehlerbehandlung
- Automatische Wiederherstellung bei Fehler
- Bestätigungsaufforderung vor Fortfahren

**Verwendung:**
```bash
# Code im aktuellen Verzeichnis modernisieren
./scripts/refactor-batch.sh modernize .

# Leistung im src-Verzeichnis optimieren
./scripts/refactor-batch.sh optimize ./src

# Code aufräumen
./scripts/refactor-batch.sh cleanup ./lib

# Sicherheitsprobleme beheben
./scripts/refactor-batch.sh security ./src
```

**💡 Tipp:** Überprüfen Sie das [vollständige Skript](scripts/refactor-batch.sh), um zu sehen, wie Bobs natürlichsprachliche Schnittstelle Batch-Refactoring sicher handhabt.

### Schritt 4.3: Dokumentationsgenerierungs-Skript

**Datei: [`scripts/generate-docs.sh`](scripts/generate-docs.sh)**

Dieses umfassende Skript generiert automatisch vollständige Dokumentation für Ihre Codebasis unter Verwendung von Bobs natürlichsprachlicher Schnittstelle.

**Funktionen:**
- Generiert API-Dokumentation
- Erstellt Architekturdokumentation
- Produziert Verwendungsbeispiele
- Generiert README, CHANGELOG, CONTRIBUTING-Leitfaden
- Erstellt FAQ und Fehlerbehebungsleitfäden
- Unterstützt Markdown- und HTML-Ausgabeformate
- Enthält detaillierte Protokollierung und Fehlerbehandlung

**Verwendung:**
```bash
# Dokumentation für aktuelles Verzeichnis generieren (Markdown-Format)
./scripts/generate-docs.sh

# Dokumentation für spezifisches Verzeichnis generieren
./scripts/generate-docs.sh ./src ./documentation

# HTML-Dokumentation generieren
./scripts/generate-docs.sh ./src ./docs html
```

**💡 Tipp:** Überprüfen Sie das [vollständige Skript](scripts/generate-docs.sh), um zu sehen, wie Bobs natürlichsprachliche Schnittstelle für automatisierte Dokumentationsgenerierung verwendet wird.

## Teil 5: CI/CD-Integration

### Schritt 5.1: GitHub Actions Integration

Siehe die vollständige GitHub Actions Workflow-Konfiguration in [`ci-cd/github-actions.yml`](ci-cd/github-actions.yml).

**Hauptfunktionen:**
- Läuft bei jedem Pull Request und Push zu main/develop
- Installiert und konfiguriert Bob CLI in der CI-Umgebung
- Führt Code-Review auf geänderten Dateien mit natürlichsprachlichen Eingabeaufforderungen durch
- Führt Sicherheitsscan und Qualitätsanalyse durch
- Lädt Berichte als Artefakte hoch
- Postet Review-Kommentare direkt auf Pull Requests
- Schlägt Build fehl, wenn kritische Sicherheitsprobleme gefunden werden

**Schnellstart:**
1. Kopieren Sie `ci-cd/github-actions.yml` nach `.github/workflows/bob-ci.yml` in Ihrem Repository
2. Fügen Sie `BOB_API_KEY` zu Ihren Repository-Secrets hinzu (Settings > Secrets and variables > Actions)
3. Passen Sie Qualitätsschwellenwerte und Analyseebenen nach Bedarf an

### Schritt 5.2: GitLab CI Integration

Siehe die vollständige GitLab CI Konfiguration in [`ci-cd/gitlab-ci.yml`](ci-cd/gitlab-ci.yml).

**Hauptfunktionen:**
- Multi-Stage-Pipeline: setup, review, security, quality, documentation, report
- Jede Stage produziert Artefakte zur Überprüfung
- Sicherheitsscan schlägt Pipeline bei kritischen Problemen fehl
- Qualitätsprüfung erzwingt minimale Qualitätsbewertung
- Komplexitäts- und Abhängigkeitsanalyse für gründliche Prüfungen
- Dokumentationsgenerierung auf main-Branch
- Zusammenfassungsberichtgenerierung mit allen Ergebnissen

**Schnellstart:**
1. Kopieren Sie `ci-cd/gitlab-ci.yml` nach `.gitlab-ci.yml` in Ihrem Repository-Root
2. Fügen Sie `BOB_API_KEY` als CI/CD-Variable hinzu (Settings > CI/CD > Variables)
3. Konfigurieren Sie Artefaktaufbewahrung und Qualitätsschwellenwerte nach Bedarf

### Schritt 5.3: Jenkins Pipeline Integration

Siehe die vollständige Jenkins Pipeline Konfiguration in [`ci-cd/jenkins-pipeline.txt`](ci-cd/jenkins-pipeline.txt).

**Hauptfunktionen:**
- Multi-Stage-Pipeline mit Bob-Integration
- Anmeldedaten sicher über Jenkins verwaltet
- Code-Review läuft nur bei Pull Requests mit natürlichsprachlichen Eingabeaufforderungen
- Sicherheitsscan schlägt Build bei kritischen Problemen fehl
- Qualitätsanalyse markiert Build als instabil, wenn unter Schwellenwert
- Komplexitäts- und Abhängigkeitsanalyse-Stages
- Dokumentation generiert und auf main-Branch veröffentlicht
- Build-Parameter für anpassbare Analyseebenen
- Artefakte für alle Stages archiviert
- Workspace nach Ausführung bereinigt

**Schnellstart:**
1. Kopieren Sie Inhalt von `ci-cd/jenkins-pipeline.txt` in ein `Jenkinsfile` in Ihrem Repository-Root
2. Fügen Sie Bob API-Schlüssel als Jenkins-Anmeldedaten mit ID `bob-api-key` hinzu (Jenkins > Credentials > System > Global credentials)
3. Installieren Sie erforderliche Jenkins-Plugins: Pipeline, Git, HTML Publisher, Email Extension
4. Konfigurieren Sie Webhook für automatische Builds
5. Passen Sie Qualitätsschwellenwerte und Analyseebenen nach Bedarf an

## Teil 6: Erweiterte Workflows

### Schritt 6.1: Bob mit anderen Tools kombinieren

Erstellen Sie leistungsstarke Workflows, indem Sie Bob mit anderen CLI-Tools kombinieren:

```bash
# TODO-Kommentare finden und Aufgaben erstellen
grep -r "TODO" ./src | bob "Konvertiere diese TODO-Kommentare in GitHub-Issues mit ordnungsgemäßer Formatierung im JSON-Format" --hide-intermediary-output > issues.json

# Git-Historie analysieren und Erkenntnisse generieren
git log --since="1 month ago" --pretty=format:"%h %s" | bob "Analysiere diese Commit-Nachrichten und stelle Erkenntnisse über Entwicklungsmuster im Markdown-Format bereit" --hide-intermediary-output > dev-insights.md

# Testergebnisse verarbeiten
npm test -- --json | bob "Analysiere diese Testergebnisse und schlage Verbesserungen im Markdown-Format vor" --hide-intermediary-output > test-analysis.md

# Code-Coverage-Analyse
npm run coverage -- --json | bob "Erstelle einen Coverage-Bericht mit Empfehlungen zur Verbesserung der Testabdeckung im Markdown-Format" --hide-intermediary-output > coverage-report.md
```

**Was passiert:**
- Leitet Ausgabe von Standard-Tools an Bob zur KI-Analyse weiter
- Konvertiert unstrukturierte Daten in umsetzbare Erkenntnisse
- Generiert Berichte und Empfehlungen
- Integriert sich nahtlos in bestehende Toolchains

### Schritt 6.2: Beispiel für benutzerdefinierten Workflow

Erstellen Sie einen vollständigen Pre-Commit-Workflow - siehe Beispiel im englischen README für vollständige Implementierungsdetails.

## Teil 7: Best Practices

### 7.1: BobShell Best Practices

1. **Spezifische Befehle verwenden**: Seien Sie spezifisch in Ihren Anfragen für bessere Ergebnisse
2. **Ausgabeformate nutzen**: Verwenden Sie geeignete Formate für verschiedene Anwendungsfälle (JSON, Markdown, HTML)
3. **Git-Integration verwenden**: Nur geänderten Code überprüfen
4. **Caching implementieren**: Bob-Antworten für wiederholte Operationen cachen

> **💡 Automatische Optimierung**
> Wenn Sie BobShell-Befehle ausführen, wählt Bobs [intelligente Ressourcenoptimierung](../bob-differentiators.md#2--intelligent-resource-optimization) automatisch das am besten geeignete Modell für jede Aufgabe aus. Sie müssen nicht angeben, welches Modell verwendet werden soll – Bob handhabt dies transparent und optimiert sowohl Qualität als auch Kosten.

### 7.2: Automatisierungs-Best-Practices

1. **Immer Backups erstellen**: Vor automatisiertem Refactoring
2. **Versionskontrolle verwenden**: Vor automatisierten Änderungen committen
3. **Nach Automatisierung testen**: Immer verifizieren, dass automatisierte Änderungen funktionieren
4. **Alles protokollieren**: Protokolle automatisierter Operationen führen
5. **Fehler elegant behandeln**: Ordnungsgemäße Fehlerbehandlung in Skripten implementieren

### 7.3: CI/CD Best Practices

1. **API-Schlüssel sichern**: Secrets-Management für Bob API-Schlüssel verwenden
2. **Geeignete Schwellenwerte setzen**: Qualitäts- und Sicherheitsschwellenwerte definieren
3. **Berichte archivieren**: Berichte für Audit und Review aufbewahren
4. **Schnell fehlschlagen**: Pipeline bei kritischen Problemen stoppen
5. **Feedback geben**: PRs mit Review-Ergebnissen kommentieren

> **🔍 Bob Findings in CI/CD**
> Integrieren Sie [Bob Findings](../bob-differentiators.md#3--bob-findings-automated-analysis-engine) in Ihre CI/CD-Pipeline für automatisiertes Sicherheitsscanning und Code-Qualitätsprüfungen. Bob kann Schwachstellen und Code-Probleme erkennen, bevor sie in die Produktion gelangen, mit spezifischen Sanierungsempfehlungen in Ihren Pipeline-Berichten.

## Übungen

### Übung 1: Benutzerdefiniertes Review-Skript erstellen

Erstellen Sie ein Skript, das:
1. Alle Python-Dateien in einem Verzeichnis überprüft
2. PEP 8-Konformität prüft
3. Potenzielle Fehler identifiziert
4. Einen Zusammenfassungsbericht generiert

### Übung 2: CI/CD-Pipeline aufbauen

Richten Sie eine vollständige CI/CD-Pipeline ein, die:
1. Bei Pull Requests läuft
2. Code-Review durchführt
3. Sicherheitsscan ausführt
4. Code-Qualität prüft
5. Ergebnisse als PR-Kommentare postet

### Übung 3: Dokumentation automatisieren

Erstellen Sie einen Workflow, der:
1. API-Dokumentation generiert
2. Verwendungsbeispiele erstellt
3. README aktualisiert
4. Dokumentationsänderungen committet

## Fehlerbehebung

### Häufige Probleme

1. **Bob CLI nicht gefunden**
   ```bash
   # Installation überprüfen
   which bob
   
   # Bei Bedarf neu installieren
   npm install -g @ibm/bob-cli
   ```

2. **Authentifizierungsfehler**
   ```bash
   # API-Schlüssel-Konfiguration prüfen
   bob config get api-key
   
   # Bei Bedarf neu konfigurieren
   bob config set api-key YOUR_API_KEY
   ```

3. **Rate Limiting**
   ```bash
   # Rate-Limit-Status prüfen
   bob status
   
   # Caching verwenden, um API-Aufrufe zu reduzieren
   bob config set cache-enabled true
   ```

## Zusammenfassung

In diesem Lab haben Sie gelernt:

✅ Wie man BobShell für interaktive und nicht-interaktive Operationen verwendet  
✅ Code-Generierung, Analyse und Review über Kommandozeile  
✅ Automatisierungsskripte für häufige Entwicklungsaufgaben zu erstellen  
✅ Bob in CI/CD-Pipelines zu integrieren (GitHub Actions, GitLab CI, Jenkins)  
✅ Benutzerdefinierte Workflows zu erstellen, die Bob mit anderen Tools kombinieren  
✅ Best Practices für CLI-Nutzung und Automatisierung

## Nächste Schritte

- **Lab 5**: Lernen Sie, wie Sie Java-Anwendungen mit Bob modernisieren
- **Lab 6**: Erstellen Sie benutzerdefinierte MCP-Server und Modi
- Erkunden Sie erweiterte BobShell-Funktionen in der Dokumentation
- Teilen Sie Ihre Automatisierungsskripte mit dem Team

## Zusätzliche Ressourcen

- [BobShell-Dokumentation](https://ibm.com/bob/docs/cli)
- [CI/CD-Integrationsleitfaden](https://ibm.com/bob/docs/cicd)
- [Automatisierungsbeispiele-Repository](https://github.com/ibm/bob-automation-examples)
- [BobShell API-Referenz](https://ibm.com/bob/docs/api)

---

**Benötigen Sie Hilfe?** Wenn Sie auf Probleme stoßen:
1. Überprüfen Sie den Fehlerbehebungsabschnitt oben
2. Lesen Sie die BobShell-Dokumentation
3. Fragen Sie in den Bob-Community-Foren
4. Kontaktieren Sie den IBM-Support

**Feedback:** Helfen Sie uns, dieses Lab zu verbessern, indem Sie Feedback geben, was gut funktioniert hat und was besser sein könnte!

---

**Bereit für die nächste Herausforderung?** → [Lab 5 starten: Java-Anwendungsmodernisierung](../lab5/README.md)

*Zuletzt aktualisiert: Dezember 2025*