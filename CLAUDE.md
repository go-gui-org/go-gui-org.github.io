# CLAUDE.md — go-gui-org

This is the `.github.io` repository for the **go-gui-org** GitHub organization.

## Organization purpose

Building a modern, cross-platform GUI framework for Go — `go-gui` — along with its
companion libraries.

## Sibling projects

| Repo | Purpose |
|------|---------|
| **go-gui** | Core framework — widgets, constraint layout, event system, GPU-accelerated retained-mode scene graph |
| **go-glyph** | Browser-quality text rendering — bidi, multi-grapheme clusters, complex scripts — plus vector icons and glyph rasterization |
| **go-charts** | Declarative charting — line, bar, area, pie, scatter, candlestick — incremental updates for real-time dashboards |
| **go-maps** | Tiled raster/vector map widget with projection handling, markers, and geospatial overlays |
| **go-term** | Embeddable terminal emulator — PTY, ANSI/VT parser, render surface as a go-gui widget |
| **go-edit** | Text editing — single-line to multi-cursor code editor, piece-table undo, syntax highlighting, completion hooks |

All sibling repos live under `github.com/go-gui-org/<repo>` and import each other
under the `github.com/go-gui-org/` module path.

## Conventions (applies to all sibling repos)

- Go modules rooted at `github.com/go-gui-org/<repo>`
- Cross-platform: macOS, Windows, Linux as first-class targets
- Public API stability is paramount — breaking changes require coordination across
  sibling repos
- README.md in each repo documents its scope, API surface, and relationship to
  `go-gui` core

## Website (this repo)

- All CSS lives inline in `index.html` `<style>` blocks
- `.feature-row` grid items (`.feature-section` text and `.feature-img`) must
  be **top-aligned** — `align-items: start`, never `center`. The text column
  and image column align to the top of the row.

### `showcase/` is generated — never edit it here

`showcase/index.html`, `main.wasm` and `wasm_exec.js` are published by the
`Deploy Showcase` workflow in `go-gui-org/go-gui`, which republishes this
repo with `force_orphan: true`. Any edit made to `showcase/` here is
silently discarded by the next go-gui push to main. The source is
`examples/showcase/index.html` in the go-gui repo — patch it there.

The showcase page is a Go WebAssembly app, so its CSP is not the same as
this repo's pages. It needs `'wasm-unsafe-eval'` in `script-src`, plus
`data:` in `font-src`/`img-src`/`media-src` (the icon font and every
embedded asset are served as data URLs). Dropping any of those leaves the
page stuck on its loading spinner, or missing all icons and images.
