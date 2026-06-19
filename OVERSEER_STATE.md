# Cane Creek Studio — Overseer State
**Last updated:** 2026-06-18  
**Session:** Tile record app spec — full redesign as experimental lab notebook  
**Updated by:** Overseer

---

## HOW TO START A NEW OVERSEER SESSION

Fetch this document:
`https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/OVERSEER_STATE.md`

And the system map:
`https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/SYSTEM_MAP.md`

Read both before proceeding.

---

## CURRENT SYSTEM STATUS

| App | Status | Version | Last touched |
|-----|--------|---------|-------------|
| Business app (index.html + app.js) | Live | v8.12 | ~2 months ago |
| Glaze Studio (glaze_studio.html) | Live | — | This week |
| Fireplace Designer (design_v2.html) | Live, stable | — | 2 weeks ago |
| Pattern Studio (pattern.html) | Live | — | 5 days ago |
| Hub (hub.html) | Live | — | 4 days ago |
| Public website | Live | — | Content pending update |
| Tile Record App | Not yet built | — | — |

---

## ACTIVE ARCHITECTURAL DECISIONS IN PROGRESS

### 1. glazes.json extraction — HIGH PRIORITY — FIRST TASK
**Status:** Pending  
**What:** Extract GLAZES array from glaze_studio.html into shared glazes.json in repo root  
**Why:** Tile record app Stage 3 needs glaze data. Two apps cannot maintain separate copies.  
**Instruction to issue:** Go to Studio chat, upload glaze_studio.html, ask Claude to extract the GLAZES array to glazes.json and update glaze_studio.html to fetch from it. Confirm it still works before proceeding.  
**Blocker for:** Tile record app Stage 3 glaze integration. Do not begin tile record Stage 3 until this is confirmed done.

### 2. Glaze mix log and recipe versioning — PENDING
**Status:** Spec discussed with Glaze App Claude, awaiting Overseer architectural sign-off  
**What:** Glaze App Claude proposed splitting glaze data into two structures:
- `glazes.json` — recipe registry with versioning and retirement
- `glaze_log.json` — per-batch mix log (date, SG, adjustments, firing result)  
**Glaze App Claude's recommendation:** glazes.json to GitHub (shared), glaze_log.json local to Glaze App (localStorage + Blob) because mix log is high-frequency write data  
**Overseer decision:** Agreed. glazes.json to repo root, readable by all apps. glaze_log.json stays local to Glaze App. Only Glaze App Claude has write authority to glazes.json.  
**Instruction to issue:** When issuing glazes.json extraction instruction, include the versioning schema the Glaze App Claude proposed. See schema below.

**glazes.json entry schema:**
```json
{
  "id": "G25",
  "version": 2,
  "status": "active",
  "name": "Chrome-Tin Cranberry OX",
  "nomenclature": "OX",
  "target_sg": 1.33,
  "cmc_pct": 0.20,
  "veegum_pct": 0.15,
  "colorants": [
    { "material": "Chrome Oxide", "amount_g": 0.06, "per_g_base": 600 }
  ],
  "version_history": [
    {
      "version": 1,
      "retired_date": "2026-05-10",
      "reason": "Chrome too borderline at 0.06% — blotchy result in Fire 1"
    }
  ]
}
```

**glaze_log.json entry schema:**
```json
{
  "glaze_id": "G25",
  "glaze_version": 2,
  "date_mixed": "2026-06-18",
  "firing_date": "2026-06-25",
  "batch_size_g": 600,
  "target_sg": 1.33,
  "actual_sg": 1.292,
  "adjustments": [],
  "result_notes": "",
  "recipe_change_triggered": false
}
```

### 3. Tile record app — Stage 1 build — NEXT AFTER glazes.json
**Status:** Fully specced, not yet built  
**Full spec:** SYSTEM_MAP.md section 9 — Tile Record App  
**Build order:** Five stages — do not deviate. Stage 1 first.  
**Stage 1 scope:** Identity, Mold, Size, Result fields only. Dashboard view with tile cards. No file uploads. No CNC layers. No glaze integration. Get data entry, storage, retrieval working first.  
**Instruction to issue after glazes.json is done:** Go to Studio chat, start tile_record.html from scratch, follow Stage 1 spec in SYSTEM_MAP.md section 9.

### 4. Netlify Blob file upload proof of concept — BEFORE Stage 4
**Status:** Not yet tested  
**What:** Stage 4 of tile record app uploads SVG and G-code files to Netlify Blob. Blob has known throttling behavior. Need to confirm file upload works reliably before building Stage 4.  
**Instruction to issue:** Before building Stage 4, ask Studio Claude to write a minimal standalone test — upload one small file to Blob, retrieve it, confirm it works. Do not build Stage 4 until this passes.

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

## WHAT WAS ESTABLISHED THIS SESSION

**Tile record app fully redesigned as experimental lab notebook:**
- Reframed from "birth certificate" to lab notebook — Peter is in discovery phase, system must serve experimentation first
- Eleven process layers defined in full detail
- Versioned process profiles added — CNC parameters, firing schedules tracked as named versioned profiles, size-tagged
- Three navigation views: Today / This Tile / Compare
- File storage architecture decided: SVG and G-code to Netlify Blob, large files (AI source, R5 photos) to Google Drive with links, Carvco files discarded as ephemeral
- Customer reference field added — optional link to business app CRM for reproducibility lookup
- Tile type field added: square field tile / art tile / liner / border / corner / other
- Five-stage build order established — Stage 1 first, compare view last
- Full spec written into SYSTEM_MAP.md section 9

**Glaze mix log architecture confirmed:**
- Glaze App Claude's proposed schema reviewed and approved
- glazes.json → shared, GitHub repo root, read by all apps, written only by Glaze App
- glaze_log.json → local to Glaze App, localStorage + Blob

**GitHub access clarification:**
- Confirmed: raw.githubusercontent.com URLs from private repos return 404 — Claude cannot self-fetch
- Peter pastes state documents manually at session start — this is the current workflow
- GitHub bridge app (programmatic read/write via PAT) discussed as future improvement — not yet built, not yet prioritized

---

## PENDING OVERSEER TASKS

| Task | Priority | Notes |
|------|----------|-------|
| Issue glazes.json extraction instruction (with versioning schema) | High | First task — blocks everything downstream |
| Issue tile record Stage 1 build instruction | High | After glazes.json confirmed working |
| Issue Netlify Blob file upload proof of concept | High | Before tile record Stage 4 |
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

- glazes.json extraction is the immediate next task. Issue instruction to Studio/Glaze chat. Include the versioning schema from this document.
- After glazes.json confirmed working, issue tile record Stage 1 build instruction to Studio chat.
- Peter confirmed working style: open equal-status relationship, disagree when wrong, suggest alternatives, think hard before answering, understands informal typing.
- Peter is firing the 9 new G-series glazes — after assessment, issue instructions to Glaze Studio Claude to build the feedback/journal tab.
- Marketing project instructions need updating — current instructions reference v8.0 and "launching spring 2026" which are both outdated.
- GitHub bridge app (PAT-based read/write) was discussed as future improvement to reduce manual paste friction. Worth building eventually but not a current priority — other work is more pressing.
