# Pawfolio — Demo

The cut-down demo of Pawfolio, linked from the Etsy listing so prospective buyers can try it before purchase.

**Live demo URL:** https://rapunzlnflt-afk.github.io/pet-care-planner-demo/
**Full app repo:** https://github.com/rapunzlnflt-afk/pet-care-planner

## This repo is NOT auto-synced with the full app

The full Pawfolio app lives in a separate repo (`pet-care-planner`). The two are independent — committing to one does NOT update the other.

**If you change a feature, color, font, or layout in the full app and want it in the demo too, you must commit it here separately.** Always keep the demo's restrictions intact (see below).

## Demo restrictions (preserve all of these)

These differentiate the demo from the paid full version:

- `DEMO_MODE = true` flag at the top of the inline script
- Green demo banner at the top with "Get the Full Version →" CTA linking to Etsy
- `localStorage.clear()` runs on every page load (data resets on refresh)
- **Export** button disabled
- **Import** button replaced with a disabled label (and the JS listener uses `?.addEventListener` so it doesn't crash on the missing input)
- **Check for updates** button disabled
- **Print / Export** sitter sheet button disabled (both main and preview)
- Backup-reminder "Export now" button disabled
- Service worker registration skipped
- Silent daily update check skipped

## Files

| File | Purpose |
|------|---------|
| `index.html` | The demo page |
| `icon-192.png`, `icon-512.png` | Paw logo (same as full app) |

## Releasing a new demo version

1. Bump `<meta name="app-version" content="X.X.X">` (line 9)
2. Make your changes — keep all 10 restrictions intact
3. Commit to `main`

GitHub Pages auto-deploys from `main`. Live demo updates ~1 minute after pushing.
