# Green Lantern — progress

Built on Pull-List-template v3: copied at template `f7ae723`, then template T0 at `9aac63d` (15 Nov 2026). The approved plan is
`PLAN.md`; the rules are `CLAUDE.md`. Sessions: Green Lantern #1 (14–18 Nov), its log in Master-Repo
`log/green-lantern-1.md`.

## Where it stands (18 Nov)
- **Stage 0 (setup): done and pushed (15 Nov).**
  - It holds template v3 copied in (first at `f7ae723`), then template T0 (`9aac63d`, John merged ASIMKARD/Pull-List-template#12): the v9-frame guard's clock is pinned to each reference's captured day.
  - T0 brought four files: `test/layout/lib.js`, `test/layout/ref/capture-frame.js`, `test/layout/47-frame-v9.test.js` and `BUILD-NOTES.md`. Every other template file is identical to template `main` `9aac63d`, apart from this tracker's own docs.
  - The harness gives 1720 assertions and the layout suite 470, with 0 failed in both.
  - The data is still the starter demo (`franchise.key` `starter`) until stage 2. The template's `FEATURE-INVENTORY.md` stays until then too, because the docs test expects it while the key is `starter`.
- **Stage 1 (arc spine): revised with the Grand Comics Database's dates (17 Nov) and John's decisions of 18 Nov.**
  - **Where:** Research-Repo `sessions/2026-11-14-green-lantern/`, branch `claude/awesome-brahmagupta-89pq1z` at `8345db0`. No pull request until John says (16 Nov).
  - **The spine:** `spine.py` → `arc-spine-v2.json`: 239 arcs over 711 issues, 13 sub-eras, 6 bands.
  - **The built order:** `stage1_order.py BUILD_DIR` → `stage1.dataset.draft.json`, built with this repo's `tools/build.py` at `a789c18` → `stage1-order.json` and `stage1-order-final.json` (the order John checks).
    - Built v1 (`4f95944e414b`), 711 rows; the verify gate passed.
    - 0 missing, 0 duplicates, 4 numbering exceptions (the September 2012 #0s).
    - On-sale dates: the DC Database states 30; the GCD orders 679 more. 311 rows moved because of the GCD dates.
  - **The independent pass:** `verify_order.py BUILD_DIR` → `verify-order.json`: 711 checked, 0 mismatches.
  - **Fixed on 17 Nov, before the report went out:**
    - every arc id had lost its capital letters (`reen-antern-…`); they are now `green-lantern-…`;
    - the 2021 annual is `green-lantern-2021-annual-1`, "Green Lantern (2021) Annual #1" (it was `green-lantern-2021-2021-annual-1`).
  - **Rebuildable from Research-Repo alone:** `sh rebuild_check.sh /path/to/Green-Lantern`, offline, with a clean clone of this repo at `a789c18`. Run from fresh clones of both repos: every one of 15 generated files is identical, byte for byte.
  - **The report:** `report2.py` → `change-report-stage1.md`, `.json` and `arc-spine.html` (the phone page).
  - **John's decisions of 18 Nov, applied** (`decisions.json`, an input):
    - Blackest Night (2009) #0 opens the Blackest Night sub-era: position 112, after GLC (2006) #38, before GL (2005) #43. On sale 2 May 2009 (ComicList, fetched and checked); the World's Finest Special 18 Dec 2024 (dc.com refused an automated fetch, so John's citation stands).
    - His question-form answers keep 38 pairs.
    - **Placement notes** (`placements.py`, 42 on 39 pages): 2 order a pair within a month, overriding 0 on-sale dates. Across months: 2 wait for T6, 2 would cross their own series (not applied), 1 is a question, 4 already agree.
    - **Publication order** runs against the on-sale dates in 9 pairs (a blank DC date sorts first; `seq` is the story order). The fix is in T6's design note.
  - **T6's design note:** `t6-design.md` in the session folder, for John before any template edit.
  - **Open:** 18 linked pairs (one question each), and 1 placement note for John's ruling (Green Lanterns: Rebirth #1, which T6 would move past Green Lanterns #1–2). Green Lanterns (2016) #22's note (about #19 onwards) would cross its own series, so it is listed, not asked.
- **Next steps, in order:**
  1. **John answers the 18 linked pairs and the placement note, and approves the stage-1 order.** His answers go into `decisions.json` (pairs) as before, the order is rebuilt, and `rebuild_check.sh` must pass again before the push.
  2. **T1 + T2,** as a template PR after T0 is merged, on the template's branch restarted from the new `main`:
     - **`schema/dataset.schema.json`:** `rows[].coreFor`, a unique list of character slugs.
     - **`tools/build.py`:**
       - validation: each name must be a character the row has as major or minor;
       - emit `issueCoreFor` next to `issuePresence`.
     - **`app.js`:**
       - a `HAS.coreFor` capability;
       - with Lantern chips on, ★ (`r[5]` today) and the Barebones depth (`planOk`, `D.issueTier[i] > F.tier`) follow the chosen Lanterns' picks.
     - **T2:** "Counts as an appearance" becomes Lead / Appearances / Including cameos.
       - It replaces the `cameos` chip, `F.cameos` and `presenceOk`.
       - It is saved by name, and an old `cameos: true` reads as Including cameos.
     - **`tools/build_workbook.py`:** Core for, Presence, Importance and Strands columns.
       - `24-workbook`'s `String.fromCharCode(64 + n)` must become a real column name: the sheet passes 26 columns.
     - **Tests:** `20-build`, a new `9m-scoped-core`, `9f-visibility` and `92-filters`.
     - **Docs:** `BUILD-NOTES.md` and the template's `PROGRESS.md`.
  3. **Stage 2,** sub-era by sub-era: `dataset.json` takes the key `green-lantern`, and `FEATURE-INVENTORY.md` is dropped.

## Decisions (John)
- **14 Nov, question forms:**
  1. Master-Repo log and archive for Green Lantern #1: approved.
  2. T1 (per-Lantern CORE through `coreFor`, plus Presence, Importance and Strands columns in the workbook) is done from GL before stage 2, as a template PR John merges. Its exact change is shown to him first.
  3. Canonical events are drafted in GL first, then go to the template's `events/` in one PR at the end of stage 5, with the hashes checked equal.
  4. Going live: after stage 2, then after every stage.
  5. The workbook is generated.
  6. Change reports are pasteable markdown, with the full report in Research-Repo and a private Artifact page for the phone.
  7. The Indigo Tribe and the Star Sapphires are Appearances chips. Tracks exist only where a series does (Red Lanterns, Larfleeze, Sinestro).
  8. Collected In goes in each arc's ⓘ blurb, with no template change.
- **14 Nov, John's reply to the plan:** T3, below.
- **15 Nov:** the plan approved.
- **15 Nov, John's stage-1 review:**
  - Sub-eras and ratings approved, and six corrections asked for (volumes named; the Tales one-shots; one canonical name per creator; stories split; GL (2023) #19–27 and the Starbreaker Supremacy; Green Lantern Dark).
  - T0 approved as its own template PR first.
  - T1 approved, with T2 "Lead only", as its own PR after T0.
  - Every template PR is pasted to John before he merges it.
  - The standing order-check rule (`CLAUDE.md`, "Green Lantern's own rules").
- **15 Nov, question forms:**
  - The Grand Comics Database is a second on-sale source, for ordering only.
  - Only true Elseworlds leave the spine: Green Lantern Dark moves to stage 7; the Flashpoint minis, Futures End, Future State and Blackstars stay.
- **15 Nov, after T0 merged:** push stage 0 and confirm CI; finish the GCD pass; the revised report lists every same-month pair and what settled it, every row the GCD moved, and every DC Database/GCD disagreement with the date kept; the final order is committed as JSON beside the cached pages.
- **16 Nov:**
  - The order must be rebuildable from Research-Repo alone (every GCD response, `gcd.json`, the before-GCD and final orders), and is checked by a script that isn't Claude's.
  - The clean-checkout test builds from a fresh clone of this repo at the commit the README names.
  - The "not settled" questions are grouped: same-day pairs with no shared story answered once; linked pairs one question each.
  - Research-Repo #5 being merged doesn't approve the order. No new Research-Repo pull request until John says.
- **18 Nov, question form:** the 36 same-day pairs keep their provisional order; Green Lantern (2005) #25 before the Ion one-shot; Green Lantern (2023) #18 before the World's Finest Special; Blackest Night #0 first (replaced by the decision below).
- **18 Nov, three decisions:**
  1. Blackest Night (2009) #0 opens the Blackest Night era, just before Green Lantern (2005) #43; its cover stays June 2009. Its on-sale date is 2 May 2009 (ComicList's Free Comic Book Day 2009 list); the World's Finest Special's is 18 Dec 2024 (dc.com).
  2. Placement notes settle same-month order (`CLAUDE.md`, "Green Lantern's own rules").
  3. Two orders: release order and story order; across months, template change T6, with its design note shown first and its own template PR after T1 + T2.

## Decided, not yet built
- **T1 + T2:** per-Lantern CORE, the workbook columns and "Lead only" appearances (both approved 15 Nov). One template PR before stage 2, pasted to John before he merges it; the plan is in "Next steps", above.
- **T3, cross-tracker progress for shared issues** (John, 14 Nov). It is built at stage 5, in its own template PR, which John approves first, like T1.
  - "An issue marked read (or skipped) in any of my trackers counts as read in every tracker that has the same issueId."
  - Each tracker writes only its own storage. It reads the others' saved progress on asimkard.github.io and never writes to them.
  - The design is in `PLAN.md`, "T3":
    - each tracker publishes `<key>:v3:shared` keyed by `issueId`;
    - the latest mark wins, or "read always wins" if John picks it in the design note;
    - Undo and Clear all act on this tracker's own marks only;
    - backups and codes carry only the tracker's own marks.
  - Tested in Chromium with two trackers sharing an event; then the iPhone steps (Safari tabs and two home-screen apps).
  - Absolute's own skin and every existing tracker stay unchanged until each is updated, and 47-frame-v9 stays green.
- **T5:** the spectrum swatches for the signature skin, at stage 8, after John sees the mock-ups.
- **T6** (John, 18 Nov): a row placed after or before another issue by a cited note, keeping its true date; Publication order ignores it; a placement that crosses its own series isn't applied but listed. The design note (`t6-design.md` in the Research-Repo session folder) also proposes a clean release order. Its own template PR, after T1 + T2, once John approves the note.

## Stages (from `PLAN.md`)
| # | Stage | State |
|---|---|---|
| 0 | Setup | done and pushed (15 Nov) |
| 1 | Arc spine | revised with John's 18 Nov decisions; 18 linked pairs and 1 note await his answers |
| 2 | Core spine (goes live as v1) | — |
| 3 | Green Lantern Corps and New Guardians | — |
| 4 | Spectrum spin-offs | — |
| 5 | Canonical events, with T3 | — |
| 6 | Pre-2004 landmarks | — |
| 7 | Elseworlds (ALT) | — |
| 8 | The look, then the signature skin's deploy | — |
