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
