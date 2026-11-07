# 🎯 Evaluation of LLM Systems

### 🧪 What are Evals?

- **Evals (Evaluations)** sind systematische und wiederholbare Tests, mit denen die **Qualität, Zuverlässigkeit und Sicherheit** eines LLM-Systems überprüft werden.
- Sie basieren auf einer Vielzahl von **Testfällen (Test Cases)** und klar definierten **Bewertungskriterien**, statt sich auf einzelne manuelle Tests zu verlassen.

### ⏱️ When to Run Evals?

- 🔧 **During Development** → Regelmäßige Tests während der Entwicklung, um Fehler und Qualitätsprobleme frühzeitig zu erkennen.
- 🚀 **Before Deployment** → Überprüfung, ob das System die definierten Qualitätsanforderungen erfüllt, bevor es produktiv eingesetzt wird.
- 📊 **In Production** → Kontinuierliche Evaluation, um Qualitätsverluste und unerwartete Verhaltensänderungen frühzeitig zu erkennen.

### 🤖 Why are Evals Important for LLMs?

- **LLMs sind probabilistisch** → Derselbe Input kann bei mehreren Durchläufen unterschiedliche Outputs erzeugen.
- **Einzelne Spot-Checks reichen nicht aus** → Wenige manuelle Tests liefern keine zuverlässige Aussage über die tatsächliche Systemqualität.
- **Systematisches Testen ist notwendig** → Mehrere Testdurchläufe helfen, Qualität, Konsistenz und Sicherheit messbar zu bewerten.

### 🎯 Goal of Evals

**Die Qualität eines LLM-Systems systematisch messen und kontinuierlich verbessern.**

- 🔍 **Quality** → Sind die Antworten korrekt und relevant?
- 🔄 **Consistency** → Liefert das System über mehrere Durchläufe hinweg zuverlässige Ergebnisse?
- 🛡️ **Safety** → Hält das System Sicherheitsrichtlinien und definierte Einschränkungen ein?

# ⚖️ Deterministic vs. Probabilistic Metrics

### 🔢 Deterministic Metrics – Deterministische Metriken

- **Deterministische Metriken** bewerten Outputs anhand fester Regeln und eindeutig definierter Kriterien.
- Bei gleichem Input und gleichen Referenzdaten liefern sie immer dasselbe Bewertungsergebnis.

- **Beispiele:**
  - 🎯 **Exact Match** → Prüft, ob der Output exakt mit der erwarteten Antwort übereinstimmt.
  - 🔤 **String Comparison** → Vergleicht zwei Texte auf Zeichenebene.
  - 📋 **Format Validation** → Prüft, ob ein Output ein vorgegebenes Format einhält, z. B. gültiges JSON.

- **Use Cases:**
  - Feste Labels und Klassifikationen.
  - Strikte JSON- und Format-Validierungen.
  - Aufgaben mit eindeutig definierten erwarteten Ergebnissen.

- **Eigenschaften:**
  - ✅ **Reliable & Reproducible** → Objektiv, konsistent und jederzeit reproduzierbar.
  - ⚠️ **Rigid** → Erkennt keine inhaltlich korrekten Antworten, wenn sie anders formuliert sind als erwartet.

### 🎲 Probabilistic Metrics – Probabilistische Metriken

- **Probabilistische Metriken** bewerten Outputs anhand von Wahrscheinlichkeiten, semantischer Bedeutung oder kontextabhängigen Qualitätskriterien.
- Sie berücksichtigen, ob eine Antwort inhaltlich korrekt und sinnvoll ist, auch wenn sie anders formuliert wurde als die Referenzantwort.

- **Beispiele:**
  - 🧠 **Semantic Similarity** → Bewertet, wie ähnlich sich zwei Texte in ihrer Bedeutung sind.
  - 🤖 **LLM-as-a-Judge** → Ein weiteres LLM bewertet die Qualität einer generierten Antwort anhand definierter Kriterien.
  - 👤 **Human Evaluation** → Menschen beurteilen beispielsweise Korrektheit, Relevanz und Verständlichkeit.

- **Use Cases:**
  - Freie Texte und offene Fragen.
  - Erklärungen und Zusammenfassungen.
  - Aufgaben, bei denen die inhaltliche Bedeutung wichtiger ist als der exakte Wortlaut.

- **Eigenschaften:**
  - ✅ **Flexible** → Erkennt auch inhaltlich korrekte Antworten mit unterschiedlicher Formulierung.
  - ⚠️ **Noisy & Subjective** → Bewertungen können variieren und sind abhängig vom Bewertungsmodell oder menschlichen Urteil.

### 🎯 Key Takeaway

**Deterministic Metrics** eignen sich für eindeutig messbare Ergebnisse, während **Probabilistic Metrics** benötigt werden, wenn die inhaltliche Bedeutung und Qualität einer Antwort bewertet werden soll.

- 🔢 **Deterministic** → Ist der Output exakt richtig formatiert oder entspricht er der erwarteten Antwort?
- 🎲 **Probabilistic** → Ist der Output inhaltlich sinnvoll, korrekt und relevant?

# 🤖 LLM-as-a-Judge

### LLM-as-a-Judge

- **LLM-as-a-Judge** bezeichnet den Ansatz, ein LLM als automatisierten Bewerter einzusetzen, um die Antworten eines anderen LLMs anhand definierter Kriterien zu bewerten.
- Beispiel: Ein LLM bewertet die Qualität von automatisch generierten **Incident-Erklärungen**.

### ✅ Suitable Use Cases – Wofür ist es geeignet?

LLM-as-a-Judge eignet sich besonders für **subjektive Qualitätsmerkmale**, die sich nur schwer mit festen Regeln messen lassen:

- 📝 **Clarity** → Ist die Antwort verständlich und klar formuliert?
- 📚 **Structure** → Ist die Antwort logisch und übersichtlich aufgebaut?
- 📖 **Runbook Alignment** → Entspricht die Antwort den Vorgaben und Prozessen des Runbooks?
- 💬 **Tone** → Ist der Kommunikationsstil angemessen?
- ⚠️ **Risk Awareness** → Werden potenzielle Risiken und Warnhinweise berücksichtigt?

### ❌ Limitations – Wofür ist es weniger geeignet?

- 🔍 **Hard Facts** → Exakte Fakten wie Fehlercodes, IDs oder technische Werte überprüfen.
- 📋 **Schema Validation** → Strikte Einhaltung technischer Datenstrukturen und Formate prüfen.
- 🎯 **Factual Accuracy** → Die tatsächliche Wahrheit einer Aussage zuverlässig verifizieren.
- 🔄 **Cross-Call Consistency** → Konsistenz über viele unabhängige Modellaufrufe hinweg sicherstellen.

Für solche Anforderungen sind **deterministische Prüfungen** oder externe Datenquellen zuverlässiger.

### 📊 Evaluation Rubric – Strukturierte Bewertung

- **Wichtig:** Ein LLM-Judge sollte niemals nur allgemein gefragt werden: *„Is this answer good?“*
- Stattdessen sollte eine **klare Bewertungsrubrik (Rubric)** mit definierten Kriterien und strukturierten Scores verwendet werden.

**Beispiel für Bewertungskriterien:**

- 🎯 **Relevance** → Beantwortet die Antwort die eigentliche Frage?
- 📖 **Alignment** → Entspricht sie den Vorgaben des Runbooks?
- 🛠️ **Actionability** → Enthält sie konkrete und umsetzbare Handlungsempfehlungen?
- ⚠️ **Risk Awareness** → Werden Risiken und mögliche Auswirkungen berücksichtigt?

### 🎯 Key Takeaway

**LLM-as-a-Judge** ermöglicht die automatisierte Bewertung subjektiver Qualitätsmerkmale, ersetzt aber keine deterministischen Prüfungen für harte Fakten und technische Anforderungen.

- 🤖 **LLM Judge** → Bewertet Qualität, Verständlichkeit und Kontext.
- 🔢 **Deterministic Checks** → Überprüfen Fakten, Formate und technische Regeln.

# 👤 Human-in-the-Loop (HITL)

### 🧑‍⚖️ When is Human-in-the-Loop Needed?

- **Human-in-the-Loop (HITL)** bedeutet, dass Menschen in den Evaluationsprozess eingebunden werden, um LLM-Ausgaben zu überprüfen und zu bewerten.
- HITL wird benötigt, wenn **automatisches Scoring oder LLM-as-a-Judge allein nicht ausreichen**, um eine zuverlässige Bewertung sicherzustellen.

**Typische Einsatzgebiete:**

- 🚨 **High Stakes** → Kritische Anwendungsbereiche wie Medizin, Finanzen, Recht, Security oder Mental Health mit hohen Risiken bei Fehlentscheidungen.
- 🔍 **Edge Cases** → Neue oder ungewöhnliche Situationen, die durch bestehende Testfälle nicht ausreichend abgedeckt sind.
- 💬 **Subjective Quality** → Bewertung von Ton, Empathie, Angemessenheit und der Frage, ob eine Antwort für Menschen tatsächlich hilfreich ist.

### 🎯 Smart Sampling – Gezielte Stichproben

- **Smart Sampling** bedeutet, nicht 100 % aller LLM-Antworten manuell zu überprüfen, sondern die Überprüfung gezielt nach Risiko und Relevanz zu steuern.

**Vorgehensweise:**

- 📊 **Risk Classification** → Einteilung der Fälle in Risikoklassen, z. B. anhand von `sev-level`, Kundentyp oder Use Case.
- 🚨 **High-Risk Cases** → Alle Fälle mit hohem Risiko werden manuell überprüft.
- 🎲 **Representative Sampling** → Aus Low- und Medium-Risk-Fällen wird eine repräsentative Stichprobe gezogen (z. B. 5–10 %).
- ⚠️ **Trigger-Based Review** → Bestimmte Schlüsselereignisse lösen automatisch eine manuelle Überprüfung aus, z. B. „Datenverlust“, „Security Incident“ oder „Compliance-Verstoß“.

**Ziel:** Hohe Sicherheit und Qualität bei gleichzeitig vertretbarem manuellem Aufwand.

### 📋 Reviewer Guidelines – Einheitliche Bewertung

- **Reviewer Guidelines** sind klare Vorgaben und Checklisten, die sicherstellen, dass verschiedene Reviewer LLM-Ausgaben nach denselben Kriterien bewerten.
- Beispiel: Evaluation eines **Incident-RAG-Systems** anhand von drei zentralen Kriterien:

**1. 🔐 Access & Privacy**
- Dürfen die angezeigten Informationen diesem Benutzer oder System überhaupt zugänglich gemacht werden?
- Werden Datenschutz- und Berechtigungsregeln eingehalten?

**2. 🚨 Correct Routing**
- Werden Security-, Compliance- oder High-Severity-Incidents korrekt eskaliert?
- Werden die richtigen Ansprechpartner eingebunden (z. B. Incident Commander, Security-Team oder On-Call)?

**3. 🔍 Facts & Hallucinations**
- Sind Root-Cause-Behauptungen durch die verfügbaren Kontextdaten belegt?
- Werden keine unbelegten Ursachen, Fakten oder Maßnahmen erfunden?

### 🎯 Key Takeaway

**Human-in-the-Loop ergänzt automatisierte Evaluation durch menschliches Urteilsvermögen und Risikobewertung.**

- 🤖 **Automated Evaluation** → Schnelle und skalierbare Überprüfung vieler Antworten.
- 👤 **Human Review** → Detaillierte Bewertung kritischer, ungewöhnlicher oder subjektiver Fälle.
- 📊 **Smart Sampling** → Gezielte Überprüfung statt manueller Kontrolle aller Antworten.

**Ergebnis:** Konsistentere Bewertungen, frühzeitige Erkennung von Risiken und eine kontinuierliche Verbesserung des LLM-Systems.
