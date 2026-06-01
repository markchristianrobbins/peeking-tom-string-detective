# Testing

You can use this interactive test sheet directly inside VS Code to verify that all systems are fully functional. Put your cursor on these checkbox lines, and mark them done!

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
- ▪️[SPEC.md](SPEC.md)
- 🔸[TESTING.md](TESTING.md)

---
## 🔵 Setup & Environment Check
- [ ] Confirm packaged extension `.vsix` file installs without error.
- [ ] Verify the extension registers 31 structural commands successfully under the `ptsd.*` namespace.
- [ ] Verify the extension activates lazily on-demand upon the execution of the first target command.

## 🟢 Interactive Target & Extraction Checks
Verify token harvesting capabilities by positioning the cursor at various points:
- [ ] **Exact Line (`lineExact`)**:
	- [ ] Position cursor on a line with multiple spaces or tabs.
	- [ ] Activating `ptsd.search.lineExact` should correctly extract the entire line, normalizing all whitespace sequences into a single space, and search for matches successfully.
- [ ] **Trimmed Line (`lineWithin`)**:
	- [ ] Position cursor on an indented block.
	- [ ] Verify `ptsd.search.lineWithin` successfully searches for matches of the line text excluding any indentation margins.
- [ ] **Quoted & Balanced Containment (`quoted`)**:
	- [ ] Position the cursor within single quotes (`'text'`), double quotes (`"text"`), or backticks (`` `text` ``). Verify the inner string is isolated.
	- [ ] Position the cursor within deep nested brackets (e.g. `const list = [ { outer: [ "inner cursor target" ] } ]`). Verify the containment resolver extracts only the narrowest balanced boundary containing the cursor position.
- [ ] **Identifier Dot-Chaining (`identifier`)**:
	- [ ] Position the cursor inside a deep nested object property string like `myObject.nestedSection.leafProperty`. 
	- [ ] Verify `ptsd.search.identifier` extracts the full dot-chain identifier instead of just a single word.
- [ ] **Word Boundaries (`word`)**:
	- [ ] Position cursor on a single plain word. Verify `ptsd.search.word` isolates the word.

## ⚡ Active Action / Verb Testing
Once a valid search term is isolated, test each execution action verb:
- [ ] **Live Peek Browser (`browse`)**:
	- [ ] Launch Browse and use arrow keys to navigate the matches QuickPick list.
	- [ ] Confirm the main text editor viewport scrolls automatically to reveal/preview each highlighted match live in context.
	- [ ] Press `Enter` on a highlighted item. Confirm the cursor and scroll viewport permanently lock onto the selected match line.
	- [ ] Press `Escape`. Confirm the viewport resets and returns safely to your original line coordinates without saving changes.
- [ ] **Downstream Jump Leap (`next`)**:
	- [ ] Run `next` action. Verify cursor leaps to the subsequent match downstream.
	- [ ] Run it at the last match in the file. Verify that a VS Code status bar message warns: "No next matching instances downstream."
- [ ] **Upstream Jump Leap (`prev`)**:
	- [ ] Run `prev` action. Verify cursor leaps to the preceding match upstream.
	- [ ] Run it at the first match in the file. Verify that a VS Code status bar message warns: "No previous matching instances upstream."

## 🕹️ Context-Aware Markdown Metadata Tracing
Open a `.md` markdown file to verify context enrichment:
- [ ] **Clipboard copy Context (`copy`)**:
	- [ ] Position cursor and trigger `copy` action on multiple matches.
	- [ ] **None**: Paste clipboard somewhere and verify only raw lines are copied.
	- [ ] **Immediate Parent**: Paste and verify each matched line has ` ## Heading Title` appended.
	- [ ] **Full Hierarchical Path**: Paste and verify matched lines have the ancestor breadcrumbs like ` # Master > ## Section > ### Subsection` appended.
- [ ] **Code Injection Context (`inject`)**:
	- [ ] Run `inject` action and choose "Full Hierarchical Path". 
	- [ ] Confirm the matched rows and their structural markdown header trails are pasted exactly onto a new line beneath your current cursor position.

## 🚀 Safe Exception & Interface Defense Controls
- [ ] **Empty Selection Defence**: Place cursor on an empty blank line. Verify empty targets (like `quoted` or `identifier`) do not show up as options in the master orchestrator picker.
- [ ] **No-Match Safe-Lock**: Search for a token that only exists on the active line and has no other repetitions. Verify that a VS Code warning modal pops up stating: "No matching instances found." and terminates gracefully.
- [ ] **Escape Grace**: Press `Escape` during any stage of the custom pickers or context prompts. Verify the system closes the UI silently without popping up error alerts.

---
## Go Back to...
- [AGENTS.md](AGENTS.md)
- [AILOG.md](AILOG.md)
- [AITASKS.md](AITASKS.md)
- [BUILD.md](BUILD.md)
- [CODE.md](CODE.md)
- [FEATURES.md](FEATURES.md)
- [MANUAL.md](MANUAL.md)
- [README.md](README.md)
- [SPEC.md](SPEC.md)
- [TESTING.md](TESTING.md)
