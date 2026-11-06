# 🎯 Evaluation of LLM Systems Deterministic vs. Probabilistic Metrics

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
