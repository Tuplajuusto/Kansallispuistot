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
- [x] **Extended park content ("Show more"): 41 of 41 — every park done.**
      Real routes, shelters, difficulty, and a tiered accessibility rating
      for all 41, researched from actual sources (luontoon.fi, official
      park pages, trip reports) rather than filler text. The last 9 were
      the trickiest batch — mostly boat-only marine/archipelago parks
      (Archipelago Sea, Bothnian Bay, Bothnian Sea, Eastern Gulf, Ekenäs)
      that genuinely don't have a mainland trail network the way land
      parks do, so their content honestly reflects that (how to get there
      by boat/kayak, island-only trails) rather than forcing them into the
      same template as everywhere else

## 🔧 In progress / partial

- [x] **Finnish luontoon.fi links: 41 of 41 — every park now has an
      explicit Finnish slug.** This was a real bug, not just incomplete
      coverage: any park without an override silently fell back to the
      *English* page even when the app was set to Finnish. Fixed the root
      cause too — the URL function no longer has a path that lets Finnish
      fall through to English at all. Confidence: most entries directly
      confirmed (Finnish Wikipedia's own reference list, which cites
      Metsähallitus by name for each park, plus a few live luontoon.fi
      URLs seen directly); the remaining handful (Hiidenportti, Hossa,
      Patvinsuo, Tiilikkajärvi, Torronsuo, Valkmusa) are grammar-derived —
      standard Finnish genitive inflection, a pattern with zero exceptions
      across every other park checked, but not individually re-verified
      against a live page one by one.
- [ ] **Swedish luontoon.fi links: 24 of 41 now covered** (was much lower
      before this pass). The remaining 17 still fall back to English for
      Swedish users specifically — same original gap, just narrower now.
      Most of the 24 are pattern-derived from one directly-confirmed
      example (Hossa: "Hossa nationalpark" — untranslated Finnish proper
      noun + the Swedish generic word), which is a reasonably safe pattern
      for single-word names but genuinely unverified per park. Worth a
      dedicated Swedish-specific verification round later — lower
      priority than Finnish since it's a smaller audience, but still a
      real gap while it lasts.
- [ ] English luontoon.fi links: 17 of 41 individually verified — same
      status as before this round, not the focus this time
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
- [ ] **MapTiler licensing — decided: switch to MML instead, not upgrade
      MapTiler.** Since this app isn't trying to be a standalone map/nav
      product — the map is a feature in service of the park-tracking
      purpose, not the product itself — the simplest fix wins over the
      "nicest" one. Plan: replace MapTiler's "Vakio" (Standard) style with
      MML's `taustakartta` layer, using the *exact same* already-working
      MML integration (same open endpoint, same auth, same URL pattern as
      the existing `maastokartta` terrain layer — just a different
      `layer=` value). If this works as expected, **MapTiler can be
      dropped entirely** — both map styles would run on MML, CC BY 4.0
      licensed, no revenue caps, no employee thresholds, nothing new to
      integrate. Not yet built — next concrete step is trying the real
      `taustakartta` tile URL to confirm it looks acceptable as the
      standard style, then wiring it in.
      Still need the API key domain/package restriction set on whichever
      keys remain in use either way.
- [ ] MML API key — same category of check as MapTiler above, not yet done
      for this one specifically. Client-side API keys are inherently visible
      in any frontend app's bundle (there's no way to truly "hide" a key
      without a backend proxy) — that's normal for keys meant for this,
      but only safe if the provider's dashboard has real usage
      restrictions (domain/package lock) configured on their end. Worth
      confirming MML's terms explicitly allow client-side use, and
      separately confirming what license tier the app is actually on.
      Also worth confirming `taustakartta` and the other open-endpoint
      layers sit under the same free/open tier as `maastokartta` already
      does, not the separate paid "sopimuspalvelu" contract service.
- [x] **Wikimedia Commons photos — checked, genuinely clean.** Commons'
      own policy states directly: "All media files on Wikimedia Commons
      can be used by anyone, including commercially." Commons rejects
      non-commercial-only licenses and fair-use uploads at the point of
      upload, so anything actually hosted there is already cleared. Only
      real obligation is attribution (photographer + license), which the
      app already does automatically per photo. No action needed.
- [x] **LIPAS data license — confirmed, genuinely good news.** Real terms
      text, provided directly: CC Nimeä 4.0 Kansainvälinen (CC BY 4.0),
      explicitly covering private, public, commercial, and non-commercial
      use. Only requirement is attribution, with a suggested citation
      format ("Jyväskylän yliopisto, Lipas Liikuntapaikat.fi") and noting
      the sample date, since the database updates continuously. Same
      clean license family as MML and Wikimedia — no action needed until
      the LIPAS/GPX integration itself actually gets built (still a
      deferred, long-term item), but the legal groundwork is now settled.
- [ ] **NationalPark font — license confirmed clean (SIL OFL 1.1), one
      small thing still to actually do.** Found the license file sitting
      right alongside the font itself: SIL Open Font License 1.1,
      copyright 2025 The National Park Project Authors. Explicitly
      permits embedding in commercial software free of charge — only
      restriction is not selling the font by itself, which doesn't apply
      here. Real remaining task: the license requires the copyright
      notice stay reasonably accessible to users. Cheapest fix — add one
      more line to the Info screen's existing credits list (already
      credits MapTiler, OSM, Wikimedia, Metsähallitus, MML), same pattern
      already established, just one more source added to it.

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

- [ ] **MML tile-caching-specific terms** — the general MML open-data license
      (CC BY 4.0) is confirmed, but a separate reviewer specifically flagged
      verifying that *long-term local caching* of map tiles is covered the
      same way as just using them live. Not yet checked as its own question.
- [ ] **Error handling** — many empty `catch (e) {}` blocks throughout
      (save, photo load/compress, tile load, share, achievement/visit save).
      Keeps the UI quiet but makes real failures invisible to you and to
      users. Worth at minimum: a short user-facing message on critical
      failures, centralized dev logging, and privacy-respecting crash
      reporting with consent for the production build. Not started — a
      real, if unglamorous, piece of work.
- [ ] **"Offline" wording honesty check** — confirm the current copy
      describes what's actually true (previously-viewed map areas stay
      available without a connection) rather than implying a full
      pre-downloaded offline park package, which doesn't exist yet. Cheap
      to fix once checked, just not yet checked directly against the
      current strings.

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

- [ ] **All-visits summary/journal view** — a chronological list of every
      logged visit across all parks, not just per-park. This is arguably
      the actual point of the multiple-visits work already built, not a
      separate feature — several outside reviews independently called out
      a real trip journal as the single biggest thing missing, and this is
      what turns the underlying data into something worth looking back on.
      **Placement**: leaning against a new tab (too much weight for what
      it is) — more natural reached from Home, e.g. the existing "Latest
      visit" card gets a "See all visits →" link, mirroring how
      achievements already work (preview strip → full view one tap away).
      **Per-row content**: date first (it's the organizing principle),
      park name, a small photo thumbnail when one exists, first line of
      the note as a preview if there's room. Distance as a smaller
      secondary detail.
      **Natural pairing**: this is exactly where the existing "quick add
      trip" idea (see below) would slot in — a "+" at the top of this
      list, rather than only reachable by finding a specific park's page
      first.
      **Open question before building, not yet settled**: chronological
      across *all* parks (a true "my whole trekking history") vs. a
      per-park visit list shown as a list instead of a swipe — genuinely
      different scope and different value, worth deciding deliberately
      rather than defaulting to one.

- [ ] **"Quick add trip" button on Home** — a shortcut for logging a visit
      without navigating to that specific park's page first. Tap the
      button, a popup opens with a park dropdown/search selector at the
      top, then the same fields already used in a park's "Your visit"
      section below it (date, note, photo, distance). Submitting writes
      to the same `log` data everything else already uses — this is a
      new entry point to existing functionality, not a new data model.
      Real use case: logging a visit after getting home from a trip,
      without hunting through Explore for the right park first. Not
      scoped beyond this — needs a decision on exact placement on Home
      (its own card? folded into an existing one?) and how the park
      dropdown should behave with 41 options (searchable text input
      matching Explore's search, most likely, rather than a plain
      long dropdown list).

- [ ] Maptoolkit.org's "Hiking" map style, for later — genuinely nice,
      purpose-built for exactly this use case (contour lines, hillshading,
      trail-friendly rendering), and worth a look again someday. Explicitly
      deferred in favor of MML for now: switching to Maptoolkit means a
      real migration (Leaflet vector-tile plugin, new license terms to
      track, a "no offline tile generation" clause that needs clarifying
      against the app's existing offline cache), while MML reuses
      integration that already exists. Right call for now since this app
      isn't trying to be a standalone map/navigation product — the map
      serves the park-tracking purpose, it isn't the purpose. Revisit if
      MML's `taustakartta` turns out to look or perform worse than hoped.

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
- [ ] Once multiple visits per park exists, add a "total visit count" stat
      to the Home journey card (e.g. "23 visits" vs. "15 parks") — a
      meaningfully different number once one park can have several visits
      logged against it. Small addition, but only makes sense after the
      data model actually supports multiple visits — noted here so it's
      not forgotten when that work happens
- [ ] **FMI forest fire warning badge — decided: yes, worth building, scope
      narrowed to fire warnings specifically, not full weather.** You
      confirmed this directly — it's exactly the kind of thing people
      forget to check before a trip, and that's the real value, not a
      weather forecast (which the "don't become a weather app" caution
      still applies to).
      **What I've actually verified** (not just assumed):
      - FMI's open data API is real, free, and needs no registration —
        confirmed directly on ilmatieteenlaitos.fi, contradicting an older
        third-party doc that claimed an API key was required
      - Metsäpalovaroitus (forest fire warning) is a real, official FMI
        product with its own page — this isn't a guess, it exists
      - **Not yet confirmed**: weather *warnings* (which fire warnings are
        a type of) are explicitly served from a *separate* interface from
        the general WFS data API — the source says so directly but I
        haven't found that specific endpoint's documentation yet
      - The main API returns WFS/GML (XML), not simple JSON — parsing
        that client-side in the app is more work than a typical REST API
        would be, worth knowing before scoping the build
      **Next step before building the real API version**: find the actual
      warnings-specific endpoint and confirm its response format, rather
      than starting to build against the general forecast API and hoping
      fire warnings work the same way
      **Simple fallback, genuinely worth considering as the actual first
      version**: skip the API entirely — a plain reminder card (Home or
      the trip-tips section) with a line like "Check current fire warnings
      before you go" linking straight to
      ilmatieteenlaitos.fi/metsapalovaroitukset. No parsing, no unknown
      endpoint, no network-failure handling to design around, delivers
      the actual behavior change (remembering to check) with a fraction
      of the effort. The live-data version is a nicer upgrade later, not
      a prerequisite for getting real value now
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
