# Linux Office

Linux Office is a Rust-first office suite project. The initial product is a
page-based word processor with Linux Wayland, Windows, and macOS as
release-blocking platforms.

Writer is the active product. Placeholders for the planned Spreadsheet,
Presentation, Notes, Database, and Diagram products live in
[`apps/`](apps/README.md). They make suite-wide ownership visible during
development without adding empty applications to the Cargo workspace.

The repository currently contains the first native GUI vertical slice:

- Typed document IDs, revisions, anchors, selections, and transactions.
- A Writer document model with paragraph editing and styles.
- Transactional undo and redo using semantic inverse operations.
- Deterministic page layout in integer EMU coordinates.
- A renderer-neutral scene containing positioned glyph runs.
- A validated, attributed-text shaping contract with positioned glyphs,
  clusters, caret positions, resolved font faces, and explicit substitution
  diagnostics.
- A reusable GPUI shaping adapter backed by the platform text system for the
  interactive application.
- A reusable GPUI backend that paints the renderer-neutral `office_scene`
  directly, including monochrome and color-emoji glyphs.
- Shared bounded file I/O and atomic replacement infrastructure.
- OpenDocument Text (`.odt`) import and export for the currently supported
  document model, with explicit compatibility warnings for unsupported
  constructs.
- A native GPUI window using Wayland on Linux.
- A scrollable page canvas with native text input, selection, clipboard,
  paragraph splitting, paragraph styles, undo, and redo.
- New, Open, Save, Save As, dirty-state tracking, and unsaved-change
  protection using native platform dialogs and the Wayland desktop portal.

Run the Writer GUI:

```sh
cargo run -p writer_app
```

Run the headless model lab:

```sh
cargo run -p writer_app --bin writer_model_lab
```

Run validation:

```sh
cargo fmt --all --check
cargo clippy --workspace --all-targets -- -D warnings
cargo test --workspace
```

The UI uses the transitional project-owned GPUI fork described in
[ARCHITECTURE.md](ARCHITECTURE.md). The fork uses canonical `font-kit`,
`reqwest`, and `async-tar` releases and enables only Wayland on Linux. The
document, layout, and scene crates do not depend on GPUI.
