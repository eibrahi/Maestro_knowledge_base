# 🐛 The Challenge of Debugging GenAI

### 🎲 Nicht-reproduzierbare Outputs

- **LLMs sind probabilistisch** → Gleicher Input kann unterschiedliche Antworten liefern.
- Klassisches Debugging nach dem Prinzip **„Bug einmal reproduzieren und fixen“** ist daher nur eingeschränkt effektiv.

### 📝 Prompt-Sensitivität

- **Prompts sind im Grunde Code** → Kleine Textänderungen oder veränderte Constraints können das Verhalten eines LLMs stark beeinflussen.
- Bereits minimale Anpassungen können zu erheblichen Unterschieden im **Output** führen.

### 🔍 Hidden Reasoning

- Sichtbar sind lediglich **Input und Output**, nicht der tatsächliche interne Entscheidungsweg des Modells.
- Klassische Debugging-Tools wie **Breakpoints** oder **State-Inspektion** greifen daher ins Leere.

### 🎯 Ergebnis

**Mehr Logs und Breakpoints allein reichen nicht aus.**

GenAI benötigt eigene **Debugging-Strategien**, die folgende Aspekte berücksichtigen:

- 🔄 **Multiple Runs** → Analyse über mehrere Durchläufe
- 📊 **Mustererkennung** → Identifikation wiederkehrender Verhaltensweisen
- ⚙️ **Prompt- und Parameter-Design** → Systematische Optimierung von Prompts und Modellparametern
