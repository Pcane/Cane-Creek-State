# Tile Technical Data — Session State
**Last updated:** 2026-06-19
**Session:** Founding document
**Updated by:** Overseer

---

## HOW TO START A NEW SESSION

Fetch this document:
`https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/TILE_RECORD_STATE.md`

Read it fully before doing anything else. Then ask Peter for the current `tile_technical_data.html` before writing any code.

---

## CURRENT STATE

**Version:** v0.1 (not yet built)
**Last change:** Founding document created by Overseer — app not yet built
**Files in play:**
- `tile_technical_data.html` — to be created in `cane-creek-app`
- `glazes.json` — exists in `cane-creek-app` root, fetch at runtime via `./glazes.json`
- `hub.html` — needs a card added after main app is working
- `TILE_RECORD_STATE.md` — this file, lives in `cane-creek-state`

---

## WHAT WAS DONE LAST SESSION

Overseer founding session 2026-06-19:
- App named: Tile Technical Data
- Storage confirmed: Netlify Blob primary, localStorage cache
- Glaze data confirmed: fetch from `./glazes.json` at runtime — do not hardcode
- File confirmed: `tile_technical_data.html` in `cane-creek-app` repo
- Hub card: add to `hub.html` after main app is working
- State document: this file in `cane-creek-state`
- New Claude project created for this app — separate from Studio Claude

---

## IN PROGRESS

Nothing yet — app not built.

---

## NEXT STEPS

1. Peter opens this project and pastes the project brief to Claude
2. Claude reads brief and this state document
3. Ask Peter: "What would you like to tackle first — the record structure and data model, or the UI layout?" Let Peter lead.
4. Suggested first build: core record structure, create/edit/list UI, localStorage save — get data flowing before worrying about Blob storage or the printable sheet
5. Blob storage integration second
6. Printable CNC reference sheet third
7. Hub card last (separate small patch to hub.html)

---

## RECORD DATA STRUCTURE

Each tile record:

**Identity**
- Tile ID (auto-generated: CCT-001, CCT-002 etc.)
- Tile / design name
- Date created
- Status: In Progress / Bisque Ready / Glaze Testing / Production Ready / Archived

**Mold**
- Mold ID
- Face size (working dimensions)
- Pocket depth
- Date poured
- Google Drive link — mold design files

**Design & CNC**
- Design name
- SVG file — Google Drive link
- Pass 1: bit, depth, stepover, feed rate, plunge rate, RPM
- Pass 2: bit, depth, stepover, feed rate, plunge rate, RPM
- Pass 3 (line grooves): bit, final depth, feed rate, plunge rate, RPM
- Raised line depth target (from standard spec table: 0.021 / 0.025 / 0.028 / 0.030 / 0.035")
- CNC notes

**Clay Body**
- Recipe version
- Batch date
- Batch size
- Deviations from standard

**Glaze**
- Glaze(s) applied — pulled live from ./glazes.json, do not hardcode
- Application method per zone (bulb syringe / dip / brush)
- Application notes

**Firing**
- Kiln (Kiln 1 / Kiln 2)
- Program (User 1 / User 2 / User 3)
- Fire date
- Peak temp reached
- Firing notes

**Results**
- Surface result (free text)
- Color accuracy (free text)
- Glaze defects (free text)
- Overall assessment
- Photo link — Google Drive
- Approved for production: Yes / No / Conditional

**Experimental**
- Experimental: Yes / No
- What was being tested
- Outcome

---

## PRINTABLE CNC REFERENCE SHEET

One-page printable output per tile record containing:
- Tile ID and name
- Mold dimensions
- All three CNC passes with full parameters
- Raised line depth target
- Google Drive links
- Date

Must be clean, readable, print well on standard letter paper. Goes on the wall next to the CNC when cutting that mold.

---

## ARCHITECTURAL DECISIONS MADE

| Decision | Reasoning |
|----------|-----------|
| Netlify Blob primary, localStorage cache | Tile records are permanent — must survive laptop wipe |
| Fetch glazes from ./glazes.json at runtime | Single source of truth — no duplicate glaze data in this app |
| Separate Claude project from Studio Claude | App is substantial — keep contexts clean |
| Same repo as all other apps (cane-creek-app) | One Netlify deployment, clean file organization |
| State doc in cane-creek-state | All state documents live in cane-creek-state, not cane-creek-app |

---

## KNOWN BUGS

None — app not yet built.

---

## DO NOT DO THESE

- Never hardcode glaze data — always fetch from `./glazes.json`
- Never use model string other than `claude-sonnet-4-5`
- Never make architectural decisions affecting other apps — flag for Overseer
- Never write code without reading current `tile_technical_data.html` first
- Never skip test cycle before further changes
- Never upload this state document to `cane-creek-app` — it belongs in `cane-creek-state`

---

## NOTES FOR NEXT SESSION

- `glazes.json` is live in `cane-creek-app` root — app fetches it at runtime via `./glazes.json`, no need to paste content into session
- Hub card for this app needs to be added to `hub.html` — do this as a separate patch after main app is working, not in the first session
- Model string is always `claude-sonnet-4-5` — no exceptions
- Dev workflow: Claude writes Perl patch script → Peter runs it in Terminal → uploads to `cane-creek-app` on GitHub → Netlify deploys → Peter tests → reports back before further changes
- State document uploads go to `cane-creek-state`, not `cane-creek-app`
