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

- 🧠 **Model** → Entscheidet, welches Tool wann und mit welchen Parametern verwendet werden soll.
- ⚙️ **Application** → Stellt Tools bereit, führt sie aus und kontrolliert deren Ausführung.
- 🛠️ **Tools** → Verbinden die Fähigkeiten des Agenten mit externen Systemen und Funktionen.
