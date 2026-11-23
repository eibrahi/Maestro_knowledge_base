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

- 🧠 **LLM** → Entscheidet, welche Funktion benötigt wird.
- ⚙️ **Python Application** → Führt die angeforderte Funktion aus.
- 📤 **Tool Result** → Liefert das Ergebnis zurück an das LLM.
- 🤖 **Agent** → Kann das Ergebnis für weitere Aktionen und Entscheidungen nutzen.
