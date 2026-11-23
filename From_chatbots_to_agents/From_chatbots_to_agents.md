# 🤖 From Chatbots to Agents

### 💬 Chatbots vs. AI Agents

- **Chatbots** sind darauf ausgelegt, auf Benutzereingaben zu reagieren und passende Antworten zu generieren.
- **AI Agents** gehen einen Schritt weiter: Sie verfolgen ein definiertes Ziel und können selbstständig mehrere Aktionen ausführen, um dieses Ziel zu erreichen.

**Die wichtigsten Unterschiede:**

- 💬 **Chatbot** → Reagiert auf Fragen und liefert Antworten.
- 🎯 **Agent** → Verfolgt ein Ziel und führt aktiv Aufgaben aus.
- 🛠️ **Tool Usage** → Agents können externe Werkzeuge und APIs nutzen, um Informationen abzurufen oder Aktionen auszuführen.
- 🔄 **Multi-Step Reasoning** → Agents können Aufgaben in mehrere Schritte zerlegen und diese nacheinander bearbeiten.

### 🎯 Goal-Oriented Behavior – Zielorientiertes Verhalten

- **Goal-Oriented Behavior** bedeutet, dass ein Agent nicht nur auf eine einzelne Eingabe reagiert, sondern auf ein definiertes Ergebnis hinarbeitet.
- Er entscheidet anhand des Ziels, welche Schritte notwendig sind, und überprüft, ob das gewünschte Ergebnis erreicht wurde.

**Beispiel: Incident Management**

- 💬 **Chatbot** → Erklärt, wie ein Security Incident behandelt werden sollte.
- 🤖 **Agent** → Analysiert den Incident, sucht relevante Informationen im Runbook, prüft den Status über eine API und erstellt ein Incident-Ticket.

### 🛠️ Tool Usage – Werkzeugnutzung

- Agents können externe Tools verwenden, um ihre Fähigkeiten über die reine Textgenerierung hinaus zu erweitern.

**Beispiele:**

- 🔍 **Search APIs** → Informationen und Daten abrufen.
- 🗄️ **Database Queries** → Datenbanken abfragen.
- 🔌 **External APIs** → Mit anderen Systemen kommunizieren.
- ⚙️ **Actions** → Tickets erstellen, Status aktualisieren oder Workflows auslösen.

### 🔄 Multi-Step Reasoning – Mehrschrittige Aufgabenbearbeitung

- **Multi-Step Reasoning** beschreibt die Fähigkeit eines Agents, komplexe Aufgaben in mehrere aufeinanderfolgende Schritte zu zerlegen.
- Die Ergebnisse eines Schrittes dienen als Grundlage für die nächsten Aktionen.
- Der Agent kann seinen weiteren Ablauf anhand der Zwischenergebnisse anpassen.

**Typischer Agent Workflow:**

1. 🎯 **Goal** → Ziel und Aufgabe verstehen.
2. 📋 **Planning** → Notwendige Schritte festlegen.
3. 🛠️ **Action** → Tools und APIs ausführen.
4. 🔍 **Observation** → Ergebnisse der Aktionen überprüfen.
5. 🔄 **Iteration** → Bei Bedarf weitere Schritte ausführen.
6. ✅ **Completion** → Ergebnis liefern oder Aufgabe abschließen.

### 🚀 From Answering to Doing

- Der zentrale Unterschied beim Wechsel von Chatbots zu Agents ist der Übergang von der reinen **Informationsbereitstellung zur zielorientierten Aufgabenerledigung**.

- 💬 **Chatbot** → Answers Questions.
- 🤖 **Agent** → Achieves Goals.
- 🛠️ **Agentic Systems** → Combine LLMs, Tools, Planning and Actions to complete complex tasks.

### 🎯 Key Takeaway

**Chatbots generate answers. AI Agents use reasoning and tools to accomplish goals.**

Der Agent arbeitet nicht nur mit Sprache, sondern kann aktiv mit seiner Umgebung und externen Systemen interagieren.

# 🔧 Introduction to Function Calling

### 🤖 What is Function Calling?

- **Function Calling** ermöglicht einem LLM, externe Funktionen und Tools gezielt anzufordern, um Aufgaben auszuführen, die über die reine Textgenerierung hinausgehen.
- Das Modell führt die Funktion dabei **nicht selbst aus**, sondern entscheidet, wann und mit welchen Parametern eine Funktion aufgerufen werden soll.
- Die eigentliche Ausführung übernimmt die Anwendung (z. B. Python).

### 🔄 How Function Calling Works

**Der typische Ablauf besteht aus vier Schritten:**

1. 🧠 **Model Requests Action** → Das LLM erkennt, dass eine externe Funktion benötigt wird, und fordert deren Ausführung mit den passenden Parametern an.
2. ⚙️ **Application Executes Function** → Die Python-Anwendung empfängt den Funktionsaufruf und führt die entsprechende Funktion aus.
3. 📤 **Tool Result** → Das Ergebnis der Funktion wird zurück an das LLM übergeben.
4. 🤖 **Model Generates Response** → Das LLM verarbeitet das Ergebnis und erstellt eine Antwort oder entscheidet über den nächsten Tool-Aufruf.

### 🛠️ Function Calling in AI Agents

- **Function Calling ist eine zentrale Grundlage für Tool-Nutzung in AI Agents.**
- Dadurch können LLMs mit externen Systemen interagieren und konkrete Aktionen auslösen.

**Beispiele:**

- 🔍 **Search** → Informationen über eine API abrufen.
- 🗄️ **Database Query** → Daten aus einer Datenbank lesen.
- 🎫 **Ticket Creation** → Ein Incident-Ticket erstellen.
- 📊 **Data Retrieval** → Aktuelle System- oder Monitoring-Daten abrufen.

### 🎯 Key Takeaway

**Function Calling verbindet die Entscheidungsfähigkeit eines LLMs mit der Ausführungsfähigkeit einer Anwendung.**

# 📋 Structured Outputs for Agents

### 🎯 Why Structured Outputs?

- **Structured Outputs** ermöglichen es einem LLM, Antworten in einem fest definierten Datenformat zu erzeugen, beispielsweise als JSON.
- Für Agents ist das besonders wichtig, da Tools und APIs häufig **strukturierte Eingaben mit definierten Feldern und Datentypen** benötigen.
- Freie Textausgaben sind für Menschen verständlich, aber für Anwendungen schwerer zuverlässig zu verarbeiten.

**Beispiel:**

- 💬 **Unstructured Output** → „Suche bitte nach dem Incident mit der ID INC-123.“
- 📋 **Structured Output** → Ein JSON-Objekt mit den Feldern `action` und `incident_id`.

### 🔄 Processing JSON with Python

- **JSON (JavaScript Object Notation)** ist ein standardisiertes Datenformat für den Austausch strukturierter Informationen.
- Mit `json.loads(...)` kann ein JSON-String in ein Python-Objekt umgewandelt werden.
- JSON-Objekte werden in Python normalerweise als **Dictionary (`dict`)** dargestellt.

**Beispiel:**

```python
import json

response = '{"action": "get_incident", "incident_id": "INC-123"}'

data = json.loads(response)

print(data["action"])
print(data["incident_id"])
```

**Ergebnis:**

```text
get_incident
INC-123
```

### ⚠️ Handling Missing Fields

- Ein valides JSON bedeutet nicht automatisch, dass alle benötigten Felder vorhanden sind.
- **Missing Fields** müssen erkannt und behandelt werden, bevor die Anwendung eine Funktion oder ein Tool aufruft.

**Beispiel:**

```python
required_fields = ["action", "incident_id"]

for field in required_fields:
    if field not in data:
        raise ValueError(f"Missing field: {field}")
```

- 🔍 **Field Validation** → Prüft, ob benötigte Felder vorhanden sind.
- 🛡️ **Type Validation** → Prüft, ob Werte den erwarteten Datentyp besitzen.
- ⚠️ **Error Handling** → Verhindert, dass fehlerhafte Daten unkontrolliert an Tools weitergegeben werden.

### 📝 Prompt Formatting vs. JSON Mode vs. Output Schemas

**1. 📝 Prompt Formatting**

- Das Modell wird durch eine Textanweisung aufgefordert, JSON zurückzugeben.
- Beispiel: „Return your answer as valid JSON.“
- **Limitation:** Das Modell kann die Anweisung trotzdem falsch interpretieren oder zusätzliche Informationen ausgeben.

**2. 📋 JSON Mode**

- Der API-Aufruf aktiviert einen speziellen Modus, der eine syntaktisch gültige JSON-Ausgabe sicherstellt.
- **Limitation:** JSON Mode garantiert nicht, dass alle benötigten Felder vorhanden sind oder die Ausgabe einem bestimmten Schema entspricht.

**3. 🛡️ Structured Outputs / Output Schemas**

- Ein definiertes **Schema** beschreibt die erwartete Struktur, die Felder und die Datentypen.
- Das Modell wird so eingeschränkt, dass die Ausgabe dem vorgegebenen Schema entspricht.
- Beispiel: `action` muss ein String sein und `incident_id` muss ebenfalls ein String sein.

### ⚖️ Why are Schemas More Reliable?

- **Schemas definieren die erwartete Struktur explizit**, anstatt sie nur durch eine Textanweisung zu beschreiben.
- Dadurch werden fehlerhafte oder unvollständige Tool-Argumente deutlich reduziert.

**Vorteile:**

- 📋 **Consistency** → Einheitliche Datenstruktur.
- 🔍 **Validation** → Definierte Felder und Datentypen.
- ⚙️ **Reliability** → Zuverlässigere Verarbeitung durch Python-Anwendungen und APIs.
- 🛡️ **Error Prevention** → Weniger Fehler bei der Übergabe an Tools.

**Wichtig:** Auch Structured Outputs garantieren nicht, dass die enthaltenen Informationen sachlich korrekt sind oder eine Aktion ausgeführt werden darf. Fachliche Validierung und Berechtigungsprüfungen bleiben notwendig.

### 🎯 Key Takeaway

**Structured Outputs verbinden die flexible Textgenerierung eines LLMs mit der zuverlässigen Datenverarbeitung einer Anwendung.**

- 📝 **Prompt Formatting** → Beschreibt das gewünschte Format durch Textanweisungen.
- 📋 **JSON Mode** → Garantiert grundsätzlich gültiges JSON, aber keine bestimmte Struktur.
- 🛡️ **Output Schema** → Definiert die erwartete Struktur und erhöht die Zuverlässigkeit der Ausgabe.

- 🧠 **LLM** → Entscheidet, welche Funktion benötigt wird.
- ⚙️ **Python Application** → Führt die angeforderte Funktion aus.

# 🔄 The Agentic Loop

### 🤖 What is the Agentic Loop?

- Der **Agentic Loop** beschreibt den wiederkehrenden Arbeitszyklus eines AI Agents, mit dem er ein definiertes Ziel schrittweise verfolgt.
- Anders als ein klassischer Chatbot, der hauptsächlich Antworten generiert, kann ein Agent Informationen aufnehmen, Entscheidungen treffen, Aktionen ausführen und deren Ergebnisse auswerten.
- Der Ablauf wiederholt sich so lange, bis das Ziel erreicht ist oder der Agent den Prozess beendet.

### 🔄 The Five Steps of the Agentic Loop

1. 👁️ **Perceive (Wahrnehmen)**
   - Der Agent erhält eine Benutzeranfrage oder neue Informationen aus seiner Umgebung.
   - Beispiel: Ein Benutzer meldet einen Security Incident.

2. 🧠 **Reason (Überlegen)**
   - Das LLM analysiert die verfügbaren Informationen und entscheidet, welcher nächste Schritt notwendig ist.
   - Beispiel: Das Modell erkennt, dass weitere Incident-Daten benötigt werden.

3. 🛠️ **Act (Handeln)**
   - Das Modell fordert über einen **Function Call** die Ausführung einer bestimmten Funktion mit definierten Parametern an.
   - Die Anwendung (z. B. Python) führt die angeforderte Funktion aus.
   - Beispiel: Eine API wird aufgerufen, um den Incident-Status abzurufen.

4. 🔍 **Observe (Beobachten)**
   - Das Ergebnis der ausgeführten Aktion wird zurück an das LLM übergeben.
   - Der Agent wertet die neuen Informationen aus.
   - Beispiel: Die API meldet, dass der Incident bereits eskaliert wurde.

5. 🔄 **Repeat or Stop (Wiederholen oder Beenden)**
   - Der Agent entscheidet anhand der neuen Informationen, ob weitere Aktionen notwendig sind oder das Ziel erreicht wurde.
   - Beispiel: Sind alle Informationen vorhanden, erstellt der Agent eine Zusammenfassung und beendet den Prozess.

### 🎯 Course Correction – Kurskorrektur

- **Course Correction** bedeutet, dass ein Agent seinen ursprünglichen Plan anhand neuer Beobachtungen anpassen kann.
- Die Ergebnisse vorheriger Aktionen beeinflussen die nächsten Entscheidungen.
- Dadurch muss ein Agent nicht einem starren Ablauf folgen, sondern kann flexibel auf unerwartete Ergebnisse reagieren.

**Beispiel:**

- 🔍 **Observation** → Eine API liefert keine Incident-Daten.
- 🧠 **Re-evaluation** → Das LLM erkennt, dass die Incident-ID möglicherweise falsch ist.
- 🔄 **Course Correction** → Der Agent fordert eine Überprüfung der ID an oder verwendet eine alternative Suchfunktion.
- 🛠️ **Next Action** → Die Suche wird mit den korrigierten Informationen erneut ausgeführt.

### ⚙️ Function Calling – Model vs. Application

- **Wichtig:** Das LLM führt externe Funktionen nicht selbst aus. Es schlägt eine Aktion vor und übergibt die erforderlichen Parameter.
- Die eigentliche Ausführung übernimmt die Anwendung.

**Aufgabenteilung:**

- 🧠 **LLM** → Entscheidet, welche Aktion notwendig ist, und erzeugt einen Function Call.
- ⚙️ **Application (Python)** → Prüft und führt die angeforderte Funktion aus.
- 📤 **Tool Result** → Liefert das Ergebnis zurück an das LLM.
- 🔄 **LLM** → Bewertet das Ergebnis und entscheidet über den nächsten Schritt.

### 🎯 Key Takeaway

**Der Agentic Loop ermöglicht es einem AI Agent, komplexe Aufgaben durch wiederholtes Wahrnehmen, Überlegen, Handeln und Beobachten zielorientiert zu erledigen.**

- 👁️ **Perceive** → Informationen aufnehmen.
- 🧠 **Reason** → Nächsten Schritt bestimmen.
- 🛠️ **Act** → Aktion über ein Tool anfordern und ausführen lassen.
- 🔍 **Observe** → Ergebnis auswerten.
- 🔄 **Repeat or Stop** → Plan anpassen oder Ziel abschließen.
- 📤 **Tool Result** → Liefert das Ergebnis zurück an das LLM.
- 🤖 **Agent** → Kann das Ergebnis für weitere Aktionen und Entscheidungen nutzen.
