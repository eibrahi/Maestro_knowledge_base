# 🧹 Preprocessing im RAG-Kontext

### 🎯 Grundidee des Preprocessings

- Rohquellen wie **PDF, HTML und Datenbanken** sind in der Regel nicht sauber genug, um direkt **gechunkt und embedded** zu werden.
- Deshalb ist eine **Preprocessing-Pipeline** erforderlich:

**Extraktion → Cleaning → Normalisierung**

### ⚙️ Extraktion vs. Cleaning

#### 📥 Extraktion

Bei der **Extraktion** werden Inhalte aus den jeweiligen Datenquellen gewonnen – einschließlich Text, grober Struktur und möglicher Störinformationen.

- 🌐 **HTML**
  - DOM → Text und Struktur (**Überschriften, Absätze, Listen, Tabellen**).

- 📄 **PDF**
  - Extraktion von **Text** sowie, soweit möglich, **Tabellen und Dokumentstrukturen**.

- 🗄️ **Datenbanken**
  - Umwandlung von **Records** in eine **Text- oder JSON-Repräsentation**.

#### 🧽 Cleaning

Beim **Cleaning** werden extrahierte Inhalte bereinigt und für die weitere Verarbeitung vorbereitet.

- 🗑️ **Noise entfernen**
  - Navigation, Footer, Werbung, Cookie-Banner und Related-Links.

- 🛠️ **Parsing-Artefakte bereinigen**
  - Duplizierte Header
  - Harte Zeilenumbrüche
  - Fehlerhafte Textfragmente

- 🔄 **Optionale Bereinigungsschritte**
  - **Deduplication** → Doppelte Inhalte entfernen.
  - **DOM-Tags entfernen** → Nicht benötigte HTML-Strukturen bereinigen.
  - **Irrelevante Spalten oder Records** entfernen.

### ⚠️ Typische Parsing- und Preprocessing-Probleme

#### 📊 PDF-Tabellen

- Bei der Extraktion können **Spalten- und Zeilenstrukturen zerstört** werden.
- Beispiel einer fehlerhaften Tabellenextraktion:

`Region Umsatz Europa Asien Amerika 10 20 30`

- Die ursprünglichen **Relationen (Region → Umsatz)** gehen verloren.
- Dadurch können **faktisch falsche Antworten** entstehen.

#### 🌐 HTML-Noise

- **Navigation, Footer, Werbung, Kommentare und Related-Articles** werden unbeabsichtigt mitindexiert.
- Das **Retrieval** liefert dadurch irrelevante Textteile.
- Ergebnis: **Unpräzise oder verwässerte Antworten**.

#### 🖼️ Fehlender Text aus Bildern und Scans

- Zahlen und Informationen befinden sich teilweise ausschließlich in **Diagrammen, Bildern oder gescannten Dokumenten**.
- Die normale Textextraktion erkennt diese Inhalte nicht.
- Diese Informationen bleiben für das **RAG-System unsichtbar**.
- Ergebnis: Das **LLM** kann ungenaue Antworten generieren, **halluzinieren** oder vage bleiben.

### 📏 Quality-Ceiling-Prinzip

- Informationen, die beim **Preprocessing verloren gehen**, stehen dem RAG-System nicht mehr zur Verfügung.
  - Kaputte Tabellenstrukturen
  - Fehlende Bildtexte
  - Verlorene Zusammenhänge

- **Retrieval und LLM** können diese Informationsverluste nicht automatisch reparieren.
- Auch ein leistungsfähiger **Retriever** oder ein starkes **LLM** liefern nur dann zuverlässige Ergebnisse, wenn der **Input korrekt** ist.

**🎯 Kernaussage: Die Preprocessing-Qualität setzt die Obergrenze der RAG-Qualität.**

### 🔄 Preprocessing-Pipeline (konzeptionell)

#### 1. 📥 Extraktion

- **PDF / HTML / DB** → Rohtext + Struktur

#### 2. 🧽 Cleaning

- Noise entfernen.
- Parsing-Artefakte korrigieren oder markieren.
- Irrelevante Inhalte filtern.

#### 3. ⚙️ Normalisierung

- **Encoding** vereinheitlichen.
- **Whitespace** normalisieren.
- Eine einfache, konsistente **Datenstruktur** sicherstellen.

#### 4. 🔧 Optionale Verarbeitung

- **Deduplizieren** → Doppelte Inhalte entfernen.
- **OCR / Captioning** → Text und Informationen aus Grafiken ergänzen.

# 📚 Document Ingestion and Chunking

### 🧱 1. Ingestion-Pipeline (nach dem Cleaning)

Nach der **Extraktion und dem Cleaning** durchläuft jedes Dokument eine **Ingestion-Pipeline** mit folgenden Schritten:

1. 📥 **Dokument laden**
2. 🧩 Dokument in **Chunks** aufteilen
3. 🧠 Jeden Chunk **einbetten (Embedding)**
4. 🗄️ **Embedding + Original-Text + Metadaten** in der **Vektordatenbank speichern**

**🎯 Wichtig:** Chunking ist genau **Schritt 2** und entscheidet darüber, *welche Inhalte überhaupt eingebettet werden*.

---

### 🧩 2. Chunking-Strategie

**Chunking** bedeutet nicht nur, einen Text nach einer festen Anzahl von Tokens aufzuteilen.

Das Ziel ist die Bildung **sinnvoller, semantischer Einheiten**.

Beispiele:

- 📋 **Regel + Ausnahme** → Zusammengehörige Informationen bleiben erhalten.
- 🔄 **Kompletter Prozessschritt** → Einzelne Schritte werden nicht auseinandergerissen.
- 📝 **Zusammengehöriger Absatz** → Inhaltliche Zusammenhänge bleiben bestehen.

**⚠️ Problem:** Schlechte Chunk-Grenzen, beispielsweise mitten in einem Satz, zerstören den Zusammenhang und verschlechtern die **Retrieval-Qualität**.

---

### ⚖️ 3. Chunk-Größe: Trade-off

Die Wahl der **Chunk-Größe** beeinflusst sowohl die Präzision des Retrievals als auch den verfügbaren Kontext.

#### 🔹 Kleine Chunks (1–2 Sätze, ~200 Tokens)

- ✅ **Hohe Präzision** bei fokussierten Fragen.
- ⚠️ **Risiko des Kontextverlusts**, beispielsweise wenn eine Ausnahme von der zugehörigen Regel getrennt wird.

#### 🔸 Große Chunks (Abschnitt/Regelblock, ~800 Tokens)

- ✅ **Mehr Kontext** und bessere Erhaltung inhaltlicher Zusammenhänge.
- ⚠️ **Mehr Rauschen**, wodurch relevante Informationen weniger punktgenau gefunden werden.

**🎯 Fazit:** Keine Chunk-Größe ist grundsätzlich besser. Die optimale Wahl hängt vom jeweiligen **Use Case** ab.

---

### 🎯 4. Einfluss auf Retrieval und Antworten

#### ✅ Gute Chunking-Strategie

- Relevante Informationen stehen **gemeinsam innerhalb eines Chunks**.
- Das **LLM erhält genau den Kontext**, der für die Beantwortung benötigt wird.

#### ❌ Schlechte Chunking-Strategie

- Wichtige Informationen werden **voneinander getrennt** oder mit irrelevanten Inhalten vermischt.
- Antworten können dadurch:
  - **Unpräzise** werden.
  - **Lückenhaft** sein.
  - **Halluziniert wirken**.
- Diese Probleme können **selbst bei guten Embeddings** auftreten.

---

### 💡 Kernaussage

**Chunking ist ein entscheidender Qualitätshebel für RAG-Systeme und nicht nur ein technisches Detail.**


# 🚀 Building a Simple RAG Pipeline

### 🏗️ 1. Aufbau einer Mini-RAG-Pipeline

Eine vollständige **Mini-RAG-Pipeline in Python** besteht aus drei zentralen Komponenten:

- 📥 **Ingestion** → Dokumente laden, verarbeiten und für die Suche vorbereiten.
- 🔍 **Retrieval** → Relevante Informationen aus dem Vector Store abrufen.
- 🤖 **LLM** → Antworten auf Basis der abgerufenen Informationen generieren.

---

### 🔄 2. Dokumentzeit vs. Queryzeit

Die **RAG-Pipeline** ist in zwei klar voneinander getrennte Prozesse unterteilt.

#### 📚 Dokumentzeit (Ingestion Pipeline)

Dokumente werden verarbeitet und für spätere Suchanfragen vorbereitet.

**Documents → Embeddings → Vector Store**

- 📄 **Documents** → Ausgangsdokumente bereitstellen.
- 🧠 **Embeddings** → Dokumentinhalte in Vektoren umwandeln.
- 🗄️ **Vector Store** → Embeddings für die spätere Suche speichern.

#### 🔎 Queryzeit (Retrieval & Generation Pipeline)

Eine Benutzeranfrage wird verarbeitet und mithilfe der gespeicherten Informationen beantwortet.

**Query → Embedding → Retrieval → Prompt/LLM**

- 💬 **Query** → Benutzeranfrage entgegennehmen.
- 🧠 **Embedding** → Anfrage in einen Vektor umwandeln.
- 🔍 **Retrieval** → Relevante Dokumente oder Chunks abrufen.
- 🤖 **Prompt/LLM** → Kontext in den Prompt integrieren und eine Antwort generieren.

---

### ⚠️ 3. Typische Fehlerquellen

#### 📄 Fehlerhafte Dokumente

- **Kaputte oder fehlerhaft verarbeitete Dokumente** können die Qualität des Retrievals beeinträchtigen.

#### 📐 Embedding-/Dimension-Mismatch

- **Unterschiedliche Embedding-Dimensionen** zwischen Modell und Vector Store können zu Fehlern bei der Speicherung oder Suche führen.

#### 🧩 Fehlender Kontext im Prompt

- Werden relevante Informationen nicht in den **Prompt** integriert, fehlt dem **LLM** die notwendige Grundlage für eine korrekte Antwort.

---

### 💡 Kernaussage

Eine funktionierende **RAG-Pipeline** benötigt eine saubere Trennung zwischen **Dokumentenverarbeitung (Dokumentzeit)** und **Anfrageverarbeitung (Queryzeit)**.

**Die Qualität der Dokumente, die Kompatibilität der Embeddings und die korrekte Kontextbereitstellung sind entscheidend für zuverlässige RAG-Antworten.**

```python
documents = [
    "Die Authentifizierung erfolgt auf der Homepage direkt", 
    "Nach der Authentifizierung wird die Validierung der Userdaten durchgefhrt", 
    "Wenn Userdaten valide sind wird der user auf die richtigen raouts geleitet"
    ]


def embed(text):
    text_lower = text.lower()
    length = len(text)
    word_count = len(text.split())
    a_count = text_lower.count("a")
    has_auth = 1 if "authentifizierung" in text_lower else 0
    has_userdaten = 1 if "userdaten" in text_lower else 0
    has_raouts = 1 if "raouts" in text_lower else 0
    return [length, word_count, a_count, has_auth, has_userdaten, has_raouts]


def distance(a, b):
    diff_sum = 0
    for i in range(len(a)):
        diff_sum += (a[i] - b[i])**2
    return diff_sum


vectors = []
for doc in documents:
    vectors.append(embed(doc))


query = "Wohin wird der User geleitet?"
query_vec = embed(query)

best_idx = 0
best_dist = distance(query_vec, vectors[0])


for i in range(1, len(vectors)):
    current_dist = distance(query_vec, vectors[i])
    if current_dist < best_dist:
        best_idx = i


def llm_answer(query, context):
    return f"Frage: {query}\n\nKontext: {context}\n\nAntwort (simuliert auf Basis des Kontexts)."

context = documents[best_idx]
answer = llm_answer(query, context)

print(answer)
```

# 🔍 Metadata Filtering in RAG Systems

### 🏷️ 1. Chunk-Metadaten

Jeder **Chunk** besitzt neben **Text und Embedding** zusätzliche strukturierte Metadaten, die wichtige Informationen über den jeweiligen Inhalt bereitstellen.

**Typische Metadatenfelder:**

- 🔢 `product_version` → Produkt- oder Softwareversion
- 🏢 `department` → Zuständige Abteilung
- 📂 `source` → Herkunft der Informationen
- 📅 `valid_from / valid_to` → Gültigkeitszeitraum
- ⚙️ `environment` → Systemumgebung
- 🔧 `service_name` → Zugehöriger Service

Diese Felder modellieren die **„formale Wahrheit“** eines Dokuments:

- **Welche Version?**
- **Welches Team?**
- **Welche Quelle?**
- **Wann gültig?**

---

### ⚙️ 2. Metadata Filtering

Beim **Metadata Filtering** wird der Suchraum vor oder während der **Vektorsuche** anhand strukturierter Kriterien eingeschränkt.

**Beispiele für Metadatenfilter:**

```python
product_version = "3.2"
department = "HR"
country = "DE"
source IN ("confluence", "github")
```

**🎯 Ziel:**

- Logisch unpassende Chunks frühzeitig ausschließen.
- Dokumente mit der **falschen Version**, dem **falschen Land** oder der **falschen Quelle** herausfiltern.
- Die Suche auf **formal relevante Informationen** begrenzen.

---

### 🧠 3. Warum Metadaten und Semantik kombinieren?

#### 🔍 Nur semantische Suche

- ✅ Findet **inhaltlich und semantisch ähnliche Informationen**.
- ⚠️ Kann jedoch Dokumente aus der **falschen Version**, dem **falschen Department** oder der **falschen Quelle** zurückliefern.

#### 🏷️ Nur Metadata Filtering

- ✅ Alle gefundenen Dokumente erfüllen die **formalen Filterkriterien**.
- ⚠️ Es bleibt unklar, welcher Chunk **semantisch am besten zur Suchanfrage passt**.

#### ✅ Kombination aus Metadaten und Semantik

Beide Verfahren ergänzen sich:

- 🏷️ **Metadata Filtering** → Definiert, *welche Chunks überhaupt berücksichtigt werden dürfen*.
- 🧠 **Semantic Search** → Ermittelt, *welche dieser Chunks am besten zur Frage passen*.

**🎯 Ergebnis:** Formal passende und gleichzeitig semantisch relevante Suchergebnisse.

---

### 🏢 4. Typische Enterprise-Szenarien

#### 📅 Date-Scoped Policies

- Suche nach **aktuell gültigen HR- oder Legal-Regelungen**.
- Einschränkung anhand des Gültigkeitszeitraums:
  - `valid_from`
  - `valid_to`

#### 🏢 Department- oder Service-spezifisches Wissen

- Unterscheidung zwischen verschiedenen Abteilungen:
  - `department = "Security"`
  - `department = "HR"`

- Einschränkung auf bestimmte Services und Umgebungen:
  - `service_name = "billing"`
  - `environment = "prod"`

#### 📚 Multi-Source-Knowledge

- Gezielte Auswahl von Informationen anhand ihrer Herkunft.

**Beispiele:**

- 💻 `source = "github"` → Technische Deployments
- 📁 `source = "sharepoint"` → Eher nicht für genaue Runbooks

---

### 💡 Kernaussage

**Metadata Filtering und semantische Suche ergänzen sich innerhalb einer RAG-Pipeline.**

- **Metadaten** stellen sicher, dass nur formal passende Dokumente berücksichtigt werden.
- **Semantische Suche** identifiziert die inhaltlich relevantesten Chunks innerhalb dieses Suchraums.

**➡️ Metadata Filtering bestimmt, welche Dokumente infrage kommen – Semantic Search entscheidet, welche davon am besten zur Anfrage passen.**

# 🧠 Context Management in RAG Pipelines

### 🎯 1. Priorisierung relevanter Dokumente

Die **Priorisierung** stellt sicher, dass nur die wichtigsten und relevantesten Informationen an das **LLM** übergeben werden.

- ✅ **Relevante Dokumente auswählen**
  - Die Dokumente mit der höchsten Relevanz für die Benutzeranfrage priorisieren.

- 🗑️ **Unwichtige oder konfliktäre Informationen entfernen**
  - Irrelevante Inhalte aussortieren.
  - Widersprüchliche Informationen erkennen und gegebenenfalls ausschließen.

- 💰 **Truncation und Kosten vermeiden**
  - Verhindern, dass wichtige Informationen aufgrund begrenzter **Kontextfenster (Context Windows)** abgeschnitten werden.
  - Den **Tokenverbrauch** und damit die Kosten reduzieren.

---

### 📝 2. Summarisierung (Summarization)

Die **Summarisierung** ist besonders sinnvoll, wenn relevante Informationen über viele kleine und unterschiedliche Quellen verteilt sind.

**Typische Datenquellen:**

- 💬 **Slack** → Nachrichten und Diskussionen
- 🎫 **Tickets** → Support- und Incident-Tickets
- 📋 **Logs** → Systemereignisse und Fehlermeldungen

**🎯 Ziel:**

- Verteilte Informationen zu einer **kompakten Zusammenfassung** verdichten.
- Redundante Inhalte reduzieren.
- Statt alle Rohdaten an das LLM zu übergeben, nur die **wesentlichen Informationen** bereitstellen.

---

### 🔄 3. Sliding Window

Die **Sliding-Window-Technik** eignet sich besonders für die Verarbeitung **sehr langer Einzelquellen**.

**Typische Use Cases:**

- 📖 **Runbooks** → Umfangreiche technische Dokumentationen
- 📋 **Logs** → Lange Protokolle und Ereignisverläufe

**Funktionsweise:**

- Lange Inhalte werden in **aufeinanderfolgende, teilweise überlappende Abschnitte** unterteilt.
- Das **Sliding Window** bewegt sich schrittweise durch die Daten.
- Dadurch bleiben **wichtige Details und der lokale Kontext** erhalten.

**🎯 Ziel:** Große Informationsmengen verarbeiten, ohne relevante Zusammenhänge zwischen benachbarten Abschnitten zu verlieren.

---

### ⚠️ 4. Risiken durch zu viel Kontext

**Mehr Kontext bedeutet nicht automatisch bessere Antworten.**

Zu große oder schlecht zusammengestellte Kontextmengen können die **Antwortqualität eines LLMs verschlechtern**.

#### ✂️ Truncation (Abschneiden von Informationen)

- Wird das **Kontextfenster überschritten**, können wichtige Informationen abgeschnitten werden.
- Dadurch fehlen dem LLM relevante Fakten für die Antwortgenerierung.

#### 🌫️ Information Noise (Informationsrauschen)

- Zu viele irrelevante Informationen können die **wichtigen Inhalte überdecken**.
- Das LLM kann dadurch Schwierigkeiten haben, die entscheidenden Informationen zu identifizieren.

---

### 💡 Kernaussage

**Effektives Context Management ist entscheidend für die Qualität, Performance und Kosteneffizienz einer RAG-Pipeline.**

- 🎯 **Priorisierung** → Die relevantesten Informationen auswählen.
- 📝 **Summarisierung** → Verteilte Informationen kompakt zusammenfassen.
- 🔄 **Sliding Window** → Lange Quellen unter Erhaltung des lokalen Kontexts verarbeiten.

**➡️ Nicht die Menge des Kontexts entscheidet über die Antwortqualität, sondern dessen Relevanz, Struktur und gezielte Auswahl.**
