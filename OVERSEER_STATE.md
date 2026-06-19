# Cane Creek Studio — Overseer State
**Last updated:** 2026-06-19
**Session:** Session 2 — glazes.json complete, Tile Technical Data launched
**Updated by:** Overseer

---

## HOW TO START A NEW OVERSEER SESSION

Fetch this document:
`https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/OVERSEER_STATE.md`

And the system map:
`https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/SYSTEM_MAP.md`

Read both before proceeding.

---

## CURRENT SYSTEM STATUS

| App | Status | Version | Last touched |
|-----|--------|---------|-------------|
| Business app (index.html + app.js) | Live | v8.12 | ~2 months ago |
| Glaze Studio (glaze_studio.html) | Live | — | 2026-06-18 |
| glazes.json | Live | — | 2026-06-19 |
| Fireplace Designer (design_v2.html) | Live, stable | — | 2 weeks ago |
| Pattern Studio (pattern.html) | Live | — | ~1 week ago |
| Hub (hub.html) | Live | — | ~1 week ago |
| Tile Technical Data (tile_technical_data.html) | In development | — | Not yet built |
| Public website | Live | — | Content pending update |

---

## ACTIVE ARCHITECTURAL DECISIONS IN PROGRESS

### 1. Tile Technical Data app — IN PROGRESS
**Status:** Project created, brief written, state doc created — ready to build
**File:** `tile_technical_data.html` in `cane-creek-app`
**State doc:** `TILE_RECORD_STATE.md` in `cane-creek-state`
**Claude project:** Separate project — "Cane Creek Tile Technical Data"
**Storage:** Netlify Blob primary, localStorage cache
**Glaze data:** Fetches `./glazes.json` at runtime
**Next step:** Peter opens Tile Technical Data project, pastes brief, starts build

### 2. Pattern Studio Stage 2 — PENDING confirmation
**Status:** Fully specced, awaiting one piece of information
**Blocker:** Peter needs to confirm Illustrator SVG export flavor before building
**Next step:** Ask Peter which Illustrator SVG export setting he uses, then issue build instructions

### 3. Glaze journal tab — PENDING
**Status:** Not yet built
**Waiting on:** Glaze firing assessment (bisque tiles fired, glaze testing next)
**Next step:** After Peter assesses glaze test results, issue instructions to Glaze Claude

### 4. Date format standardization — MEDIUM PRIORITY
**Status:** Identified, not yet actioned
**What:** Glaze studio and business app use inconsistent date formats
**Resolution:** Standardize on ISO 8601 (YYYY-MM-DD) across all apps
**Next step:** After next glaze studio session, ask Claude to audit all date handling

---

## WHAT WAS DONE THIS SESSION (2026-06-19)

- Confirmed glazes.json is complete and live in `cane-creek-app` repo root
- Confirmed Glaze Claude updated GLAZE_STATE.md
- Confirmed storage for Tile Technical Data: Netlify Blob primary, localStorage cache
- Named app: Tile Technical Data
- Decided: separate Claude project (not Studio Claude) — app is too substantial to share context
- Wrote founding project brief: `TILE_TECHNICAL_DATA_PROJECT_BRIEF.md`
- Wrote founding state document: `TILE_RECORD_STATE.md`
- Fixed long-standing URL error: all state document URLs now correctly point to `cane-creek-state` repo, not `cane-creek-app`
- Added rule to SYSTEM_MAP: never put state documents in cane-creek-app
- Updated SYSTEM_MAP section 2 to properly document the three-repo structure
- Updated SYSTEM_MAP data ownership table to reflect glazes.json as shared source

---

## PENDING OVERSEER TASKS

| Task | Priority | Notes |
|------|----------|-------|
| Monitor Tile Technical Data build | High | New project launched — check in after first session |
| Issue glaze journal tab instructions | Medium | After Peter assesses glaze test firing results |
| Update Marketing project instructions | Medium | Remove "launching spring 2026", fix version to v8.12 |
| Confirm Illustrator SVG flavor with Peter | Medium | Unblocks Pattern Studio Stage 2 |
| Issue date format standardization | Medium | After next glaze/marketing session |
| Create WEBSITE_STATE.md | Low | When website work resumes |
| Hub cards — Pattern Studio + Tile Technical Data | Low | Two cards to add — do as one patch to hub.html |

---

## NOTES FOR NEXT OVERSEER SESSION

- State document URL bug is now fixed in all four documents produced this session. Upload all four to their correct repos: SYSTEM_MAP.md and OVERSEER_STATE.md go to `cane-creek-state`; TILE_RECORD_STATE.md goes to `cane-creek-state`; project brief is for Peter's reference only (not uploaded to GitHub).
- Glaze firing assessment is upcoming — after results, Glaze Claude needs instructions to build the journal/feedback tab.
- Hub needs two cards added: Pattern Studio and Tile Technical Data. Worth batching these as one small patch to hub.html rather than two separate sessions.
- Marketing project instructions are stale (reference v8.0 and "launching spring 2026") — needs updating before outreach begins.
