# Build

## Go to...
- ▪️[AGENTS.md](AGENTS.md)
- ▪️[AILOG.md](AILOG.md)
- ▪️[AITASKS.md](AITASKS.md)
- 🔸[BUILD.md](BUILD.md)
- ▪️[CODE.md](CODE.md)
- ▪️[FEATURES.md](FEATURES.md)
- ▪️[MANUAL.md](MANUAL.md)
- ▪️[README.md](README.md)
- ▪️[SPEC.md](SPEC.md)
- ▪️[TESTING.md](TESTING.md)

---

## 🏗️ 1. Workspace Configuration & Manifest
Peeping Tom String Detective is designed to be highly lightweight and is assembled as a bundle-free JavaScript extension targeting the VS Code Extension Host.

### Extension Packaging Manifest (`package.json`)
Our configuration uses declarations inside `package.json` to manage development workflows, dependencies, packaging limits, and command registrations:
- **Major Target Engine**: Compiles and activates against VS Code engines matching `^1.80.0` or higher.
- **Main Script Entry Point**: Points directly to `/extension.js` via the package manifest `"main"` field.
- **On-Demand Lazy Activation**: Utilizes VS Code's modern lazy activation pattern. `"activationEvents"` is intentionally maintained as a blank array `[]` because VS Code automatically initializes the extension on-demand as soon as any command declared under the `"contributes.commands"` namespace is executed by the user.

### Source Code File Inclusion Rules
To optimize package distribution and maintain clean downloads on the extension marketplace, only a focused set of file targets are marked under the manifest's `"files"` checklist:
- Executable script entry paths: `extension.js`
- Design resources or workspace indicators: `icon.jpg`
- Key legal and help files: `README.md`, `LICENSE`
- AI Primary Files metadata files: `AGENTS.md`, `AILOG.md`, `AITASKS.md`, `BUILD.md`, `FEATURES.md`, `MANUAL.md`, `SPEC.md`, `TESTING.md`


## 📦 2. Compilation and Packaging Workflow
Since the code runs directly on standard Node APIs, it requires no intermediate bundlers, transpilers, or build steps.

### Compiling and Designing VSIX Packages
To generate a local installable package (`.vsix` asset), standard package modules can be called:
1. Ensure developer packages are installed:
	```bash
	npm install
	```
2. Execute the packaging script declared in the manifest under `package`:
	```bash
	npm run package
	```
	This calls Microsoft's compiler CLI `vsce package` under the hood. The resulting packaged artifact will be saved in the directory root as:
	```text
	peeking-tom-string-detective-1.0.0.vsix
	```

### Workspace Installation Guidelines
To load the packaged `.vsix` file into local IDE assets:
1. **Using Terminal CLI**:
	```bash
	code --install-extension peeking-tom-string-detective-1.0.0.vsix
	```
2. **Using the Interactive UI**:
	- Open VS Code or Cursor.
	- Launch the Extensions tab (`Ctrl+Shift+X` or `Cmd+Shift+X`).
	- Select the `...` Actions menu top right.
	- Choose **Install from VSIX...** and select the `.vsix` compiled bundle.

---
## Go back to...
- ▪️[AGENTS.md](AGENTS.md)
- ▪️[AILOG.md](AILOG.md)
- ▪️[AITASKS.md](AITASKS.md)
- 🔸[BUILD.md](BUILD.md)
- ▪️[CODE.md](CODE.md)
- ▪️[FEATURES.md](FEATURES.md)
- ▪️[MANUAL.md](MANUAL.md)
- ▪️[README.md](README.md)
- ▪️[SPEC.md](SPEC.md)
- ▪️[TESTING.md](TESTING.md)
