# STUDIO_STATE.md — Cane Creek Studio Tools

Last updated: June 2026 — founding document

## Files in scope
- hub.html — studio landing page
- pattern.html — Pattern Studio (fish-scale generator + seed importer)
- design_v2.html — Design Studio (fireplace surround layout)
- tile_record.html — NOT YET BUILT (blocked on glazes.json)
- debug_design_v2.html — 36-test debug suite for design_v2
- debug_pattern2.html — 76-test debug suite for Pattern Studio IMP engine

## hub.html
Four cards: Business App (/), Glaze Studio (/glaze_studio.html), Design Studio (/design_v2.html), Pattern Studio (/pattern.html). All apps have ← Hub backlink in their headers. Logo image is broken — base64 was truncated during a patch session. Fix by restoring full base64 from git history.

## design_v2.html
Fireplace surround layout tool. Features: zone drawing with snap, ashlar quad pattern editor (TLE), liner calculations, mold count output, hearth preview, placed art tiles, CNC reference output, debug report.

### Critical architecture
- calcAshlarLinerFix() is the SINGLE authority for ashlar liner widths — do not let fixWithLiner() or pattern suggestion cards override it
- Auto-liner runs on JSON load and on pattern assignment
- Mold count subtracts field tiles covered by placed art tiles
- Ashlar zones suppressed from "cuts BAD" warnings in debug report
- 36-test debug suite (debug_design_v2.html) must pass before any app changes deploy

### Known state
- Living Room Fireplace JSON: 47.5" × 48" wall, firebox 8.375" × 18.125", 0.75" side liners applied, ashlar pattern assigned to Zone 1
- Sidebar toggle working
- Right-click stone deletion working
- Print output: mold sizes + pressing counts only (no tile names, no zone breakdown)

### Pending
- Mold inventory tracking deferred — will connect to business app later via iframe or linked tab
- Worksheet B and Calculator B (whole-face field layouts, Motawi style) — scoped but not started

## pattern.html — Pattern Studio

### Stage 1 (complete, do not touch)
Fish-scale generator: scale geometry, SVG export at mold size, production checks.

### Stage 2 (mostly complete)
- Seed importer: strict SVG parse (M L H V C S Q T Z only, A rejected loudly), heal pass, inset with ear removal
- Glaze-physics validation: landing zones, tapers, pinch, overlap, duplicate detection
- Transform stack: mirror-H/V, rotate-copy, draggable axes snapping 1/32", reorderable recipe
- Composition validation: ghost dedup, spatial grid, per-seed-pool invariant checks
- Overlap modes: Cutout / Shingle / Flag dropdown, live recomposition
- Click-to-spotlight flag display with numbered badges
- 76-test debug suite (debug_pattern2.html) passing including Peter's real artwork

### Stage 2 remaining
- Canvas switch to mold/wet dimensions (6.57" tile, 6.20" design area)
- Export SVG at mold size — asks "what fired tile size?" divides by 0.914
- Import scale question — "fired or wet?"
- Seed recipe library (save/load)
- Fish-scale generator collapsed to bottom accordion

### Open question before remaining Stage 2 work
Peter's Illustrator SVG export flavor — "Export As > SVG" vs "Save As > SVG" — not yet confirmed. Ask before writing export/import code.

### Dev workflow (non-negotiable for pattern.html)
1. Discuss approach before writing code
2. Never touch fish-scale Stage 1 code
3. Run debug_pattern2.html (76 tests) before touching pattern.html
4. Syntax-check with node --check on extracted script blocks
5. Peter tests locally (opens HTML file in browser) before GitHub upload

### Shrinkage math confirmed
8.6% measured as (wet minus fired) / wet. Multiplier: 0.914 wet-to-fired, 1/0.914 = 1.0941 fired-to-wet (mold size).

## tile_record.html — NOT YET BUILT
Blocked until glazes.json exists. When ready:
- Single fired face size input → all dimensions cascade (working size, shrinkage, CNC depths)
- CNC three-pass settings pre-filled
- Glaze spec pulls live from glazes.json
- SVG upload/download
- Google Drive link field (not file storage)
- Printable one-page CNC reference sheet

### Tile production standards (do not alter)
- Working/mold face: 6.570 × 6.570"
- Fired face: 6.000 × 6.000"
- Shrinkage: 8.6%
- Fired thickness: 0.407" (pocket depth 0.445" × 0.914)
- Default raised line: 0.035" CNC depth → 0.032" fired height
- Safety margin: 0.125" all sides
- Design safe area: 6.320 × 6.320"
- Grout joint: 0.125"
