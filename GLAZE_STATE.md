# GLAZE_STATE.md — Cane Creek Glaze Studio

Last updated: June 2026 — auto-written by Glaze Studio app

---

## Current files in cane-creek-app repo

- `glaze_studio.html` — six-tab studio calculator, all features live
- `glazes.json` — seed data (source of truth is Netlify Blob: key=glazes)

---

## Architecture

- Glaze data primary store: Netlify Blob via `/.netlify/functions/data`, key=`glazes`
- On first load: if Blob empty, seeds from `glazes.json` then Blob is source of truth
- `glazes.json` auto-backed up to GitHub on every glaze promotion (test→active)
- `writeToGitHub()` embedded in app — reads PAT from localStorage key `github_pat`
- `GLAZE_STATE.md` written to Cane-Creek-State when Peter types "update state"

---

## Glaze counts

- Active: 1 glazes
- Test: 38 glazes
- Retired: 17 glazes
- Total: 56 glazes

## Active glazes
G12

## Test glazes
G11, G16, G21, G24, G25, G25HC, G26, G27, G28, G29, G30, G31, G32, G33, G34, G35, G36, G37, G38, G39, G40, G41, G42, G43, TG1, TG2, TG3, TM1, TG4, TG5, TM2, TG6, TG7, TM3, TG8, TM4, TG9, TG10

## Retired glazes
G1, G2, G3, G6, G7, G8, G9, G10, G13, G14, G15, G17, G18, G19, G20, G22, G23

---

## Glaze system

- Base slurry: SG 1.33 | f 0.404 | CMC 0.20% | Veegum 0.15%
- Three series: G (gloss), M (matte), S (satin)
- Test prefixes: TG, TM, TS — auto-numbered
- Versioning: any recipe or application change = new version (G35v2 format)
- Status: active | test | retired — reversible in all directions
- Dropdown indent: test glazes indented under parent when based_on points to same-series test glaze

---

## Dev workflow

- Peter uploads current `glaze_studio.html` at session start via GitHub URL
- Studio Claude fetches this file before starting any work
- Deliver complete ready-to-upload files only — no patch scripts, no diffs
- Peter uploads to GitHub, Netlify deploys in ~30 seconds
- Type "update state" to write this file back to GitHub

---

## Tabs (in order)

1. Clay — batch directions, 30 lb clay body
2. Glaze Slurry — clear gloss base by gallons
3. Stock Colors — bench recipe card, lifecycle management, Blob-backed save
4. Firing Report — results entry, markdown export, CSV import
5. SG & CMC Adjuster
6. Materials List
