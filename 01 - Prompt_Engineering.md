# Prompt Engineering – Cheat Sheet

## Lektion 1 – Was ist Prompt Engineering

**Kernideen**

- Prompt Engineering = Prompts bewusst designen, damit LLMs verlässliche, nützliche Antworten liefern.
- Gute Prompts haben 3 Bausteine:
  - **Rolle** (wer ist das Modell?)
  - **Kontext** (in welchem Setting arbeitet es?)
  - **Output-Format** (wie soll die Antwort aussehen?)
- Bessere Prompts ⇒ bessere Qualität, weniger Halluzinationen, weniger Trial & Error.

**Merkformel**

> Rolle + Kontext + Output-Format

---

## Lektion 2 – Prompting Techniken

**Techniken**

- **Zero-Shot**
  - Keine Beispiele, nur Anweisung.
  - Einsatz: einfache, bekannte Tasks (Übersetzen, leichte Umformung, kurze Erklärungen).

- **Few-Shot**
  - Du gibst **Beispiele** vor (Input → gewünschter Output).
  - Einsatz: eigenes Schema / Format, Labels, interne Klassifikationen.

- **Chain-of-Thought**
  - Modell soll **Schritte / Gedankengang** explizit machen.
  - Einsatz: mehrstufiges Denken, Root-Cause-Analysen, komplexe Entscheidungen.

**Merksatz**

- Few-Shot = **Beispiele geben**  
- Chain-of-Thought = **Schritte zeigen lassen**

---

## Lektion 3 – Prompt-Formatierung und Struktur

**Struktur im Prompt**

- Klar trennen:
  - **Anweisung** (was das Modell tun soll)
  - **Kontext** (Hintergrund, System, Business-Kontext)
  - **Input** (Logs, SQL, Beschreibungen, Text)
  - **Output-Vorgabe** (Form, Länge, Zielgruppe)

**Wichtige Elemente**

- **Labels / Sections**:
  - Beispiel:
    - `Kontext:`
    - `Aufgabe:`
    - `Input:`
    - `Output-Format:`

- **Delimiter**:
  - Klare Start-/End-Markierung von Input-Blöcken.
  - Modell erkennt Bereiche sauberer und hält Format besser ein.

**Effekt**

- Antworten werden:
  - klarer,
  - konsistenter,
  - format-treuer.

---

## Lektion 4 – Reduzierung von Halluzinationen mit Prompting

**Grounding**

- Kontext explizit mitgeben:
  - Logs, Doku, Schema, Config, Tickets, etc.
- Dazu sagen:
  - „Antworte nur basierend auf diesem Kontext …“

**Citations**

- Antworten prüfbar machen:
  - „Zitiere relevante Stellen aus der Doku / den Logs wörtlich als Beleg.“
  - „Füge nach jeder Aussage die passende Textstelle an.“

**Scope begrenzen**

- Thema und Umfang einschränken:
  - „Nur diese Tabelle …“
  - „Nur dieses Log-Snippet …“
  - „Maximal 3 Punkte / maximal 5 Sätze …“

**Unsicherheit erlauben**

- Anweisung:
  - „Wenn Informationen fehlen, erfinde nichts.“
  - „Sage explizit, dass du es nicht sicher sagen kannst.“
  - „Formuliere Vermutungen als Hypothesen.“

**Risiko-Erkennung**

- Hohe Hallu-Gefahr bei:
  - sehr vagen Fragen,
  - extrem breiten Fragen ohne Kontext,
  - sehr spezifischen Fragen zu Systemen, deren Doku nicht gegeben ist.

---

## Lektion 5 – Iterieren und Debugging von Prompts

**Debugging-Mindset**

- Bei schlechter Antwort:
  - nicht „Modell ist schlecht“,
  - sondern zuerst: „Mein Prompt ist noch nicht klar genug.“

**Typische Prompt-Bugs**

1. **Mehrdeutig**
   - Unklare Aufgabe („Analysiere das“, „Fasse zusammen“).
   - Keine Zielgruppe, kein Fokus, keine Längenangabe.

2. **Kontext fehlt**
   - Kein Tech-Stack, keine Logs, keine Ziele, kein Business-Kontext.

3. **Widersprüchlich**
   - „Antworte kurz, aber extrem detailliert.“
   - „Für Senior Engineers und Management gleichzeitig.“

**Iterationszyklus**

1. Prompt ausführen (**Test**).
2. Antwort beobachten:
   - Was genau ist schlecht? (zu allgemein, Thema verfehlt, Format ignoriert, halluziniert …)
3. Vermutete Ursache im Prompt:
   - Mehrdeutig?
   - Kontext fehlt?
   - Widersprüchlich?
4. **Gezielt** 1–2 Dinge ändern:
   - Ziel präzisieren,
   - Kontext ergänzen,
   - Zielgruppe klar setzen,
   - Output-Format schärfen.
5. Neu testen und ggf. wiederholen.

**AI als Prompt-Reviewer**

- Meta-Prompt-Beispiel:

  „Hier ist mein Prompt: `<DEIN PROMPT>`.  
  Analysiere ihn und sag mir:  
  1. Wo ist er mehrdeutig?  
  2. Wo fehlt Kontext?  
  3. Gibt es widersprüchliche Anforderungen?  
  Mach 1–2 konkrete Verbesserungsvorschläge mit kurzer Begründung.“

---

# Prompt Engineering Cheat Sheet

## Grundprinzip

Ein guter Prompt besteht meistens aus:

```text
Rolle + Aufgabe + Kontext + Constraints + Output-Format + Beispiel
```

### Beispiel

```text
Du bist ein Senior Data Engineer.

Erkläre einem Junior den Unterschied zwischen Batch und Streaming.

Kontext:
Wir verwenden Databricks und Kafka.

Vorgaben:
- einfach erklären
- maximal 5 Bulletpoints
- ein kleines Beispiel verwenden

Output:
Markdown
```

---

# 1. Zero-Shot Prompting

## Was ist das?

Du gibst dem Modell **nur die Aufgabe**, aber keine Beispiele.

```text
Aufgabe → Antwort
```

## Beispiel

```text
Erkläre einem Studenten einfach den Unterschied zwischen
INNER JOIN und LEFT JOIN.
```

## Wann verwenden?

Gut für:

- einfache Fragen
- bekannte Themen
- Zusammenfassungen
- Übersetzungen
- Standardaufgaben

## Vorteile

- schnell
- wenig Prompt-Aufwand
- gut für einfache Aufgaben

## Nachteile

Das Modell muss selbst interpretieren, **wie genau die Antwort aussehen soll**.

### Merksatz

> Keine Beispiele → Zero Shot

---

# 2. Few-Shot Prompting

## Was ist das?

Du gibst dem Modell **mehrere Beispiele**, damit es erkennt, welches Muster oder Format du erwartest.

```text
Beispiel 1
Beispiel 2
Beispiel 3
→ neue Aufgabe
```

## Beispiel

```text
Ordne Support-Tickets einer Kategorie zu.

Beispiele:

Input:
"Mein Passwort funktioniert nicht."

Output:
Authentication

Input:
"Die Anwendung ist extrem langsam."

Output:
Performance

Input:
"Ich kann keine Verbindung zur Datenbank herstellen."

Output:
Database

Nun klassifiziere:

"Mein Benutzerkonto wurde gesperrt."
```

Erwartete Antwort:

```text
Authentication
```

## Wann verwenden?

Sehr gut für:

- Klassifikation
- strukturierte Ausgaben
- Unternehmensstandards
- Schreibstil
- Datenextraktion
- wiederkehrende Aufgaben

## Vorteile

Du **zeigst** dem Modell, was du willst, statt es nur zu beschreiben.

### Merksatz

> Beispiele geben → Few Shot

---

# 3. Chain of Thought – CoT

## Was ist das?

Bei Chain of Thought wird eine komplexere Aufgabe **systematisch in Zwischenschritte zerlegt**.

Praktisch ist es sinnvoll, nach einer strukturierten Herleitung zu fragen.

## Einfaches Beispiel

```text
Berechne den Endpreis.

Ein Produkt kostet 120 €.
Es gibt 25 % Rabatt.
Danach werden 19 % MwSt. berechnet.

Gehe strukturiert vor:

1. Ausgangspreis
2. Rabatt berechnen
3. Preis nach Rabatt
4. MwSt. berechnen
5. Endpreis
```

## Struktur

```text
Problem
  ↓
Schritt 1
  ↓
Schritt 2
  ↓
Schritt 3
  ↓
Lösung
```

## Wann verwenden?

Gut für:

- Mathematik
- SQL-Logik
- Architekturfragen
- Debugging
- Analysen
- komplexe Probleme

## Vorteil

Komplexe Aufgaben werden nachvollziehbarer und weniger fehleranfällig.

### Merksatz

> Komplexe Aufgabe → in Schritte zerlegen

---

# 4. Tree of Thought – ToT

## Was ist das?

Bei Chain of Thought wird meist **ein Lösungsweg verfolgt**.

Tree of Thought geht einen Schritt weiter und untersucht **mehrere mögliche Lösungswege parallel**.

```text
             Problem
          /     |      \
       Idee A  Idee B  Idee C
         |       |       |
      Analyse Analyse Analyse
          \      |      /
           Vergleich
              ↓
           Ergebnis
```

## Beispiel

```text
Wir wollen eine RAG-Anwendung für einen IT-Support bauen.

Entwickle drei mögliche Architekturen:

A: einfache MVP-Architektur
B: skalierbare Cloud-Architektur
C: Enterprise-Architektur

Bewerte jede Architektur anhand von:

- Komplexität
- Kosten
- Skalierbarkeit
- Wartbarkeit
- Implementierungsaufwand

Vergleiche anschließend die Trade-offs.
```

## Wann verwenden?

Sehr gut bei:

- Softwarearchitektur
- Produktideen
- Strategie
- Lösungsdesign
- Debugging
- komplexen technischen Entscheidungen

## Unterschied zu CoT

```text
Chain of Thought:

Problem
  ↓
Schritt
  ↓
Schritt
  ↓
Lösung
```

```text
Tree of Thought:

Problem
 ├── Lösung A
 ├── Lösung B
 └── Lösung C
      ↓
   Vergleich
```

### Merksatz

> Ein Lösungsweg = CoT  
> Mehrere Lösungswege = ToT

---

# 5. Iterative Prompting

## Was ist das?

Beim iterativen Prompting versuchst du nicht, direkt mit einem Prompt das perfekte Ergebnis zu erzeugen.

Du verbesserst das Ergebnis Schritt für Schritt.

```text
Version 1
   ↓
Feedback
   ↓
Version 2
   ↓
Verbesserung
   ↓
Version 3
```

## Beispiel

### Prompt 1

```text
Erstelle eine Architektur für eine RAG-Anwendung.
```

### Prompt 2

```text
Vereinfache die Architektur auf ein MVP.
```

### Prompt 3

```text
Ergänze eine Vector Database.
```

### Prompt 4

```text
Ergänze LangGraph für Agent Workflows.
```

### Prompt 5

```text
Ergänze Monitoring mit Langfuse.
```

## Wann verwenden?

Sehr sinnvoll bei:

- Programmierung
- Dokumenten
- Architektur
- Produktentwicklung
- Datenanalyse
- längeren Projekten

## Vorteile

Du steuerst das Ergebnis kontrolliert in die gewünschte Richtung.

### Merksatz

> Prompting ist ein Prozess, kein einzelner Prompt

---

# 6. Self-Criticism / Self-Review

## Was ist das?

Das Modell erstellt zuerst eine Lösung und überprüft diese danach **kritisch auf Fehler, Schwächen oder Verbesserungspotenzial**.

## Struktur

```text
1. Lösung erstellen
2. Schwachstellen suchen
3. Verbesserungen vorschlagen
4. Lösung überarbeiten
```

## Beispiel

```text
Erstelle eine REST-API-Architektur für ein Event-System.

Danach überprüfe deine eigene Lösung auf:

- Security-Probleme
- Skalierungsprobleme
- unnötige Komplexität
- fehlende Komponenten
- schlechte Designentscheidungen

Erstelle anschließend eine verbesserte Version.
```

## Beispiel für Code

```text
Analysiere folgenden Python-Code.

Schritt 1:
Finde Bugs.

Schritt 2:
Finde mögliche Security-Probleme.

Schritt 3:
Bewerte Lesbarkeit und Wartbarkeit.

Schritt 4:
Erstelle eine verbesserte Version.
```

## Wann verwenden?

Sehr gut bei:

- Code Reviews
- Architektur
- Texten
- Konzepten
- SQL
- Dokumentationen

### Merksatz

> Erst erstellen → dann kritisieren → dann verbessern

---

# 7. Reverse Engineering Prompting

## Was ist das?

Beim Reverse Engineering gibst du dem Modell ein **bereits vorhandenes Ergebnis** und lässt es analysieren, welche Struktur, Regeln oder Logik dahinterstecken.

Normalerweise:

```text
Regeln → Output
```

Beim Reverse Engineering:

```text
Output → Regeln erkennen
```

## Beispiel

Vorhandener Report:

```text
Incident: Database Connection Failure

Severity: High

Cause:
Database server unavailable.

Impact:
Application cannot retrieve customer data.

Action:
Check database availability and network connectivity.
```

Prompt:

```text
Analysiere dieses Format.

Identifiziere:

- Struktur
- Schreibstil
- Reihenfolge
- Ton
- Detailgrad

Erstelle daraus eine allgemeine Prompt-Vorlage,
mit der weitere Incident Reports im gleichen Stil erstellt werden können.
```

Mögliches Ergebnis:

```text
Du bist ein IT Incident Analyst.

Erstelle einen Incident Report mit:

1. Incident
2. Severity
3. Cause
4. Impact
5. Action

Schreibe kurz, sachlich und technisch.
```

## Wann verwenden?

Besonders nützlich bei:

- Unternehmensdokumenten
- bestehenden Reports
- Code
- APIs
- SQL Queries
- Schreibstilen
- bestehenden Prompts
- Templates

### Merksatz

> Du hast das Ergebnis und willst herausfinden, wie man es erzeugt

---

# Die 7 wichtigsten Strategien im Überblick

| Strategie | Grundidee | Typischer Einsatz |
|---|---|---|
| **Zero Shot** | Keine Beispiele | Einfache Aufgaben |
| **Few Shot** | Beispiele vorgeben | Klassifikation, Format |
| **Chain of Thought** | Problem in Schritte zerlegen | Logik, Mathematik |
| **Tree of Thought** | Mehrere Lösungswege prüfen | Architektur, Strategie |
| **Iteration** | Ergebnis schrittweise verbessern | Komplexe Projekte |
| **Self-Criticism** | Eigene Lösung überprüfen | Code, Konzepte |
| **Reverse Engineering** | Vorhandenes Ergebnis analysieren | Templates, Reports |

---

# Universal Prompt Template

```markdown
# Rolle
Du bist ein erfahrener [ROLLE].

# Aufgabe
Deine Aufgabe ist es, [AUFGABE].

# Kontext
[RELEVANTER KONTEXT]

# Vorgehen
1. Analysiere die Aufgabe.
2. Zerlege sie in sinnvolle Teilprobleme.
3. Prüfe mehrere Optionen, wenn sinnvoll.
4. Identifiziere mögliche Fehler oder Risiken.
5. Erstelle anschließend das Ergebnis.

# Anforderungen
- [ANFORDERUNG 1]
- [ANFORDERUNG 2]
- [ANFORDERUNG 3]

# Output
Gib das Ergebnis als [MARKDOWN / JSON / TABELLE / CODE] aus.
```

---

# Strategien kombinieren

Die Strategien müssen nicht einzeln verwendet werden.

In der Praxis kannst du mehrere kombinieren:

```text
Few Shot
+
Tree of Thought
+
Self-Criticism
+
Iteration
```

## Beispiel

```text
Du bist ein Senior Software Architect.

Entwickle eine Architektur für eine RAG-Anwendung.

Hier sind zwei Beispiele für gute Architekturvorschläge:
[Beispiel 1]
[Beispiel 2]

Erstelle drei mögliche Lösungsansätze:

1. MVP
2. Cloud-native
3. Enterprise

Vergleiche die drei Ansätze hinsichtlich:

- Kosten
- Skalierbarkeit
- Komplexität
- Wartbarkeit

Überprüfe danach deine eigene Empfehlung auf Schwächen und
erstelle eine verbesserte Version.

Output:
Markdown
```

---

# Kurzform zum Lernen

```text
Zero Shot
→ Keine Beispiele

Few Shot
→ Beispiele geben

Chain of Thought
→ Schrittweise denken

Tree of Thought
→ Mehrere Lösungswege untersuchen

Iteration
→ Schrittweise verbessern

Self-Criticism
→ Eigene Lösung überprüfen

Reverse Engineering
→ Vom Ergebnis auf Regeln schließen
```

# Wichtigste Regel

> Je komplexer die Aufgabe, desto wichtiger werden Kontext, klare Anforderungen, Beispiele und ein definiertes Output-Format.

Ein guter Prompt sagt dem Modell nicht nur **was** es tun soll, sondern auch:

```text
WER soll antworten?
WAS soll gemacht werden?
WARUM / in welchem Kontext?
WIE soll vorgegangen werden?
WELCHE Regeln gelten?
WIE soll das Ergebnis aussehen?
```
