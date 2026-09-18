# Kansallispuistot — Progress Tracker

How to use this file: check boxes as `[x]` when done, move items between
sections as things change, delete or add lines freely. This is yours to edit
directly in VS Code — nothing here is generated automatically by the app.

Last updated: 2026-09-11

---

## ✅ Done — core app

- [x] **Multiple visits per park** — real data-model change, not just UI.
      log[parkId] is now an array of visits (was one object). Swipeable
      card in ParkDetail shows "Visit 3/15" with prev/next arrows and dot
      indicators, "+ Add visit" appends a new entry, delete removes a
      single visit (or routes through the same warned un-mark flow if
      it's the last one). Migration runs automatically on existing data
      and on importing older backup files. Achievement/stat calculations
      (photo count, seasons, distance) correctly sum across all visits,
      not just one per park. Home shows a "total visits" stat once it's
      actually different from "parks visited."
- [x] **Photo storage moved to IndexedDB** — photos no longer live as
      base64 strings inside the size-limited log JSON. Real quota upgrade
      that became necessary once multi-visit removed the old natural
      ceiling (41 photos max, one per park) — an engaged user logging
      many visits to a favorite park had no cap anymore. Write path,
      migration, cleanup-on-delete, and export/import (which reconstructs
      real photo bytes so backups stay portable across devices) all
      updated together, plus all three photo-reading UI spots (ParkDetail,
      Explore cards, Home's latest-visit card).
- [x] **Collapsing header on ParkDetail** — hero photo compresses as you
      scroll (160px → 68px), badge and title shrink and reposition rather
      than disappearing. Real accessibility fix built into it: the back
      button's text label collapses to icon-only first, specifically so
      it can't visually collide with the badge once the header is short —
      caught and fixed a genuine overlap risk, not just prettifying.
      Same technique applied to Explore's header too (title/location-row/
      filter-pills collapse down to just the search bar on scroll).
- [x] **Fixed and confirmed on-device: header would visibly jitter on
      scroll for unvisited parks specifically.** First attempt (an
      epsilon guard filtering small scroll-position changes) reduced but
      didn't eliminate it — confirmed insufficient by the user testing on
      a real device. Real fix: replaced continuous scroll-position
      tracking with hysteresis (collapse past 70px, expand again only
      below 20px, on both ParkDetail's hero and Explore's header) — a
      genuine dead zone between the two thresholds, not a guessed noise
      threshold that happens to be small enough. Structurally can't
      flicker near a boundary regardless of noise amplitude. Side
      benefit: since the target now only changes at two infrequent,
      well-separated moments instead of every scroll frame, real CSS
      transitions could be brought back safely (removed earlier
      specifically because they fought continuous tracking) — collapse/
      expand now animates smoothly instead of snapping.
- [x] Fixed: switching between Home/Explore/Map/Achievements kept
      whatever scroll position the previous tab was left at, since all
      four share one underlying scroll container. Now resets to top on
      every tab switch.
- [x] **Fixed and confirmed on-device: Share button needed a second tap
      most of the time.** First attempt (wrapping the fallback modal's
      state update in requestAnimationFrame) addressed a real but
      secondary paint-timing issue — confirmed insufficient by the user
      testing on a real device. Real cause: the button gave zero visual
      feedback when tapped, and canvas rendering + font loading (first
      use especially) takes a genuinely perceptible moment — with nothing
      visibly happening, a second tap isn't user error, it's the expected
      reaction, and with no guard against it that second tap could
      trigger a real concurrent second run. Fixed with a proper
      `isSharing` loading state: the button shows a spinner and disables
      itself the instant it's tapped (immediate proof the tap
      registered), and a real re-entry guard ignores a second tap while
      the first is still working rather than letting both run.
- [x] Share card content improved — added a real stats row (regions,
      total visits, photos) matching what the in-app Home card actually
      shows, so the shared image reflects genuine progress rather than
      just a bare percentage and progress bar.
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
      URLs seen directly).
      **Correction, worth recording honestly**: the grammar-derived
      entries were NOT actually error-free — two were wrong and caught
      only because the user checked the real pages directly, not because
      the grammar reasoning held: Perämeri's genitive was written as
      "peramerin" (should be "perameren" — meri → meren, like Itämeren,
      not merin) and Puurijärvi-Isosuo as "...isosuon..." (should be
      "...isonsuon..." — a compound adjective+noun like "Isosuo" declines
      both parts together: iso → ison + suo → suon). Both fixed directly
      in the code. The earlier "zero exceptions" confidence claim was
      itself wrong — Finnish genitive inflection has more edge cases
      (consonant gradation, compound agreement) than the sample checked
      at the time suggested.
      **Follow-up verification done**: Hiidenportti, Hossa, Patvinsuo,
      and Tiilikkajärvi are now directly confirmed via real luontoon.fi
      URLs seen in search results — all four were already correct.
      Torronsuo and Valkmusa didn't turn up a direct primary-source hit
      this round, but both follow the simplest, most regular inflection
      pattern (o-stem/a-stem + n, already confirmed correct across many
      other parks) — much lower risk than the two errors that actually
      broke, which both involved genuine irregularities (consonant
      gradation, compound-word agreement). Still technically unverified,
      just not equally suspect.
- [x] **Swedish luontoon.fi links: 41 of 41 — fully covered.** Jumped from
      24 after the user provided 17 real, directly-verified URLs in one
      batch. These are a meaningfully higher confidence tier than the
      earlier 24 (which were mostly pattern-derived from a single
      confirmed example) — these are actual confirmed pages, not guesses.
      One correction caught in the same batch: Pyhä-Häkki's Swedish slug
      was wrong (had "-nationalpark", real page uses "-national-park" —
      an inconsistent suffix on luontoon.fi's own site, not something
      that could have been predicted from pattern alone).
      **Worth remembering**: this batch proved the "just concatenate the
      Finnish name + nationalpark" fallback pattern isn't universally
      safe — Teijo's real Swedish name is "Tykö" (a genuinely different
      word, not a translation of "Teijo") and Etelä-Konnevesi's is
      "Södra Konnevesi" (translated, not transliterated).
      **A second mistake, worth recording honestly rather than quietly
      fixing**: right after the 17-URL batch, a verification sweep
      claimed Puurijärvi-Isosuo was "the one remaining gap." That was
      wrong — Puurijärvi already had a correct Swedish entry (added in an
      earlier session), and the check simply had a blind spot: it used
      simple line-adjacency (grep -B1) to match a park id to its "sv:"
      line, which silently breaks on any multi-line-formatted entry like
      Puurijärvi's. The user caught this by testing the actual app and
      reporting it opened the correct Swedish page. A proper parse (match
      each full `id: { ... }` block, not adjacent lines) found the real
      gap: Urho Kekkonen, confirmed and added
      ("urho-kekkonens-nationalpark"). Lesson: a "verification sweep"
      built on a fragile parsing method can produce a confident, wrong
      answer — worth designing the actual check to match the data's real
      structure next time, not a shortcut that happens to work for most
      entries.
- [x] **English luontoon.fi links: confirmed working, all 41** — direct
      confirmation from the user testing the actual app, not an
      individual per-park re-verification on my end. Worth noting the
      distinction honestly: this is real-world ground truth (the
      strongest kind, same as how the Puurijärvi Swedish correction got
      caught), not the same as having individually checked all 41 English
      slugs myself the way the earlier 17 were. If a future edit touches
      `enSlug()` or the English override table, that's worth re-testing
      rather than assuming it still holds.
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
- [x] **NationalPark font — license confirmed clean (SIL OFL 1.1) and
      credited.** Found the license file alongside the font itself: SIL
      Open Font License 1.1, copyright 2025 The National Park Project
      Authors — explicitly permits embedding in commercial software free
      of charge. Added the required copyright notice to the Info screen's
      credits list (all 3 languages), same pattern as the other credits
      there. Nothing further needed on this one.

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
- [ ] Richer "trip" concept for each visit — named route taken, duration,
      a personal 1–5 star rating, alongside the date/note/photo/distance
      that already exist. Elaborates on (doesn't replace) the existing
      "multiple visits per park" backlog item — worth designing together
      once that data-model change actually happens, rather than bolting
      fields on piecemeal

## 📋 Backlog — bigger, real work, sequence deliberately

- [ ] Multiple photos per single visit (still just one photo per visit —
      multiple *visits* per park is done, see below, but each individual
      visit still holds only one photo slot)
- [ ] Structured route objects (name/length/difficulty as real fields, not
      one text paragraph) — deferred until something actually needs to query
      routes individually (e.g. drawing one on the map, filtering by length)
- [ ] **Offline map download — refined design, planned but not started.**
      Better approach than the original idea (pre-fetching a park's whole
      bounding box, which needed geographic data that doesn't actually
      exist for any park yet): instead, let the user zoom/pan the map to
      whatever area they want, then explicitly download that visible
      area plus a zoom range around it. Simpler to build too — no new
      per-park geo data needed, "download what's currently on screen" is
      something the map already knows.
      **Real size math done for Lemmenjoki** (Finland's largest park,
      ~2850 km², ~70×55km bounding box, ~68.5°N — tiles cover less
      ground at northern latitudes, so this is close to the worst case):
      a single zoom level ranges from ~2 MB (z11) to ~538 MB (z15) —
      roughly quadrupling per level deeper. z11-z13 (whole-park view) is
      ~44 MB; z11-z14 (real trail-following detail) is ~179 MB; z13-z15
      is ~706 MB. The zoom range offered is effectively the whole size
      decision, not a minor tuning knob — "one more zoom level" and "an
      order of magnitude bigger download" are the same choice. Leaning
      toward roughly z11-z14 as the actual range to offer, but that's a
      real product call to make deliberately, not picked arbitrarily.
      **Requirements now confirmed, not just nice-to-haves**:
      - Show the estimated size *before* downloading (calculated from
        the math above), not just enforce a silent cap — let the person
        decide the trade-off knowingly rather than guessing or being
        blocked without explanation
      - Downloaded areas must be exempt from the existing LRU tile-cache
        eviction, or a deliberately-saved area for an upcoming trip could
        get quietly evicted by ordinary browsing before the trip happens
      - A "downloaded areas" list with delete/free-space capability is no
        longer optional once real file sizes like these are in play —
        someone needs a way to see and manage what's actually using space
      Not started. Real next step when this gets picked up: settle the
      actual zoom range and hard size cap using the numbers above, then
      design the download-progress UI and the management list together,
      not the tile-fetching logic first.

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
- [ ] User accounts + cloud sync (Supabase/Firebase) — discarded for now,
      not necessarily forever. Real reason it's a bigger call than a
      normal backlog item: changes the app from offline-only/zero-server-
      cost to needing real backend infrastructure, ongoing hosting costs,
      and GDPR obligations for storing personal data server-side. Revisit
      deliberately if that trade-off ever looks worth it — not something
      to quietly reconsider alongside smaller ideas.

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

- [ ] **Trip prep hub — consolidated plan, combining two previously
      separate ideas, ready to build.** One Home entry point ("Suunnitteletko
      retkeä? — Katso vinkit" / "Planning a trip? Check tips here"), same
      small visual weight as the existing Nature First card, sitting
      alongside it (personal-stats stuff like Journey/Latest visit/
      Achievements at the top of Home, "good to know" reference cards
      like this one and Nature First at the bottom). Tapping it opens one
      screen containing both pieces together, not two separate features:
      - **Trip-length tips** (three tabs/sections that build on each other):
        - *Day trip*: check weather + trail conditions/closures before
          leaving, tell someone your route and return time. Pack: water,
          food, weather layers + rain gear, proper footwear, offline map
          downloaded, headlamp (even for day trips), basic first aid,
          charged phone, way to carry trash out
        - *3-day trip* (adds to the above): overnight gear (tent or
          reserved hut/lean-to), sleeping bag + pad, stove + fuel (open
          fires often restricted), food for every day plus one spare,
          water purification, paper map as backup, check hut/campsite
          reservation requirements, know your bail-out point
        - *Longer trips* (adds to the above): real map + compass skill
          (not just GPS), share route + check-in points with someone at
          home, basic first aid knowledge, emergency numbers written on
          paper, gear repair kit, realistic daily distances with a
          rest-day buffer
      - **Fire warning reminder** (newly decided to live here, not as a
        separate Home card — resolves that earlier open placement
        question directly): a plain line — "Check current fire warnings
        before you go" — linking straight to
        ilmatieteenlaitos.fi/metsapalovaroitukset. Deliberately the
        simple version already decided on earlier, not the live API:
        no parsing, no unknown endpoint, no network-failure handling to
        design around, delivers the real behavior change (remembering to
        check) for a fraction of the effort. The live-data version
        remains a possible future upgrade, not a prerequisite — if it's
        ever picked up, the earlier research already confirmed FMI's
        open data API is real, free, and needs no registration
        (confirmed directly on ilmatieteenlaitos.fi), but the main API
        returns WFS/GML (XML), not simple JSON, and the specific
        warnings endpoint (separate from the general forecast API) was
        never actually located — worth picking up from there, not
        re-researching from zero.
      Deliberately does NOT repeat the existing Nature First card's
      content (Everyone's Right / leave-no-trace ethics) — this is pure
      practical logistics, that one stays the ethics/etiquette card.
      **Open question before building**: tappable checkboxes for the trip
      tips (matches the app's whole "check things off" character, though
      nothing would persist — fresh list each time you open it) vs. plain
      static lists (simpler to build). Leaning checkboxes but not decided.
      One fact worth verifying before it ships: whether 112 genuinely
      works without signal in Finland the way it's commonly said to —
      don't want to state that as fact without checking.
      Not started — planning only, per explicit request.

- [ ] Export trail journal as a nicer document (PDF) — different from the
      raw-data export above: this one is for sharing/printing a personal
      "park passport" with photos and notes laid out nicely, not for
      restoring your data. Nice-to-have, lower priority than the plain
      JSON export since that one solves a real data-loss risk and this one
      is more decorative
- [ ] Multi-attribute compound filters on Explore (e.g. "accessible AND
      wishlist AND Lapland" at once) — builds on filters that already exist
      individually, just not combinable yet
- [ ] Badge unlock animation (confetti / SVG draw-in) when completing a
      milestone — fun, low-risk polish, no functional risk
- [ ] Premium cosmetic map styles / exclusive themes (ties into the
      monetization fix above)
- [ ] Gold-leaf "Supporter Badge" next to username (also ties into
      monetization — note: app currently has no concept of a username/
      profile at all, so this implies adding one)
