# GLAZE_STATE.md — Cane Creek Glaze Studio

Last updated: June 2026 — glazes.json extraction complete

## Current files
- glaze_studio.html — deployed at cane-creek-app.netlify.app/glaze_studio.html
- glazes.json — deployed at cane-creek-app.netlify.app/glazes.json ✓ NEW

## What the app is
Five-tab studio calculator. Tab 1: Clay batch directions (30 lb only — no 60 lb). Tab 2: Glaze slurry directions by gallons (1–5 gal). Tab 3: Stock color mixing directions for all G-series glazes. Tab 4: SG & CMC adjuster. Tab 5: Materials list.

## Architecture
- glazes.json lives in cane-creek-app repo root, served by Netlify alongside the app files
- glaze_studio.html fetches it as ./glazes.json on DOMContentLoaded (async)
- tile_record.html will fetch the same ./glazes.json when built — this was the blocker, now unblocked
- GLAZE_STATE.md lives in Cane-Creek-State repo (state documents only, not app data)

## Glaze system
- Base slurry: SG 1.33, f=0.404, CMC 0.20%, Veegum 0.15%
- Tile 6 in base — not EPK kaolin (early versions used EPK, corrected)
- All colorants: direct-weigh with pre-wet. No stock solutions except G1/G2 cobalt which are too small to weigh directly even at 600g batch
- Scale: EXC5002, reads to 0.01g, reliable from ~0.03g
- Minimum batch warning triggers if any colorant drops below 0.03g at chosen batch size
- Chrome Oxide gets inline caution — 0.05g error shifts color toward green

## Glaze palette — G1 through G43
OX = pure oxide | MX = Mason stain + oxide | MS = pure Mason stain (retirement candidates) | HC = high calcium variant

Key glazes:
- G21 Dark Brown OX — reference glaze, benchmark for depth and break
- G25 Chrome-Tin Cranberry OX — chrome must be via stock dilution (0.06% is borderline)
- G25-HC — adds Wollastonite W-20 to boost calcium to 18% for stronger red
- G36 Turquoise OX — standard base gives blue-green; true turquoise needs separate Frit 3110 alkaline base
- G41 Deep Teal OX — uses cobalt carbonate not cobalt oxide
- G43 Celadon Grey-Green OX — needs Titanium Dioxide (TiO2), not yet on shelf ★
- G44/G45 — decided against, not in app

MS glazes (G3, G7–G10, G13–G15, G19–G20, G22–G23) are retirement candidates after oxide replacements are tested.

## First firing results (8 tiles)
- G21 brown: came out well — confirmed as reference
- G12/G7/G1: thin but even — lower SG strategy worked for edge effects but prevented ridge break
- G2: like a wash
- Red (G25): blotchy
- G11: solid dark green, no variation
- Most MS stains: opaque and flat

## Pending work
1. ~~Extract GLAZES array to glazes.json~~ ✓ COMPLETE — June 2026
2. Firing assessment coming — 9 new G-series glazes being poured and fired
3. Add glaze journal tab — deferred until after next firing assessment
4. Tile Record app — now unblocked, glazes.json is available at ./glazes.json

## Materials to order
- Titanium Dioxide (TiO2) — for G43 ★
- Light Rutile confirmation — verify light not dark is on shelf
- Ferro Frit 3110 — optional, only if pursuing true alkaline turquoise (G36)

## Clay body
- Recipe: Tile 6 26.14%, OM4 Ball Clay 20.92%, Silica M325 20.92%, G-200 EU Feldspar 24.06%, Talc 2.09%, Bentonite HPM-20 1.88%, Christy Fine Grog 4.00%
- Barium Carbonate: 0.345% of dry batch — toxic, N100 mask required, pre-mix in stages
- Water: 27% of wet weight
- Batches: 30 lb only
