# MARKETING_STATE.md — Cane Creek Business App

Last updated: June 2026 — founding document

## Current version
app.js: v8.12 (confirmed running via console test)
index.html: current — shell with PIN login for Peter and Suzie

## What the app is
Full business operating system at cane-creek-app.netlify.app. Ten sections: Dashboard (with P&L), Billing, Customers, Quotes, Production, Tile Catalog, Marketing, Email, Reports, Studio. PIN login. Section locking prevents Peter and Suzie editing the same section simultaneously. Data stored in localStorage and Netlify blob storage.

## Critical architecture — do not change
- Apollo owns all contact data. Claude owns fit assessment only.
- re-assess NEVER writes contacts. This was the core bug fixed in v8.7–v8.12.
- Franchise blocklist in place — Case Design and similar national chains blocked from AI
- Model string: claude-sonnet-4-5 — never change this
- Patch workflow: perl patch → upload app.js to GitHub → run JS test in browser console → upload JSON → only then re-assess

## Prospect data state
- 496 fabricated contacts removed in v8.7–v8.12 cleanup
- 48 Chrysalis Award winners imported as prospects
- 86 incorrectly mapped Apollo category values fixed
- Apollo CSV import: still needs auto-map patch for industry categories
- Cleanup pipeline: still marks newly imported records as Not a Fit before research — needs fix

## Test workflow
Test script saved as test_research.js in ~/Downloads/cane-creek-patch/
15-company test. Specific checks:
- Garman Homes: must still have Chip Garman (not Ryan/Denise)
- Absolute Construction: must still have Nelu Skumpija (not Brandon/Britt)
- Mountain Kitchen: must still have Cindy McGowan (not Sarah)
- Case Design: must return Not a Fit (blocklist)
- Dunning: must have no contacts added

## Pending work
- Apollo CSV import auto-map for industry categories
- Fix cleanup pipeline not marking new imports as Not a Fit before research
- Email tab (Microsoft Graph) — integration status unknown, needs verification
- P&L dashboard — confirm all metrics pulling live from billing/expense data

## Glaze/studio data
- Glaze data lives in glaze_studio.html not in this app
- Studio tab has: notebook, inventory, kiln log, expenses, app settings
- No integration with glaze_studio.html yet — deferred
