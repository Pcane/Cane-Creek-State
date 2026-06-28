# GLAZE_STATE.md -- Cane Creek Glaze Studio
**Last updated:** 2026-06-28
**Session:** June 28 morning -- firing review, new recipes, major app updates
**Owner:** Glaze Studio Claude

---

## SESSION START CHECKLIST

1. Read this file
2. Read SYSTEM_HEALTH.md from the Cane Creek Studio folder
3. Read the most recently modified COMM_STRUCTURE file
4. Read NOTEBOOK_GLAZE.md
5. Fetch MESSAGES.json: https://raw.githubusercontent.com/Pcane/Cane-Creek-State/main/MESSAGES.json
6. Fetch DATA_INDEX.json: https://raw.githubusercontent.com/Pcane/Cane-Creek-State/main/DATA_INDEX.json
7. Fetch GLAZE_APP_DATA.md: https://raw.githubusercontent.com/Pcane/Cane-Creek-State/main/GLAZE_APP_DATA.md
8. Check for pending messages addressed to glaze-claude before asking Peter what to work on

---

## WHAT HAPPENED THIS SESSION -- 2026-06-28 (morning)

### Firing Review Completed
All June 26 results reviewed with tile photos. Key findings:
- G30 Cobalt Blue -- good result, application shadow visible (hand-hold during pour). Rutile effect subtle at 1% -- direction is good, needs more rutile.
- G38 Orange -- right side (straight gloss) gave rich warm golden-orange. Left side (50/50 matte/gloss) gave muted olive-grey. Rutile needs gloss base to develop.
- G29 Vanadium Yellow -- muted olive-yellow, one coat thin, double pour better. Iron edge effect at 0.25% RIO not visible.
- G40 Cobalt+Manganese direction -- DROPPED. Manganese is hazardous (neurotoxic) and never produces purple in oxidation at cone 6. Not worth the risk.

### New Recipes Created This Session
- **G30v2** -- Cobalt Blue doubled rutile: Cobalt Oxide 2.424g + Light Rutile 12.12g. Based on G30.
- **G30v3** -- Transparent Blue Wash: Cobalt Oxide 2.424g + Light Rutile 6.06g. SG 1.33. Based on G30.
- **G30v4** -- Transparent Medium Blue: Cobalt Oxide 2.424g + Light Rutile 6.06g. SG 1.36. Based on G30.
- **G30v5** -- Dark Blue: Cobalt Oxide 2.424g + Light Rutile 6.06g. SG 1.38. Based on G30.
- **TG5** -- Cobalt + Iron: Cobalt Oxide 2.424g + RIO 4.85g (0.8%). Based on G30.
- **TG8** -- Rutile Amber: Light Rutile 19.392g + RIO 6.06g (1%). Based on G38.
- **G29v2** -- Vanadium Yellow + Iron Edge: Vanadium Yellow 14.544g + RIO 4.545g (0.75%). Based on G29.
- **G25v2** -- Chrome-Tin Cranberry Red doubled chrome: Chrome Oxide 0.727g + Tin Oxide 25.2g. Based on G25.
- **G38v2** -- Orange Satin: Light Rutile 19.392g, 50/50 G2926B/matte base mix. Based on G38.

### Retired/Dropped This Session
- G12 -- retired (superseded by G29)
- Manganese dropped from all future recipes -- hazardous, not useful in cone 6 oxidation
- G35 -- retired (too commercial)

### App Updates Deployed (Two Builds)
**Build 1 (last night):**
- Bench card: name large font, base label large font, target SG displayed
- Rename button in lifecycle bar
- Expectations moved to Mix Record Step 1, removed from Kiln Load Step 2
- Edit and Delete buttons on firing history records

**Build 2 (this morning):**
- Base mix: new glaze modal supports 50/50 or any % split between two bases. Bench card shows split mL amounts.
- CMC% and Darvan drops per 600g added as recipe fields -- show on bench card
- CMC stock addition calculator: tells you grams of 10% CMC stock to add when raising CMC%, scaled to batch size
- Warning and Notes fields REMOVED -- replaced with Intent field (single text) + structured intended attributes
- Intended attributes: finish, transparency, primary color, secondary color, light application color, heavy application color, effects (checkboxes)
- Firing results fully structured: color dropdowns (primary + secondary), defects checkboxes, observed effects checkboxes, result notes field removed
- Photo URL placeholder updated to Cloudinary format

### Image Workflow Established
- Cloudinary account: cloud name dmnkvz4k8
- Direct URL format: https://res.cloudinary.com/dmnkvz4k8/image/upload/[version]/[filename]
- Cloudinary domain blocked in Claude bash sandbox -- cannot fetch directly
- Workflow: paste images directly into chat for review; store Cloudinary URL in firing record Photo URL field
- GitHub images folder created in cane-creek-app repo (private repo -- raw URLs not publicly accessible)

### Cobalt Number Correction
- App shows Cobalt Oxide 2.424g for G30 -- THIS IS THE CORRECT NUMBER
- Earlier session notes suggesting 3.27g were wrong -- disregard
- All G30 variants use 2.424g Cobalt Oxide

### Key Design Decisions
- Structured data everywhere -- no free text notes fields in firing records
- SG variants replace coat-count variants -- G30v3/v4/v5 are same recipe at different SG targets
- CMC% and Darvan are permanent recipe fields, set empirically then recorded
- Manganese permanently dropped from studio palette -- hazardous
- 50/50 base mix is a recipe property, not an application note -- G38v2 is a separate recipe
- Color palette confirmed: Black, Dark Brown, Brown, Amber, Honey Gold, Orange, Cream, White, Off-White, Olive, Dark Green, Green, Teal, Sky Blue, Cobalt Blue, Pink, Red, Grey, Clear

---

## APP ARCHITECTURE -- CRITICAL REFERENCE

**glaze_studio.html data flow:**
- Blob (Netlify) = live working data. Primary read/write for all glaze operations.
- ./glazes.json (Netlify static) = seed file only.
- GLAZE_APP_DATA.md -> Cane-Creek-State = auto-written on every app load. Primary session-start read.
- glazes.json -> Cane-Creek-State = structured cross-Claude data layer. Not read by app.
- bases.json -> Cane-Creek-State = same.

**JS constraint -- CRITICAL:**
Pure ASCII only in JS. No template literals with ${}. No unicode in script block.
Use createElement/appendChild for complex HTML. Prevents GitHub upload corruption.

**Push tool workflow:**
No direct GitHub write from Claude sessions. Use one-page HTML push tool reading PAT from localStorage.getItem('github_pat').

---

## CURRENT GLAZE STATUS

**Active (6):** G11 Trans Dark Green, G16 White, G21 Trans Earthy Brown, G25 Chrome-Tin Cranberry Red, G26 Sky Blue, G38 Orange

**Test (existing):** G29 Vanadium Yellow + Iron Edge, G30 Cobalt Blue + Rutile Break

**Test (new -- not yet fired):**
- TG1/G40v2 -- Iron Black revised (RIO 39.4g + Rutile 3.03g)
- TG2/G44 -- Honey Amber (Rutile 12.12g + RIO 6.06g)
- TG3/G45 -- Olive Brown (RIO 18.18g + Chrome 1.818g)
- TG4/G46 -- Copper Blue-Green (Copper Carb 3.636g + RIO 3.03g)
- TG5 -- Cobalt + Iron (Cobalt Oxide 2.424g + RIO 4.85g)
- TG8 -- Rutile Amber (Rutile 19.392g + RIO 6.06g)
- G25v2 -- Chrome-Tin doubled chrome (Chrome 0.727g + Tin 25.2g)
- G29v2 -- Vanadium Yellow + 0.75% RIO
- G30v2 -- Cobalt doubled rutile (Cobalt 2.424g + Rutile 12.12g)
- G30v3 -- Transparent Blue Wash SG 1.33
- G30v4 -- Transparent Medium Blue SG 1.36
- G30v5 -- Dark Blue SG 1.38
- G38v2 -- Orange Satin (50/50 gloss/matte)

**Suspended:** G12 (retiring), G24, G25HC

**Base slurry G2926B-001:** SG 1.39, f=0.5967, mixed June 24

**Colorant note:** All recipes calibrated to Spanish Red Iron Oxide -- studio standard.

---

## PENDING

1. Enter G30 firing results in app (tile exists, results not logged)
2. Enter all new recipes from this session into app
3. Retire G12 in app
4. Fix G25/G25HC base_id if still showing G2926B
5. Test syringe protocol: SG 1.35-1.36, Darvan 3-4 drops, CMC 0.25% -- start G11 or G21
6. Fire all new TG series glazes
7. NOTEBOOK_GLAZE.md Chapter 6 -- User 3 Seg 1 HLD 00.00 -> 00.10 still pending
8. Bring G2926B to target SG 1.35, record final water total for true working f factor
9. TiO2 acquisition -- unblocks G43 celadon
10. Nickel oxide acquisition -- for sage/olive greens direction
11. Update glazes.json in Cane-Creek-State with all new recipes

---

## WATCH LIST

1. G2926B not at target SG -- stock at 1.39, not 1.35. Peter dilutes at colorant mixing stage.
2. f factor empirical at SG 1.39 = 0.5967. True working f at SG 1.35 not established.
3. G25 color development -- needs two coats or more colorant. If grey/washed, boron level is cause.
4. Water calculation gap -- colorant dry mass not factored in. Monitor.

---

## PALETTE DEVELOPMENT PLAN

**Confirmed working:**
- G11 Dark Green, G16 White, G21 Earthy Brown, G38 Orange

**Pending fire:**
- Blues: G30v2-v5, TG5 (cobalt + iron direction)
- Amber/honey: TG2/G44, TG8
- Olive/brown: TG3/G45
- Copper blue-green: TG4/G46
- Chrome-tin red: G25v2
- Yellow: G29v2
- Orange satin: G38v2

**Gaps remaining:**
- Mid sage/olive greens -- nickel oxide direction identified, not yet purchased
- True Arts and Crafts blue -- cobalt tests pending
- Matte and satin series -- after gloss palette complete

---

## KEY DECISIONS -- PERMANENT

- Any recipe or application change creates a new version (G35v2 format, no exceptions)
- Firing-first workflow: one glaze record = one physical tile = one firing
- Mislabeling risk: food coloring in base slurry batches is permanent ID protocol
- GitHub web UI corrupts JS template literals -- all JS must be pure ASCII
- Google Drive MCP has no update/overwrite -- create new file each session, read most recently modified
- GLAZE_APP_DATA.md written by app to Cane-Creek-State on every load -- fetch at session start
- Blob is live data store -- glazes.json in Cane-Creek-State is structured data layer copy only
- Spanish Red Iron Oxide is studio standard -- all recipes calibrated to it
- Syringe glazes: SG 1.35-1.36, Darvan 3-4 drops per 600g, CMC 0.25%
- Rutile alone gives orange/peach -- needs RIO to push toward amber
- Manganese PERMANENTLY DROPPED -- neurotoxic, not useful in cone 6 oxidation
- Chrome + iron in equal proportions = muddy -- use one as dominant, one as trace modifier
- Cobalt Oxide for G30 series is 2.424g per 600g -- confirmed correct app number
- CMC stock solution is 10% (100g CMC per 1000g water)
- Cloudinary cloud name: dmnkvz4k8
- Color palette: Black, Dark Brown, Brown, Amber, Honey Gold, Orange, Cream, White, Off-White, Olive, Dark Green, Green, Teal, Sky Blue, Cobalt Blue, Pink, Red, Grey, Clear
- SG variants replace coat-count variants for shelf inventory
- CMC% and Darvan drops are permanent recipe fields set empirically
