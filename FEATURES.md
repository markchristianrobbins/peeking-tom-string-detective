# Features

---
## Back to...
- ▪️[AGENTS.md](AGENTS.md)
- ▪️[AILOG.md](AILOG.md)
- ▪️[AITASKS.md](AITASKS.md)
- ▪️[BUILD.md](BUILD.md)
- ▪️[CODE.md](CODE.md)
- 🔸[FEATURES.md](FEATURES.md)
- ▪️[MANUAL.md](MANUAL.md)
- ▪️[README.md](README.md)
- ▪️[SPEC.md](SPEC.md)
- ▪️[TESTING.md](TESTING.md)

Welcome to **Peeping Tom String Detective (PTSD)**!
This guide details all user-facing capabilities, UI patterns, and commands offered by the extension to inspect matches of identical or relative segments in active documents.

## Feature Groups

### 🔍 1. Dynamic Token Extraction & Identification
<a id="extraction" name="extraction"></a>
Automatically retrieves and targets diverse lexical segments exactly where the active keyboard cursor resides, avoiding any manual copy-paste actions.
- **[Exact Line Parsing (`lineExact`)](#exact-line-parsing)** - Grabs the literal code or text line.
- **[Trimmed Line Harvesting (`lineWithin`)](#trimmed-line-harvesting)** - Automatically trims leading/trailing spaces for quick comparisons.
- **[Quoted/Braced Containment Resolver (`quoted`)](#quotedbraced-containment-resolver)** - Intelligently locates nested scopes of paired wrappers like quotes and brackets.
- **[Identifier Parser (`identifier`)](#identifier-parser)** - Extracts deep dot-notated objects or variable names.
- **[Word Bound Locator (`word`)](#word-bound-locator)** - Resolves standard term boundaries.

### 🗺️ 2. Advanced Section Context Tracking
<a id="context" name="context"></a>
Specifically active within Markdown documentation (.md files) to keep logical coordinate breadcrumbs appended alongside matches.
- **[Immediate Heading Capturer (`immediateSection`)](#immediate-heading-capturer)** - Finds the closest parent header above current lines.
- **[Full Ancestry Path Generator (`pathSection`)](#full-ancestry-path-generator)** - Builds sequential breadcrumb paths from the document root down.

### ⚡ 3. Multi-Functional Navigation & Clipboard Verbs
<a id="verbs" name="verbs"></a>
Exposes powerful actions to interact with matching results.
- **[Live Preview Browsing (`browse`)](#live-preview-browsing)** - Dynamically scrolls the editor to look at highlighted matches.
- **[Directional Match Leaps (`next` / `prev`)](#directional-match-leaps)** - Leaps focus onto next/previous match positions.
- **[Context-Aware Clipboard copy (`copy`)](#context-aware-clipboard-copy)** - Copies matches with options for markdown metadata.
- **[Context-Aware Code Injection (`inject`)](#context-aware-code-injection)** - Inserts matches directly beneath current lines.


## All Features

### Exact Line Parsing
- Group: [Dynamic Token Extraction & Identification](#extraction)
Targets the literal content of the current cursor's line, preserved in its original spacing form. Normalizes spaces and tabs when doing search queries to find matches.

### Trimmed Line Harvesting
- Group: [Dynamic Token Extraction & Identification](#extraction)
Acts as a quick shorthand tool to search for matching lines regardless of outer margins, ignoring start/end indentations.

### Quoted/Braced Containment Resolver
- Group: [Dynamic Token Extraction & Identification](#extraction)
Crawls outwards from the cursor position to find the bounds of matched bracket/brace/quote symbols (`"`, `'`, `` ` ``, `[`, `{`, `(`, etc.) and returns the string content inside. In nested expressions, it extracts the narrowest wrapping level containing the cursor.

### Identifier Parser
- Group: [Dynamic Token Extraction & Identification](#extraction)
Scans active lines to isolate JavaScript, TypeScript, or JSON-styled identifier chains under the cursor, such as object properties (`myObject.deepProperty.member`).

### Word Bound Locator
- Group: [Dynamic Token Extraction & Identification](#extraction)
Invokes standard editor word range bindings to find instances matching simple keyword text under the cursor.

### Immediate Heading Capturer
- Group: [Advanced Section Context Tracking](#context)
Traverses upwards from any matching markdown line to determine which heading (e.g. `## Feature Groups`) it logically belongs to.

### Full Ancestry Path Generator
- Group: [Advanced Section Context Tracking](#context)
Parses all parent, grandparent, and ancestor markdown headings to build hierarchical breadcrumbs representing section structures (e.g., `# Features > ## Feature Groups > ### 🗺️ 2...`).

### Live Preview Browsing
- Group: [Multi-Functional Navigation & Clipboard Verbs](#verbs)
Launches an immersive QuickPick list of matches. Scrolling through this list automatically scrolls the main editor to instantly look at (preview) the matched area in context without modifying the user's cursor position or permanent selection.

### Directional Match Leaps
- Group: [Multi-Functional Navigation & Clipboard Verbs](#verbs)
Provides direct single-click jumps downstream (`next`) or upstream (`prev`) relative to the active line index.

### Context-Aware Clipboard copy
- Group: [Multi-Functional Navigation & Clipboard Verbs](#verbs)
Saves matching strings to the clipboard. In markdown documents, it prompts the user to select whether they want to copy just the raw lines, or suffix them with their parent heading or complete ancestry breadcrumbs.

### Context-Aware Code Injection
- Group: [Multi-Functional Navigation & Clipboard Verbs](#verbs)
Inserts matches directly underneath the current cursor line. In markdown mode, this supports appending structural heading contexts to results.

---
## Go Back to...
- ▪️[AGENTS.md](AGENTS.md)
- ▪️[AILOG.md](AILOG.md)
- ▪️[AITASKS.md](AITASKS.md)
- ▪️[BUILD.md](BUILD.md)
- ▪️[CODE.md](CODE.md)
- 🔸[FEATURES.md](FEATURES.md)
- ▪️[MANUAL.md](MANUAL.md)
- ▪️[README.md](README.md)
- ▪️[SPEC.md](SPEC.md)
- ▪️[TESTING.md](TESTING.md)
