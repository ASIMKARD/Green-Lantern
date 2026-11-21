# Green Lantern — progress

Built on Pull-List-template v3: copied at template `f7ae723`, then template T0 at `9aac63d` (15 Nov 2026). The approved plan is
`PLAN.md`; the rules are `CLAUDE.md`. Sessions: Green Lantern #1 (14–21 Nov), its log in Master-Repo
`log/green-lantern-1.md`.

## Where it stands (21 Nov)
- **Stage 0 (setup): done and pushed (15 Nov).**
  - It holds template v3 copied in (first at `f7ae723`), then template T0 (`9aac63d`, John merged ASIMKARD/Pull-List-template#12): the v9-frame guard's clock is pinned to each reference's captured day.
  - T0 brought four files: `test/layout/lib.js`, `test/layout/ref/capture-frame.js`, `test/layout/47-frame-v9.test.js` and `BUILD-NOTES.md`. Every other template file is identical to template `main` `9aac63d`, apart from this tracker's own docs.
  - The harness gives 1720 assertions and the layout suite 470, with 0 failed in both.
  - The data is still the starter demo (`franchise.key` `starter`) until stage 2. The template's `FEATURE-INVENTORY.md` stays until then too, because the docs test expects it while the key is `starter`.
- **Stage 1 (arc spine): approved by John, 20 Nov.** Revised with the Grand Comics Database's dates (17 Nov) and John's decisions of 18–20 Nov. The research folder is in ASIMKARD/Research-Repo#6, which John is merging (still open when last checked, 21 Nov).
  - **Where:** Research-Repo `sessions/2026-11-14-green-lantern/`, branch `claude/awesome-brahmagupta-89pq1z` at `f3d9fdf`. No pull request until John says (16 Nov).
  - **The spine:** `spine.py` → `arc-spine-v2.json`: 239 arcs over 711 issues, 13 sub-eras, 6 bands.
  - **The built order:** `stage1_order.py BUILD_DIR` → `stage1.dataset.draft.json`, built with this repo's `tools/build.py` at `a789c18` → `stage1-order.json` and `stage1-order-final.json` (the order John checks).
    - Built v1 (`51cea521ed3a`), 711 rows; the verify gate passed.
    - 0 missing, 0 duplicates, 4 numbering exceptions (the September 2012 #0s).
    - On-sale dates: the DC Database states 30; the GCD orders 679 more. 311 rows moved because of the GCD dates.
  - **The independent pass:** `verify_order.py BUILD_DIR` → `verify-order.json`: 711 checked, 0 mismatches.
  - **Fixed on 17 Nov, before the report went out:**
    - every arc id had lost its capital letters (`reen-antern-…`); they are now `green-lantern-…`;
    - the 2021 annual is `green-lantern-2021-annual-1`, "Green Lantern (2021) Annual #1" (it was `green-lantern-2021-2021-annual-1`).
  - **Rebuildable from Research-Repo alone:** `sh rebuild_check.sh /path/to/Green-Lantern`, offline, with a clean clone of this repo at `a789c18`. Run from fresh clones of both repos: every one of 16 generated files is identical, byte for byte.
  - **The report:** `report2.py` → `change-report-stage1.md`, `.json` and `arc-spine.html` (the phone page).
  - **John's decisions of 18 Nov, applied** (`decisions.json`, an input):
    - Blackest Night (2009) #0: on sale 2 May 2009 (ComicList, fetched and checked); the World's Finest Special 18 Dec 2024 (dc.com refused an automated fetch, so John's citation stands).
    - His question-form answers keep 38 pairs.
    - **Placement notes** (`placements.py`, 42 on 39 pages): 2 order a pair within a month, overriding 0 on-sale dates. Across months: 2 wait for T6, 2 would cross their own series (not applied), 1 is a question, 4 already agree.
    - **Publication order** runs against the on-sale dates in 9 pairs (a blank DC date sorts first; `seq` is the story order). The fix is in T6's design note.
  - **T6's design note:** `t6-design.md` in the session folder, for John before any template edit.
  - **John's decisions of 19 Nov, applied:**
    - Blackest Night (2009) #0 goes just after GL (2005) #43, before Blackest Night #1: position 113. Its reading-order month is #43's through the template's `sortDate`; its cover stays June 2009. T6 would write it as `place`.
    - His answers to linked pairs 1–4 (pair 3 swapped, with his reason).
    - **The method** (`collections.py`, `stage1_order.py`, `verify_order.py`): story links need evidence; on a series-by-series event page, interleaved collections are the chapter order. 39 of 173 collections count. Two agree on GL (2011) #20 before GLC (2011) #20 (over the dates); 12 pairs with no link take the Group A rule; no source disagrees with the order kept.
  - **John's answers of 20 Nov, applied:**
    - New Guardians (2011) #20 before Red Lanterns (2011) #20; Green Lantern (2005) #48 before Blackest Night #5 (his fix; positions 129 and 130).
    - For T6: Hal Jordan and the GLC: Rebirth #1 moves just before Green Lanterns: Rebirth #1.
  - **The reading step** (`readings.json`): all 33 same-day pairs on one event page read. 12 pick up, 16 have no link, 5 can't be told (a synopsis is missing). Every "picks up" agrees with the order. The build stops if a quote isn't in its cached synopsis or such a pair is unread.
  - **Open:** no questions. Green Lanterns (2016) #22's note (about #19 onwards) would cross its own series, so it is listed, not asked.
- **Next steps, in order:**
  1. **Done (20 Nov): John approved the stage-1 order.** He is merging Research-Repo#6.
  2. **T1 + T2: open as ASIMKARD/Pull-List-template#13 (21 Nov).** John held it for two changes, now made: a chosen character's picks show at every depth, and a character with no picks doesn't scope. Template branch `claude/awesome-brahmagupta-89pq1z` at `f61f2e9`; harness 1765, layout 470, 0 failed. John merges after his check.
     - **Once John merges it:** copy the changed template files into this repo and record the template commit here and in `CLAUDE.md`. The files: `app.js`, `tools/build.py`, `tools/build_workbook.py`, `schema/dataset.schema.json`, `BUILD-NOTES.md`, `CLAUDE.md`'s visibility list, the tests and fixtures. Then rebuild and run both suites.
     - **What was built** (the original plan, kept for reference):
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
- **19 Nov:**
  - Linked pairs 1–4 answered (pair 3: Green Lantern Corps (2006) #39 before Blackest Night #2, because Blackest Night #2 ends with the Corps "fighting for its life against the Black Lanterns on Oa", the battle GLC #39 starts).
  - Decision 1 changed: Blackest Night (2009) #0 goes just after Green Lantern (2005) #43, before Blackest Night #1; its cover stays June 2009.
  - The method (`CLAUDE.md`, "Green Lantern's own rules"): story links need evidence; interleaved collections are an event's chapter order; open pairs are shown with the synopsis ends.

- **21 Nov:**
  - Stage 1's order approved; John is merging Research-Repo#6 (still open when last checked, 21 Nov).
  - #13 held for two changes:
    - the depths must nest with a character chosen (a bug);
    - John's decision: "if none of the chosen characters has any core picks (for Green Lantern: Green Arrow, the Indigo Tribe, the Star Sapphires), ★ and Barebones fall back to the overall core, as with no character chosen. With several chosen, only those with picks count."
- **20 Nov:**
  - Answers: New Guardians #20 before Red Lanterns #20; for T6, Hal Jordan and the GLC: Rebirth #1 just before Green Lanterns: Rebirth #1.
  - T6's design note approved, with the four recommendations.
  - A fix: Green Lantern (2005) #48 comes before Blackest Night #5 (wrongly given the Group A rule).
  - The reading step (`CLAUDE.md`, "Green Lantern's own rules").

## Decided, not yet built
- **T1 + T2:** per-Lantern CORE, the workbook columns and "Lead only" appearances (both approved 15 Nov). Built; template PR #13 open (21 Nov), pasted to John before he merges it.
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
- **Stage 5, collections as chapter order** (John, 20 Nov): judge interleaving around the pair, meaning both series alternate near the two issues, not anywhere in the book.
  - A book that interleaves one story but prints others as blocks shouldn't count as chapter order for the blocks. Example: Green Lantern by Geoff Johns Omnibus Vol. 1 interleaves the Sinestro Corps War but prints Recharge #1–5 before Green Lantern (2005) #1–20.
  - Write it into `collections.py`'s rule at stage 5 (in that stage's own research folder); nothing in stage 1 changes.
- **T6** (John, 18 Nov): a row placed after or before another issue by a cited note, keeping its true date; Publication order ignores it; a placement that crosses its own series isn't applied but listed. The design note (`t6-design.md` in the Research-Repo session folder) also gives a clean release order. **Approved, 20 Nov**, with its four recommendations: "between A and B" lands nearest the row's own date; the release date is `date.order` with a citation; "before the epilogue of" places the row before the whole issue; the "Placed after …" line shows. Its own template PR, after T1 + T2.

## Stages (from `PLAN.md`)
| # | Stage | State |
|---|---|---|
| 0 | Setup | done and pushed (15 Nov) |
| 1 | Arc spine | approved (20 Nov); Research-Repo#6 open for John's merge |
| 2 | Core spine (goes live as v1) | — |
| 3 | Green Lantern Corps and New Guardians | — |
| 4 | Spectrum spin-offs | — |
| 5 | Canonical events, with T3 | — |
| 6 | Pre-2004 landmarks | — |
| 7 | Elseworlds (ALT) | — |
| 8 | The look, then the signature skin's deploy | — |
