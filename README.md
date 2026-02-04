# Ruby/Prism AST Tree Viewer — Spec

[visit Viewer](https://ko1.github.io/astv/)

## Purpose
Visualize Prism AST as a compact tree and compare it with a traditional text representation.

## Inputs
- Ruby source (parsed in the browser via Ruby.wasm + Prism)
- JSON (AST object) pasted manually

## Initial Load Behavior
- If URL has `?p=...`, its value is inserted into the Ruby editor.
- Otherwise the sample Ruby code is used.
- After the editor is populated, Ruby -> AST is executed automatically.

## Core Behavior
- Ruby input -> `Prism.parse` -> JSON -> Tree
- Text tab shows `result.value.inspect`
- Tree tab shows a compact node graph

## Node Rules
- A node is an object that has a `type` key.
- An array becomes child nodes only if **all** elements are node objects.
- Empty arrays are treated as additional info (not child nodes).
- Any object **without** `type` is treated as additional info.
- `location` is additional info.
- `locals` is additional info.

## Representative Value
- A node displays: `type` as the representative value.
- If the node has `name`, show: `type (name)`.

## Relations
- Relation labels are shown outside the node box.
- For array relations, show size: `relation (size: N)`.

## Details / Expansion
- Additional info is stored as details and can be expanded by clicking the node.
- Click again to collapse.
- While selecting text, clicking does not toggle expansion.
- Expand All / Collapse All buttons control every node.

## Text vs Tree
- Output pane is tabbed: Tree / Text.

## Ruby Editor
- Simple syntax highlight (overlay + highlight.js).
- Ctrl+Enter triggers Ruby -> AST.
- A node with `location` highlights the corresponding Ruby source range on hover.

## URL Share
- `?p=...` populates the Ruby editor.
- `Copy URL` builds a shareable URL with current editor content.

## UI Layout
- Left: Ruby input + JSON input
- Right: Tree/Text output
- Footer shows Ruby.wasm load status and version

## Security Notes
- Tree rendering uses DOM APIs (`textContent`) to reduce XSS risk.
- Ruby.wasm executes user-provided code; heavy input can freeze the page.

## Credits
- Built with assistance from Codex.

## Copyright
Copyright (c) 2026 Koichi Sasada

Repository:
```
https://github.com/ko1/astv
```
