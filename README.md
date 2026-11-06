# Pawfolio — Demo

The cut-down demo of Pawfolio, linked from the Etsy listing so prospective buyers can try it before purchase.

**Live demo URL:** https://cleartrackapps.com/pet-care-planner-demo/
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
- **Sitter mode / Send to a sitter** (mirrors app v3.40.0) run against a local fake inbox (`pawfolioDemoInbox` in demo storage). `window.PAWFOLIO_INTAKE_FN_URL` is set to `demo-offline:pawfolio-sitter-inbox` and `PawfolioIntake.register/lookupCode/submit/list/ack` are replaced before use, so nothing goes to Supabase. Encryption is real. Sample sitter Happy Tails Pet Sitting, code `WAGS-2468`; sample clients Maya Chen and Jordan Lee (Jordan arrives as a new form when Sitter mode is turned on). Client card **Print** disabled.
- **Live dose link in Sitter mode** (mirrors app v3.41.0): sample client Maya Chen's latest form carries a `doseShare`, so her card shows a **Today's doses** button and a **Doses** badge in Clients. In the demo the button shows a labeled demo note (and can open the Medications dose-sharing preview); it never opens the sample URL, so nothing goes to Supabase. On the client side, Send to a sitter's review shows the Pawfolio Complete "Set up dose sharing" path with a demo note and never sends a `doseShare`.
- **Addresses and directions** (mirrors app v3.41.0): sample clients have clearly fake addresses (Maya Chen, 1234 Sample Willow Ln, Granbury, TX; Jordan Lee, 5678 Example Cedar Ct, Granbury, TX), shown on one line in Clients and matched by search. Client cards show Call, Text, Directions (Apple Maps on iPhone/iPad, Google Maps elsewhere). Pet Sitter Info has a Home address field; the sample owner Sam Rivera's is 1208 Pecan Hollow Dr, Granbury, TX 76048, and it prefills Send to a sitter.
- **Clients map** (mirrors app v3.42.0): Clients > **Map** shows sample clients as pins around Granbury, TX, with Open client, Directions, Move pin, a "No address yet" list, and Plan a route (Apple Maps on iPhone/iPad iOS 18.4+ with a Google Maps fallback, Google Maps elsewhere). Leaflet is vendored in `vendor/leaflet/` (no CDN) and loads only when the map opens; tiles are OpenStreetMap. Extra sample clients: Priya Patel (42 Sample Harbor Dr), Ben Ortiz (77 Example Ranch Rd) and Casey Morgan (no address). Sample addresses have preset spots (`DEMO_GEO`), so no geocoding request is sent for them; any other address goes through the same OpenStreetMap Nominatim lookup as the app. Moved pins reset on refresh like all demo data. The map sits between the demo banner and buy bar.
- **Separate clients on shared devices** (mirrors app v3.42.1): a form only updates a client when the clientId and the owner name both match, so two people sending from the same browser get two cards. On a client card, a previous version has **Make this a separate client** (with a confirm), which moves it into its own client card. Try it on Maya Chen's earlier version. Like all demo data, it resets on refresh.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The demo page |
| `icon-192.png`, `icon-512.png` | Paw logo (same as full app) |
| `intake-crypto.js` | Sitter intake encryption, byte-identical copy of the app's file (do not edit here) |

## Releasing a new demo version

1. Bump `<meta name="app-version" content="X.X.X">` (line 9)
2. Make your changes — keep all 10 restrictions intact
3. Commit to `main`

GitHub Pages auto-deploys from `main`. Live demo updates ~1 minute after pushing.
