/
Review full current state before giving next-steps guidance

Before answering, I spotted a real issue in the tracker itself — my last edit accidentally left the old, vague "Trip prep tips" entry sitting right below the new fully-specced one, creating a duplicate. Let me clean that up first, then check the truncated middle section:
Edited a file, read a file

Good, that's the full accurate picture now — file's clean. Here's where things actually stand:
Multiple visits per park — bigger than it looks, worth doing right

This has been sitting "on hold" deliberately, and I'd keep it that way for one more round, not because it's not wanted — because three other things all converge on it and doing them together is genuinely better than bolting them on one at a time:

    Multiple photos per visit — same underlying limitation (one slot per park)
    Richer trip details (named route, duration, 1–5 rating) — you asked about this a few messages back; it only makes sense once a visit is its own record, not a single overwritable slot
    Photo storage — already flagged as "becomes urgent" once this ships, since photos now show up in three places (Explore cards, Home, park detail)

This is a real data-model change — log[parkId] = {date, note, photo} becomes log[parkId] = [{date, note, photo}, {date, note, photo}, ...] — which touches the visit form, every place that reads "your visit," the export/import format, and probably the achievement logic. I'd suggest this as the next substantial build, designed once rather than three separate patches.
Content — the actual mechanical process

Same batch rhythm as every round so far: I search real sources (luontoon.fi, Wikipedia infoboxes) for routes/shelters/difficulty/accessibility, write it in all three languages, add it to the data, validate. 25 parks left, typically 4 per batch — so roughly 6 more rounds to reach 41/41. No blockers, just volume. Happy to start the next batch anytime you say go.
What else is genuinely next, ranked

    Trip tips section — fully specced now, nothing left to decide except checkbox-vs-static-list. Real candidate to just build next.
    MapTiler + MML key restrictions — not code, just logging into two dashboards. Cheap, and it's the one open security-adjacent item.
    Full 3-language QA sweep — walking the whole app checking for untranslated strings. Tedious but not hard.
    "Nearest wishlist park" on Home — genuinely cheap (both data pieces already exist), good quick win if you want something small between bigger pushes.

What do you want to tackle first — start the multi-visit redesign, keep chipping at content, or knock out the cheap wins (keys + trip tips) while that's being decided?

Do the nro 4. And add to more round of info
Building a nearest wishlist park feature and more content.
Building a nearest wishlist park feature and more content.

Let's build the "Nearest wishlist park" feature first, then move to the next content batch.
Ran 15 commands, edited 3 files, and 11 more tools
Summary

#4 built: "Nearest wishlist park" card on Home — shows the closest park on your wishlist by straight-line distance from your current location, tappable to jump straight there. Only appears once you actually have both location access and at least one wishlisted park, so it stays invisible rather than showing a broken/empty state on a fresh setup.

Content batch done: Hossa, Lemmenjoki, Pyhä-Luosto, Salla — 20 of 41 parks now have full extended info, exactly halfway. Lemmenjoki was a genuinely different case worth knowing about: it's Finland's largest park by far, and most of it is real trackless wilderness — so unlike most parks where we list specific named trails, its entry honestly says most of the park has no marked routes at all and requires real backcountry skill, which is accurate rather than pretending it has a tidy trail network like the smaller parks do.

Tracker cleanup: while updating it, caught and removed a stale duplicate idea entry (the old "nearest wishlist park" idea, now superseded by the actual built feature) rather than leaving both versions sitting in the file.

21 parks left — same rhythm going forward whenever you want the next batch.
Finnish national parks
Code·JSX 
Progress
Document·MD 

Do another round
Ran 2 commands, searched the web

Excellent detail for Torronsuo. Let's get Liesjärvi, Kurjenrahka, and Valkmusa:
Ran 5 commands, edited 2 files, and 8 more tools

Torronsuo, Liesjärvi, Kurjenrahka, Valkmusa — all four researched and added. 24 of 41 now done, past the halfway point.

A couple of things worth knowing from this batch: Torronsuo explicitly does not allow overnight camping (day-trip only, worth having correctly flagged rather than assumed), and Liesjärvi's "accessible" trail (Peukaloisen polku) is honestly labeled by the source itself as a demanding accessible route — uneven ground and elevation changes, assistant recommended — which is exactly the kind of nuance the tiered accessibility badge was built for, rather than a flat yes/no.

17 parks left. Same offer as always — say the word for the next batch whenever you want to keep going.
Finnish national parks
Code·JSX 
Progress
Document·MD 
Write a message…


Claude is AI and can make mistakes. Please double-check cited sources.
Progress · MD
# Kansallispuistot — Progress Tracker
 
How to use this file: check boxes as `[x]` when done, move items between
sections as things change, delete or add lines freely. This is yours to edit
directly in VS Code — nothing here is generated automatically by the app.
 
Last updated: 2026-09-11
 
---
 
## ✅ Done — core app
 
- [x] All 41 parks: name, region, blurb, badge, coordinates, official link
- [x] Real interactive map (Leaflet) with MapTiler standard + MML terrain layers
- [x] Location: nearest-park sort, native permission flow, in-app pre-permission modal
- [x] Fullscreen map view, now sized at 62vh with tightened surrounding chrome
- [x] Visit log: date, personal note, one photo per visit (compressed client-side)
- [x] Wishlist ("want to visit"), independent of visited status — shown in list + map
- [x] Achievements: 5 milestones, 8 motif-based, Four Seasons, Photographer, Planner,
      hidden "Grand Master" meta-achievement (unlocks when all others are complete)
- [x] Achievement detail popups showing which parks count toward each one
- [x] Multi-photo galleries per park (from Wikipedia), swipe + tap-to-enlarge, with
      real per-photo attribution (photographer + license)
- [x] Offline caching: map tiles (LRU-capped) + photos, manual "clear cache" option
- [x] Android back button correctly threaded through every screen (incl. lightbox,
      fullscreen map, modals, and now Home-as-root navigation)
- [x] Full FI / SV / EN localization (Finnish default)
- [x] Custom app icon, 19 unique original badge motifs (not Metsähallitus's real
      trademarked emblems — deliberate IP-safe design choice)
- [x] In-app Info screen: source credits (MapTiler, OSM, Wikimedia, Metsähallitus,
      MML), privacy policy link, real feedback email locked in
      (kansallispuistot.app@gmail.com)
- [x] "Report a mistake" — per-park and general feedback links, mailto-based
- [x] Real dark/light theme system — 18 CSS custom properties, both palettes,
      instant toggle in Info screen, saved preference, defaults to system
      setting on first launch. Status bar AND native navigation bar both
      follow the active theme (nav bar needs a plugin — see setup note
      below). Shareable progress card also renders in the correct theme now.
- [x] Full navigation redesign — bottom tab bar (Home / Explore / Map),
      replacing the old top segmented control and the old Parks/Map/Achievements
      split. Achievements is reached via a link from Home, not a permanent tab.
      Each screen has its own contextual header instead of one fixed block with
      a permanently-visible progress bar.
- [x] New Home screen — real data, not placeholders: circular progress ring,
      regions/photos/wishlist stats, latest-visit card (shows your own photo if
      you added one for that visit), achievements preview strip, Everyman's
      Right tip card
- [x] Explore list redesigned as medium photo cards — badge centered against
      the text block, filter pills (All/Unvisited/Wishlist/4 region groups) with
      real filtering logic, and cards show your own uploaded photo when you have
      one for that park, falling back to a decorative gradient otherwise
- [x] "Show more" per-park section: routes, shelters, difficulty, accessibility
      (tiered badge: accessible / partly accessible / none), GPX-availability
      note, "info last checked" date
- [x] Optional "distance hiked" field on each visit — plain manual number
      input (km), sits between date and note, same save pattern as the note
      field. Data lives in the same log entry as everything else, ready for
      whatever gets built on top of it later (a total-km stat, an
      achievement, etc. — none of that exists yet, just the raw data now)
- [x] Export / import your own data (JSON) — Info screen has two buttons:
      export bundles your visit log, wishlist, language, and theme into a
      JSON file (uses native Share on Android, falls back to browser
      download); import reads a file back in, asks for confirmation since
      it replaces current data, then restores everything including your
      photos (they're already stored as data URLs inside each log entry,
      so they travel with the export automatically)
- [x] "Nearest wishlist park" card on Home — shows the closest park on your
      wishlist by straight-line distance, only shown when both location
      access and at least one wishlisted park exist; tapping it opens that
      park directly
- [x] "Käydyt" (Visited) filter pill on Explore, plus a direct link from
      the Home journey card to jump straight there with it pre-applied
## 🔧 In progress / partial
 
- [ ] Extended park content ("Show more"): 24 of 41 done
      (Nuuksio, Oulanka, Koli, Repovesi, Pallas-Yllästunturi, Urho Kekkonen,
      Seitseminen, Helvetinjärvi, Riisitunturi, Syöte, Linnansaari, Kolovesi,
      Isojärvi, Leivonmäki, Rokua, Teijo, Hossa, Lemmenjoki, Pyhä-Luosto,
      Salla, Torronsuo, Liesjärvi, Kurjenrahka, Valkmusa) — 17 remaining,
      ongoing batch by batch — past the halfway point now
- [ ] luontoon.fi official links: 17 of 41 individually verified
      (all compound/hyphenated names — highest risk of pattern breaking).
      1 real bug already found + fixed (Puurijärvi-Isosuo). 24 remaining are
      simple single-word names, lower risk but unverified.
- [ ] Park coordinates — spot-check in progress. Päijänne was found to be
      ~40 km off (and its region was wrong too — fixed both). Found via
      visually comparing against the real MML terrain outlines, which is a
      genuinely good way to keep catching these — keep reporting any park
      that looks visually wrong on the terrain map. The other 40 haven't
      been systematically re-verified.
- [ ] Region-group classification for the filter pills (Lapland/Lakeland/
      North/South) — built and working (real bug already found + fixed: it
      was checking the wrong language's region text), but the grouping
      itself is a reasonable first pass, not an authoritative Finnish
      administrative classification. Worth a second look eventually.
- [x] Play Store closed testing — completed, app submitted for production review
- [ ] MapTiler account: commercial-use terms + API key domain restriction —
      needs confirming in your MapTiler dashboard
- [ ] MML API key — same category of check as MapTiler above, not yet done
      for this one specifically. Client-side API keys are inherently visible
      in any frontend app's bundle (there's no way to truly "hide" a key
      without a backend proxy) — that's normal for keys meant for this,
      but only safe if the provider's dashboard has real usage
      restrictions (domain/package lock) configured on their end. Worth
      confirming MML's terms explicitly allow client-side use the way
      MapTiler's do.
## 🔌 Setup needed for latest features
 
- [ ] Install @capgo/capacitor-navigation-bar for the native Android
      navigation bar to follow the theme toggle (the status bar already does
      this via the core plugin — the nav bar needs this separate one).
      Note: the original package name given (@capacitor-community/navigation-bar)
      was wrong / doesn't exist — corrected to the actively-maintained one:
      npm install @capgo/capacitor-navigation-bar
      npx cap sync android
## ⚠️ Legal / compliance — read before acting
 
- [ ] Monetization must NOT be a bare "tip jar." Verified against Finnish
      Ministry of Interior + Poliisihallitus sources: private individuals
      cannot get a money-collection permit for themselves under
      Rahankeräyslaki, even for something framed as a "tip" — permits are
      reserved for non-profits.
      **Heads up**: a second external review (independently) suggested
      exactly this risky pattern — a voluntary "buy me a coffee ☕" button
      with nothing given in exchange. That's still the same legal problem
      regardless of how gently it's framed or how many people suggest it.
      Fix: sell an actual feature/product instead (this makes it
      ordinary commerce, not a money collection):
      - Idea: "Supporter" one-time purchase unlocking a cosmetic badge
      - Idea: premium map style / app theme
      - Idea: paid offline map pack bundle
  - [ ] Get real legal confirmation before shipping any payment feature —
        the above is well-sourced but not a substitute for actual legal advice
- [ ] Paid app (€1.99) is live in testing — remember paid→free is reversible
      anytime, free→paid is NOT (already learned this one the hard way once)
## 🐛 Known issues / needs on-device verification
 
- [x] MML terrain layer — confirmed working on-device
- [x] Share button — confirmed working
- [x] Language switcher on very narrow screens — fixed, confirmed working
- [x] Fullscreen map button too transparent — fixed (was 90% opacity +
      blur, now fully opaque)
- [x] Map preview popup too transparent, text barely visible in dark mode
      — fixed, same root cause as the button above (95% opacity + blur letting
      busy map tiles wash out the text)
- [x] Park name unreadable in light theme — real bug: the hero photo
      overlay title got swept into the systematic light-theme color
      conversion and started following the page theme instead of staying a
      constant light color, even though it sits on a permanently-dark photo.
      Fixed.
- [ ] New theme system needs a real walkthrough — this was the single
      biggest mechanical change made to the app (146 individual color
      classes converted to CSS variables across the whole file). Validated
      structurally (parser, brace/paren balance) but that doesn't prove
      every screen looks right when actually toggled — walk through list,
      map, park detail, achievements, and all modals in both themes
- [x] Navigation bar color sync — confirmed working on-device
- [ ] Full 3-language QA sweep — walk every button, error message, park
      entry, achievement, and map label in FI/SV/EN specifically looking
      for anything left untranslated. A good, concrete suggestion from an
      external review — one missed string is the kind of thing that makes
      an otherwise-polished app feel unfinished, and it's easy to miss
      individual strings when everything's been added incrementally over
      a long build like this one
## 📋 Backlog — cheap, high value (good next picks)
 
- [ ] Navigate button — one-tap link to Google/Apple Maps for directions
- [ ] More hiking-behavior achievements (e.g. shelter-based, winter-specific)
- [ ] Richer share card on logging a single visit (photo + badge + park name
      overlay, not just the overall progress card) — Instagram-Story-shaped
- [ ] Dynamic seasonal challenge UI (e.g. "Ruska Challenge" — visit Lapland
      parks in September) — reuses existing visit-date + achievement system
## 📋 Backlog — bigger, real work, sequence deliberately
 
- [ ] Multiple visits per park (Nuuksio 2024, 2025, ... each with own
      date/note/photo) — on hold, paired with:
- [ ] Multiple photos per visit — on hold, same reason (both need a real
      data-model change: visit history array instead of one slot per park)
- [ ] Photo storage upgrade (move off current storage toward IndexedDB or
      native Filesystem) — becomes more urgent once the above two ship, and
      now that photos show up on Explore cards + Home too (more places
      touching the same stored images)
- [ ] Structured route objects (name/length/difficulty as real fields, not
      one text paragraph) — deferred until something actually needs to query
      routes individually (e.g. drawing one on the map, filtering by length)
- [ ] Explicit "Download park for offline" button — pre-fetch a park's full
      tile bounding box at set zoom levels, instead of relying on the user
      having already panned over the area. Real value for spotty-signal
      parks (Lemmenjoki, UKK, etc.)
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
 
- [ ] **Trip prep tips / packing checklists — now fully specced, ready to
      build.** Placement decided: a small teaser card on Home, same visual
      weight as the existing Nature First card, sitting right alongside it
      (personal-stats stuff like Journey/Latest visit/Achievements at the
      top of Home, "good to know" reference cards like this one and Nature
      First at the bottom). Tapping the teaser opens a dedicated full
      screen with three tabs/sections that build on each other:
      - **Day trip**: check weather + trail conditions/closures before
        leaving, tell someone your route and return time. Pack: water,
        food, weather layers + rain gear, proper footwear, offline map
        downloaded, headlamp (even for day trips), basic first aid,
        charged phone, way to carry trash out
      - **3-day trip** (adds to the above): overnight gear (tent or
        reserved hut/lean-to), sleeping bag + pad, stove + fuel (open
        fires often restricted), food for every day plus one spare, water
        purification, paper map as backup, check hut/campsite reservation
        requirements, know your bail-out point
      - **Longer trips** (adds to the above): real map + compass skill
        (not just GPS), share route + check-in points with someone at
        home, basic first aid knowledge, emergency numbers written on
        paper, gear repair kit, realistic daily distances with a rest-day
        buffer
      Deliberately does NOT repeat the existing Nature First card's
      content (Everyone's Right / leave-no-trace ethics) — this is pure
      practical logistics, that one stays the ethics/etiquette card.
      **Open question before building**: tappable checkboxes (matches the
      app's whole "check things off" character, though nothing would
      persist — fresh list each time you open it) vs. plain static lists
      (simpler to build). Leaning checkboxes but not decided.
      One fact worth verifying before it ships: whether 112 genuinely
      works without signal in Finland the way it's commonly said to —
      don't want to state that as fact without checking.
- [ ] Export trail journal as a nicer document (PDF) — different from the
      raw-data export above: this one is for sharing/printing a personal
      "park passport" with photos and notes laid out nicely, not for
      restoring your data. Nice-to-have, lower priority than the plain
      JSON export since that one solves a real data-loss risk and this one
      is more decorative
- [ ] Richer "trip" concept for each visit — named route taken, duration,
      a personal 1–5 star rating, alongside the date/note/photo/distance
      that already exist. Elaborates on (doesn't replace) the existing
      "multiple visits per park" backlog item — worth designing together
      once that data-model change actually happens, rather than bolting
      fields on piecemeal
- [ ] FMI (Finnish Meteorological Institute) open API — live weather +
      forest fire warnings. **Worth noting a real tension here**: a
      different review explicitly warned against scope-creeping into "a
      weather app." A lightweight per-park snippet (today's forecast, a
      fire-warning badge if active) is a different thing from a full
      weather feature and seems like the reasonable middle ground, but
      this deserves an actual decision, not just adding it to the pile
- [ ] Multi-attribute compound filters on Explore (e.g. "accessible AND
      wishlist AND Lapland" at once) — builds on filters that already exist
      individually, just not combinable yet
- [ ] Badge unlock animation (confetti / SVG draw-in) when completing a
      milestone — fun, low-risk polish, no functional risk
- [ ] User accounts + cloud sync (Supabase/Firebase) — NOT a simple backlog
      item, flagging deliberately separate from the rest. This changes the
      app from offline-only/zero-server-cost to needing real backend
      infrastructure, ongoing hosting costs, and GDPR obligations for
      storing personal data server-side. Worth a real decision on its own,
      not something to casually greenlight alongside smaller ideas
- [ ] Premium cosmetic map styles / exclusive themes (ties into the
      monetization fix above)
- [ ] Gold-leaf "Supporter Badge" next to username (also ties into
      monetization — note: app currently has no concept of a username/
      profile at all, so this implies adding one)
 
