# Cane Creek Studio — Overseer State
**Last updated:** 2026-06-21
**Session:** URL fix + glazes.json marked complete
**Updated by:** Overseer

---

## HOW TO START A NEW OVERSEER SESSION

Fetch this document:
`https://raw.githubusercontent.com/Pcane/Cane-Creek-State/main/OVERSEER_STATE.md`

And the system map:
`https://raw.githubusercontent.com/Pcane/Cane-Creek-State/main/SYSTEM_MAP.md`

Read both before proceeding. Do not rely on any files attached to the Claude project — always fetch fresh from GitHub.

---

## CURRENT SYSTEM STATUS

| App | Status | Version | Last touched |
|-----|--------|---------|-------------|
| Business app (index.html + app.js) | Live | v8.12 | ~2 months ago |
| Glaze Studio (glaze_studio.html) | Live | — | 2026-06-20 |
| Fireplace Designer (design_v2.html) | Live, stable | — | 2 weeks ago |
| Pattern Studio (pattern.html) | Live | — | 5 days ago |
| Hub (hub.html) | Live | — | 4 days ago |
| Public website | Live | — | Content pending update |
| Tile Record App | Not yet built | — | — |

---

## ACTIVE ARCHITECTURAL DECISIONS IN PROGRESS

### 1. glazes.json extraction — COMPLETE
**Status:** Done — glazes.json is live in cane-creek-app repo root
**Both glaze_studio.html and tile_technical_data.html fetch from ./glazes.json at runtime**
**No further action needed**

### 2. GitHub write capability — HIGH PRIORITY — NEXT TASK
**Status:** Architected, not yet built
**What:** PAT-based GitHub API write capability so apps can update Cane-Creek-State files
**Why:** Glaze Studio needs to update glazes.json and STUDIO_NOTEBOOK.md glaze section when recipes change. Tile Record app needs to update CNC parameters section when process profiles change.
**How:** Personal Access Token stored in localStorage. Apps call GitHub API directly. Token never hardcoded, never committed to repo.
**Build as:** Standalone utility built into each app that needs it — not a separate app
**Who needs write access first:** Glaze Studio Claude — glaze recipes section of STUDIO_NOTEBOOK.md and glazes.json
**Instruction to issue:** Go to Glaze Studio chat, issue GitHub write instruction. Test thoroughly before extending to Tile Record app.

### 3. Glaze development system — HIGH PRIORITY — AFTER GITHUB WRITE
**Status:** Fully specced — ready to build
**Scope:** Significant expansion of glaze_studio.html capabilities
**Spec:** See GLAZE DEVELOPMENT SYSTEM SPEC section below

### 4. Tile record app Stage 1 — PENDING GitHub write capability
**Status:** Spec complete, not yet built
**Blocker:** GitHub write capability should be in place first
**State document:** TILE_RECORD_STATE.md in cane-creek-state

### 5. Pattern Studio Stage 2 — PENDING confirmation
**Status:** Fully specced, awaiting one piece of information
**Blocker:** Peter needs to confirm Illustrator SVG export flavor before building
**Next step:** Ask Peter which Illustrator SVG export setting he uses, then issue build instructions

### 6. Date format standardization — MEDIUM PRIORITY
**Status:** Identified, not yet actioned
**What:** Glaze studio and business app use inconsistent date formats
**Resolution:** Standardize on ISO 8601 (YYYY-MM-DD) across all apps
**Instruction to issue:** After next glaze studio session, ask Claude to audit all date handling and standardize

---

## GLAZE DEVELOPMENT SYSTEM SPEC
Decided 2026-06-20. Build in glaze_studio.html after GitHub write capability is in place.

### Core concept
The app is the permanent repository of keeper glazes and their recipes.
AI conversations are the working bench — analysis and recipe suggestion happens outside the app.
The cycle is: app generates firing report → Peter pastes into AI conversation → AI suggests new recipes → Peter uploads CSV → app ingests and assigns T-numbers.

### Glaze lifecycle
Three statuses: Test / Active / Retired

**Test glazes — T-prefix naming**
Format: TG (gloss), TM (matte), TS (satin) + sequential number
Examples: TG-01, TM-03, TS-02
Number is sequential within each surface type independently.
Surface type is Peter's intended target at creation — may not match result.

**Promotion to Active**
When a test glaze proves out, Peter promotes it to Active.
On promotion: assigned next available G-number (G43, G44 etc.)
Surface type override available at promotion — TG-04 can promote as a satin glaze if that's what it turned out to be.
Full recipe history carries over linked to the G-number.
T-number retired — not reused.

**Retirement**
Any Active glaze can be retired. Stays visible in library with Retired status.
Never deleted — history preserved.

### Four capabilities to build (in this order)

**1. glazes.json with lifecycle fields**
Add status field to every glaze record: "test" / "active" / "retired"
Add T-number field for test glazes.
Add promotion history — what T-number became what G-number and when.

**2. T-naming and G-promotion UI**
When adding a new test glaze: select surface type (Gloss/Matte/Satin), app auto-assigns next T-number.
Promote button on any test glaze — assigns next G-number, prompts surface type confirmation.
Retire button on any active glaze.

**3. CSV upload intake**
Peter uploads a CSV of new test recipes (from AI conversation or UMF calculator).
App ingests, auto-assigns T-numbers based on surface type column in CSV.
CSV format: surface_type (G/M/S), colorant_1_name, colorant_1_pct, colorant_2_name, colorant_2_pct (repeat as needed), notes. Name/description optional.
App assigns T-number automatically — not in CSV.

**4. Firing report generator**
Single export button — generates structured text document.
Contents: clay body recipe, base glaze recipe, SG target, f-factor, application method, and per-glaze: colorant recipe, SG at application, visual result (color, surface, transparency, defects).
Output: clean text Peter can paste directly into any AI conversation.
No AI inside the app for this — report goes out, recipes come back as CSV.

### What stays outside the app
AI analysis of firing results — happens in Claude or other AI conversations.
Recipe suggestions — generated by AI or UMF calculator, delivered as CSV.
UMF calculator — planned as standalone app (glaze_chem.html), not a tab in glaze_studio.

---

## FIRING ASSESSMENT — 2026-06-20
Peter fired 9 new G-series glazes. Results and diagnosis below.
Root cause: glazes applied at severely diluted SG (1.22-1.29 vs target 1.33). Thin application = incomplete fusion = matte surface. Not a recipe problem for most glazes.

### Group 1 — SG correction only, refire at 1.33
| Glaze | Applied SG | Result | Action |
|-------|-----------|--------|--------|
| G26 Copper Celadon | 1.235 | Off white, satin | Refire at 1.33 |
| G28 Chrome Green + Iron | 1.240 | Medium brown, matte | Refire at 1.33 |
| G30 Cobalt + Rutile | 1.280 | Matte to satin, speckled | Refire at 1.33 |
| G35 UNC Blue + Rutile | 1.220 | Blotchy, matte to satin | Refire at 1.33 |
| G40 Tenmoku Iron Black | 1.270 | Dark brown, matte | Refire at 1.33 |
| G42 Warm Amber | 1.292 | Rough surface, thin | Refire at 1.33 |

### Group 2 — Recipe adjustment needed
**G38 — Rutile Ochre (8% rutile)**
Problem: Rutile at 8% is a matting agent — SG fix alone won't produce gloss.
Options: Drop rutile to 2-3% + add 0.5-1% RIO to hold warm color. OR accept as intentional satin at proper SG.

**G29 — Vanadium Yellow + Iron**
Problem: Vanadium stains resist gloss at cone 6 oxidation. Iron addition compounds the matting.
Options: Drop vanadium to 3-4%, remove iron, retest. OR consider Mason 6485 Zirconium Yellow as alternative if gloss is required.

**G25 — Chrome-Tin Cranberry**
Problem: Chrome at 0.06% is far too low — tin wins and opacifies white. Chrome-tin pinks need 0.1-0.3% chrome.
Adjusted recipe: Chrome Oxide 0.72g (0.12%) + Tin Oxide 18.18g (3%) per 600g base at SG 1.33.
Critical: Fire G25 isolated from other tin-bearing glazes — chrome volatilizes and contaminates neighbors.

### Glazes that fired well
| Glaze | Applied SG | Result |
|-------|-----------|--------|
| G21 Dark Brown | 1.167 | Good — high iron compensates for thin application |
| G11 Transparent Dark Green | 1.252 | Nice gloss, good break, slight transparency on edges |

---

## PENDING OVERSEER TASKS

| Task | Priority | Notes |
|------|----------|-------|
| Issue GitHub write capability instruction to Glaze Studio Claude | High | Next task — unblocks notebook and lifecycle system |
| Issue glaze development system build instruction | High | After GitHub write confirmed working |
| Issue Tile Record app Stage 1 build instruction | High | After GitHub write in place |
| Update Marketing project instructions | Medium | Remove "launching spring 2026", fix version to v8.12 |
| Create MARKETING_STATE.md founding document | Medium | Needs current app state |
| Create GLAZE_STATE.md founding document | Medium | Needs current glaze studio state |
| Create STUDIO_STATE.md founding document | Medium | Covers pattern, design_v2, hub |
| Create WEBSITE_STATE.md in website repo | Low | When website work resumes |
| Issue Pattern Studio card add to hub.html | Low | Simple one-line change |
| Issue date format standardization | Medium | After next glaze studio session |
| Confirm Illustrator SVG flavor with Peter | Medium | Unblocks Pattern Studio Stage 2 |

---

## NOTES FOR NEXT OVERSEER SESSION

- GitHub write capability is the immediate next action — go to Glaze Studio chat and build it there first.
- After GitHub write confirmed working, issue glaze development system build instructions — full spec is in this document above.
- Peter needs to refire Group 1 glazes at SG 1.33 before any recipe changes. G25 retest uses adjusted recipe (0.12% chrome, 3% tin). Fire G25 isolated.
- UMF calculator is planned as standalone app glaze_chem.html — not a tab in glaze_studio. Defer until glaze development system is built.
- Core principle confirmed: app is permanent repository of keeper glazes and recipes. AI conversations are the working bench.
- Remove old project files (SYSTEM_MAP.md, OVERSEER_STATE.md) from this Claude project settings — they cause stale fetches on session start. Let the GitHub fetch do the work instead.
- Marketing project instructions need updating — current instructions reference v8.0 and "launching spring 2026" which are both outdated.
