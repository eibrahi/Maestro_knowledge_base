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

# 🔐 Security and Access Control in RAG

### ⚠️ 1. Kernrisiko in RAG-Systemen

Ein zentrales Sicherheitsrisiko in **RAG-Systemen** besteht darin, dass der **Retriever** hochrelevante, aber **nicht autorisierte Dokumente** zurückliefern kann.

- 🔍 **Retriever**
  - Kann Dokumente anhand ihrer semantischen Relevanz finden, ohne automatisch die Zugriffsberechtigungen zu berücksichtigen.

- 🚨 **Unberechtigter Datenzugriff**
  - Das **LLM** erhält möglicherweise Zugriff auf vertrauliche oder private Informationen.
  - **Beispiel:** Gehaltsinformationen anderer Mitarbeiter.

---

### 🛡️ 2. Drei Schutzansätze

#### 👤 Per-User Vector Stores

- Jeder Benutzer erhält einen eigenen **Vector Store**.
- ✅ **Vorteil:** Einfache Trennung der Daten und Zugriffsbereiche.
- ⚠️ **Nachteil:** Schwer skalierbar bei einer großen Anzahl von Benutzern.

#### 🏷️ Metadata Filtering

- Verwendung eines **globalen Vector Stores** mit strukturierten Zugriffsfiltern.
- Die Zugriffsbeschränkung erfolgt anhand von **Metadaten**.

**Beispiele für Filterkriterien:**

- `employee_id` → Zugriff anhand der Mitarbeiter-ID.
- `roles` → Zugriff anhand definierter Benutzerrollen.

#### 🔎 Post-Retrieval Checks

- Zusätzliche **Berechtigungsprüfung** nach dem Retrieval.
- Dient als **zweite Sicherheitsschicht**.
- ⚠️ **Wichtig:** Post-Retrieval Checks ersetzen keine saubere Zugriffskontrolle während des Retrievals.

---

### 🏗️ 3. Security-by-Design

**Security muss von Anfang an Bestandteil der RAG-Architektur sein** und darf nicht erst nachträglich integriert werden.

Die Sicherheitsmaßnahmen betreffen den gesamten **RAG-Lifecycle**.

#### 📥 Ingestion – Metadaten

- Relevante **Zugriffs- und Sicherheitsmetadaten** bereits bei der Datenaufnahme berücksichtigen.

#### 🗄️ Storage – Struktur

- Daten und Dokumente innerhalb des **Vector Stores** strukturiert und entsprechend den Zugriffsanforderungen organisieren.

#### 🔍 Retrieval – Filter

- **Metadata Filtering** einsetzen, um nicht autorisierte Dokumente bereits bei der Suche auszuschließen.

#### 🤖 Response – Checks

- Zusätzliche **Sicherheitsprüfungen** vor der Ausgabe der generierten Antwort durchführen.

---

### 💡 Kernaussage

**Security and Access Control müssen über den gesamten RAG-Lifecycle hinweg berücksichtigt werden.**

- 👤 **Per-User Vector Stores** → Trennung der Daten nach Benutzern.
- 🏷️ **Metadata Filtering** → Zugriffskontrolle über Metadaten und Rollen.
- 🔎 **Post-Retrieval Checks** → Zusätzliche Sicherheitsprüfung.

**➡️ Security-by-Design: Ingestion → Metadaten | Storage → Struktur | Retrieval → Filter | Response → Checks.**

# 🎯 When RAG Isn't the Answer

### 📚 1. Long Context

**Long Context** eignet sich, wenn das benötigte Wissen **klein, stabil und vollständig im Kontextfenster platzierbar** ist.

- ✅ **Einsatzkriterien**
  - **Kleine Wissensbasis** → Überschaubare Informationsmenge.
  - **Stabile Informationen** → Inhalte ändern sich selten.
  - **Begrenzter Kontext** → Alle relevanten Informationen passen in das Kontextfenster des LLMs.

- 📋 **Typische Use Cases**
  - Kleine FAQs
  - Mini-Dokumentationen
  - Feste Regeln

---

### 🔍 2. RAG (Retrieval-Augmented Generation)

**RAG** eignet sich, wenn das benötigte Wissen **umfangreich ist oder häufig aktualisiert wird** und gezielt nachgeschlagen werden muss.

- ✅ **Einsatzkriterien**
  - **Große Wissensbasis** → Umfangreiche Dokumentensammlungen.
  - **Dynamische Informationen** → Inhalte ändern sich regelmäßig.
  - **Gezieltes Retrieval** → Relevante Informationen werden bei Bedarf abgerufen.

- 📋 **Typische Use Cases**
  - Runbooks
  - Policies
  - Produktkataloge
  - Dynamische Regeln

---

### 🧠 3. Fine-Tuning

**Fine-Tuning** eignet sich, wenn das **Verhalten, die Mustererkennung oder der Stil eines Modells** angepasst werden sollen.

Der Fokus liegt dabei **nicht auf ständig wechselnden Fakten**, sondern auf dem gewünschten Modellverhalten.

- ✅ **Einsatzkriterien**
  - **Verhalten (Behavior)** → Anpassung des Antwortverhaltens.
  - **Patterns** → Erlernen spezifischer Muster.
  - **Stil (Style)** → Anpassung der Ausdrucksweise.
  - **Latenz-Anforderungen** → Einsatz bei strengen Anforderungen an die Antwortgeschwindigkeit.

- 📋 **Typische Use Cases**
  - Tonalität
  - Code-Stil
  - Klassifikationsregeln mit harter Latenz-Anforderung

---

### ⚖️ 4. Vergleich der Ansätze

| Ansatz | Einsatzkriterien | Typische Use Cases |
|---|---|---|
| 📚 **Long Context** | Kleines, stabiles Wissen, das in das Kontextfenster passt | FAQs, Mini-Dokus, feste Regeln |
| 🔍 **RAG** | Große oder häufig aktualisierte Wissensbasis | Runbooks, Policies, Produktkataloge, dynamische Regeln |
| 🧠 **Fine-Tuning** | Anpassung von Verhalten, Patterns und Stil | Tonalität, Code-Stil, Klassifikationsregeln |

---

### 💡 Kernaussage

Die Wahl zwischen **Long Context, RAG und Fine-Tuning** hängt von der Art des Wissens und den Anforderungen an das LLM-System ab.

- 📚 **Long Context** → Kleines, stabiles Wissen direkt bereitstellen.
- 🔍 **RAG** → Große oder dynamische Wissensbestände gezielt durchsuchen.
- 🧠 **Fine-Tuning** → Modellverhalten, Muster und Stil anpassen.

**➡️ Nicht jedes Wissensproblem benötigt RAG. Entscheidend ist die passende Architektur für den jeweiligen Use Case.**
