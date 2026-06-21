# GLAZE_STATE.md — Cane Creek Glaze Studio

Last updated: June 2026 — lifecycle UI built and live

---

## Current files in cane-creek-app repo

- `glaze_studio.html` — six-tab studio calculator, lifecycle UI live
- `glazes.json` — 42 glazes, all with status fields (active/test/retired)

## What the app does

Six-tab studio calculator:
1. **Clay** — batch directions, 30 lb clay body
2. **Glaze Slurry** — clear gloss base by gallons (1–5 gal)
3. **Stock Colors** — bench recipe card + mixing directions + lifecycle management
4. **SG & CMC Adjuster** — calculates what to add to existing bottles
5. **Materials List** — complete inventory
6. **Firing Report** — pending next session

## Architecture

- `glazes.json` lives in `cane-creek-app` repo root, served by Netlify
- `glaze_studio.html` fetches it as `./glazes.json` async on DOMContentLoaded
- `tile_record.html` will fetch same `./glazes.json` when built — still unblocked
- `GLAZE_STATE.md` lives in `Cane-Creek-State` repo (state documents only)

---

## Glaze system

**Base slurry:** SG 1.33 | f 0.404 | CMC 0.20% | Veegum 0.15%

**Three series:**
- G — Gloss target
- M — Matte target
- S — Satin target

**Test prefixes:** TG, TM, TS — auto-numbered (TG1, TG2, TM1 etc.)

**Versioning:** any change to recipe or application parameters = new version. Format: G35v2, M1v2 etc. No exceptions.

**Status field:** `active` | `test` | `retired` — reversible in all directions.

**Current assignments:**
- G1–G24 → active
- G25–G43, G25HC → test
- No glazes retired yet

**Retired glazes** hidden by default in dropdown. "Show retired" checkbox to reveal.

---

## Lifecycle UI — built and live

On the Stock Colors tab:

**Bench recipe card** — large format, readable at arm's length while mixing:
- Glaze ID: 32px
- Colorant weights: 36px
- Colorant names: 20px
- Status badge, clear base weight

**Lifecycle buttons** — appear below bench card, context-sensitive:
- Test glaze: Promote to active | Retire
- Active glaze: Move to test | Retire
- Retired glaze: Restore to active | Restore to test

**New Test Glaze modal:**
- Series selector (G/M/S)
- Auto-assigns next T-number
- Colorant entry (name + g per 600g)
- Type, notes, warning fields

**Important:** status changes and new glazes are in-memory only. Must export updated `glazes.json` to GitHub to make permanent. Export function not yet built — currently Peter downloads from the app session and uploads manually.

---

## Firing report system — pending

To be built as Tab 6 next session.

**Per firing (header, stated once):**
- Clay body recipe
- Base glaze recipe
- Cone 6 oxidation (always)
- Date
- Kiln notes (free text, optional)

**Per glaze tested:**
- Glaze ID and name
- SG at application
- Application method: pour / dip / brush / spray
- Water bath pre-dip: yes / no
- Coat count
- Color observed
- Finish: gloss / satin / matte
- Defects: bubbles / dry / rough / cracks / pinholes / wrong color / other (checklist)
- Free text notes
- Photo URL (GitHub raw URL to tile photo)

**Export format:** GitHub markdown with photo URLs inline. Any AI can fetch the raw URL and read the full record including images. Overseer confirmed: smartphone JPEGs fine for now, Cloudinary available if repo gets heavy.

**Glaze selection for report:** checklist of test-status glazes, pre-filtered. Option to include active glazes.

---

## Firing results to date

**Cone 6 oxidation — first test firing:**

| Glaze | SG | Result |
|---|---|---|
| G21 | 1.167 | Good ✓ — reference benchmark confirmed |
| G11 | 1.252 | Nice gloss, slight transparency, edge break ✓ — two to three bubble craters |
| G25 | 1.292 | All white, dry, rough sandpaper surface |
| G26 | 1.235 | Off white, satin, imperfections show |
| G28 | 1.240 | Medium brown, matte |
| G29 | 1.220 | Very dry, rough, pale yellow, matte |
| G30 | 1.280 | Light speckled, matte to satin, not unattractive |
| G35 | 1.220 | Blotchy, white in thin areas, matte to satin |
| G38 | 1.260 | Matte taupe |
| G40 | 1.270 | Dark brown, good matte, one bubble crater |
| G42 | 1.292 | Thin, rough, amber to light amber |

Clear base (G24) fires glossy reliably at SG 1.30–1.33. Root cause of failures still under investigation — suspected refractory colorants suppressing melt rather than base chemistry or application thickness.

---

## Glaze notes — key glazes

- **G21** — reference glaze, benchmark for all others. 5% iron, 1% rutile.
- **G11** — confirmed gloss with chrome oxide alone at 0.2%. Chrome alone works; chrome + iron (G28) does not.
- **G10** — wet slurry additions, not dry weights. Made from leftover slurries. Retirement candidate. Preserve as-is.
- **G43** — blocked pending Titanium Dioxide (TiO2) not yet on shelf.
- **G25** — chrome-tin red. All white result in first firing — needs further testing.
- **G25HC** — high calcium variant of G25, not yet fired.

---

## Materials to order

- Titanium Dioxide (TiO2) — for G43 ★
- Light Rutile — confirm light not dark is on shelf
- Ferro Frit 3110 — optional, only if pursuing alkaline turquoise (G36)

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

## Pending work — priority order

1. **Upload status-field glazes.json** — fixes empty dropdown bug. File ready in Downloads.
2. **Test lifecycle UI** — confirm bench card, promote/retire buttons, new test glaze modal all work on live site.
3. **Build Firing Report tab (Tab 6)** — next session.
4. **glazes.json export function** — so status changes made in-app can be downloaded without manual reconstruction.
5. **tile_record.html** — still unblocked, deferred until glaze studio is stable.

---

## Dev workflow

- Peter uploads current `glaze_studio.html` at session start
- Fetch this file before starting any work
- Deliver complete ready-to-upload files only — no patch scripts, no diffs
- Peter uploads directly to GitHub, Netlify deploys in ~30 seconds
- Peter tests in browser, reports results before further changes
- Update this file and tell Peter to upload at end of every session
