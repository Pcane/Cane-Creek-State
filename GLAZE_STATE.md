# GLAZE_STATE.md — Cane Creek Glaze Studio

Last updated: June 2026 — full glaze development system complete

---

## Current files in cane-creek-app repo

- `glaze_studio.html` — six-tab studio calculator, all features live
- `glazes.json` — 42 original glazes + 14 imported test glazes (TG1–TG10, TM1–TM4)

---

## What the app does

Six tabs in this order:
1. **Clay** — batch directions, 30 lb clay body
2. **Glaze Slurry** — clear gloss base by gallons (1–5 gal)
3. **Stock Colors** — bench recipe card, mixing directions, lifecycle management, glazes.json export
4. **Firing Report** — results entry, markdown export, CSV import
5. **SG & CMC Adjuster** — calculates what to add to existing bottles
6. **Materials List** — complete inventory

---

## Architecture

- `glazes.json` lives in `cane-creek-app` repo root, served by Netlify
- `glaze_studio.html` fetches it as `./glazes.json` async on DOMContentLoaded
- All changes (status, new glazes) are in-memory only until "Save glazes.json" is clicked
- **Persistence gap:** saving glazes.json still requires manual download and GitHub upload — automated solution needed, flag to Overseer
- `GLAZE_STATE.md` lives in `Cane-Creek-State` repo (state documents only)

---

## Glaze system

**Base slurry:** SG 1.33 | f 0.404 | CMC 0.20% | Veegum 0.15%

**Three series:**
- G — Gloss target
- M — Matte target
- S — Satin target

**Test prefixes:** TG, TM, TS — auto-numbered (TG1, TG2, TM1 etc.)

**Versioning:** any change to recipe or application parameters = new version. Format: G35v2. No exceptions.

**Status field:** `active` | `test` | `retired` — reversible in all directions.

**Current assignments:**
- G1–G24 → active
- G25–G43, G25HC → test
- TG1–TG10, TM1–TM4 → test (imported from reformulations CSV)
- No glazes retired yet

---

## Dropdown structure — built and live

- **Active glazes** — flat list, no indents. Always. Promoted glazes lose indent permanently.
- **Test glazes** — indented under parent (↳) only when `based_on` points to another test glaze in the same series. Orphans (no `based_on`, parent is active/retired, or parent is different series) appear unindented.
- **Retired** — flat list when shown, no indents.
- Cross-series `based_on` links do not exist — M-series glazes have no `based_on` until they spawn M-series versions.
- `based_on` field in New Test Glaze modal — optional, empty for genuinely new glazes.

---

## Lifecycle UI — built and live

**Bench recipe card** on Stock Colors tab:
- Glaze ID: 32px, colorant weights: 36px, colorant names: 20px
- Status badge, clear base weight
- Readable at arm's length while mixing

**Lifecycle buttons** — context-sensitive:
- Test glaze: Promote to active | Retire
- Active glaze: Move to test | Retire
- Retired glaze: Restore to active | Restore to test

**New Test Glaze modal:**
- Series selector (G/M/S)
- Auto-assigns next T-number
- Based on field (optional — empty for genuinely new glazes)
- Colorant entry (name + g per 600g)
- Type, notes, warning fields

**glazes.json export:** "Save glazes.json" button on Stock Colors tab — downloads current in-memory state for upload to GitHub.

---

## Firing report — built and live (Tab 4)

**Per firing header:**
- Date, kiln notes
- Context for AI consultant (free text — orient the AI with goals and history)
- Clay body and base glaze printed automatically

**Per glaze:**
- SG at application, method (pour/dip/brush/spray), water bath pre-dip, coat count
- Color observed, finish (gloss/satin/matte)
- Defects checklist (bubbles/dry/rough/cracks/pinholes/wrong color/not transparent/crawling)
- Free text notes
- Photo URL (GitHub raw URL)

**Export:** markdown file download → upload to GitHub → share raw URL with AI consultants.

**CSV import** — bottom of Firing Report tab:
- Drag and drop or click to select
- Preview before committing
- T-numbers auto-assigned by app
- `based_on` field preserved

**CSV format for AI consultants:**
`Based_on, Name, Series, Type, Colorant_1_name, Colorant_1_gPer600g, Colorant_2_name, Colorant_2_gPer600g, Colorant_3_name, Colorant_3_gPer600g, Notes`
- Series must be G, M, or S
- Type must be oxide, stain, or new
- Do not include T-numbers — app assigns them

---

## M-series inaugurated

Four glazes established as M-series from firing 2 results:
- TM1 — Chrome Iron Red-Brown Matte (recipe from G28)
- TM2 — Cobalt Blue Rutile Matte (recipe from G30)
- TM3 — Rutile Ochre Taupe Matte (recipe from G38)
- TM4 — Tenmoku Iron Black Matte (recipe from G40)

M-series glazes have no `based_on` until they spawn M-series versions. Recipe origin noted in notes field only.

---

## Firing results to date

**Firing 1 — cone 6 oxidation:**

| Glaze | SG | Result |
|---|---|---|
| G21 | 1.167 | Good ✓ — reference benchmark |
| G11 | 1.252 | Nice gloss, edge break ✓ — few pinholes |
| G25 | 1.292 | White sandpaper, matte — failed |
| G26 | 1.235 | Off white satin — failed |
| G28 | 1.240 | Medium brown matte |
| G29 | 1.220 | Pale yellow matte, dry |
| G30 | 1.280 | Earthy blue matte — good matte candidate |
| G35 | 1.220 | Light blue matte |
| G38 | 1.260 | Taupe matte |
| G40 | 1.270 | Dark brown matte — perfect matte |
| G42 | 1.292 | Amber, dry/rough surface |

**Key insight:** Lower SGs tried for transparency/edge effects but producing matte results. Clear base (G24) fires glossy reliably at SG 1.30–1.33. Goal is glossy transparent finish with edge effects — target look is rich pooled amber-gold similar to classic Arts and Crafts tile glazes.

**Reformulation strategy:** Adding Frit 3134 (3–5% = 18–30g per 600g base) directly to colored glazes to boost flux and achieve gloss at lower SG. TG1–TG10 are the reformulation test glazes.

---

## Glaze notes — key glazes

- **G21** — reference glaze, benchmark. 5% iron, 1% rutile. Glossy at SG 1.167.
- **G11** — chrome oxide alone at 0.2% gives gloss. Chrome + iron (G28) does not.
- **G10** — wet slurry additions, not dry weights. Preserve as-is.
- **G43** — blocked pending Titanium Dioxide (TiO2) not yet on shelf.
- **G42** — amber direction is closest to target Arts and Crafts look. Highest priority test.

---

## Materials to order

- Titanium Dioxide (TiO2) — for G43 ★
- Light Rutile — confirm light not dark is on shelf

---

## Clay body

| Material | % |
|---|---|
| Tile 6 | 26.14% |
| OM4 Ball Clay | 20.92% |
| Silica M325 | 20.92% |
| G-200 EU Feldspar | 24.06% |
| Talc | 2.09% |
| Bentonite HPM-20 | 1.88% |
| Christy Fine Grog | 4.00% |
| Barium Carbonate ⚠ | 0.345% — toxic, N100 mask required |

Water: 27% of wet weight. Batches: 30 lb only.

---

## Pending — next session

1. **Automated glazes.json persistence** — flag to Overseer, review business app solution
2. **UMF calculator** — deferred until more firing data. Revisit after next firing.
3. **tile_record.html** — still unblocked, deferred until glaze studio stable
4. **Firing report persistence** — results lost on page refresh. Low priority — export immediately workaround acceptable for now.

---

## Dev workflow

- Peter uploads current `glaze_studio.html` at session start via GitHub URL
- Fetch this file before starting any work
- Deliver complete ready-to-upload files only — no patch scripts, no diffs
- Peter uploads directly to GitHub, Netlify deploys in ~30 seconds
- Peter tests in browser, reports results before further changes
- Update this file and tell Peter to upload at end of every session
