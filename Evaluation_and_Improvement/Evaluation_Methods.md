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
