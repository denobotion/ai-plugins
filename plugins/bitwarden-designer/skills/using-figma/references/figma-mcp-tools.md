# Figma Dev Mode MCP Server — Tool Reference

Per-tool reference for the Figma MCP server. Source: Figma's official developer documentation
at `developers.figma.com/docs/figma-mcp-server/tools-and-prompts/`. Some tools are marked
**remote only** — they are unavailable on desktop server installations.

## Read tools

### `get_design_context`

The primary read tool. Returns code (default: React + Tailwind), a screenshot, and structural
design metadata for a Figma Design or Figma Make selection.

- **Accepts:** a Figma selection or a frame URL.
- **Framework parameter:** a `clientFrameworks` field controls the code output (e.g., `angular`,
  `vue`, `react`). When the designer or downstream skill doesn't need framework-bound code,
  prefer the lighter-weight tools below.
- **Returns:** code reference, screenshot, design metadata.

### `get_metadata`

Sparse XML of layer IDs, names, types, positions, and sizes. Use as the cheap-orientation
read.

- **Accepts:** selection or page.
- **Returns:** layer-tree XML.

### `get_screenshot`

Visual screenshot of a selection (Figma Design or FigJam). No code, no metadata noise. Often
auto-captured as part of `get_design_context`, but available separately when only the image
is needed.

- **Accepts:** selection.
- **Returns:** PNG image.

### `get_variable_defs`

Extracts variables and styles used in the selection — colors, spacing, typography. The right
tool for "what tokens does this design use" and for detecting raw values that should be
library-bound.

- **Accepts:** selection.
- **Returns:** variable and style definitions.

### `get_libraries`

Lists subscribed and available design libraries on the file. Useful before proposing a new
pattern: confirm the design system is reachable and that the right library is loaded.

- **Accepts:** file context.
- **Returns:** library list with availability.

### `search_design_system`

Text-query the design system for components, variables, or styles. The best first move when
the designer says "we need a new pattern" — search before proposing.

- **Accepts:** text query.
- **Returns:** matching components, variables, or styles.

### `get_figjam`

Equivalent to `get_metadata` for FigJam boards: XML of layer IDs, names, types, positions,
sizes, and screenshots.

- **Accepts:** FigJam board selection.
- **Returns:** structural XML.

### `whoami`

Returns the authenticated Figma user (email, plans, seat type). Use when permission or seat
type matters — e.g., diagnosing why a write tool is unavailable.

## Code Connect tools

These map Figma components to their code counterparts. Mostly relevant inside
`evolving-design-system-components`; rarely needed in critique or copy review.

### `get_code_connect_map`

Returns existing mappings, source files, and snippets for selected component instances.

- **Accepts:** selected instance node IDs.
- **Returns:** mapping metadata.

### `get_code_connect_suggestions`

Returns suggested mappings for selected components. Auto-triggered by Figma in some flows.

### `get_context_for_code_connect`

Returns property definitions and variant options for a component. Used in combination with the
Code Connect skill flow.

### `add_code_connect_map`

Maps a Figma node to a code component reference. **Write tool — confirm with user first.**

### `send_code_connect_mappings`

Submits confirmed mappings. Auto-triggered after suggestions in some flows.

## Write tools

All write tools modify Figma state. Confirm scope and target before invoking, and report
exactly what was created or changed.

### `create_new_file`

Creates a new Design or FigJam file.

- **Accepts:** team or organization selection.

### `upload_assets`

Uploads PNG/JPG/GIF/WebP images (max 10 MB) into a Figma file, either as fills or as new
frames.

- **Accepts:** image file plus optional target node URL.

### `use_figma`

Generic create / modify / delete on Figma objects (Design or FigJam).

- **Accepts:** object type, properties, actions.
- **Returns:** the created, modified, or deleted objects.

### `generate_figma_design`

Sends a representation of live UI code into Figma as design layers.

- **Accepts:** UI code, target file or clipboard.
- **Returns:** generated design layers.

### `generate_diagram`

Generates a FigJam diagram from Mermaid syntax or a natural-language description.

- **Accepts:** Mermaid source or natural language.
- **Returns:** FigJam diagram.

## URL parsing reference

The Figma MCP server consumes node IDs in `:`-separated form, but URLs use `-`. When extracting
from a URL, convert.

```
https://www.figma.com/design/<fileKey>/<fileName>?node-id=<a>-<b>
                              ^^^^^^^                         ^^^^^^
                              fileKey                         nodeId (rewrite to a:b)
```

For Figma Make files, the URL scheme is the same but the host path differs. For FigJam, the
host path uses `/board/` instead of `/design/`.

If the URL has no `node-id`, the tools default to the whole file context — which is almost
never what's wanted. Ask the user to point at a specific frame.
