# 🧠 Reasoning Strategies

### 🔄 ReAct – Reasoning + Acting

- **ReAct (Reasoning and Acting)** kombiniert schrittweises Überlegen mit der Ausführung von Aktionen.
- Der Agent wechselt zwischen **Reasoning** und **Acting**, wertet neue Beobachtungen aus und passt seine nächsten Schritte dynamisch an.
- Der ursprüngliche Plan kann jederzeit anhand neuer Informationen verändert werden.

**Typischer Ablauf:**

1. 🧠 **Reason** → Aktuelle Situation analysieren und nächsten Schritt bestimmen.
2. 🛠️ **Act** → Eine Aktion über ein Tool ausführen lassen.
3. 🔍 **Observe** → Ergebnis der Aktion auswerten.
4. 🔄 **Repeat** → Nächsten Schritt anhand der neuen Informationen bestimmen.

**Eigenschaften:**
- ✅ **Flexible** → Kann auf unerwartete Situationen und neue Informationen reagieren.
- ⚠️ **Less Predictable** → Der Ablauf kann sich während der Ausführung verändern.
- ⚠️ **Higher Tool Usage** → Mehrere aufeinanderfolgende Tool-Aufrufe können zusätzliche Kosten und Latenz verursachen.

**Use Cases:**
- Offene Aufgaben ohne vollständig bekannten Lösungsweg.
- Recherche und Informationsbeschaffung.
- Incident-Analyse und dynamisches Troubleshooting.

### 📋 Plan-and-Solve – Erst planen, dann ausführen

- **Plan-and-Solve** bedeutet, dass der Agent zunächst einen vollständigen oder weitgehend festgelegten Lösungsplan erstellt und anschließend die einzelnen Schritte abarbeitet.
- Die Ausführung folgt einer vorher definierten Reihenfolge, statt nach jedem Schritt den gesamten Ablauf neu zu planen.

**Typischer Ablauf:**

1. 🎯 **Understand** → Aufgabe und Ziel verstehen.
2. 📝 **Plan** → Notwendige Schritte festlegen.
3. ⚙️ **Execute** → Geplante Schritte nacheinander ausführen.
4. ✅ **Complete** → Ergebnis liefern und Aufgabe abschließen.

**Eigenschaften:**
- ✅ **Structured** → Klarer und nachvollziehbarer Ablauf.
- ✅ **Predictable** → Schritte und Reihenfolge sind weitgehend vorhersehbar.
- ⚠️ **Less Flexible** → Unerwartete Ergebnisse können eine Anpassung oder Neuplanung erforderlich machen.

**Use Cases:**
- Klar definierte und wiederkehrende Aufgaben.
- Standardisierte Datenverarbeitung.
- Automatisierte Workflows mit festen Prozessschritten.

### ⚖️ ReAct vs. Plan-and-Solve

| Kriterium | ReAct | Plan-and-Solve |
|---|---|---|
| Vorgehen | Schrittweise | Erst planen, dann ausführen |
| Flexibilität | Hoch | Geringer |
| Vorhersehbarkeit | Geringer | Höher |
| Anpassung | Laufend | Bei Bedarf neu planen |
| Geeignet für | Offene Aufgaben | Klare Aufgaben |

### 🎯 Choosing the Right Strategy

- 🔄 **ReAct** → Wenn der Lösungsweg nicht vollständig bekannt ist und der Agent flexibel auf neue Informationen reagieren muss.
- 📋 **Plan-and-Solve** → Wenn das Ziel und die notwendigen Arbeitsschritte bereits klar definiert sind.

**Beispiel: Incident Management**

- 🔍 **ReAct** → Ein Agent untersucht einen unbekannten Incident, fragt Monitoring-Daten ab und passt seine Analyse anhand neuer Erkenntnisse an.
- 📋 **Plan-and-Solve** → Ein Agent führt einen standardisierten Incident-Report-Prozess mit festgelegten Schritten aus.

### 🎯 Key Takeaway

**ReAct priorisiert Flexibilität und dynamische Entscheidungen, während Plan-and-Solve auf Struktur und einen vorher festgelegten Ablauf setzt.**


- 🔄 **ReAct** → Think → Act → Observe → Adapt.
- 📋 **Plan-and-Solve** → Plan → Execute → Complete.

# **🛠️ Defining Tools for Agents – Tools für Agenten definieren**

### **🔧 What is a Tool? – Was ist ein Tool?**

- Ein **Tool** ist eine externe Funktion oder Schnittstelle, die einem AI-Agenten ermöglicht, Aufgaben außerhalb seiner eigentlichen Sprachverarbeitung auszuführen.
- Tools erweitern die Fähigkeiten eines Agenten, indem sie ihm Zugriff auf externe Systeme, Daten oder ausführbare Funktionen geben.
- Dadurch kann ein Agent nicht nur Informationen generieren, sondern auch aktiv Aktionen durchführen.
- **Beispiele:**
  - 🔍 **Search Tool** → Sucht nach aktuellen Informationen im Internet oder in Wissensquellen.
  - 💻 **Code Execution** → Führt Python-Code aus, um Berechnungen oder Datenanalysen durchzuführen.
  - 🗄️ **Data Retrieval** → Ruft Informationen aus Datenbanken oder APIs ab.
  - 📧 **External Actions** → Führt Aktionen aus, z. B. E-Mails versenden oder Termine erstellen.

### **🗂️ Tool Categories – Tool-Kategorien**

- 🔍 **Search Tools** → Beschaffen Informationen aus externen Quellen, beispielsweise Websuche oder Dokumentensuche.
- 💻 **Code Execution Tools** → Führen Code aus und ermöglichen komplexe Berechnungen, Datenverarbeitung und Analysen.
- 🗄️ **Data Retrieval Tools** → Greifen auf Datenbanken, APIs oder andere Datenquellen zu und liefern relevante Informationen.
- ⚙️ **Action Tools** → Führen konkrete Aktionen in externen Anwendungen oder Systemen aus.

### **🎯 Precise Tool Definitions – Präzise Tool-Definitionen**

- Eine **Tool-Definition** beschreibt eindeutig, welche Funktion ein Tool erfüllt und wie ein Agent es verwenden kann.
- Dazu gehören:
  - **Name** → Eindeutige Bezeichnung des Tools.
  - **Description** → Beschreibung der Funktion und des Einsatzzwecks.
  - **Parameters** → Festgelegte Eingabeparameter, beispielsweise Suchbegriff oder Kunden-ID.
  - **Return Value** → Definiertes Rückgabeformat und die gelieferten Ergebnisse.
- **Warum ist Präzision wichtig?**
  - ✅ **Reliability** → Der Agent kann das passende Tool gezielter auswählen.
  - ✅ **Consistency** → Einheitliche Ein- und Ausgaben reduzieren Fehler.
  - ✅ **Predictability** → Das Verhalten des Agenten wird besser vorhersehbar.
  - ⚠️ **Ambiguity** → Unklare Beschreibungen können dazu führen, dass der Agent falsche Tools auswählt oder Parameter falsch übergibt.

### **🤖 Model vs. Application Responsibility – Verantwortung zwischen Modell und Anwendung**

\- Bei einem Agenten werden die Aufgaben zwischen dem **AI-Modell** und der **Anwendung (Application)** aufgeteilt.

**🧠 Model – Verantwortung des Modells**

- Versteht die Benutzeranfrage.
- Entscheidet, welches Tool für die Aufgabe geeignet ist.
- Erstellt den Tool-Aufruf mit den benötigten Parametern.
- Interpretiert die zurückgegebenen Ergebnisse und entscheidet über die nächsten Schritte.

**⚙️ Application – Verantwortung der Anwendung**

- Stellt die verfügbaren Tools bereit und definiert deren Schnittstellen.
- Führt die vom Modell angeforderten Tools tatsächlich aus.
- Validiert Eingaben und behandelt Fehler.
- Kontrolliert Berechtigungen und stellt sicher, dass nur erlaubte Aktionen ausgeführt werden.
- Gibt die Ergebnisse an das Modell zurück.

### **🎯 Key Takeaway**

**Tools erweitern Agenten um die Fähigkeit, externe Informationen abzurufen und konkrete Aktionen auszuführen. Präzise Tool-Definitionen sorgen dafür, dass der Agent die richtigen Funktionen zuverlässig verwenden kann.**

# **🔌 Tool Protocols and the Agent Ecosystem – Tool-Protokolle und das Agenten-Ökosystem**

### **🌐 Model Context Protocol (MCP) – Standardisierte Tool-Kommunikation**

- **MCP (Model Context Protocol)** ist ein offenes Protokoll, das standardisiert, wie AI-Anwendungen mit externen Tools, Datenquellen und Services kommunizieren.
- Ein Agent kann über MCP verfügbare Tools automatisch entdecken, ohne dass jedes Tool individuell im Agent-Code programmiert werden muss.
- **Wie funktioniert die Tool-Discovery?**
  1. 🔗 **Connection** → Der Agent bzw. die Anwendung verbindet sich mit einem MCP-Server.
  2. 🔍 **Discovery** → Der Client fragt den Server nach den verfügbaren Tools.
  3. 📋 **Tool Definitions** → Der Server liefert Tool-Namen, Beschreibungen und benötigte Parameter (Schema).
  4. 🧠 **Selection** → Das Modell entscheidet, welches Tool für die aktuelle Aufgabe geeignet ist.
  5. ⚙️ **Execution** → Die Anwendung sendet den Tool-Aufruf an den MCP-Server und erhält das Ergebnis zurück.

### **🛠️ Handwritten vs. Protocol-Based Tool Definitions – Manuelle vs. protokollbasierte Tool-Definitionen**

\- **Handwritten Tool Definitions** → Tools werden direkt im Anwendungscode definiert und implementiert.

- Entwickler müssen Namen, Beschreibungen, Parameter und Ausführungslogik selbst festlegen.
- Änderungen an Tools erfordern häufig Anpassungen am Agent-Code.
- Gut geeignet für kleine, überschaubare Anwendungen mit wenigen Tools.

\- **Protocol-Based Tool Definitions (MCP)** → Tools werden über ein standardisiertes Protokoll von externen MCP-Servern bereitgestellt.

- Der Agent kann verfügbare Tools dynamisch entdecken.
- Tool-Beschreibungen und Parameterschemas werden vom MCP-Server geliefert.
- Neue kompatible Tools können hinzugefügt werden, ohne den Agent-Code individuell anzupassen.
- Gut geeignet für größere Agenten-Systeme mit unterschiedlichen externen Services.

| Kriterium       | Handwritten         | MCP / Protocol-Based         |
| --------------- | ------------------- | ---------------------------- |
| Tool-Definition | Direkt im Code      | Über MCP-Server              |
| Tool-Discovery  | Manuell             | Standardisiert               |
| Erweiterbarkeit | Eher aufwendig      | Flexibler                    |
| Wartung         | Agent-Code anpassen | Oft ohne Agent-Code-Änderung |
| Integration     | Individuell         | Einheitliches Protokoll      |

### **🔄 Maintenance Advantage – Wartungsvorteil**

- Ein wesentlicher Vorteil von MCP ist die **Trennung zwischen Agent und Tool-Implementierung**.
- Solange ein MCP-Server die vereinbarte Protokollschnittstelle und die erwarteten Tool-Schemas beibehält, können interne Änderungen am Tool vorgenommen werden, ohne den Agent-Code anzupassen.
- Auch neue kompatible Tools können bereitgestellt werden, ohne jedes Mal die Agent-Logik umzuschreiben.
- **Beispiel:**
  - Ein Agent verwendet ein Tool `get_customer_data`, um Kundendaten abzurufen.
  - Der MCP-Server ändert intern die Datenbank oder den API-Anbieter.
  - Name, Parameter und Rückgabeformat des Tools bleiben kompatibel.
  - Der Agent kann weiterhin unverändert mit dem Tool arbeiten.

\- **Vorteile:**

- ✅ **Loose Coupling** → Agent und Tool-Implementierung sind voneinander entkoppelt.
- ✅ **Maintainability** → Änderungen können unabhängig voneinander erfolgen.
- ✅ **Scalability** → Neue Tools und Services lassen sich einfacher integrieren.
- ⚠️ **Compatibility** → Änderungen an Tool-Namen, Parametern oder Rückgabeformaten können weiterhin Anpassungen erfordern.

### **🎯 Key Takeaway**

**MCP standardisiert die Kommunikation zwischen Agenten und externen Tools. Dadurch können Agenten Tools dynamisch entdecken und verwenden, ohne jede Integration individuell programmieren zu müssen.**

- 🔍 **Discovery** → Der Agent entdeckt verfügbare Tools über einen MCP-Server.
- 🛠️ **Protocol-Based** → Tool-Definitionen werden standardisiert bereitgestellt statt manuell im Agent-Code hinterlegt.
- 🔄 **Maintenance** → Kompatible Änderungen an der internen Tool-Implementierung benötigen keine Änderung am Agent-Code.
- 🔗 **Loose Coupling** → Agent und Tools können unabhängig voneinander weiterentwickelt werden.

- 🧠 **Model** → Entscheidet, welches Tool wann und mit welchen Parametern verwendet werden soll.
- ⚙️ **Application** → Stellt Tools bereit, führt sie aus und kontrolliert deren Ausführung.
- 🛠️ **Tools** → Verbinden die Fähigkeiten des Agenten mit externen Systemen und Funktionen.
