# 🎯 Evaluating RAG Quality

### 📊 1. Zwei Qualitätsdimensionen bei RAG

Die Qualität eines **RAG-Systems** wird anhand von zwei zentralen Dimensionen bewertet:

#### 🔍 Retrieval-Relevanz (Retrieval Relevance)

> **Frage:** „Hat das System die richtigen und ausreichenden Dokumente zur Frage gefunden?“

**Typische Beispiele für Retrieval-Failures:**

- ❌ **Falscher Service** → Dokumente gehören zu einem anderen Service.
- ❌ **Alte Version** → Veraltete Dokumentation wird abgerufen.
- ❌ **Falsche Umgebung** → Nur Staging-Dokumentation statt Production.

#### 🤖 Generation-Faithfulness

> **Frage:** „Hält sich die Antwort strikt an diese Dokumente?“

**Typische Beispiele für Generation-Failures:**

- ❌ **Erfundene Scripts** → Das LLM generiert nicht existierende Scripts.
- ❌ **Falsche SLO-Aussagen** → Falsche Angaben zu Service Level Objectives.
- ❌ **Falsche Behauptungen** → „Es gibt keine Dokumentation“, obwohl diese im Kontext vorhanden ist.

---

### ⚠️ 2. Typische Fehlerarten

#### 🔴 Irrelevantes Retrieval

- **Falscher Service**
- **Falsche Umgebung**
- **Veraltete Runbooks**
- **Nur allgemeine Policies**

**Ergebnis:** Selbst eine gut formulierte Antwort ist wertlos, wenn die zugrunde liegenden Informationen nicht relevant sind.

#### 🟠 Halluzination trotz gutem Kontext

- Die richtigen **Runbooks oder Logs** sind vorhanden.
- Das **LLM** generiert trotzdem falsche oder erfundene Informationen.

**Typische Beispiele:**

- Erfundene Scripts
- Falsche Werte
- Behauptung, dass **keine SLOs definiert** sind, obwohl diese im Kontext vorhanden sind.

#### 🟡 Missing Information

- Die benötigten Informationen sind **nicht im bereitgestellten Kontext vorhanden**.

**Typische Beispiele:**

- Neue Region
- Neues Deployment

**✅ Gute Antwort:**

- Fehlende Informationen transparent kommunizieren.
- Gegebenenfalls **eskalieren**.

**❌ Schlechte Antwort:**

- Das Modell versucht, fehlende Informationen zu erraten.
- Ergebnis: **Halluzination aufgrund fehlender Informationen**.

---

### 🛠️ 3. Warum Retrieval und Generation getrennt evaluieren?

Für ein gezieltes **Debugging** eines RAG-Systems müssen zwei unabhängige Fragen beantwortet werden.

#### 🔍 1. Retrieval

> „Wurden die passenden Dokumente zur Frage gefunden?“

- Überprüfung der **Relevanz und Vollständigkeit** der abgerufenen Dokumente.

#### 🤖 2. Generation

> „Ist die Antwort durch diese Dokumente gedeckt und widerspruchsfrei?“

- Überprüfung der **Faithfulness** und der inhaltlichen Korrektheit der generierten Antwort.

---

### ⚙️ 4. Gezielte Optimierung

Durch die getrennte Evaluation lässt sich die Ursache eines Qualitätsproblems eindeutig zuordnen.

- 🔍 **Retriever verbessern**
  - Wenn die falschen oder unzureichenden Dokumente gefunden werden.

- 🤖 **Antwortverhalten / Prompting optimieren**
  - Wenn das LLM trotz korrekter Dokumente falsche Aussagen generiert.

- 🔒 **Modell-Constraints verschärfen**
  - Wenn die Antwort nicht ausreichend an den bereitgestellten Kontext gebunden ist.

---

### 💡 Kernaussage

**RAG-Qualität besteht aus zwei unabhängigen Dimensionen: Retrieval-Relevanz und Generation-Faithfulness.**

- 🔍 **Retrieval-Relevanz** → Werden die richtigen Informationen gefunden?
- 🤖 **Generation-Faithfulness** → Bleibt die generierte Antwort bei diesen Informationen?

**➡️ Nur durch die getrennte Bewertung beider Dimensionen lassen sich Fehlerursachen gezielt identifizieren und RAG-Systeme systematisch verbessern.**
