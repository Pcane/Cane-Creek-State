# Tile Technical Data — Session State
**Last updated:** 2026-06-19
**Session:** v1.1 build session
**Updated by:** Studio Claude (Tile Record app)

---

## HOW TO START A NEW SESSION

Fetch this document:
`https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/TILE_RECORD_STATE.md`

Read it fully before doing anything else. Then ask Peter for the current
`tile_technical_data.html` before writing any code.

---

## CURRENT STATE

**Version:** v1.1
**Last change:** AKA field, mold size selector, molds.json, glaze section
rewrite (tile type: Art/Field/Liner), Cloudinary photo upload in Results
and glaze map for art tiles.

**Files in play:**
- `tile_technical_data.html` — live in `cane-creek-app`, v1.1
- `glazes.json` — live in `cane-creek-app` root
- `molds.json` — live in `cane-creek-app` root (new in v1.1)
- `hub.html` — hub card NOT YET added (do after v1.1 confirmed working)
- `TILE_RECORD_STATE.md` — this file, lives in `cane-creek-state`

---

## WHAT WAS DONE LAST SESSION (v1.1 — 2026-06-19)

- Added AKA / Client Name field to Identity section (optional rename;
  shows in topbar under design name; canonical design name unchanged)
- Mold section: added Mold Size dropdown, fetches from ./molds.json
- Design & CNC: mold size drives standard GCode info block (Pass 1 & 2
  show standard file name + Drive link for that size); Pass 3 always
  manual (design-specific)
- Glaze section rewritten: tile type selector (Art / Field / Liner)
  - Art tile: syringe zones (bulb syringe only) + field coat block
    (any method except syringe) + glaze map photo upload (Cloudinary)
  - Field / Liner tile: single glaze + method (no syringe option)
- Results section: replaced Google Drive photo link with Cloudinary
  upload — inline preview in record
- molds.json created with _readme block; seeds 6x6 (GCode filenames
  present, Drive links blank until Peter adds them), 4x4, 3x3
  (no GCode yet)
- Clay body autofill confirmed blocked pending standards.json

---

## IN PROGRESS

- Peter to add 6x6 rough/finish Drive links to molds.json in GitHub
- Peter to confirm v1.1 is working in browser
- Hub card for tile_technical_data not yet done — next after v1.1 confirmed

---

## NEXT STEPS

1. Peter tests v1.1 — report back before any further changes
2. Add Drive links for 6x6 GCode files into molds.json
3. Hub card — separate small patch to hub.html
4. Clay body autofill — wire up when standards.json is built
   (fetch ./standards.json on newRecord(), prefill clayRecipeVersion
   and optionally kilnProgram; same runtime fetch pattern as glazes.json)
5. Blob storage activation — when Netlify functions are deployed

---

## RECORD DATA STRUCTURE (current — v1.1)

**Identity**
- tileId (auto: CCT-001 etc.)
- tileName (canonical design name — used in all file names)
- akaName (optional client/display rename)
- dateCreated
- status: In Progress / Bisque Ready / Glaze Testing / Production Ready / Archived

**Mold**
- moldId
- moldSize (from molds.json dropdown)
- moldFaceSize (working dimensions)
- moldPocketDepth
- moldDatePoured
- moldDriveLink (Google Drive — mold design files)

**Design & CNC**
- designName
- svgDriveLink
- cnc1: bit, depth, stepover, feed, plunge, rpm (standard — ref molds.json)
- cnc2: bit, depth, stepover, feed, plunge, rpm (standard — ref molds.json)
- cnc3: bit, depth, feed, plunge, rpm (design-specific, always manual)
- raisedLineTarget
- cncNotes

**Clay Body** (manual until standards.json exists)
- clayRecipeVersion
- clayBatchDate
- clayBatchSize
- clayNotes

**Glaze**
- tileType: 'Art' | 'Field' | 'Liner'
- Art tile fields:
  - glazeZones: [{glazeId, method:'Bulb syringe', notes}]
  - fieldCoatGlazeId, fieldCoatMethod, fieldCoatNotes
  - glazeMapUrl (Cloudinary)
- Field/Liner tile fields:
  - singleGlazeId, singleMethod, singleNotes

**Firing**
- kilnUsed: Kiln 1 / Kiln 2
- kilnProgram: User 1 / User 2 / User 3
- fireDate
- peakTemp
- firingNotes

**Results**
- surfaceResult
- colorAccuracy
- glazeDefects
- overallAssess
- photoUrl (Cloudinary — uploaded in app, shows inline)
- approvedForProd: Yes / No / Conditional

**Experimental**
- isExperiment: Yes / No
- experimentTest
- experimentOutcome

---

## SERVICES IN USE

| Service | Purpose | Credentials |
|---------|---------|-------------|
| Netlify Blob | Primary record storage | Auto via Netlify (stub — not yet activated) |
| Cloudinary | Photo storage and serving | Cloud: dmnkvz4k8 / Preset: cane_creek_tiles |
| Google Fonts | Typography | Public CDN — no key |
| glazes.json | Glaze data | ./glazes.json in cane-creek-app root |
| molds.json | Mold size / GCode library | ./molds.json in cane-creek-app root |
| standards.json | Studio-wide standards (PLANNED) | ./standards.json — not yet built |
| Google Drive | Linked files (URLs only, no API) | None |

---

## ARCHITECTURAL DECISIONS MADE

| Decision | Reasoning |
|----------|-----------|
| Netlify Blob primary, localStorage cache | Tile records are permanent |
| Fetch glazes from ./glazes.json | Single source of truth |
| Fetch molds from ./molds.json | Same pattern — never hardcode mold data |
| standards.json planned for clay/kiln defaults | Overseer confirmed pattern |
| Cloudinary for photos | Already in use across studio apps — shared account |
| AKA field not rename — additive | Canonical name stays in file names; AKA is display only |
| Tile type drives glaze UI | Art/Field/Liner have meaningfully different glaze workflows |
| Syringe bulbing Art-tile-only | Field and Liner tiles never use syringe |

---

## KNOWN BUGS

None reported. v1.1 not yet confirmed tested by Peter.

---

## DO NOT DO THESE

- Never hardcode glaze data — always fetch from ./glazes.json
- Never hardcode mold data — always fetch from ./molds.json
- Never use model string other than claude-sonnet-4-5
- Never make architectural decisions affecting other apps — flag for Overseer
- Never write code without reading current tile_technical_data.html first
- Never skip test cycle before further changes
- Never upload this state document to cane-creek-app — it belongs in cane-creek-state

---

## NOTES FOR NEXT SESSION

- standards.json will follow same runtime fetch pattern as glazes.json and molds.json
- Hub card for this app goes in hub.html — separate patch, after v1.1 confirmed
- Blob activation needs Netlify function deployment — coordinate with Overseer
- Peter needs to add 6x6 GCode Drive links to molds.json manually in GitHub
- Clay body autofill: wire on newRecord() when standards.json exists —
  fetch ./standards.json, read currentClayRecipeVersion (or whatever key
  Overseer names it), prefill clayRecipeVersion field
