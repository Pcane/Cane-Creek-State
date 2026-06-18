# Cane Creek Studio — Overseer State
**Last updated:** 2026-06-17  
**Session:** Founding session  
**Updated by:** Overseer

---

## HOW TO START A NEW OVERSEER SESSION

Fetch this document:
`https://raw.githubusercontent.com/Pcane/cane-creek-app/refs/heads/main/OVERSEER_STATE.md`

And the system map:
`https://raw.githubusercontent.com/Pcane/cane-creek-app/refs/heads/main/SYSTEM_MAP.md`

Read both before proceeding.

---

## CURRENT SYSTEM STATUS

| App | Status | Version | Last touched |
|-----|--------|---------|-------------|
| Business app (index.html + app.js) | Live | v8.12 | ~2 months ago |
| Glaze Studio (glaze_studio.html) | Live | — | Last week |
| Fireplace Designer (design_v2.html) | Live, stable | — | 2 weeks ago |
| Pattern Studio (pattern.html) | Live | — | 5 days ago |
| Hub (hub.html) | Live | — | 4 days ago |
| Public website | Live | — | Content pending update |
| Tile Record App | Not yet built | — | — |

---

## ACTIVE ARCHITECTURAL DECISIONS IN PROGRESS

### 1. glazes.json extraction — HIGH PRIORITY
**Status:** Pending  
**What:** Extract GLAZES array from glaze_studio.html into shared glazes.json in repo root  
**Why:** Tile record app needs glaze data. Two apps cannot maintain separate copies.  
**Instruction to issue:** Go to Studio chat, upload glaze_studio.html, ask Claude to extract the GLAZES array to glazes.json and update glaze_studio.html to fetch from it. Confirm it still works before proceeding.  
**Blocker for:** Tile record app glaze integration

### 2. Tile record app — PENDING glazes.json
**Status:** Spec complete, not yet built  
**Spec document:** Established in session 2026-06-17 — see SYSTEM_MAP.md section 9  
**Blocker:** glazes.json must exist first  
**Next step after glazes.json:** Issue build instructions to Studio chat

### 3. Pattern Studio Stage 2 — PENDING confirmation
**Status:** Fully specced, awaiting one piece of information  
**Blocker:** Peter needs to confirm Illustrator SVG export flavor before building  
**Next step:** Ask Peter which Illustrator SVG export setting he uses, then issue build instructions

### 4. Date format standardization — MEDIUM PRIORITY
**Status:** Identified, not yet actioned  
**What:** Glaze studio and business app use inconsistent date formats  
**Resolution:** Standardize on ISO 8601 (YYYY-MM-DD) across all apps  
**Instruction to issue:** After next glaze studio session, ask Claude to audit all date handling and standardize

---

## WHAT WAS ESTABLISHED THIS SESSION

This was the founding session. The following was established:

**Repo audit completed:**
- Deleted: design.html, measure.html, design_v2 (1).html, fireplace-fixed.json, glaze.html
- Renamed: studio_calc.html → glaze_studio.html
- Confirmed: index.html is the business app shell, not a duplicate
- Result: Clean 11-file repo

**Tile standards confirmed** (all in SYSTEM_MAP.md section 6-7)

**CNC three-pass system confirmed** (all in SYSTEM_MAP.md section 7)

**Tile record app fully specced** (SYSTEM_MAP.md section 9)

**System architecture established:**
- Two projects: Marketing (existing) and Studio Overseer (new)
- State document system via GitHub raw URLs
- Overseer writes system map, coding Claudes write state documents
- SYSTEM_MAP.md is single source of truth

---

## PENDING OVERSEER TASKS

| Task | Priority | Notes |
|------|----------|-------|
| Issue glazes.json extraction instruction | High | First architectural task |
| Update Marketing project instructions | Medium | Remove "launching spring 2026", fix version to v8.12 |
| Create MARKETING_STATE.md founding document | Medium | Needs current app state |
| Create GLAZE_STATE.md founding document | Medium | Needs current glaze studio state |
| Create STUDIO_STATE.md founding document | Medium | Covers pattern, design_v2, hub |
| Create WEBSITE_STATE.md in website repo | Low | When website work resumes |
| Issue Pattern Studio card add to hub.html | Low | Simple one-line change |
| Issue date format standardization | Medium | After next glaze/marketing session |
| Confirm Illustrator SVG flavor with Peter | Medium | Unblocks Pattern Studio Stage 2 |

---

## NOTES FOR NEXT OVERSEER SESSION

- Peter is firing the 9 new G-series glazes tomorrow and assessing the day after. After assessment, issue instructions to glaze studio Claude to build the feedback/journal tab.
- The tile record app printable sheet mockup was built and iterated in today's session — Peter approved the layout. Full spec is in SYSTEM_MAP.md.
- Marketing project instructions need updating — current instructions reference v8.0 and "launching spring 2026" which are both outdated.
- Peter confirmed working style: open equal-status relationship, disagree when wrong, suggest alternatives, think hard before answering, understands informal typing.
