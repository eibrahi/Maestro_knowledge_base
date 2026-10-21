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
