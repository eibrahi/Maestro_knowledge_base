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

# 🚀 Advanced RAG Techniques

### 🔄 1. Re-ranking

**Re-ranking** optimiert die Reihenfolge bereits abgerufener Dokumente, um die relevantesten Informationen höher zu priorisieren.

- 📥 **Ausgangssituation**
  - Es wurden bereits **k Dokumente** durch das Retrieval gefunden.
  - Das Problem liegt in der **Reihenfolge der Suchergebnisse**.

- 🧠 **Lösungsansatz**
  - Ein zweites, leistungsfähigeres **Modell** bewertet die gefundenen Dokumente erneut.
  - Die Dokumente werden anhand ihrer **Relevanz neu sortiert**.

---

### 🔍 2. Query Expansion

**Query Expansion** verbessert die Suche, indem eine ursprüngliche Suchanfrage erweitert oder umformuliert wird.

- ⚠️ **Ausgangssituation**
  - **Vokabular-Mismatch** zwischen Suchanfrage und Dokumenten.
  - Wichtige Dokumente werden beim Retrieval nicht gefunden.

- 🛠️ **Lösungsansatz**
  - Die ursprüngliche **Query** wird erweitert oder umformuliert.
  - Verwendung von:
    - **Synonymen**
    - **Verwandten Begriffen**
    - **Alternativen Formulierungen**

- 🎯 **Ziel**
  - Mehr passende und relevante Dokumente beim **Retrieval** finden.

---

### 🔎 3. Hybrid Search

**Hybrid Search** kombiniert die **Keyword-Suche** mit der **semantischen Suche**.

- 🔑 **Keyword Search**
  - Suche nach **exakten Strings**.
  - Typische Beispiele:
    - **Error-Codes**
    - **IDs**
    - **Config-Keys**

- 🧠 **Semantic Search**
  - Suche anhand der **Bedeutung natürlicher Sprache**.
  - Identifikation inhaltlich ähnlicher Informationen.

- ✅ **Kombination**
  - Verbindet die Vorteile der **exakten Suche** mit denen der **semantischen Ähnlichkeit**.

---

### ⚖️ 4. Trade-off: Wann sind Advanced RAG Techniques sinnvoll?

Fortgeschrittene RAG-Techniken erhöhen die Komplexität einer RAG-Pipeline und sollten daher gezielt eingesetzt werden.

**✅ Sinnvoll bei:**

- Klar identifizierten **Retrieval-Problemen**.
- **Kritischen Use Cases**, bei denen die Qualität der Suchergebnisse besonders wichtig ist.

**⚠️ Nicht erforderlich, wenn:**

- Eine einfache RAG-Pipeline bereits ausreichend gute Ergebnisse liefert.
- Keine konkreten Retrieval-Probleme vorliegen.

---

### 💡 Kernaussage

Die verschiedenen **Advanced RAG Techniques** adressieren unterschiedliche Retrieval-Probleme:

- 🔄 **Re-ranking** → Optimiert die **Reihenfolge** gefundener Dokumente.
- 🔍 **Query Expansion** → Verbessert die **Auffindbarkeit** relevanter Dokumente.
- 🔎 **Hybrid Search** → Kombiniert **exakte Keywords** mit **semantischer Bedeutung**.

**➡️ Simple RAG first, keep it simple. ✅**
