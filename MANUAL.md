# Manual

This guide describes the structural architecture, module layout, internal algorithms, optimization behaviors, and technical specifications of the Peeping Tom String Detective (PTSD) extension.

---
## Back to...
- ▪️[AGENTS.md](AGENTS.md)
- ▪️[AILOG.md](AILOG.md)
- ▪️[AITASKS.md](AITASKS.md)
- ▪️[BUILD.md](BUILD.md)
- ▪️[CODE.md](CODE.md)
- ▪️[FEATURES.md](FEATURES.md)
- 🔸[MANUAL.md](MANUAL.md)
- ▪️[README.md](README.md)
- ▪️[SPEC.md](SPEC.md)
- ▪️[TESTING.md](TESTING.md)


## 🏗️ 1. Architecture Overview
PTSD is integrated as a lightweight workspace extension running in the VS Code Host environment. It utilizes standard `vscode` namespace APIs to coordinate between the main Text Editor buffers and visual QuickPick interaction dialogs. 

```text
                  ┌───────────────────────────────┐
                  │      Command Activation       │
                  │   (Orchestrated or Static)    │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │       Cursor Coordinates      │
                  │   (editor.selection.active)   │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │     getExtractors Engine      │
                  │  (Line/Trim/Quotes/ID/Words)  │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │       findMatches Loop        │
                  │ (Space Normalization Applied) │
                  └───────────────┬───────────────┘
                                  ▼
                  ┌───────────────────────────────┐
                  │      executeVerb Router       │
                  └──────┬─────────────────┬──────┘
                         │                 │
                         ▼                 ▼
          ┌─────────────────────┐   ┌─────────────────────┐
          │  Live Browser UI    │   │  Code/Clip Writers  │
          │ (Auto scroll peek)  │   │ (Context Appendage) │
          └─────────────────────┘   └─────────────────────┘
```


## 🧠 2. Core Modules & Systems

### A. Context Extractor (`getExtractors`)
- Read-only parser acting on coordinates of active document tabs.
- Scans around Cursor horizontal characters to extract raw coordinates, balanced delimiters, property words, and variables.

### B. Markdown Ancestry Surveyor (`getMarkdownContexts`)
- Active if the underlying document ID is `markdown`.
- Iterates reversed lines from the match index upward to capture parent `# Heading` elements.
- Uses stack accumulation to construct direct parents and full path hierarchies.

### C. Master Match Engine (`findMatches`)
- Scans full documents sequentially.
- If looking for exact matches, normalizes spacing using whitespace deduplication regex blocks before establishing equality. Other extraction types fall back to standard `includes()` queries.

### D. Interactive Selector Orchestrator (`promptVerbAndExecute`)
- Shows nested QuickPick modals with live matching tallies.
- Chains the target choosing flow seamlessly into action selectors.

### E. Action Vector Router (`executeVerb`)
- Coordinates the execution of user actions: Browse, Next/Previous jump, Copy, or Inject.


## 🔎 3. Core Algorithms

### A. Nested Brace/Quote Balanced Parser
To retrieve the narrowest enclosing quoted string or brackets containing the cursor, the extension loops through registered bounding pairs:
1. Performs sequential character scans using `lineText.indexOf(pair.open, searchStart)`.
2. Matches right-bounds:
   - For identical boundary characters (like `'` or `"`), scans straight ahead to locate the next pairing character.
   - For opening and closing symbols (like `{}` or `[]`), runs a tracking counter (increasing on open bounds, decreasing on close bounds) to locate the balanced closing pair.
3. Performs a bounding validation check: `charIdx >= startIdx && charIdx <= endIdx + 1`.
4. Saves boundaries if the matching range is narrower than any previously saved bounding structures (`matchLength < narrowestLength`).

### B. Identifier Dot-Chain Extractor
- Employs the dot-notation RegExp pattern `/[a-zA-Z_$][a-zA-Z0-9_$]*(?:\.[a-zA-Z_$][a-zA-Z0-9_$]*)*/g`.
- Crawls forward on the matched line, checking index coordinates against active cursor borders to extract fully qualified property chains under the cursor.

### C. Spacing-Insensitive Exact Match Normalizer
To ensure search queries are resilient against spacing differences, exact matching normalizes whitespace using:
```js
const normalize = (str) => str.trim().replace(/[\t ]+/g, ' ');
```
This strips outer spaces and scales multiple spaces/tabs down to a single character before match comparisons.

### D. Live-Preview QuickPick Scroll Engine
- Generates QuickPick arrays with a label specifying match line indexes and body texts.
- Leverages the `onDidChangeActive` event listener on standard VS Code QuickPick inputs.
- When an item in the list is highlighted, focuses and scrolls the editor viewport directly (`editor.revealRange`) to peek at the Match location in real-time.
- If confirmed (Accepted), permanently locks the scroll focus and cursor coordinates onto that match.
- If canceled (Hidden/Dismissed), safely disposes of the QuickPick state without affecting original selections.


## 🛰️ 4. Commands, Keybindings & Context Flags
The extension contributes three major command layers registered inside the `ptsd.*` namespace:
1. **The Dynamic Master Router**:
   - `ptsd.orchestrate`: Triggers the target token choosing menu, then asks for the action verb.
2. **Standard Specialized Shortcuts**:
   - `ptsd.search.<targetType>`: Bypasses the target choosing picker. Directly prompts the user only for the action to take (Browse, Next, Copy, etc.).
3. **Direct Action Combinations**:
   - `ptsd.<targetType>.<actionVerb>`: Bypasses ALL menu pickers, executing the specific action immediately on the active context. Highly recommended for keyboard shortcut bindings.


## 🔧 5. Workspace Build & Configuration
The workspace configuration consists of a standard pure CommonJS Node runtime:
- **Zero-Bundler Assembly**: VS Code loads `extension.js` directly as a lightweight single file module.
- **Dependency Map**: Employs `@types/vscode` devDependencies for full IDE typing support during development.
- **Lint & Validation**: Code can be easily checked for syntax correctness or styling guidelines before packaging. No manual compiler/transpiler stages are required.

---
## Go back to...
- ▪️[AGENTS.md](AGENTS.md)
- ▪️[AILOG.md](AILOG.md)
- ▪️[AITASKS.md](AITASKS.md)
- ▪️[BUILD.md](BUILD.md)
- ▪️[CODE.md](CODE.md)
- ▪️[FEATURES.md](FEATURES.md)
- 🔸[MANUAL.md](MANUAL.md)
- ▪️[README.md](README.md)
- ▪️[SPEC.md](SPEC.md)
- ▪️[TESTING.md](TESTING.md)
