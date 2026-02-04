# AST Tree Viewer (Spec)

## Purpose
Visualize Ruby/Prism AST as a compact tree and compare it with the traditional text output.

## Inputs
- Ruby source (parsed by Prism in the browser via Ruby.wasm)
- JSON (AST object) pasted manually

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

## UI
- Left: Ruby input + JSON input
- Right: Tree/Text output tabs
- Footer shows Ruby.wasm load status and version

## Security
- Tree rendering uses DOM APIs (`textContent`) instead of `innerHTML` to reduce XSS risk.
