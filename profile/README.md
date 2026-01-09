<div align="center">
  <a href="https://velox-apps.github.io/velox/documentation/veloxruntime/"> 📚 Docs <a>
  —
  <a href="https://discord.gg/nZKv7kkvb"> 🎙 Discord <a>
</div>

# Velox

Velox brings the Tauri model to Swift: build desktop apps with a web UI and a Swift backend, backed by the Tao/Wry runtime under the hood. It aims to feel native to Swift developers while keeping the HTML/CSS/JS workflow you already know.

## Why use Velox

- Swift-first APIs for app lifecycle, windows, and webview control.
- Web UI + Swift backend in a single desktop app, no Rust required.
- Flexible asset loading: inline HTML for tiny apps or bundled assets for larger ones.
- Familiar IPC-style command bridge between your frontend and Swift logic.

## Get started quickly with create-velox-app

`create-velox-app` is the official scaffolding CLI that spins up a working project with sensible defaults and templates (vanilla, Hummingbird, Vue, Svelte, plus TypeScript variants).

```bash
swift run create-velox-app MyApp
```

The generated app is a bundled-assets Velox app with an `app://` asset loader and an `ipc://` command bridge. Set `VELOX_DEV_URL` to point the webview at a dev server for fast frontend iteration.

Explore the templates and usage details in `create-velox-app/README.md`.


## Velox CLI

Velox includes a CLI tool for development workflow, similar to Tauri's CLI.

### Building the CLI

```bash
swift build --product velox
```

The CLI binary will be available at `.build/debug/velox`.

### Commands

#### `velox init` - Initialize a New Project

Initialize Velox in a new or existing directory:

```bash
# Initialize with defaults (derives name from directory)
velox init

# Specify product name and identifier
velox init --name "MyApp" --identifier "com.example.myapp"

# Overwrite existing files
velox init --force
```

This creates:
```
your-project/
├── Package.swift       # Swift package manifest
├── Sources/
│   └── YourApp/
│       └── main.swift  # App entry point with IPC handlers
├── assets/
│   └── index.html      # Frontend UI template
└── velox.json          # Velox configuration
```

#### `velox dev` - Development Mode

Run the app in development mode with hot reloading:

```bash
# Run with auto-detected target
velox dev

# Specify a target explicitly
velox dev MyApp

# Run in release mode
velox dev --release

# Disable file watching
velox dev --no-watch

# Override dev server port
velox dev --port 3000
```

Features:
- Executes `beforeDevCommand` from velox.json (e.g., `npm run dev`)
- Waits for dev server at `devUrl` if configured
- Builds and runs the Swift app
- Watches for Swift file changes and rebuilds automatically
- Graceful shutdown with Ctrl+C

#### `velox build` - Production Build

Build the app for production:

```bash
# Release build (default)
velox build

# Debug build
velox build --debug

# Create macOS app bundle (.app)
velox build --bundle

# Specify target
velox build MyApp

# Debug build with app bundle
velox build --debug --bundle
```

The `--bundle` flag creates a complete macOS app bundle:
```
.build/release/MyApp.app/
├── Contents/
│   ├── Info.plist      # Generated from velox.json
│   ├── MacOS/
│   │   └── MyApp       # Executable
│   └── Resources/
│       └── assets/     # Frontend files (from frontendDist)
```
