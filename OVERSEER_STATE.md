# Cane Creek Studio — Overseer State
**Last updated:** 2026-06-18  
**Session:** Tile record app spec, shared notebook architecture, GitHub write capability  
**Updated by:** Overseer

---

## HOW TO START A NEW OVERSEER SESSION

At the start of every session, before doing anything else, fetch both documents below. Do not respond to Peter until you have read both.

Fetch this document:
`https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/OVERSEER_STATE.md`

And the system map:
`https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/SYSTEM_MAP.md`

Confirm you are up to speed before proceeding.

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
**Active glazes to mark active:** G11, G16 (warm white — Tin Oxide 2%), G21, G25, G26, G28, G29, G30, G35, G38, G40, G42  
**Clear gloss slurry:** Add as new entry — recipe is in the studio notebook Chapter 2 Section 3  
**All other G1–G24 glazes:** Mark retired, reason "retired by Peter 2026-06-18 — pending future review"  
**Instruction to issue:** Go to Glaze Studio chat, upload glaze_studio.html, extract GLAZES array to glazes.json using versioning schema below. Update glaze_studio.html to fetch from glazes.json. Confirm working before closing session.  
**Blocker for:** Tile record app Stage 3, GitHub write to notebook glaze section

### 2. GitHub write capability — HIGH PRIORITY — SECOND TASK
**Status:** Architected, not yet built  
**What:** PAT-based GitHub API write capability so apps can update Cane-Creek-State files  
**Why:** Glaze Studio needs to update glazes.json and STUDIO_NOTEBOOK.md glaze section when recipes change. Tile Record app needs to update CNC parameters section when process profiles change.  
**How:** Personal Access Token stored in localStorage. Apps call GitHub API directly. Token never hardcoded, never committed to repo.  
**Build as:** Standalone utility built into each app that needs it — not a separate app  
**Who needs write access:**
- Glaze Studio Claude — glaze recipes section of STUDIO_NOTEBOOK.md and glazes.json
- Tile Record Claude — CNC/Carvco/UGS parameters section of STUDIO_NOTEBOOK.md
- No other apps need write access  
**Instruction to issue:** After glazes.json extraction confirmed working, issue GitHub write instruction to Glaze Studio Claude first. Test thoroughly before extending to Tile Record app.

### 3. STUDIO_NOTEBOOK.md — HIGH PRIORITY — THIRD TASK
**Status:** Pending  
**What:** Upload studio notebook to Cane-Creek-State as STUDIO_NOTEBOOK.md. Structure the four critical sections so apps can update them cleanly.  
**Four critical sections (app-maintained):**
1. Glaze recipes — owned by Glaze Studio Claude
2. CNC/Carvco/UGS parameters — owned by Tile Record Claude
3. Clay body recipe — manual update by Peter (changes rarely)
4. Image file references — owned by Tile Record Claude  
**Everything else in notebook:** Background, stable, Peter updates manually when needed  
**Note:** Notebook does not need reorganization before upload — upload as-is, structure the four critical sections clearly so apps know exactly where to write  
**Instruction to issue:** Peter uploads current studio notebook to Cane-Creek-State as STUDIO_NOTEBOOK.md. Then issue instruction to Glaze Studio Claude to wire notebook glaze section updates alongside glazes.json updates.

### 4. Glaze mix log and recipe versioning — PENDING
**Status:** Spec discussed with Glaze App Claude, Overseer approved  
**glazes.json** — recipe registry, GitHub repo root, readable by all apps, written only by Glaze Studio Claude  
**glaze_log.json** — per-batch mix log, local to Glaze App, localStorage + Blob  

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

### 5. Tile record app — Stage 1 build — AFTER tasks 1-3
**Status:** Fully specced, not yet built  
**Full spec:** SYSTEM_MAP.md section 9  
**Build order:** Five stages — do not deviate. Stage 1 first.  
**Stage 1 scope:** Identity, Mold, Size, Result fields only. Dashboard view with tile cards. No file uploads. No CNC layers. No glaze integration.

### 6. Netlify Blob file upload proof of concept — BEFORE tile record Stage 4
**Status:** Not yet tested  
**What:** Test file upload to Blob before building Stage 4  
**Why:** Known throttling risk — must confirm before building

### 7. Pattern Studio Stage 2 — PENDING confirmation
**Status:** Fully specced, awaiting one piece of information  
**Blocker:** Peter needs to confirm Illustrator SVG export flavor  

### 8. Date format standardization — MEDIUM PRIORITY
**Status:** Identified, not yet actioned  
**Resolution:** ISO 8601 (YYYY-MM-DD) across all apps  

---

## WHAT WAS ESTABLISHED THIS SESSION

**Tile record app fully redesigned as experimental lab notebook** — see SYSTEM_MAP.md section 9 for full spec.

**Shared notebook architecture decided:**
- STUDIO_NOTEBOOK.md lives in Cane-Creek-State (public repo)
- Four critical sections maintained by apps: glaze recipes, CNC parameters, clay body, image references
- Everything else in notebook is background — Peter updates manually
- Glaze Studio Claude owns glaze section
- Tile Record Claude owns CNC/image sections
- Clay body changes so rarely that manual update is fine
- GitHub write capability (PAT-based) is required before any app can update the notebook

**Build sequence confirmed:**
1. glazes.json extraction
2. GitHub write capability
3. STUDIO_NOTEBOOK.md in Cane-Creek-State
4. Tile record app Stage 1
5. Remaining tile record stages

**GitHub access clarified:**
- Cane-Creek-State is public — any Claude can self-fetch via raw URL
- Apps write back via PAT-based GitHub API calls

---

## PENDING OVERSEER TASKS

| Task | Priority | Notes |
|------|----------|-------|
| Issue glazes.json extraction instruction | High | First task — use active glaze list and schema above |
| Issue GitHub write capability instruction | High | Second task — Glaze Studio first |
| Issue STUDIO_NOTEBOOK.md upload instruction to Peter | High | Third task — upload as-is, structure four critical sections |
| Issue tile record Stage 1 build instruction | High | After tasks 1-3 confirmed working |
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

- glazes.json extraction is the immediate next task. Issue instruction to Glaze Studio chat. Include active glaze list and versioning schema from this document.
- After glazes.json confirmed working, issue GitHub write capability instruction.
- After GitHub write working, Peter uploads studio notebook to Cane-Creek-State, then wire notebook updates into Glaze Studio.
- Peter is firing the new G-series glazes — after assessment, issue instructions to Glaze Studio Claude to build the feedback/journal tab.
- Marketing project instructions need updating — current instructions reference v8.0 and "launching spring 2026" which are both outdated.
- Peter confirmed working style: open equal-status relationship, disagree when wrong, suggest alternatives, think hard before answering, understands informal typing.
