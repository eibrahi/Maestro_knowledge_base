# 🐛 The Challenge of Debugging GenAI

### 🎲 Nicht-reproduzierbare Outputs

- **LLMs sind probabilistisch** → Gleicher Input kann unterschiedliche Antworten liefern.
- Klassisches Debugging nach dem Prinzip **„Bug einmal reproduzieren und fixen“** ist daher nur eingeschränkt effektiv.

### 📝 Prompt-Sensitivität

- **Prompts sind im Grunde Code** → Kleine Textänderungen oder veränderte Constraints können das Verhalten eines LLMs stark beeinflussen.
- Bereits minimale Anpassungen können zu erheblichen Unterschieden im **Output** führen.

### 🔍 Hidden Reasoning

- Sichtbar sind lediglich **Input und Output**, nicht der tatsächliche interne Entscheidungsweg des Modells.
- Klassische Debugging-Tools wie **Breakpoints** oder **State-Inspektion** greifen daher ins Leere.

### 🎯 Ergebnis

**Mehr Logs und Breakpoints allein reichen nicht aus.**

GenAI benötigt eigene **Debugging-Strategien**, die folgende Aspekte berücksichtigen:

- 🔄 **Multiple Runs** → Analyse über mehrere Durchläufe
- 📊 **Mustererkennung** → Identifikation wiederkehrender Verhaltensweisen
- ⚙️ **Prompt- und Parameter-Design** → Systematische Optimierung von Prompts und Modellparametern

# 🔍 What is Observability in LLM Apps?

### 📊 Observability

- **Observability** bezeichnet die Fähigkeit, anhand von **Logs, Metriken und Traces** zu verstehen, *warum* sich ein **LLM-System** auf eine bestimmte Weise verhält.

### 📝 Logging

- **Detaillierte Informationen pro Request**:
  - 📥 **Prompt** → Eingabe an das LLM
  - 📤 **Response** → Generierte Antwort
  - 🔢 **Tokens** → Tokenverbrauch
  - 🤖 **Model-Version** → Verwendete Modellversion
  - ⚠️ **Errors** → Aufgetretene Fehler

### 📈 Monitoring

- **Aggregierte Sicht auf die Gesundheit und Performance des Systems**:
  - ⏱️ **Latenz** → Antwortzeit des Systems
  - 🚨 **Fehlerrate** → Häufigkeit auftretender Fehler
  - 💰 **Tokenverbrauch** → Verbrauchte Tokens

### 🔗 Tracing

- **Tracing** ermöglicht die Nachverfolgung des **kompletten Ablaufs eines einzelnen Requests** durch den gesamten **LLM-Flow**.

# 💰 Cost Optimization

### 🧮 Berechnung der LLM-Kosten

- **LLM-Kosten** werden anhand der verbrauchten **Input- und Output-Tokens** sowie der jeweiligen **Tokenpreise** berechnet.

### ⚙️ Die drei wichtigsten Optimierungshebel

- 📝 **Prompt kürzen**
  - Unnötige Informationen entfernen.
  - Wichtigen Kontext beibehalten.

- 🤖 **Kleineres Modell verwenden**
  - Für einfache Aufgaben wie beispielsweise **Umformulierungen** ein kleineres Modell einsetzen.

- 🔄 **Caching einsetzen**
  - Wiederholte oder identische Anfragen zwischenspeichern.
  - Beispiel: **HR-FAQ** mit häufig gestellten Fragen.

### ⚠️ Risiken bei der Kostenoptimierung

Eine zu starke Optimierung kann die **Qualität und Zuverlässigkeit** des LLM-Systems beeinträchtigen.

- 🔍 **Zu stark gekürzte Prompts**
  - Bei komplexem Debugging können wichtige Informationen verloren gehen.

- 🗄️ **Falsches Caching**
  - Bei sich schnell ändernden Daten können veraltete oder unpassende Antworten zurückgegeben werden.
