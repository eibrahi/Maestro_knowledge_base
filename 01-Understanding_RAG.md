# 🧠 The Knowladge Cuttoff Problem

- Ein **LLM** kennt nur Muster aus seinem **Trainingsdatensatz**.
- Ab dem **Knowledge Cutoff** ist alles Neue draußen.
- **Typisch fehlen:**
  - 🔒 **Private Daten** (interne Systeme, Wikis, Runbooks, Schemas …)
  - 📰 **Events nach dem Cutoff** (News, Incidents, neue Features …)
  - 📚 **Spezielle Domain-Dokumente**, die nie im Training waren
- Ein noch so guter **Prompt** kann fehlende Informationen nicht ersetzen – das muss über die **System-/Architektur** gelöst werden, nicht über **„Prompt-Magie“**.

# 🧠 Was ist RAG?

- **RAG (Retrieval-Augmented Generation)**: gezieltes **Retrieval** von externen, relevanten Daten + **Generierung** der Antwort mit diesen Daten im Prompt.

- 🎯 **Kernvorteil**: Antworten sind **gegroundet** in konkreten Dokus/Repos/Logs statt nur im Modellgedächtnis.

- ⚖️ **Abgrenzung**:
  - **RAG > Fine-Tuning** bei großen Dokus, privaten Daten, häufigen Änderungen.
  - **RAG > langes Kontext-Fenster / Prompt Stuffing**, weil es **selektiv** arbeitet.

# 🏗️ RAG Architecture

### 🔄 RAG-Loop

**Query** → **Embed** → **Search** → **Retrieve** → **Prompt augmentieren** → **LLM-Antwort**

### ⚙️ Rollen

- 🧠 **Embedding-Modell** (Query vorbereiten)
- 🗄️ **Vektor-Store** (relevante Dokus finden)
- 🤖 **LLM** (Antwort formulieren)

### ⚠️ Problemfall

**Schlechtes Retrieval ⇒ schlechte/irrelevante Antwort**, egal wie stark das LLM ist.

# 🧠 Embedding Models for Retrieval

- 📝 **Text (Query oder Chunk)** → **Retrieval-Embedding-Vektor**

- 🔍 **Ähnliche Bedeutung** ⇒ **nahe Vektoren** → so funktioniert die Suche.

- ⚙️ Diese **Retrieval-Embeddings** sind **nicht** die gleichen wie die kontextuellen **Token-Embeddings im LLM**, die nur für die **Generierung** da sind.

# 🧠 Choosing an Embedding Model

### ⚙️ Kernkriterien für Embedding-Modelle

Die **4 wichtigsten Kriterien** bei der Auswahl eines Embedding-Modells:

- 📐 **Vektor-Dimensionen**
- 📏 **Kontextlänge**
- 🌍 **Multilingualität**
- ⚡ **Speed vs. Accuracy**

### 🎯 Domain Fit

- Der **Domain Fit** (z. B. Tech, Medizin, HR) beeinflusst die **Retrieval-Qualität** maßgeblich.

### 🔍 Auswahl des passenden Embedding-Modells

- Für unterschiedliche **RAG-Use-Cases** sollte ein **passendes Embedding-Profil** ausgewählt und die Entscheidung begründet werden.

### ⚠️ Modellwechsel

- Ein späterer **Wechsel des Embedding-Modells** erfordert ein **vollständiges Re-Embedding** aller Daten.
- Dies verursacht zusätzlichen **Zeit- und Kostenaufwand**.

# 🗄️ Vector Databases

### 📌 Definition einer Vektordatenbank

- Eine **Vektordatenbank** dient der Speicherung und **Similarity Search** (Ähnlichkeitssuche) von **Embeddings**.

### 🔍 Unterschied zwischen klassischen Datenbanken und Vektordatenbanken

- 🗃️ **Klassische Datenbank** → Suche nach **exakten Werten**
- 🧠 **Vektordatenbank** → Suche anhand **semantischer Ähnlichkeit**

### ⚙️ Rolle im RAG-Flow

- 🧠 **Embedding-Modell** → Erstellt die **Vektoren (Embeddings)**.
- 🗄️ **Vektordatenbank** → **Indexiert** die Vektoren und ruft **relevante Chunks** ab.
- 🤖 **LLM** → Generiert auf Basis der abgerufenen Informationen die **Antwort**.

# 🗄️ Choosing a Vector Database

### ⚙️ Kriterien zur Auswahl einer Vektordatenbank

Die wichtigsten Kriterien bei der Wahl einer **Vektordatenbank**:

- ☁️ **Hosting** → Hosted vs. Self-Hosted
- 📈 **Skalierung** → Skalierbarkeit der Datenbank
- ⚡ **Query-Speed** → Geschwindigkeit der Suchanfragen
- 🔍 **Metadaten-Filter** → Filterung anhand von Metadaten
- 💰 **Kosten** → Betriebskosten und Ressourcenbedarf
- 👥 **Team-Fit** → Passung zu vorhandenen Kompetenzen und Technologien

### ⚖️ Vergleich der Datenbanktypen

- 🐘 **PostgreSQL + Vektor-Extension** → Relationale Datenbank mit erweiterten Vektorsuchfunktionen
- 🧠 **Purpose-built Vektordatenbank** → Speziell für die Speicherung, Indexierung und Suche von Vektoren entwickelte Datenbank
- 🔄 **Trade-offs** → Unterschiede hinsichtlich Performance, Skalierbarkeit, Flexibilität und Betriebsaufwand

### 🎯 Auswahl für konkrete RAG-Projekte

- Für den **Data-Engineering-Assistenten** sollte eine **passende Vektordatenbank** anhand der definierten Kriterien ausgewählt werden.
- Die **Datenbankentscheidung** sollte technisch und wirtschaftlich begründet sein.
