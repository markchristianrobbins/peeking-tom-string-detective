# Spec

This document compiles the user requirements and instructions from `AGENTS.md` and provides detailed documentation of how the extension was architected and built.

---
## Back to...
- ▪️[AGENTS.md](AGENTS.md)
- ▪️[AILOG.md](AILOG.md)
- ▪️[AITASKS.md](AITASKS.md)
- ▪️[BUILD.md](BUILD.md)
- ▪️[CODE.md](CODE.md)
- ▪️[FEATURES.md](FEATURES.md)
- ▪️[MANUAL.md](MANUAL.md)
- ▪️[README.md](README.md)
- 🔸[SPEC.md](SPEC.md)
- ▪️[TESTING.md](TESTING.md)

---

## 📋 Originally Requested Specifications

### 1. Application & Identification
- **Name**: Peeping Tom String Detective (PTSD) / `peeking-tom-string-detective`
- **Goal**: Introduce a high-precision, multi-context token harvesting and visual review navigation system. PTSD enables developers to immediately isolate, browse, traverse, copy, and inject recurring text patterns (lines, trimmed contents, quotes, symbols, identifiers, and words) in real-time from active document buffers.

### 2. Context Extraction Specifications
The tool must automatically detect and extract five distinct token dimensions from the active cursor coordinates:
- **Exact Line (`lineExact`)**: The literal content of the current cursor's line, preserved in its original spacing form.
- **Trimmed Line (`lineWithin`)**: The current cursor line, with leading and trailing whitespaces stripped.
- **Quoted / Braced Substring (`quoted`)**: The inner contents of balanced bounding characters enclosing the current cursor position. Bounding pairs include double quotes (`"`), single quotes (`'`), backticks (`` ` ``), square brackets (`[`), curly braces (`{`), and parentheses (`()`). In nested situations, it must resolve the narrowest valid scope containing the cursor.
- **Identifier Substrings (`identifier`)**: Nested alphanumeric/dot identifier names under the cursor matching the standard regex pattern: `/[a-zA-Z_$][a-zA-Z0-9_$]*(?:\.[a-zA-Z_$][a-zA-Z0-9_$]*)*/g`.
- **Word Boundaries (`word`)**: The standard token bounds retrieved via the editor's text provider or `document.getWordRangeAtPosition`.

### 3. Match Engine Specifications
Matching operations must conform to the following policies:
- **Exact Match (`lineExact`)**: The search comparison must be space-and-tab-insensitive by normalizing multiple runs of whitespace/tabs into a single space and stripping peripheral whitespace from both candidates before resolving matches.
- **Substring Match (others)**: Performs standard case-sensitive lookup checks using direct containment queries (`rawText.includes(target)`).

### 4. Advanced Markdown Context Harvesting
When processing markdown documents (.md files), each match candidate must be enriched with its logical document outline coordinates:
- **Immediate Parent Section**: The nearest preceding heading (e.g. `## Section 1`) discovered when scanning upward from the match line.
- **Hierarchical Ancestry Path**: The complete chain of contextual heading layers traced back to the document root (e.g., `# Root > ## Parent > ### Match Area`).

---

## 🛠️ Implementation Details (How We Built It)

### 1. Robust Dual-Stage Multi-Picker Orchestrator
- Declares the master coordinator command `ptsd.orchestrate`.
- Inspects the active document and active cursor positions to dynamically harvest other valid tokens.
- Generates a custom `QuickPick` showing labels of match scopes alongside previews of actual values.
- Presents a nested Action Verb Picker offering high-order operations (`browse`, `next`, `prev`, `copy`, and `inject`).

### 2. Static Target Sub-Routers
- Contributes standalone shortcut loops (`ptsd.search.<type>`) that bypass the target choosing stage, focusing directly on action inputs.
- Registers 25 independent direct combinations (`ptsd.<type>.<verb>`) to bypass pickers entirely, enabling instant hotkey bindings.

### 3. Immersive Live Preview Browsing
- Implements an interactive hover state on the `browse` list using VS Code's `onDidChangeActive` QuickPick hook.
- Updates the main viewport scroll location continuously when scrolling through search matching alternatives, letting users view candidate areas without selecting them.
- Disposes of state cleanly and restores selection anchors smoothly when the interaction is confirmed or dismissed (via Escape).

---

## 🎯 Implemented Technical Concerns & Optimization Features
- **Empty Element Defenses**: Only triggers picker options for tokens that successfully return a non-empty string.
- **No-Match Safe-Locks**: Displays a standard VS Code warning message (`showWarningMessage`) rather than opening empty pickers if a resolved string search term yields 0 occurrences in the file.
- **Escape Grace**: Traps unaccepted picker dialog finishes gracefully to prevent console or crash warnings in the VS Code host shell.
- **Safe Markdown Injection**: Insert ranges are relative to the active selection line, ensuring that code pastes do not conflict with concurrent modification handles.

---
## Go Back to...
- ▪️[AGENTS.md](AGENTS.md)
- ▪️[AILOG.md](AILOG.md)
- ▪️[AITASKS.md](AITASKS.md)
- ▪️[BUILD.md](BUILD.md)
- ▪️[CODE.md](CODE.md)
- ▪️[FEATURES.md](FEATURES.md)
- ▪️[MANUAL.md](MANUAL.md)
- ▪️[README.md](README.md)
- 🔸[SPEC.md](SPEC.md)
- ▪️[TESTING.md](TESTING.md)
