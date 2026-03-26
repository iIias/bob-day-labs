# Lab 3: Code-Übersetzung - Python zu JavaScript

## Überblick

In diesem Lab lernen Sie, wie Sie Bob verwenden, um Code von einer Programmiersprache in eine andere zu übersetzen, während Sie die Funktionalität beibehalten und sprachspezifische Best Practices anwenden. Sie werden ein Python-Datenverarbeitungsskript nach JavaScript (Node.js) übersetzen.

> **🧠 Bob-Differenzierungsmerkmal: [Intelligente Ressourcenoptimierung](../bob-differentiators.md#2--intelligent-resource-optimization)**
> Während dieses Labs wählt Bob automatisch das richtige KI-Modell für jede Übersetzungsaufgabe aus. Komplexe Sprachfeature-Mappings verwenden leistungsstarke Modelle für Genauigkeit, während einfache Syntaxkonvertierungen leichtere Modelle für Geschwindigkeit verwenden. Diese [automatische Modellauswahl](../bob-differentiators.md#automatic-model-selection) geschieht transparent und optimiert sowohl Qualität als auch Kosten.

**Dauer**: 45 Minuten
**Schwierigkeitsgrad**: Fortgeschrittene

## Was Sie übersetzen werden

Ein Python-Datenverarbeitungsskript, das:
- CSV-Dateien liest
- Statistische Berechnungen durchführt
- Ergebnisse nach JSON exportiert
- Type Hints und moderne Python-Features verwendet

**Ziel**: Äquivalente JavaScript (Node.js) Implementierung

## Lernziele

Am Ende dieses Labs werden Sie:
- ✅ Ask-Modus verwenden, um Quellcode zu analysieren
- ✅ Architect-Modus verwenden, um Übersetzungsstrategie zu planen
- ✅ Code-Modus verwenden, um Übersetzung zu implementieren
- ✅ Sprachspezifische Muster verstehen
- ✅ Python-Features auf JavaScript-Äquivalente abbilden
- ✅ Code-Funktionalität über Sprachen hinweg beibehalten
- ✅ Best Practices in beiden Sprachen anwenden

## Voraussetzungen

Stellen Sie vor dem Start sicher, dass Sie Folgendes haben:
- [ ] Lab 1 und Lab 2 abgeschlossen (oder vertraut mit Bobs Modi)
- [ ] Python 3.8+ installiert
- [ ] Node.js 14+ installiert
- [ ] Bob installiert und läuft
- [ ] Verständnis der Grundlagen von Python und JavaScript

## Lab-Struktur

```
Lab 3 Zeitplan (45 Minuten)
├── Schritt 1: Python-Code analysieren (10 Min.)
├── Schritt 2: Übersetzungsstrategie planen (10 Min.)
├── Schritt 3: Übersetzung implementieren (20 Min.)
└── Schritt 4: Verifizieren & Vergleichen (5 Min.)
```

---

## Schritt 1: Python-Code mit Ask-Modus analysieren (10 Minuten)

### Den Quellcode verstehen

Lassen Sie uns den Python-Datenprozessor untersuchen, den wir übersetzen werden.

### 1.1: Python-Code überprüfen

Öffnen Sie `lab3/source/data_processor.py` und überprüfen Sie die Code-Struktur.

**Wichtige zu beachtende Features:**
- Klassenbasiertes Design
- Type Hints (`: str`, `-> Dict`)
- Context Manager (`with open()`)
- List Comprehensions
- Dictionary-Operationen
- CSV- und JSON-Verarbeitung

### 1.2: In den Ask-Modus wechseln

Öffnen Sie Bob und wechseln Sie in den **Ask-Modus** (❓).

### 1.3: Code-Struktur verstehen

**Eingabeaufforderung für Bob:**

```
Analysiere den Python-Code in lab3/source/data_processor.py und erkläre:
1. Was ist der Gesamtzweck dieses Codes?
2. Was sind die Hauptkomponenten und ihre Verantwortlichkeiten?
3. Welche Python-spezifischen Features werden verwendet?
4. Was sind die wichtigsten Datenstrukturen und Algorithmen?
```

**Erwartete Antwort:**

Bob sollte erklären:
- **Zweck**: Verarbeitet CSV-Daten und generiert statistische Zusammenfassungen
- **Komponenten**: 
  - `DataProcessor`-Klasse mit Methoden zum Laden, Analysieren und Exportieren
  - Datei-I/O-Operationen
  - Statistische Berechnungen
- **Python-Features**:
  - Type Hints für bessere Code-Dokumentation
  - Context Manager für sichere Dateiverarbeitung
  - List Comprehensions für prägnante Datenverarbeitung
  - Dictionary Comprehensions
- **Datenstrukturen**: Listen, Dictionaries, CSV-Zeilen

### 1.4: Übersetzungsherausforderungen identifizieren

**Eingabeaufforderung für Bob:**

```
Welche Herausforderungen könnten wir bei der Übersetzung dieses Python-Codes nach JavaScript haben?
Berücksichtige:
- Unterschiede in der Sprachsyntax
- Unterschiede in eingebauten Bibliotheken
- Async/Sync-Muster
- Unterschiede im Typsystem
```

**Erwartete Herausforderungen:**

1. **Datei-I/O**: Pythons `with open()` vs Node.js asynchrone Dateioperationen
2. **CSV-Parsing**: Pythons `csv`-Modul vs JavaScript-Bibliotheken
3. **Type Hints**: Pythons Type Hints vs JSDoc oder TypeScript
4. **List Comprehensions**: Pythons prägnante Syntax vs JavaScript Array-Methoden
5. **Synchron vs Asynchron**: Pythons synchrones I/O vs Node.js asynchrone Muster

**💡 Wichtige Erkenntnis**: Den Quellcode gründlich zu verstehen ist entscheidend vor der Übersetzung.

---

## Schritt 2: Übersetzungsstrategie mit Plan-Modus planen (10 Minuten)

Jetzt erstellen wir einen detaillierten Übersetzungsplan.

### 2.1: In den Plan-Modus wechseln

Wechseln Sie von Ask zu **Plan-Modus** (🎯).

### 2.2: Übersetzungs-Mapping erstellen

**Eingabeaufforderung für Bob:**

```
Erstelle einen detaillierten Übersetzungsplan für die Konvertierung des Python-Datenprozessors nach JavaScript.
Füge hinzu:
1. Feature-für-Feature-Mapping (Python → JavaScript)
2. Bibliotheks-/Modul-Äquivalente
3. Benötigte Syntaxtransformationen
4. Empfohlene JavaScript-Muster
5. Dateistruktur für die JavaScript-Version
```

**Erwartetes Mapping:**

| Python-Feature | JavaScript-Äquivalent | Hinweise |
|----------------|----------------------|----------|
| `class DataProcessor` | `class DataProcessor` | Klassen funktionieren ähnlich |
| `def __init__(self, filename: str)` | `constructor(filename)` | Constructor-Syntax unterscheidet sich |
| `with open(file)` | `fs.promises.readFile()` | Asynchron in JavaScript |
| `csv.DictReader` | `csv-parser`-Bibliothek | Benötigt npm-Paket |
| List Comprehension | `Array.map()`, `Array.filter()` | Ausführlicher |
| Type Hints | JSDoc-Kommentare | Optional aber empfohlen |
| `if __name__ == '__main__'` | Direkte Ausführung oder Modulprüfung | Anderes Muster |

### 2.3: Modulstruktur planen

**Eingabeaufforderung für Bob:**

```
Entwerfe die JavaScript-Modulstruktur für den übersetzten Code.
Sollten wir verwenden:
- ES6-Module oder CommonJS?
- Klassen oder funktionalen Ansatz?
- Async/await oder Promises?
- Zusätzliche Fehlerbehandlung?
```

**Empfohlene Struktur:**

```javascript
// CommonJS für Node.js-Kompatibilität verwenden
// ES6-Klassensyntax verwenden (ähnlich wie Python)
// Async/await für saubereren asynchronen Code verwenden
// Umfassende Fehlerbehandlung hinzufügen
// JSDoc für Typdokumentation einschließen
```

### 2.4: Abhängigkeiten identifizieren

**Eingabeaufforderung für Bob:**

```
Welche npm-Pakete werden wir für die JavaScript-Version benötigen?
Liste die Pakete und ihre Zwecke auf.
```

**Erforderliche Pakete:**
- `csv-parser`: Zum Parsen von CSV-Dateien
- `fs` (eingebaut): Für Dateioperationen
- Keine zusätzlichen Pakete erforderlich (einfach halten)

**💡 Wichtige Erkenntnis**: Der Architect-Modus hilft, eine klare Roadmap vor dem Codieren zu erstellen.

> **💡 Kontextverwaltung in Aktion**
> Während Sie an dieser Übersetzung arbeiten, verwendet Bob [dynamische Kontextfenster-Kompression](../bob-differentiators.md#dynamic-context-window-compression), um sowohl den Python-Quellcode als auch den JavaScript-Zielcode effizient im Speicher zu verwalten. Dies ermöglicht es Bob, den vollständigen Kontext beider Codebasen beizubehalten und gleichzeitig Token-Nutzung und Kosten zu minimieren.

---

## Schritt 3: Übersetzung mit Code-Modus implementieren (20 Minuten)

Jetzt übersetzen wir den Code mit Bobs Code-Modus.

### 3.1: In den Code-Modus wechseln

Wechseln Sie zu **Code-Modus** (💻).

### 3.2: Paketkonfiguration erstellen

**Eingabeaufforderung für Bob:**

```
Erstelle eine package.json-Datei für den JavaScript-Datenprozessor mit:
- Name: data-processor
- Version: 1.0.0
- Abhängigkeiten: csv-parser
- Haupteinstiegspunkt: data_processor.js
- Skripte zum Ausführen des Prozessors
```

### 3.3: Vollständige Klasse übersetzen

**Eingabeaufforderung für Bob:**

```
Übersetze die gesamte DataProcessor-Klasse von Python nach JavaScript.
Füge hinzu:
- Constructor, der Pythons __init__ entspricht
- Alle Methoden mit äquivalenter Funktionalität
- JSDoc-Kommentare für Typdokumentation
- Async/await für Dateioperationen
- Fehlerbehandlung
- Hauptausführungslogik
```

**Was Bob erstellen wird:**

Bob wird die gesamte Klassenstruktur auf einmal übersetzen und eine vollständige JavaScript-Implementierung mit allen Methoden erstellen. Die Übersetzung wird Folgendes enthalten:

```javascript
/**
 * DataProcessor - Analysiert CSV-Dateien und generiert Statistiken
 * Übersetzt von Python nach JavaScript
 */
const fs = require('fs').promises;
const { createReadStream } = require('fs');
const csv = require('csv-parser');

class DataProcessor {
    constructor(filename) { ... }
    async loadData() { ... }
    calculateStatistics() { ... }
    async exportResults(outputFile) { ... }
}

// Hauptausführungslogik
if (require.main === module) { ... }
```

**Hinweis**: Bob wird alle Komponenten auf einmal übersetzen. Die folgenden Abschnitte erklären wichtige Aspekte der Übersetzung zu Ihrem Verständnis.

---

### 3.4: Datei-I/O-Übersetzung verstehen

Lassen Sie uns nun untersuchen, wie Bob spezifische Komponenten übersetzt hat. **Wechseln Sie in den Ask-Modus** (❓), um den übersetzten Code zu erkunden.

**Eingabeaufforderung für Bob:**

```
Erkläre, wie du die load_data-Methode von Python nach JavaScript übersetzt hast.
Was sind die Hauptunterschiede zwischen Pythons Context Manager und JavaScripts Stream-basiertem Ansatz?
```

**Wichtige Übersetzungspunkte:**

**Python-Original:**
```python
def load_data(self) -> None:
    with open(self.filename, 'r') as file:
        reader = csv.DictReader(file)
        self.data = [row for row in reader]
```

**JavaScript-Übersetzung:**
```javascript
async loadData() {
    return new Promise((resolve, reject) => {
        const results = [];
        createReadStream(this.filename)
            .pipe(csv())
            .on('data', (row) => results.push(row))
            .on('end', () => {
                this.data = results;
                resolve();
            })
            .on('error', reject);
    });
}
```

### 3.5: Übersetzung statistischer Berechnungen verstehen

**Eingabeaufforderung für Bob:**

```
Erkläre, wie du die calculate_statistics-Methode übersetzt hast.
Wie hast du Pythons List Comprehensions und eingebaute Funktionen nach JavaScript konvertiert?
```

**Wichtige Übersetzungspunkte:**

**Python-Original:**
```python
def calculate_statistics(self) -> Dict:
    numeric_fields = [k for k in self.data[0].keys()
                     if self.data[0][k].replace('.', '').isdigit()]
    values = [float(row[field]) for row in self.data]
    stats[field] = {
        'mean': sum(values) / len(values),
        'min': min(values),
        'max': max(values)
    }
```

**JavaScript-Übersetzung:**
```javascript
calculateStatistics() {
    const numericFields = Object.keys(this.data[0])
        .filter(key => !isNaN(parseFloat(this.data[0][key])));
    const values = this.data.map(row => parseFloat(row[field]));
    stats[field] = {
        mean: values.reduce((a, b) => a + b, 0) / values.length,
        min: Math.min(...values),
        max: Math.max(...values)
    };
}
```

### 3.6: JSON-Export-Übersetzung verstehen

**Eingabeaufforderung für Bob:**

```
Erkläre, wie du die export_results-Methode übersetzt hast.
Was ist der Unterschied zwischen Pythons synchronem Dateischreiben und JavaScripts asynchronem Ansatz?
```

### 3.7: Hauptausführungslogik verstehen

**Eingabeaufforderung für Bob:**

```
Erkläre, wie du Pythons if __name__ == '__main__'-Muster nach JavaScript übersetzt hast.
Warum hast du eine asynchrone IIFE (Immediately Invoked Function Expression) verwendet?
```

**JavaScript-Übersetzung:**
```javascript
// Hauptausführung
if (require.main === module) {
    (async () => {
        try {
            const processor = new DataProcessor('data.csv');
            await processor.loadData();
            await processor.exportResults('statistics.json');
            console.log('✅ Verarbeitung abgeschlossen!');
        } catch (error) {
            console.error('❌ Fehler:', error.message);
            process.exit(1);
        }
    })();
}

module.exports = DataProcessor;
```

**💡 Wichtige Erkenntnis**: Der Code-Modus handhabt die tatsächliche Übersetzung unter Beibehaltung der Funktionalität.

---

## Schritt 4: Verifizieren & Vergleichen (5 Minuten)

Lassen Sie uns beide Versionen testen und die Ergebnisse vergleichen.

### 4.1: Beispieldaten erstellen

Erstellen Sie eine Beispiel-CSV-Datei zum Testen:

**data.csv:**
```csv
name,age,score,grade
Alice,25,95.5,A
Bob,30,87.3,B
Charlie,22,92.1,A
Diana,28,88.7,B
```

### 4.2: Python-Version ausführen

```bash
cd lab3/source
python data_processor.py
```

**Erwartete Ausgabe:**
```
Verarbeitung abgeschlossen!
Ergebnisse in statistics.json gespeichert
```

**statistics.json:**
```json
{
  "age": {
    "mean": 26.25,
    "min": 22,
    "max": 30,
    "count": 4
  },
  "score": {
    "mean": 90.9,
    "min": 87.3,
    "max": 95.5,
    "count": 4
  }
}
```

### 4.3: JavaScript-Version ausführen

**Hinweis**: Bob hat die JavaScript-Übersetzung im `lab3/`-Verzeichnis erstellt (nicht in einem separaten Zielordner).

```bash
# Zum lab3-Verzeichnis navigieren, wo sich die übersetzte JavaScript-Datei befindet
cd lab3
npm install
node data_processor.js
```

**Erwartete Ausgabe:**
```
✅ Verarbeitung abgeschlossen!
Ergebnisse in statistics.json gespeichert
```

### 4.4: Ergebnisse vergleichen

**Eingabeaufforderung für Bob (Ask-Modus):**

```
Vergleiche die Python- und JavaScript-Implementierungen.
Was sind die Hauptunterschiede in:
1. Code-Struktur
2. Syntax
3. Async-Verarbeitung
4. Fehlerbehandlung
5. Leistungsmerkmale
```

### 4.5: Funktionalität verifizieren

Beide Versionen sollten identische Ausgaben produzieren:
- ✅ Gleiche statistische Berechnungen
- ✅ Gleiche JSON-Struktur
- ✅ Gleiche Dateiverarbeitung
- ✅ Äquivalente Fehlerbehandlung

---

## Herzlichen Glückwunsch! 🎉

Sie haben Lab 3 erfolgreich abgeschlossen! Sie haben gelernt:

- ✅ Code-Struktur über Sprachen hinweg zu analysieren
- ✅ Übersetzungsstrategien systematisch zu planen
- ✅ Sprachspezifische Features abzubilden
- ✅ Übersetzungen unter Beibehaltung der Funktionalität zu implementieren
- ✅ Async/Sync-Unterschiede zu handhaben
- ✅ Best Practices in beiden Sprachen anzuwenden
- ✅ Übersetzten Code auf Korrektheit zu verifizieren

> **🎯 Intelligente Optimierung in Aktion**
> Während dieses Labs arbeitete Bobs [intelligente Ressourcenoptimierung](../bob-differentiators.md#2--intelligent-resource-optimization) im Hintergrund. Bob wählte automatisch Frontier-Klasse-Modelle für komplexe Übersetzungsentscheidungen (wie das Mapping von Pythons Context Managern zu JavaScripts asynchronen Mustern) und leichtere Modelle für einfache Syntaxkonvertierungen. Diese Optimierung kann KI-Kosten um bis zu 60% reduzieren und gleichzeitig qualitativ hochwertige Ergebnisse liefern!

## Gelernte Übersetzungsmuster

### 1. Klassenübersetzung
**Python:**
```python
class DataProcessor:
    def __init__(self, filename: str):
        self.filename = filename
```

**JavaScript:**
```javascript
class DataProcessor {
    constructor(filename) {
        this.filename = filename;
    }
}
```

### 2. List Comprehensions → Array-Methoden
**Python:**
```python
values = [float(row[field]) for row in self.data]
```

**JavaScript:**
```javascript
const values = this.data.map(row => parseFloat(row[field]));
```

### 3. Datei-I/O
**Python:**
```python
with open(filename, 'r') as file:
    data = file.read()
```

**JavaScript:**
```javascript
const data = await fs.promises.readFile(filename, 'utf8');
```

### 4. Type Hints → JSDoc
**Python:**
```python
def calculate_statistics(self) -> Dict:
    pass
```

**JavaScript:**
```javascript
/**
 * @returns {Object} Statistik-Objekt
 */
calculateStatistics() {
    // ...
}

## Sprachvergleich

| Feature | Python | JavaScript |
|---------|--------|------------|
| **Typisierung** | Optionale Type Hints | JSDoc oder TypeScript |
| **Async** | Standardmäßig synchron | Standardmäßig asynchron (Node.js) |
| **Datei-I/O** | Eingebaut, synchron | Benötigt fs-Modul, asynchron |
| **CSV** | Eingebautes csv-Modul | Benötigt csv-parser |
| **Arrays** | List Comprehensions | Array-Methoden (map, filter) |
| **Klassen** | class-Schlüsselwort | class-Schlüsselwort (ES6+) |
| **Module** | import/from | require/module.exports |

## Angewandte Best Practices

### Python Best Practices
- ✅ Type Hints für Klarheit
- ✅ Context Manager für Ressourcen
- ✅ List Comprehensions für Lesbarkeit
- ✅ Docstrings für Dokumentation
- ✅ PEP 8 Style Guide

### JavaScript Best Practices
- ✅ JSDoc für Typdokumentation
- ✅ Async/await für asynchrone Operationen
- ✅ Promises für asynchrone Muster
- ✅ Fehlerbehandlung mit try/catch
- ✅ Moderne ES6+-Syntax
- ✅ Modulexporte für Wiederverwendbarkeit

## Häufige Übersetzungsherausforderungen

### Herausforderung 1: Synchron vs Asynchron
**Problem**: Pythons synchrones I/O vs JavaScripts asynchrones I/O

**Lösung**: Async/await in JavaScript verwenden
```javascript
async loadData() {
    await fs.promises.readFile(this.filename);
}
```

### Herausforderung 2: Eingebaute Bibliotheken
**Problem**: Pythons umfangreiche Standardbibliothek vs JavaScripts minimaler Kern

**Lösung**: npm-Pakete verwenden
```bash
npm install csv-parser
```

### Herausforderung 3: List Comprehensions
**Problem**: Pythons prägnante List Comprehensions

**Lösung**: Array-Methoden verwenden
```javascript
// Python: [x*2 for x in numbers if x > 0]
// JavaScript:
numbers.filter(x => x > 0).map(x => x * 2)
```

### Herausforderung 4: Typsicherheit
**Problem**: Pythons optionale Typisierung vs JavaScripts dynamische Typisierung

**Lösung**: JSDoc oder TypeScript verwenden
```javascript
/**
 * @param {string} filename
 * @returns {Promise<void>}
 */
async loadData(filename) { }
```

## Nächste Schritte

### Mehr Übersetzungen üben
Versuchen Sie zu übersetzen:
1. **Web Scraper** - Python requests → JavaScript axios
2. **API-Server** - Python Flask → JavaScript Express
3. **Datenanalyse** - Python pandas → JavaScript Datenbibliotheken
4. **CLI-Tool** - Python argparse → JavaScript commander

### Erweiterte Themen erkunden
- TypeScript für bessere Typsicherheit
- Asynchrone Iteratoren in JavaScript
- Generator-Funktionen
- Funktionale Programmiermuster
- Leistungsoptimierung

### Plattformübergreifende Tools erstellen
- Bibliotheken erstellen, die in beiden Sprachen funktionieren
- APIs erstellen, die von beiden konsumiert werden können
- Tools entwickeln, die die Stärken jeder Sprache nutzen

## Fehlerbehebung

### Python-Probleme

**Problem**: `ModuleNotFoundError: No module named 'csv'`
```bash
# csv ist eingebaut, Python-Version prüfen
python --version  # Sollte 3.x sein
```

**Problem**: Type Hint-Fehler
```bash
# Type Hints sind optional, Code läuft trotzdem
# Oder Python 3.8+ für bessere Unterstützung verwenden
```

### JavaScript-Probleme

**Problem**: `Cannot find module 'csv-parser'`
```bash
npm install csv-parser
```

**Problem**: Async/await funktioniert nicht
```bash
# Node.js 14+ für vollständige async/await-Unterstützung sicherstellen
node --version
```

**Problem**: Datei nicht gefunden-Fehler
```bash
# Überprüfen, ob Dateipfade relativ zum Ausführungsverzeichnis sind
# path.join() für plattformübergreifende Pfade verwenden
const path = require('path');
const filePath = path.join(__dirname, 'data.csv');
```

## Zusätzliche Ressourcen

### Python-Ressourcen
- [Python-Dokumentation](https://docs.python.org/)
- [Type Hints Leitfaden](https://docs.python.org/3/library/typing.html)
- [CSV-Modul](https://docs.python.org/3/library/csv.html)

### JavaScript-Ressourcen
- [Node.js-Dokumentation](https://nodejs.org/docs/)
- [MDN JavaScript-Leitfaden](https://developer.mozilla.org/de/docs/Web/JavaScript)
- [csv-parser](https://www.npmjs.com/package/csv-parser)

### Übersetzungsleitfäden
- [Python zu JavaScript Cheat Sheet](https://github.com/topics/python-to-javascript)
- [Async-Muster](https://javascript.info/async-await)
- [JSDoc-Leitfaden](https://jsdoc.app/)

## Glossar / Glossary

| Englischer Begriff | Deutscher Begriff | Erklärung |
|-------------------|-------------------|-----------|
| Translation | Übersetzung | Konvertierung von Code zwischen Sprachen |
| Type Hints | Type Hints / Typhinweise | Optionale Typannotationen in Python |
| List Comprehension | List Comprehension | Pythons prägnante Syntax für Listen |
| Context Manager | Context Manager | Pythons with-Statement für Ressourcenverwaltung |
| Async/Await | Async/Await | Asynchrone Programmiermuster |
| Promise | Promise / Versprechen | JavaScripts asynchrones Objekt |
| Array Methods | Array-Methoden | JavaScripts Funktionen für Arrays |
| JSDoc | JSDoc | JavaScript-Dokumentationskommentare |
| Module | Modul | Wiederverwendbare Code-Einheit |
| CSV | CSV | Comma-Separated Values (Komma-getrennte Werte) |

## Feedback

Wie war dieses Lab? Wir würden gerne hören:
- War der Übersetzungsprozess verständlich?
- Waren die Sprach-Mappings klar?
- Welche anderen Sprachen möchten Sie übersetzen?

---

**Herzlichen Glückwunsch zum Abschluss aller drei Bob Bootcamp Labs!** 🎓

Sie haben gemeistert:
- Anwendungen mit Bob erstellen (Lab 1)
- Sicherheitsanalyse und Korrekturen (Lab 2)
- Code-Übersetzung zwischen Sprachen (Lab 3)

**Sie sind jetzt bereit, Bob für reale Entwicklungsprojekte zu verwenden!**

---

**Bereit für mehr?** → [Lab 4 starten: BobShell und Kommandozeilen-Nutzung](../lab4/README.md)

*Zuletzt aktualisiert: Dezember 2025*