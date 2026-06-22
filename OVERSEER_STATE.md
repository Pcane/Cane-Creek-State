# Cane Creek Studio — Overseer State
**Last updated:** 2026-06-22
**Session:** Full system onboarding — architecture review, glaze contamination discovery, state management design
**Updated by:** Overseer

---

## HOW TO START A NEW OVERSEER SESSION

Fetch this document:
`https://raw.githubusercontent.com/Pcane/Cane-Creek-State/main/OVERSEER_STATE.md`

Read it fully before proceeding. Do not rely on memory or any attached files — always fetch fresh from GitHub.

---

## OVERSEER ROLE

- Ensure project Claudes share services and don't duplicate solutions
- Catch cross-project conflicts before they cause problems
- Maintain the master running list and architectural decisions
- Flag issues to Peter, propose fixes, wait for approval before acting
- Keep sessions efficient — Peter's time is the scarcest resource
- Do not block innovation
- No apologies, no "you're right" — direct and equal relationship

---

## CURRENT SYSTEM STATUS

| App | Status | Version | Last touched |
|-----|--------|---------|-------------|
| Business app (index.html + app.js) | Live | v8.12 | ~2 months ago |
| Glaze Studio (glaze_studio.html) | Live, active daily use | — | 2026-06-22 |
| Fireplace Designer (design_v2.html) | Live, stable | — | 2 weeks ago |
| Pattern Studio (pattern.html) | Live | — | 5 days ago |
| Hub (hub.html) | Live | — | 4 days ago |
| Tile Technical Data (tile_technical_data.html) | Live, v1.1 | v1.1 | 2026-06-19 |
| Public website | Live | — | Content pending update |

---

## CLAUDE PROJECTS

| Project | Scope | State doc |
|---------|-------|-----------|
| Overseer (this) | Architecture, coordination, running list | OVERSEER_STATE.md |
| Cane Creek Glaze Studio | glaze_studio.html | GLAZE_STATE.md |
| Cane Creek — Tile Technical Data | tile_technical_data.html | TILE_RECORD_STATE.md |
| Cane Creek Website | Website repo | WEBSITE_STATE.md |
| Cane Creek Studio Tools | pattern.html, design_v2.html, hub.html | STUDIO_STATE.md |
| Cane Creek Marketing | app.js marketing sections | MARKETING_STATE.md |

**UNKNOWN:** Which project owns ai.js and app.js — Peter to confirm next session.

---

## SHARED SERVICES INVENTORY

All project Claudes must use these shared services. Do not duplicate.

| Service | Location | Used by |
|---------|----------|---------|
| AI calls (Claude API) | netlify/functions/ai.js | All apps |
| Data persistence | netlify/functions/data.js | Business app, Glaze Studio |
| Netlify Blobs | Via data.js | Business app, Glaze Studio |
| GitHub write | NOT YET BUILT — highest priority | Will be: all apps |
| Microsoft Graph API | app.js | Business app (email) |
| Hunter.io | ai.js | Business app (prospects) |
| SerpAPI | ai.js — NOTE: blocked from Netlify, must run via GitHub Actions or Mac terminal | Business app (news digest) |
| glazes.json | repo root, fetched at runtime | Glaze Studio, Tile Technical Data |

---

## REPOSITORY STRUCTURE

| Repo | Contents |
|------|----------|
| github.com/Pcane/cane-creek-app | All app files, netlify functions, glazes.json, molds.json |
| github.com/Pcane/Cane-Creek-State | All state docs |

**Live app:** cane-creek-app.netlify.app
**Note:** Two Netlify deployments exist — always use cane-creek-app.netlify.app NOT cane-creek-tile-co.netlify.app

---

## ACTIVE ARCHITECTURAL DECISIONS

### 1. GitHub write capability — HIGHEST PRIORITY BLOCKER
**Status:** Architected, not yet built
**What:** PAT-based GitHub API write function so apps can update state docs and data files automatically
**How:** Personal Access Token stored in localStorage. Single shared Netlify function (github.js or new action in ai.js) — NOT standalone per-app implementations
**OVERRIDE:** Previous Overseer spec said "build as standalone utility in each app." This is overridden. Shared service only — duplication is exactly what Overseer exists to prevent.
**Why shared:** Single maintenance surface, single security surface, consistent behavior across all apps
**Unblocks:** State doc automation, glaze lifecycle system, Tile Technical Data blob activation, everything else
**Build in:** Whichever project Claude owns ai.js — confirm with Peter first

### 2. State management architecture
**Status:** Designed today, GitHub write capability must be built first
**How it works:**
- Each project Claude has standing instruction: fetch state doc from GitHub at session start
- Each project Claude updates state doc via GitHub write at session end (or after significant decisions)
- Overseer project knowledge contains only a pointer URL — content always fetched fresh
- State repo is PUBLIC or uses non-expiring PAT — eliminates token expiry problem
**Session-end reliability:** Claude updates state after every significant decision point, not only at session end. Reduces risk of lost updates if session ends abruptly.
**Peter's effort:** Zero, once GitHub write is built and tested

### 3. Glaze development system
**Status:** Specced, blocked behind GitHub write capability
**Full spec:** In previous OVERSEER_STATE.md — carry forward unchanged
**Key points:** T-prefix naming (TG/TM/TS), G-number promotion, CSV intake, firing report generator, AI analysis stays outside the app

### 4. Finish-type separation
**Status:** Decided today — not yet built
**What:** Separate glaze dropdowns by finish type — Matte / Satin / Gloss — across ALL apps that reference glazes
**Scope:** Glaze Studio, Tile Technical Data, anywhere glazes appear
**Note:** Already partially embedded in T-naming system (TG/TM/TS) — UI needs to reflect this

### 5. Glaze contamination — discovered 2026-06-22
**What happened:** A glaze bottle was mislabeled (gloss/matte mix-up). Test glazes mixed from that bottle have unknown gloss/matte ratio. Physical slurry compromised — recipes in glazes.json are intact.
**Confirmed clean:** G11 (Chrome Green), G16 (White), G21 (Dark Brown — benchmark), G24 (Clear Gloss)
**Decision:** Do NOT wipe glazes.json. Mark compromised glazes as "suspended" status. Remix from dry materials using existing recipes. Retest from clean slurry.
**New status needed:** "suspended" — for contaminated/uncertain batches

### 6. Tile Technical Data
**Status:** Live v1.1, built 2026-06-19
**Gap:** Netlify Blob integration stubbed — pushToBlob and pullFromBlob are empty functions. Most data-critical app in suite, weakest persistence. Fix is high priority once GitHub write is done.
**Missing from hub:** No card on hub.html — add it
**CNC overlap with Pattern Studio:** Both apps touch CNC/Carvco output. Resolution: Pattern Studio owns geometry export (SVG → Carvco). Tile Technical Data owns production record and machine parameter reference. Not true duplication — different concerns.

### 7. Date format standardization
**Status:** Identified, not actioned
**Resolution:** Standardize on ISO 8601 (YYYY-MM-DD) across all apps

---

## MASTER RUNNING LIST — as of 2026-06-22

### Ready to action now (unblocked)
1. Update `claude-sonnet-4-5` → `claude-sonnet-4-6` — do all three locations simultaneously: ai.js, app.js, Marketing project instructions. One coordinated change.
2. Add auth check at top of ai.js before action routing (simple top-level check, Peter confirmed this is planned)
3. Fix pattern.html nav link — `glaze.html` → `glaze_studio.html`
4. Marketing project instructions — remove "never change model string" instruction, remove "launching spring 2026", update version reference from v8.0 to v8.12
5. Kiln element health bar labels in Business App — clarify they show initial reference readings, not current readings (label fix only — the data is correct)
6. Add masterNotebook to pushAllToCloud in app.js

### Blocked behind GitHub write capability
7. Build shared GitHub write function — ai.js new action or dedicated github.js Netlify function
8. Activate Tile Technical Data Netlify Blob integration (currently stubbed)
9. Add "suspended" glaze status
10. Mandatory finish-type field on glaze creation
11. Separate glaze dropdowns by finish type (Matte/Satin/Gloss)
12. Bottle label print/export from glaze card — ID, finish type, SG target, mix date
13. Full glaze lifecycle system (T-naming, G-promotion, CSV intake, firing report)
14. State doc automation — Claude writes, pushes via PAT at session end

### Needs decision / more information
15. M-series glazes in reformulations.csv — evaluate for promotion into main glaze list under correct finish category
16. Confirm Illustrator SVG export flavor — unblocks Pattern Studio Stage 2
17. Which Claude project owns ai.js and app.js — Peter to confirm

### Deferred by Peter's decision
18. Refactor app.js (452kb) into modules — defer until after current feature work
19. GCode delivery — consider moving from Google Drive to repo/Netlify
20. molds.json — 4x4 and 3x3 GCode files not yet created
21. Pattern Studio CNC/Carvco export workflow — not a priority yet
22. SYSTEM_PROMPT visible in browser devtools — low priority
23. Add tile_technical_data.html card to hub.html

### Known bugs
24. nextTNumber() / nextTNumberPreview() potential drift on mid-session CSV import
25. "update state" keyboard listener fires inside textareas/inputs — needs exclusion
26. Test glazes only in Blob if never promoted — no automatic backup path

---

## CROSS-PROJECT CONFLICT LOG

| Conflict | Status | Resolution |
|----------|--------|------------|
| GitHub write — standalone vs shared | Resolved 2026-06-22 | Shared service only — previous spec overridden |
| Model string "never change" in Marketing instructions | Open | Remove instruction, update to claude-sonnet-4-6 |
| Delivery method — complete files vs Perl patches | Clarified 2026-06-22 | Perl patches for app.js only (452kb). Complete files for individual HTML apps. Must be explicit in every project's instructions. |
| Pattern Studio / Tile Technical Data CNC overlap | Resolved 2026-06-22 | Different concerns — not true duplication. Pattern owns geometry, Tile Technical Data owns production record. |

---

## DECISIONS THAT MUST NOT BE REVERSED

- SerpAPI cannot be called from Netlify — must use GitHub Actions or Mac terminal
- TextEdit on Mac corrupts JavaScript — always use Terminal cat command for JS files
- Two Netlify deployments exist — always cane-creek-app.netlify.app
- Template literals (backticks) must be properly closed — missing one breaks entire app silently
- AI analysis of glaze results stays outside the app — app is repository, AI conversations are working bench
- GitHub write function must be shared — not standalone per-app

---

## PROJECT CLAUDE INSTRUCTIONS TEMPLATE

Every project Claude must have these standing instructions:

1. Fetch your state doc from GitHub at session start — URL in project knowledge
2. Read it fully before responding to anything
3. Update state doc after every significant decision or completed feature — do not wait for session end
4. Use shared services — check SHARED SERVICES INVENTORY before building anything new
5. Flag any cross-project architectural decisions clearly — Overseer needs to know
6. Deliver complete files for HTML apps, Perl patches for app.js
7. Never duplicate a service that already exists in ai.js or data.js
8. Model string: claude-sonnet-4-6
9. No apologies, no sycophancy — direct working relationship with Peter

---

## STATE DOC TEMPLATE — CURRENT VERSION

```
## SHARED SERVICES USED
List every shared service this app touches

## FLAGS FOR OVERSEER  
Anything needing cross-project coordination — leave blank if nothing
```
Add these two sections to the standard template for all project state docs.

---

## NOTES FOR NEXT OVERSEER SESSION

- Confirm which project Claude owns ai.js — that's where GitHub write gets built first
- Once confirmed, issue GitHub write build instruction — spec is clear, just needs building
- After GitHub write tested and working, issue glaze development system build instruction
- Glaze contamination: Peter needs to mark compromised test glazes as suspended and remix from dry materials. App needs "suspended" status first.
- State repo — consider making public to eliminate token expiry problem permanently
- SerpAPI key is exposed in plain text in the Master Notebook — should move to Netlify environment variables
- Running list items 1, 4 are ready to action right now with no blockers — good candidates for next session
