# Cane Creek Studio — System Map
**Last updated:** 2026-06-19
**Updated by:** Overseer
**Version:** 1.2

---

## HOW TO START A NEW OVERSEER SESSION

Fetch this document:
`https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/SYSTEM_MAP.md`

Then fetch the overseer state:
`https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/OVERSEER_STATE.md`

Confirm you are up to speed before proceeding.

---

## 1. SYSTEM OVERVIEW

Cane Creek Tile Co. is a sole-maker handmade ceramic raised-line art tile studio in Alamance County, NC. Peter Cane is the sole maker — every tile made by one pair of hands, start to finish. Suzie Cane handles billing and administration. Pre-launch, targeting architects and interior designers. Direct sales only, no wholesale.

The digital suite consists of three GitHub repos, two Netlify deployments, and a set of HTML/JS apps. All apps are single-file HTML with embedded CSS and JS. No build step. No framework. Vanilla JS only.

---

## 2. REPOSITORIES

### `Pcane/cane-creek-app` (private)
**Live at:** cane-creek-app.netlify.app
**Purpose:** Internal studio and business tools
**Auto-deploys:** Yes, from main branch via Netlify

| File | Purpose | Status |
|------|---------|--------|
| `index.html` | Business app shell | Live |
| `app.js` | Business app logic (~6,300+ lines) | Live |
| `hub.html` | Studio tools launcher | Live |
| `glaze_studio.html` | Glaze calculator and session tracking | Live |
| `design_v2.html` | Fireplace surround tile layout calculator | Live |
| `pattern.html` | Pattern Studio — SVG pattern generator | Live |
| `tile_technical_data.html` | Tile Technical Data app | In development |
| `glazes.json` | Shared glaze library — single source of truth | Live |
| `netlify/functions` | Serverless functions | Live |
| `netlify.toml` | Netlify configuration | Live |
| `manifest.json` | PWA manifest | Live |
| `sw.js` | Service worker | Live |
| `README.md` | Repo documentation | Live |

### `Pcane/cane-creek-state` (private)
**Purpose:** State documents for all Claude projects
**Auto-deploys:** No — documents only

| File | Purpose | Status |
|------|---------|--------|
| `SYSTEM_MAP.md` | This file | Live |
| `OVERSEER_STATE.md` | Overseer session state | Live |
| `MARKETING_STATE.md` | Marketing Claude session state | Live |
| `GLAZE_STATE.md` | Glaze Studio Claude session state | Live |
| `STUDIO_STATE.md` | Studio tools Claude session state | Live |
| `TILE_RECORD_STATE.md` | Tile Technical Data Claude session state | Live |
| `WEBSITE_STATE.md` | Website Claude session state | Pending creation |
| `STUDIO_NOTEBOOK.md` | Studio Master Notebook — clay, glaze, CNC, kiln reference | Live |

### `Pcane/cane-creek-website` (private)
**Live at:** thehandmadetile.com
**Purpose:** Public-facing marketing website
**Auto-deploys:** Yes, from main branch via Netlify

| File | Purpose | Status |
|------|---------|--------|
| `index.html` | Homepage | Live, content pending update |

---

## 3. STACK

| Layer | Technology |
|-------|-----------|
| Hosting | Netlify |
| Storage | localStorage + Netlify Blob (cloud backup) |
| AI | Anthropic API — always `claude-sonnet-4-5` |
| Email | Microsoft Graph API |
| Contact discovery | Apollo.io |
| Prospect research | SerpApi (free tier, 100 searches/month) |
| Version control | GitHub |
| Dev environment | Mac Terminal, Perl patch scripts |
| DNS | GoDaddy |
| Design files | Google Drive (per-tile folders) |
| CNC software | Carvco |
| CNC controller | UGS |

---

## 4. DEV WORKFLOW — NEVER DEVIATE

1. Coding Claude writes patch script
2. Peter runs `perl patch_vX_X.pl [filename]` in Terminal from `~/Downloads/cane-creek-patch/`
3. Peter uploads patched file to `cane-creek-app` AND updated state document to `cane-creek-state` in same commit to each repo
4. Netlify auto-deploys (~30 seconds)
5. Peter tests in browser via JS console script
6. Peter uploads result JSON to Claude for analysis before any full re-assess

**Note:** GitHub raw URLs cache for up to 5 minutes. Wait a few minutes after uploading before starting a fresh session to ensure Claude fetches the latest state.

**Rules:**
- Never write code without completing the test cycle first
- Never run re-assess without test cycle
- Always use model string `claude-sonnet-4-5` — no other string ever
- One focused change set per conversation
- Always read relevant code section before changing it
- Update changelog header in app file every session
- Update state document every session — this is not optional

---

## 5. STATE DOCUMENTS — HOW THEY WORK

Each project has its own state document in the `cane-creek-state` repo. When a conversation gets long or a new Claude starts, it fetches the state document and picks up exactly where the last session left off.

**IMPORTANT: All state documents live in `Pcane/cane-creek-state`, NOT in `cane-creek-app`.**

| Document | Project | Fetch URL |
|----------|---------|-----------|
| `SYSTEM_MAP.md` | Overseer | `https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/SYSTEM_MAP.md` |
| `OVERSEER_STATE.md` | Overseer | `https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/OVERSEER_STATE.md` |
| `MARKETING_STATE.md` | Marketing | `https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/MARKETING_STATE.md` |
| `GLAZE_STATE.md` | Glaze Studio | `https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/GLAZE_STATE.md` |
| `STUDIO_STATE.md` | Studio tools | `https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/STUDIO_STATE.md` |
| `TILE_RECORD_STATE.md` | Tile Technical Data | `https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/TILE_RECORD_STATE.md` |
| `WEBSITE_STATE.md` | Website | `https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/WEBSITE_STATE.md` |
| `STUDIO_NOTEBOOK.md` | All Claudes | `https://raw.githubusercontent.com/Pcane/cane-creek-state/refs/heads/main/STUDIO_NOTEBOOK.md` |

**At the end of every session** the coding Claude delivers:
- Patched code file(s) → Peter uploads to `cane-creek-app`
- Updated state document → Peter uploads to `cane-creek-state`

Both uploads happen in the same commit to their respective repos.

---

## 6. TILE STANDARDS — CONFIRMED

These are the confirmed production standards for all new molds. All derived values cascade from these numbers.

### Working dimensions (mold / wet clay / design — all identical)
| Parameter | Value |
|-----------|-------|
| Face size | 6.570 × 6.570" |
| Pocket depth | 0.445" |
| Safety margin | 0.125" all sides |
| Design safe area | 6.320 × 6.320" |

### Shrinkage
| Parameter | Value |
|-----------|-------|
| Shrinkage factor | 8.6% |
| Fired face size | 6.000 × 6.000" |
| Fired thickness | 0.407" |

### Raised line spec — Motawi benchmark (default)
| CNC depth | Fired height | Base width (mold) | Base width (fired) |
|-----------|-------------|-------------------|-------------------|
| 0.021" | 0.018" | 0.042" | 0.038" |
| 0.025" | 0.023" | 0.049" | 0.045" |
| 0.028" | 0.026" | 0.052" | 0.048" |
| 0.030" | 0.027" | 0.055" | 0.050" |
| **0.035" ★** | **0.032"** | **0.060"** | **0.055"** |

★ Default target. Shallower = more refined but vulnerable to glaze overrun. Deeper = stronger, more forgiving.

**Note:** 6×6 is standard but other sizes are possible (4×4, 3×3, random ashlar etc.). Safety margin and line spec stay constant. All dimensions derive from fired face size via shrinkage factor.

---

## 7. CNC OPERATIONS — THREE-PASS SYSTEM

### Pass 1 — Rough pocket (SpeTool M02002)
| Parameter | Value |
|-----------|-------|
| Bit | SpeTool M02002 — 1/4" ball nose, 2-flute, fixed diameter |
| Toolpath | 2D Pocket |
| Start depth | 0.000" |
| Final depth | 0.445" |
| Step down | 0.138" |
| Stepover | 0.100" |
| Spindle | 18,000 RPM |
| Feed rate | 80 IPM |
| Plunge rate | 25 IPM |
| Cut direction | Conventional |
| Est. run time | ~45 min |

### Pass 2 — Finish pass (1/4" bull-nose end mill)
| Parameter | Value |
|-----------|-------|
| Bit | 1/4" bull-nose end mill (to be sourced) |
| Toolpath | 2D Pocket |
| Start depth | 0.435" |
| Final depth | 0.445" |
| Step down | 0.005" |
| Stepover | 0.016" (test value — assess surface quality, was 0.008" for ~5hrs) |
| Spindle | 18,000 RPM |
| Feed rate | 18 IPM |
| Plunge rate | 8 IPM |
| Cut direction | Climb |
| Est. run time | ~2.5 hrs |

### Pass 3 — Line grooves (Amana 45763)
| Parameter | Value |
|-----------|-------|
| Bit | Amana 45763 — 60° V-bit, 0.020" tip, 1/4" shank, 2-flute |
| Toolpath | 2D Profile — centerline vectors, Layer 3 only |
| Start depth | 0.000" |
| Final depth | Tile-specific (see raised line spec table) |
| Tolerance | 0.001" |
| Spindle | 18,000 RPM |
| Feed rate | 25 IPM |
| Plunge rate | 8 IPM |
| Cut direction | Conventional |
| Ramp moves | Off |

---

## 8. GLAZE SYSTEM

### Base slurry targets
| Parameter | Value |
|-----------|-------|
| Specific gravity | 1.33 |
| Flux factor (f) | 0.404 |
| CMC | 0.20% |
| Colorant method | Direct-weigh with pre-wet |

### G-series glazes
Glazes G1–G43+ established. Full nomenclature system: OX/MX/MS/HC.

**Data location:** `glazes.json` in root of `cane-creek-app` repo. Both `glaze_studio.html` and `tile_technical_data.html` fetch from this single file at runtime via `./glazes.json`. Never duplicate glaze data in any app.

**Glazing method:** Wax all backs → water submersion → bulb-apply colors into recesses → fast clear dip.

---

## 9. APP MAP

### Business App (`index.html` + `app.js`)
**Purpose:** CRM, billing, marketing, production tracking
**Data:** localStorage + Netlify Blob
**Model:** `claude-sonnet-4-5` always
**Current version:** v8.12
**Managed by:** Cane Creek Marketing project
**State document:** `MARKETING_STATE.md` in `cane-creek-state`

### Glaze Studio (`glaze_studio.html`)
**Purpose:** Glaze calculation, session tracking, G-series library
**Data:** localStorage + Netlify Blob
**Glaze data:** Fetches from `./glazes.json` at runtime
**Pending:** Glaze session feedback/journal tab
**State document:** `GLAZE_STATE.md` in `cane-creek-state`

### Fireplace Designer (`design_v2.html`)
**Purpose:** Fireplace surround tile layout calculator
**Data:** localStorage
**Status:** Stable, 36-test debug suite passing

### Pattern Studio (`pattern.html`)
**Purpose:** Tile pattern generator with SVG export
**Data:** localStorage
**Pending Stage 2:** Seed import, transform stack, overlap modes, validation, recipe library
**Blocker:** Confirm Illustrator SVG export flavor before Stage 2
**State document:** `STUDIO_STATE.md` in `cane-creek-state`

### Hub (`hub.html`)
**Purpose:** Studio tools launcher
**Pending:** Add Tile Technical Data card (after app is working)

### Tile Technical Data (`tile_technical_data.html`)
**Purpose:** Permanent structured record for every tile — design through fired result
**Data:** Netlify Blob primary, localStorage cache
**Glaze data:** Fetches from `./glazes.json` at runtime
**Status:** In development
**Key features:** Printable one-page CNC reference sheet, live glaze data pull, Google Drive file links
**State document:** `TILE_RECORD_STATE.md` in `cane-creek-state`
**Managed by:** Cane Creek Tile Technical Data project (separate Claude project)

### Public Website (`index.html` in cane-creek-website)
**Purpose:** Public marketing site
**Status:** Live, content pending full update
**Pending:** Formspree contact form, inner pages
**State document:** `WEBSITE_STATE.md` in `cane-creek-state` (pending creation)

---

## 10. DATA OWNERSHIP

| Data | Owner | Location | Shared with |
|------|-------|----------|-------------|
| Prospect records | app.js | localStorage + Blob | Nothing yet |
| Glaze library | glazes.json | cane-creek-app repo | glaze_studio.html + tile_technical_data.html |
| Glaze sessions | glaze_studio.html | localStorage + Blob | Nothing |
| Tile records | tile_technical_data.html | localStorage + Blob | Nothing yet |
| CNC standards | SYSTEM_MAP.md | cane-creek-state | All apps (read only) |
| Tile standards | SYSTEM_MAP.md | cane-creek-state | All apps (read only) |
| Design files | Google Drive | Drive | tile_technical_data.html links to them |
| Pattern seeds | pattern.html | localStorage | tile_technical_data.html (pending) |

---

## 11. PENDING ARCHITECTURAL DECISIONS

| Decision | Priority | Notes |
|----------|----------|-------|
| Pattern Studio Stage 2 | Medium | Confirm Illustrator SVG flavor first |
| Standardize date format across all apps | Medium | Use ISO 8601 everywhere — glaze studio and business app currently inconsistent |
| Glaze journal tab in glaze_studio | Medium | Build after firing assessment |
| Website inner pages | Medium | Fireplaces, Backsplash, Dados, About, How It's Made |
| Formspree contact form on website | Low | Wire when content is ready |
| Pattern Studio card in hub.html | Low | Simple add, low effort — do alongside Tile Technical Data hub card |

---

## 12. KNOWN TECHNICAL DEBT

| Item | Location | Priority |
|------|----------|----------|
| Pattern Studio card missing from hub.html | hub.html | Low |
| Tile Technical Data card missing from hub.html | hub.html | Low — add when app is working |
| GRBL ALARM:3 false limit-switch triggers | CNC hardware | Medium — permanent capacitor fix needed (`$21=0` is current workaround) |
| Date format inconsistency across apps | Multiple | Medium |

---

## 13. KNOWN BUGS

*None currently logged. Add here as discovered.*

---

## 14. DO NOT DO THESE — LESSONS LEARNED

| Rule | Reason |
|------|--------|
| Never run simultaneous API calls to Netlify blob | Blob storage throttles after ~12 records — use sequential calls with 2.5s delay |
| Never use model string other than `claude-sonnet-4-5` | Hard requirement, no exceptions |
| Never write app.js without uploading current version first | Code will be based on stale version |
| Never add Motawi, Heath, Fireclay etc. as prospects | These are competitor signal markers only, not prospects |
| Never fabricate contact emails | Apollo owns verified email enrichment — guessed emails are not a substitute |
| Never skip the test cycle before re-assess | Previous attempt throttled Netlify blob after ~12 records |
| Never put state documents in cane-creek-app | State documents live in cane-creek-state — no exceptions |
| Never hardcode glaze data in any app | glazes.json is the single source of truth — all apps fetch from it |

---

## 15. DECISION LOG

| Date | Decision | Reasoning | Rejected alternatives |
|------|----------|-----------|----------------------|
| 2026-06-17 | Split into Marketing project and Studio Overseer project | app.js alone is 6,300+ lines — combining with studio files would hit project capacity | Single combined project |
| 2026-06-17 | Use GitHub for state documents | Already in stack, any Claude can fetch raw URL, versioned automatically | Pasting state at start of each session |
| 2026-06-17 | Tile safety margin set at 0.125" | Standard protection for edge chipping, gives clean mold land area | 3/16" (too wide), 1/16" (too tight) |
| 2026-06-17 | Finish pass stepover set to 0.016" as test | Original 0.008" produced ~5hr run time — halving to assess surface quality tradeoff | Keep at 0.008" |
| 2026-06-17 | Store design files in Google Drive, not in app | SVG and AI files too large for app storage — app stores link only | Upload files directly to app |
| 2026-06-17 | Colorant method switched to direct-weigh with pre-wet | Stock solutions determined impractical | Stock solution system |
| 2026-06-19 | State documents moved to separate cane-creek-state repo | Clean separation between app code and session state — avoids confusion | Keep state docs in cane-creek-app |
| 2026-06-19 | glazes.json extracted from glaze_studio.html | Tile Technical Data app needs glaze data — single source of truth, no duplication | Keep hardcoded in glaze_studio.html |
| 2026-06-19 | Tile Technical Data app gets its own Claude project | App is substantial — separate from Studio Claude to keep contexts clean | Add to Studio Claude project |
| 2026-06-19 | Tile Technical Data storage: Netlify Blob primary, localStorage cache | Tile records are permanent artifacts — must survive laptop wipe | localStorage only |

---

## 16. OVERSEER INSTRUCTIONS

The Cane Creek Studio Overseer does not write application code. It thinks at the system level only.

**Responsibilities:**
- Maintain and update this system map and OVERSEER_STATE.md
- Make architectural decisions before coding begins
- Identify when a change in one app affects another
- Ensure data structures are consistent across apps
- Ensure API usage is efficient and not duplicated
- Proactively identify opportunities to improve seamlessness between apps
- Issue precise copy-paste-ready instructions to coding Claudes
- Review handoff notes and update system map accordingly

**When issuing instructions to a coding Claude:**
Include: which project/chat to use, which files to upload first, the exact change required, the data format expected, any constraints from other apps, what to include in the state document update.

**At the start of every overseer session:**
Fetch SYSTEM_MAP.md and OVERSEER_STATE.md from `cane-creek-state` using the URLs in section 5.

**At the end of every overseer session:**
Deliver updated SYSTEM_MAP.md and OVERSEER_STATE.md for Peter to upload to `cane-creek-state`.

**Model string:** Always `claude-sonnet-4-5` — no other string ever.

---

*This document is the single source of truth for system architecture. When anything changes, update here first.*
