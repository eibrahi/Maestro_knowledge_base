# ⚙️ Building an Eval Pipeline

### 🔄 Eval Pipeline – End-to-End Evaluation

- Eine **Eval-Pipeline** automatisiert den gesamten Evaluationsprozess eines LLM-Systems – von den Testdaten bis zur Auswertung der Ergebnisse.

**Die vier zentralen Schritte:**

1. 📚 **Test Dataset** → Sammlung definierter Testfälle mit Fragen, Kontexten und erwarteten Ergebnissen.
2. 🧪 **Eval Functions** → Ausführung verschiedener Evaluationsfunktionen, z. B. Exact Match, Faithfulness oder LLM-as-a-Judge.
3. 📊 **Scoring** → Berechnung und Zusammenfassung der Bewertungsergebnisse anhand definierter Metriken.
4. 📈 **Reporting** → Erstellung eines Reports mit Scores, Fehlern und erkannten Qualitätsproblemen für Engineers.

### 🚀 Integration into the Dev Workflow

- **Ziel:** Evaluationen automatisch in den Entwicklungs- und Deployment-Prozess integrieren, um Qualitätsprobleme frühzeitig zu erkennen.

**Vorgehensweise:**

- ⚡ **Clear Triggers** → Definieren, wann die Eval-Pipeline gestartet wird, z. B. bei Code-Änderungen, Prompt-Anpassungen oder vor einem Deployment.
- 🔄 **Automated Execution** → Die Pipeline führt die definierten Tests automatisch aus.
- 📊 **Engineering Report** → Die Ergebnisse werden dokumentiert und den Engineers zur Verfügung gestellt.
- 🚨 **Quality Gates** → Bei Unterschreitung definierter Qualitätsgrenzen kann ein Deployment blockiert werden.

### 🌱 Continuous Improvement – Die Pipeline als lebendes System

- Eine **Eval-Pipeline ist kein einmaliges Test-Setup**, sondern muss kontinuierlich erweitert und verbessert werden.
- Fehler aus der Produktion liefern neue Erkenntnisse für zukünftige Evaluationen.

**Continuous Improvement Loop:**

1. 🚨 **Production Failures** → Fehler und Qualitätsprobleme in der Produktion erkennen.
2. 🧪 **New Test Cases** → Erkannte Fehler als neue Testfälle in das Eval-Dataset aufnehmen.
3. ⚙️ **Updated Criteria** → Bewertungsmetriken und Evaluationskriterien bei Bedarf anpassen.
4. 📊 **Improved Reporting** → Reports erweitern, um neue Fehlerbilder und Qualitätsentwicklungen sichtbar zu machen.
5. 🔄 **Re-Evaluation** → Verbesserungen erneut testen und überprüfen.

### 🎯 Key Takeaway

**Eine Eval-Pipeline automatisiert die Qualitätsprüfung eines LLM-Systems und ermöglicht kontinuierliche Verbesserungen über den gesamten Entwicklungs- und Produktionszyklus.**

- 📚 **Test Dataset** → Was wird getestet?
- 🧪 **Eval Functions** → Wie wird getestet?
- 📊 **Scoring & Reporting** → Wie werden Ergebnisse bewertet und dargestellt?
- 🔄 **Continuous Improvement** → Wie werden Fehler zur Verbesserung genutzt?

# 🔄 Regression Testing for Prompts

### 🧪 When to Run the Eval Suite?

- Die **Eval-Suite** sollte nach jeder relevanten Änderung am LLM-System ausgeführt werden, um sicherzustellen, dass bestehende Funktionen weiterhin korrekt arbeiten.
- Getestet wird immer mit demselben **Fixed Test Set**, damit Ergebnisse vergleichbar und Veränderungen messbar bleiben.

**Typische Auslöser:**

- 📝 **Prompt Changes** → Änderungen an System- oder User-Prompts.
- 🤖 **Model Changes** → Wechsel oder Update der verwendeten Modellversion.
- ⚙️ **Configuration Changes** → Anpassungen wichtiger LLM-Parameter oder Systemkonfigurationen.

### ⚠️ What is a Regression?

- Eine **Regression** liegt vor, wenn eine Änderung am LLM-System eine bestehende Funktion oder Qualitätsmetrik unbeabsichtigt verschlechtert.
- Eine Verbesserung in einem Bereich kann gleichzeitig eine Verschlechterung in einem anderen Bereich verursachen.

**Beispiel:**

- 📝 **Summary Quality** → Eine Prompt-Anpassung verbessert die Qualität der generierten Zusammenfassungen.
- 📋 **JSON Validity** → Gleichzeitig liefert das Modell häufiger ungültiges JSON.

**Ergebnis:** Eine isolierte Verbesserung bedeutet nicht automatisch, dass sich die Gesamtqualität des Systems verbessert hat.

### 🛡️ Prompt as Code – Prompts wie Code behandeln

- **Prompts sind ein Bestandteil der Softwarelogik** und sollten genauso systematisch versioniert, getestet und überprüft werden wie klassischer Programmcode.
- Änderungen an Prompts dürfen nicht ungeprüft in die Produktion übernommen werden.

**Best Practices:**

- 📚 **Version Control** → Prompts versionieren und Änderungen nachvollziehbar dokumentieren.
- 🧪 **Automated Eval Suite** → Nach relevanten Änderungen automatisch alle definierten Tests ausführen.
- 🚦 **Quality Gates** → Kritische Qualitätsmetriken müssen definierte Mindestanforderungen erfüllen.
- 🚀 **Deployment Gate** → Kein Deployment, solange wichtige Evaluationsmetriken die definierten Grenzwerte nicht erfüllen.

### 🎯 Key Takeaway

**Regression Testing stellt sicher, dass Änderungen an Prompts, Modellen oder Konfigurationen bestehende Qualitätsmerkmale nicht unbeabsichtigt verschlechtern.**

- 🔄 **Fixed Test Set** → Vergleichbare Testergebnisse über verschiedene Versionen hinweg.
- ⚠️ **Regression Detection** → Verschlechterungen in einzelnen Qualitätsmetriken erkennen.
- 🛡️ **Eval as Deployment Gate** → Evaluation als verbindliche Qualitätskontrolle vor dem Deployment.

# ⚖️ A/B Testing LLM Outputs

### 🧪 What is A/B Testing?

- **A/B-Testing für LLMs** vergleicht zwei unterschiedliche Versionen eines LLM-Systems (z. B. Prompt, Modell oder Config), um herauszufinden, welche Version bessere Ergebnisse liefert.
- Beide Versionen erhalten **dieselben Inputs** und werden mit **derselben Scoring-Methode** bewertet.
- Vor dem Test wird ein klares **Decision Criterion** definiert, anhand dessen entschieden wird, wann Version B gegenüber Version A gewinnt.

### 🔄 A/B Testing vs. Regression Testing

- ⚖️ **A/B Testing** → Vergleicht zwei Versionen miteinander, um festzustellen, welche besser performt.
- 🔍 **Regression Testing** → Prüft, ob Änderungen bestehende Funktionen oder Qualitätsmetriken unbeabsichtigt verschlechtern.

**Unterschied:**
- A/B-Testing beantwortet: *Welche Version ist besser?*
- Regression Testing beantwortet: *Hat eine Änderung bestehende Qualität verschlechtert?*

### 📋 Requirements – Pflicht-Bausteine eines A/B-Tests

- 📚 **Shared Test Set** → Beide Versionen werden mit exakt denselben Testfällen und Inputs getestet.
- 📊 **Consistent Scoring** → Beide Versionen werden anhand derselben Metriken und Bewertungskriterien beurteilt.
- 🎯 **Decision Criterion** → Vorab definieren, anhand welcher Kriterien eine Version gewinnt (z. B. höhere Faithfulness bei gleichbleibender JSON-Validität).

### 🎯 Key Takeaway

**A/B-Testing ermöglicht einen fairen und systematischen Vergleich verschiedener LLM-Versionen.**

- 🅰️ **Version A** → Bestehender Prompt, Modell oder Config.
- 🅱️ **Version B** → Neue Variante, die getestet wird.
- ⚖️ **Fair Comparison** → Gleiche Inputs, gleiche Scoring-Methode und klare Entscheidungskriterien.
