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

