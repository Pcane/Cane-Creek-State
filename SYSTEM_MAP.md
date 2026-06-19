# Cane Creek Studio — System Map
**Last updated:** 2026-06-18  
**Updated by:** Overseer  
**Version:** 1.2

---

## HOW TO START A NEW OVERSEER SESSION

Fetch this document:
`https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/SYSTEM_MAP.md`

Then fetch the overseer state:
`https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/OVERSEER_STATE.md`

Confirm you are up to speed before proceeding.

---

## 1. SYSTEM OVERVIEW

Cane Creek Tile Co. is a sole-maker handmade ceramic raised-line art tile studio in Alamance County, NC. Peter Cane is the sole maker — every tile made by one pair of hands, start to finish. Suzie Cane handles billing and administration. Pre-launch, targeting architects and interior designers. Direct sales only, no wholesale.

The digital suite consists of two GitHub repos, two Netlify deployments, and a set of HTML/JS apps. All apps are single-file HTML with embedded CSS and JS. No build step. No framework. Vanilla JS only.

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
| `tile_record.html` | Tile lab notebook — not yet built | Pending |
| `glazes.json` | Shared glaze library — not yet extracted | Pending |
| `netlify/functions` | Serverless functions | Live |
| `netlify.toml` | Netlify configuration | Live |
| `manifest.json` | PWA manifest | Live |
| `sw.js` | Service worker | Live |
| `README.md` | Repo documentation | Live |
| `SYSTEM_MAP.md` | This file | Live |
| `OVERSEER_STATE.md` | Overseer session state | Live |
| `MARKETING_STATE.md` | Marketing Claude session state | Live |
| `GLAZE_STATE.md` | Glaze Studio Claude session state | Live |
| `STUDIO_STATE.md` | Studio tools Claude session state | Live |

### `Pcane/cane-creek-website` (private)
**Live at:** thehandmadetile.com  
**Purpose:** Public-facing marketing website  
**Auto-deploys:** Yes, from main branch via Netlify

| File | Purpose | Status |
|------|---------|--------|
| `index.html` | Homepage | Live, content pending update |
| `WEBSITE_STATE.md` | Website Claude session state | Pending creation |

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
2. Peter runs `perl patch_vX_X.pl app.js` in Terminal from `~/Downloads/cane-creek-patch/`
3. Peter uploads patched file AND updated state document to GitHub in same commit
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
- Update changelog header in app.js every session
- Update state document every session — this is not optional

---

## 5. STATE DOCUMENTS — HOW THEY WORK

Each project has its own state document in GitHub. When a conversation gets long or a new Claude starts, it fetches the state document and picks up exactly where the last session left off.

| Document | Project | Fetch URL |
|----------|---------|-----------|
| `SYSTEM_MAP.md` | Overseer | `https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/SYSTEM_MAP.md` |
| `OVERSEER_STATE.md` | Overseer | `https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/OVERSEER_STATE.md` |
| `MARKETING_STATE.md` | Marketing | `https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/MARKETING_STATE.md` |
| `GLAZE_STATE.md` | Glaze Studio | `https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/GLAZE_STATE.md` |
| `STUDIO_STATE.md` | Studio tools | `https://raw.githubusercontent.com/Pcane/Cane-Creek-State/refs/heads/main/STUDIO_STATE.md` |
| `WEBSITE_STATE.md` | Website | `https://raw.githubusercontent.com/Pcane/cane-creek-website/refs/heads/main/WEBSITE_STATE.md` |

**At the end of every session** the coding Claude delivers:
- Patched code file(s)
- Updated state document

Peter uploads both to GitHub in the same commit.

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
Glazes G25–G43 established. Full nomenclature system: OX/MX/MS/HC.

**Data location:** Currently hardcoded as `GLAZES` array in `glaze_studio.html`.

**Pending architectural decision:** Extract `GLAZES` array to shared `glazes.json` in repo root. Both `glaze_studio.html` and the tile record app read from this single source. M-series (matte) glazes added later — shared file handles this cleanly. **This must happen before tile record app glaze integration is built.**

**Glazing method:** Wax all backs → water submersion → bulb-apply colors into recesses → fast clear dip.

---

## 9. APP MAP

### Business App (`index.html` + `app.js`)
**Purpose:** CRM, billing, marketing, production tracking  
**Data:** localStorage + Netlify Blob  
**Model:** `claude-sonnet-4-5` always  
**Current version:** v8.12  
**Managed by:** Cane Creek Marketing project  
**State document:** `MARKETING_STATE.md`

### Glaze Studio (`glaze_studio.html`)
**Purpose:** Glaze calculation, session tracking, G-series library  
**Data:** localStorage + Netlify Blob  
**Pending:** Glaze session feedback/journal tab  
**Pending:** Extract GLAZES to glazes.json  
**State document:** `GLAZE_STATE.md`

### Fireplace Designer (`design_v2.html`)
**Purpose:** Fireplace surround tile layout calculator  
**Data:** localStorage  
**Status:** Stable, 36-test debug suite passing  

### Pattern Studio (`pattern.html`)
**Purpose:** Tile pattern generator with SVG export  
**Data:** localStorage  
**Pending Stage 2:** Seed import, transform stack, overlap modes, validation, recipe library  
**Blocker:** Confirm Illustrator SVG export flavor before Stage 2  
**State document:** `STUDIO_STATE.md`

### Hub (`hub.html`)
**Purpose:** Studio tools launcher  
**Pending:** Add Pattern Studio card  

### Public Website (`index.html` in cane-creek-website)
**Purpose:** Public marketing site  
**Status:** Live, content pending full update  
**Pending:** Formspree contact form, inner pages  
**State document:** `WEBSITE_STATE.md` (pending creation)

### Tile Record App (`tile_record.html`) — NOT YET BUILT
**Purpose:** Complete lifecycle lab notebook for every tile from design intent through fired result. Serves both as production record and experimental notebook. Primary navigation is by tile, not by process or version tree.  
**Data:** localStorage + Netlity Blob (records and small files); Google Drive links (large files)  
**Blocker:** glazes.json must exist first  
**Build order:** Stage 1 first — do not attempt full build in one session  
**State document:** `TILE_RECORD_STATE.md` (created when app is built)

#### TILE RECORD APP — FULL SPEC

##### UI Layout — Three Screens

**Screen 1 — Dashboard (Today view)**
- Top section: current active standards at a glance — current line spec, active CNC profiles, current clay body. Flags recent changes.
- Below: tile records grid/list, most recent first. Each card shows tile ID, design name, date, tile type, status, thumbnail if photo exists.
- Filter bar: filter by status, glaze, size, tile type, date range, customer.

**Screen 2 — Tile Record (This Tile view)**
- Single tile, all eleven process layers flat on one scrollable page.
- Collapsible sections per layer. Key parameters visible collapsed, full detail on expand.
- Top: tile ID, design name, tile type, status, date, intent (what you were trying to achieve).
- File attachments inline: SVG, G-code files, in-process photos accessible directly. Drive links for AI source and R5 final photos.
- Bottom: result section — photos, outcome notes, rating, what to change next time.
- Required fields enforced — cannot mark tile complete without them.
- Print button generates clean one-page summary.

**Screen 3 — Compare view**
- Select two tiles or two profile versions.
- Side by side. Parameters highlighted where they differ. Results shown below each column.
- **Build last — most complex view.**

##### Data Layers — Eleven Process Layers Per Tile Record

**1. Identity**
- Tile ID (auto-generated, e.g. T001)
- Date created
- Tile type: square field tile / art tile / liner / border / corner / other
- Status: experiment / production / retired
- Customer reference (optional — links to customer ID in business app)
- Design name
- Illustrator source file link (Google Drive)
- What you were trying to achieve (required)

**2. Mold**
- Mold ID
- Shape: square / rectangle / other
- Green face size
- Pocket depth
- Safety margin
- Mold generation / version number

**3. Size**
- Target fired face size
- Target fired thickness
- Shrinkage factor used
- Actual measured fired face size
- Actual measured fired thickness
- Actual shrinkage (calculated from measured values)
- Notes on size deviation

**4. CNC Pass 1 — Roughing**
- Profile reference (e.g. "CNC-Pass1-6x6-v2") — must be size-tagged
- Any deviations from profile (free text)
- Notes

**5. CNC Pass 2 — Finish**
- Profile reference — must be size-tagged
- Any deviations from profile
- Notes

**6. CNC Pass 3 — Line Grooves**
- Profile reference — must be size-tagged
- Target line depth
- Actual measured line height post-cut
- Actual measured line base width post-cut
- Any deviations from profile
- Notes

**7. Clay**
- Clay body
- Green slab thickness
- Pressing method
- Green face size measured (confirm matches mold)

**8. Drying**
- Duration
- Conditions
- Notes

**9. Bisque Firing**
- Date
- Cone
- Schedule used (references firing profile)
- Kiln position
- Notes / result

**10. Glazing — repeated per glaze applied**
- Glaze ID + version (pulled from glazes.json)
- Actual SG on application day
- Bisque pre-wet: yes/no, duration in seconds
- Application method: dip / pour / spray / brush / bulb
- Coat count
- Sequence order (1st, 2nd, 3rd applied)
- Notes

**11. Glaze Firing**
- Date
- Cone
- Schedule used (references firing profile)
- Kiln position
- Notes

**12. Result**
- In-process photos (phone snaps, stored in Netlify Blob)
- Final photos (Canon R5, Google Drive link)
- What actually happened (required)
- Rating: keeper / experiment / retire (required)
- What you would change next time (required)
- Recipe or profile change triggered: yes / no — if yes, note which profile and new version number

##### File Storage Per Tile Record

| File | Size | Storage | Notes |
|------|------|---------|-------|
| Illustrator source (.ai) | Large | Google Drive | Link stored in tile record |
| SVG for Carvco | Small | Netlify Blob | Uploaded directly into tile record |
| G-code Pass 1 (.nc) | Tiny | Netlify Blob | Uploaded directly into tile record |
| G-code Pass 2 (.nc) | Tiny | Netlify Blob | Uploaded directly into tile record |
| G-code Pass 3 (.nc) | Tiny | Netlify Blob | Uploaded directly into tile record |
| In-process photos | Medium | Netlify Blob | Uploaded directly into tile record |
| Final photos (R5) | Large | Google Drive | Link stored in tile record |

Carvco project files are ephemeral — not stored. G-code is the permanent CNC record.

##### Versioned Process Profiles

CNC parameters, firing schedules are captured as versioned profiles — not re-entered per tile. Each CNC profile is size-tagged. Profiles live in localStorage + Blob alongside tile records.

Profile naming convention: `[type]-[size]-v[n]`
Examples: `CNC-Pass1-6x6-v1`, `CNC-Pass3-4x4-v2`, `Bisque-v1`, `GlazeFire-v1`

When a profile changes:
- Old version retired with required reason field and date
- New version created and becomes active
- Every tile record references the specific profile version used at time of making
- Compare view can show tiles made with v1 vs v2 side by side

Profile types:
- CNC Pass 1 (size-tagged)
- CNC Pass 2 (size-tagged)
- CNC Pass 3 / line spec (size-tagged)
- Bisque firing schedule
- Glaze firing schedule

##### Navigation Views

1. **Today** — current active profile versions for every process, current active glazes. What you are working with right now. Recent changes flagged.
2. **This Tile** — complete flat record for one tile. Every layer, every parameter, every result. Printable one-page summary.
3. **Compare** — select two tiles or two profile versions, see results side by side with differences highlighted. Build this last.

##### Integration Points
- Reads `glazes.json` for active glaze library — read only, never writes to glazes.json
- Links to Google Drive for Illustrator source files and R5 final photos
- Links to Pattern Studio seeds (pending Pattern Studio Stage 2)
- Customer reference field links to customer ID in business app CRM — optional, neither app breaks if empty
- Business app order records may reference tile ID — connection is optional in both directions

##### Build Stages — Do Not Deviate From This Order

**Stage 1 — Core record (build first)**
Identity, Mold, Size, Result fields only. Get data entry, storage, and retrieval working. Dashboard view with tile cards. No file uploads yet. No CNC layers yet. No glaze integration yet.
Confirm Stage 1 is working before proceeding.

**Stage 2 — CNC and clay layers**
Add process layers 4–8 (CNC passes, clay, drying, bisque). Add versioned process profiles. Add profile reference fields to tile record.
Confirm Stage 2 before proceeding.

**Stage 3 — Glaze integration**
Add glazing layer (layer 10). Pull active glazes from glazes.json. Add glaze firing layer (layer 11).
Requires glazes.json to exist first — hard blocker.
Confirm Stage 3 before proceeding.

**Stage 4 — File storage**
Add SVG and G-code upload to Netlify Blob. Add in-process photo upload. Add Drive link fields for large files.
Test Blob upload behavior carefully — known throttling risk at scale.
Confirm Stage 4 before proceeding.

**Stage 5 — Compare view**
Build compare view last. Most complex. Two-tile and two-profile comparison with diff highlighting.

---

## 10. DATA OWNERSHIP

| Data | Owner | Location | Shared with |
|------|-------|----------|-------------|
| Prospect records | app.js | localStorage + Blob | Nothing yet |
| Glaze library | glaze_studio.html → glazes.json | localStorage + Blob → repo root | Tile record app (read only) |
| Glaze sessions / mix log | glaze_studio.html | localStorage + Blob | Nothing |
| Tile records | tile_record.html | localStorage + Blob | Business app (customer ref, read only) |
| Process profiles | tile_record.html | localStorage + Blob | Nothing |
| CNC standards | SYSTEM_MAP.md | GitHub | All apps (read only) |
| Tile standards | SYSTEM_MAP.md | GitHub | All apps (read only) |
| Design files (.ai, R5 photos) | Google Drive | Drive | Tile record app links to them |
| SVG + G-code files | tile_record.html | Netlify Blob | Nothing |
| Pattern seeds | pattern.html | localStorage | Tile record app (pending) |

---

## 11. PENDING ARCHITECTURAL DECISIONS

| Decision | Priority | Notes |
|----------|----------|-------|
| Extract GLAZES to glazes.json | High | Blocks tile record app Stage 3 glaze integration |
| Tile record app Stage 1 build | High | After glazes.json extraction — see build stages above |
| Netlify Blob file upload proof of concept | High | Test before Stage 4 — known throttling risk |
| Pattern Studio Stage 2 | Medium | Confirm Illustrator SVG flavor first |
| Standardize date format across all apps | Medium | Use ISO 8601 everywhere |
| Pattern Studio card in hub.html | Low | Simple add, low effort |
| Glaze journal tab in glaze_studio | Medium | Build after firing assessment |
| Website inner pages | Medium | Fireplaces, Backsplash, Dados, About, How It's Made |
| Formspree contact form on website | Low | Wire when content is ready |

---

## 12. KNOWN TECHNICAL DEBT

| Item | Location | Priority |
|------|----------|----------|
| GLAZES array hardcoded in glaze_studio.html | glaze_studio.html | High |
| Pattern Studio card missing from hub.html | hub.html | Low |
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
| Never build tile record app all at once | Too complex — follow the five stage build order in section 9 |
| Never build tile record Stage 3 without glazes.json existing | Hard dependency — glaze integration will not work without it |

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
| 2026-06-18 | Tile record app framed as experimental lab notebook, not just production record | Peter is still in discovery phase — system must serve experimentation first, production second | Production-only record |
| 2026-06-18 | CNC process profiles versioned and size-tagged | Different tile sizes need different CNC parameters — profiles must be size-specific | Single profile per pass type |
| 2026-06-18 | G-code stored in Netlify Blob, Carvco files discarded | G-code is ground truth of what machine ran — Carvco files are ephemeral tooling, not archive | Store Carvco project files |
| 2026-06-18 | SVG stored in Netlify Blob, not Google Drive | Small file, needs to be directly in tile record for reliability — Drive links can rot | Drive link only |
| 2026-06-18 | Large files (AI source, R5 photos) stay in Google Drive with links | Too large for Blob — Drive handles large files cleanly | Upload everything to Blob |
| 2026-06-18 | Tile record built in five stages | Too complex to build at once — staged build is testable and lower risk | Single build session |
| 2026-06-18 | Business app and tile record connected via optional customer reference | Tiles sold to customers need reproducibility lookup — connection must be optional so neither app breaks without the other | Tight coupling between apps |

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
Fetch this document and OVERSEER_STATE.md from GitHub raw URLs above.

**At the end of every overseer session:**
Deliver updated SYSTEM_MAP.md and OVERSEER_STATE.md for Peter to upload to GitHub.

**Model string:** Always `claude-sonnet-4-5` — no other string ever.

---

*This document is the single source of truth for system architecture. When anything changes, update here first.*
