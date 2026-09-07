# Kansallispuistot — Progress Tracker

How to use this file: check boxes as `[x]` when done, move items between
sections as things change, delete or add lines freely. This is yours to edit
directly in VS Code — nothing here is generated automatically by the app.

Last updated: 2026-09-06

---

## ✅ Done — core app

- [x] All 41 parks: name, region, blurb, badge, coordinates, official link
- [x] Real interactive map (Leaflet) with MapTiler standard + MML terrain layers
- [x] Location: nearest-park sort, native permission flow, in-app pre-permission modal
- [x] Fullscreen map view
- [x] Visit log: date, personal note, one photo per visit (compressed client-side)
- [x] Wishlist ("want to visit"), independent of visited status — shown in list + map
- [x] Achievements: 5 milestones, 8 motif-based, Four Seasons, Photographer, Planner,
      hidden "Grand Master" meta-achievement (unlocks when all others are complete)
- [x] Achievement detail popups showing which parks count toward each one
- [x] Multi-photo galleries per park (from Wikipedia), swipe + tap-to-enlarge, with
      real per-photo attribution (photographer + license)
- [x] Offline caching: map tiles (LRU-capped) + photos, manual "clear cache" option
- [x] Android back button correctly threaded through every screen (incl. lightbox,
      fullscreen map, modals)
- [x] Full FI / SV / EN localization (Finnish default)
- [x] Custom app icon, 19 unique original badge motifs (not Metsähallitus's real
      trademarked emblems — deliberate IP-safe design choice)
- [x] In-app Info screen: source credits (MapTiler, OSM, Wikimedia, Metsähallitus,
      MML), privacy policy link
- [x] Status bar / nav bar color matched to app theme
- [x] "Show more" per-park section: routes, shelters, difficulty, accessibility
      (tiered badge), GPX-availability note, "info last checked" date

## 🔧 In progress / partial

- [ ] Extended park content ("Show more"): **8 of 41 done**
      (Nuuksio, Oulanka, Koli, Repovesi, Pallas-Yllästunturi, Urho Kekkonen,
      Seitseminen, Helvetinjärvi) — 33 remaining, ongoing batch by batch
  - [ ] Next batch suggestion: Riisitunturi, Syöte, Linnansaari, Kolovesi
- [ ] luontoon.fi official links: **17 of 41 individually verified**
      (all compound/hyphenated names — highest risk of pattern breaking).
      1 real bug already found + fixed (Puurijärvi-Isosuo). 24 remaining are
      simple single-word names, lower risk but unverified.
- [ ] Play Store closed testing — running (day 7+ as of last check)
- [ ] MapTiler account: commercial-use terms + API key domain restriction —
      needs confirming in your MapTiler dashboard

## ⚠️ Legal / compliance — read before acting

- [ ] **Monetization must NOT be a bare "tip jar."** Verified against Finnish
      Ministry of Interior + Poliisihallitus sources: private individuals
      cannot get a money-collection permit for themselves under
      Rahankeräyslaki, even for something framed as a "tip" — permits are
      reserved for non-profits. **Fix**: sell an actual feature/product
      instead (this makes it ordinary commerce, not a money collection):
      - Idea: "Supporter" one-time purchase unlocking a cosmetic badge
      - Idea: premium map style / app theme
      - Idea: paid offline map pack bundle
  - [ ] Get real legal confirmation before shipping any payment feature —
        the above is well-sourced but not a substitute for actual legal advice
- [ ] Paid app (€1.99) is live in testing — remember paid→free is reversible
      anytime, free→paid is NOT (already learned this one the hard way once)

## 🐛 Known issues / needs on-device verification

- [ ] MML terrain layer: URL format + Basic Auth built correctly against the
      real capabilities doc, but never confirmed working from inside the
      actual app (only confirmed via browser login prompt) — check this
      on next device test
- [ ] Language switcher on very narrow screens (fixed once for S22-class
      widths — recheck if any other device reports it cutting off again)

## 📋 Backlog — cheap, high value (good next picks)

- [ ] Navigate button — one-tap link to Google/Apple Maps for directions
- [ ] Map filters — visited / unvisited / nearby / by region chips
- [ ] "My journey" stats view — km² explored, most-visited region, yearly recap
- [ ] Share progress as an image ("12/41 parks 🌲") — free organic marketing
- [ ] More hiking-behavior achievements (e.g. shelter-based, winter-specific)
- [ ] Social share card generator on logging a visit (photo + badge + "X/41
      completed" overlay, Instagram-Story-shaped) — bigger version of the
      plain share-progress idea above
- [ ] Dynamic seasonal challenge UI (e.g. "Ruska Challenge" — visit Lapland
      parks in September) — reuses existing visit-date + achievement system

## 📋 Backlog — bigger, real work, sequence deliberately

- [ ] Multiple visits per park (Nuuksio 2024, 2025, ... each with own
      date/note/photo) — **on hold, paired with:**
- [ ] Multiple photos per visit — **on hold**, same reason (both need a real
      data-model change: visit history array instead of one slot per park)
- [ ] Photo storage upgrade (move off current storage toward IndexedDB or
      native Filesystem) — becomes more urgent once the above two ship
- [ ] Structured route objects (name/length/difficulty as real fields, not
      one text paragraph) — deferred until something actually needs to query
      routes individually (e.g. drawing one on the map, filtering by length)
- [ ] Explicit "Download park for offline" button — pre-fetch a park's full
      tile bounding box at set zoom levels, instead of relying on the user
      having already panned over the area. Real value for spotty-signal
      parks (Lemmenjoki, UKK, etc.)
- [ ] Tiered accessibility system to match luontoon.fi's actual grading
      (already have a basic 3-tier version; luontoon.fi's is more granular)

## 🗺️ Backlog — long-term / separate projects

- [ ] LIPAS integration — real structured trail geometry (actual coordinate
      paths), CC BY 4.0 licensed, genuinely commercial-use-friendly
- [ ] GPX route rendering on the map (Metsähallitus provides open GPX per
      trail) — natural payoff of the LIPAS work above; turns the app from a
      tracker into a real navigation aid
- [ ] Light navigation (live position shown against a real trail line) —
      the actual reward once GPX/LIPAS trail lines exist on the map
- [ ] "Plan a trip for me" recommendation engine — needs much richer
      per-park tag data (difficulty, features, dog-friendly, etc.) across
      all 41 parks first; premature until content coverage is deeper

## 🚫 Discarded / deliberately out of scope

- [ ] GPS hike recording (live distance/pace/elevation tracking) — needs
      special Android background-location permission + real engineering;
      more like building a different app. Not pursuing.
- [ ] Splitting data/components into separate files/folders — reasonable
      for a team codebase, unnecessary complexity for a solo dev's static
      41-park dataset. Current single-file structure is fine as-is.
- [ ] Pre-curated fixed photo database (vs. today's live Wikipedia fetch) —
      solved the same problem (attribution) a much cheaper way already;
      only revisit if live attribution turns out insufficient in practice

## 💡 Ideas mentioned but not yet decided on

- [ ] Premium cosmetic map styles / exclusive themes (ties into the
      monetization fix above)
- [ ] Gold-leaf "Supporter Badge" next to username (also ties into
      monetization — note: app currently has no concept of a username/
      profile at all, so this implies adding one)
