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

# ⚡ Handling Latency and Rate Limits

### ⏱️ LLM-Latenz

- Die **Latenz eines LLMs** wird hauptsächlich durch folgende Faktoren beeinflusst:
  - 🧠 **Model-Compute** → Rechenaufwand des Modells
  - 📝 **Prompt- und Antwortlänge** → Umfang der Eingabe und generierten Ausgabe
  - ☁️ **Provider-Kapazität** → Verfügbare Rechenressourcen des Anbieters

- **User Experience**:
  - Nutzer nehmen vor allem die **Wartezeit** wahr, nicht einzelne Millisekunden.
  - Eine wichtige Kennzahl ist die **Time to First Token (TTFT)** → Zeit bis zur Ausgabe des ersten Tokens.

### 🚀 Perceived Speed – Wahrgenommene Geschwindigkeit

- 🌊 **Streaming**
  - Erste Tokens werden bereits während der Generierung ausgegeben.
  - Verbessert die **wahrgenommene Geschwindigkeit**, obwohl die Gesamtzeit gleich oder ähnlich bleibt.
  - **Ideale Use Cases:** Chat-Anwendungen, AI Assistants und IDE-Hilfen.

- 📦 **Batching**
  - Mehrere unabhängige Requests werden in einem Call zusammengefasst.
  - Ermöglicht einen **höheren Durchsatz** und reduziert den **Overhead**.
  - **Ideale Use Cases:** Offline- und Bulk-Jobs wie Ticketverarbeitung, Log-Analysen und Reviews.

### 🚦 Rate Limits & Retries

- 🔐 **HTTP 401 – Authentication Error**
  - Ursache: **Authentifizierungs- oder API-Key-Problem**.
  - Lösung: **API-Key und Konfiguration überprüfen und korrigieren**.
  - ⚠️ **Keine wiederholten Retries**, solange das Authentifizierungsproblem besteht.

- ⚠️ **HTTP 429 – Rate Limit / Quota Exceeded**
  - Ursache: **Rate Limit oder Quota** erreicht.
  - Lösung: **Anfragefrequenz reduzieren** und eine geeignete Retry-Strategie implementieren.
  - **Exponential Backoff** → Wartezeit zwischen Wiederholungsversuchen schrittweise erhöhen:
    - `1s → 2s → 4s → 8s → …`
  - Optional **Jitter** hinzufügen, um gleichzeitige Wiederholungsversuche zu vermeiden.

# 🔍 Tracing the Call Chain

### 🔗 Request Trace

- Ein **Request Trace** bildet die vollständige Spur **einer einzelnen Anfrage** durch alle Schritte der Pipeline ab.
- Dadurch lässt sich nachvollziehen, welche Komponenten und Prozesse während der Verarbeitung durchlaufen werden.

### ⏱️ Trace-Timeline & Bottleneck-Analyse

- Eine **Trace-Timeline** visualisiert den zeitlichen Ablauf der einzelnen Verarbeitungsschritte.
- Sie ermöglicht die schnelle Identifikation von **Bottlenecks (Engpässen)** innerhalb der Pipeline.
- Dadurch wird sichtbar, **welcher Schritt die Performance beeinträchtigt**.

### ⚠️ Typische Performance-Patterns

- 🔍 **Langsames Retrieval**
  - Die Suche und Bereitstellung relevanter Informationen benötigt zu viel Zeit.

- 💰 **Teures Re-Ranking**
  - Die erneute Bewertung und Sortierung abgerufener Dokumente verursacht hohen Zeit- oder Ressourcenaufwand.

- 🔄 **Redundante API-Calls**
  - Unnötige oder doppelte API-Aufrufe erhöhen Latenz und Kosten.
  - Beispiel: **Doppeltes Retrieval** derselben Informationen.

### 🤖 Bedeutung von Tracing bei RAG & AI Agents

- Bei **RAG-Systemen und AI Agents** ist Tracing besonders wichtig, da eine Anfrage mehrere Verarbeitungsschritte und Komponenten durchläuft.
- Im Gegensatz zu einem **einfachen LLM-Call** entstehen zusätzliche Abhängigkeiten und potenzielle Fehlerquellen.
- **Tracing** ermöglicht es, diese Abläufe transparent nachzuvollziehen und gezielt zu optimieren.
