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
