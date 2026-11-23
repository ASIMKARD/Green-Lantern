# Green Lantern — progress

Built on Pull-List-template v3: copied at template `f7ae723`, then template T0 at `9aac63d` (15 Nov 2026), then T1 + T2 at `b9a0128` (21 Nov), then T7 at `d5c1585` (22 Nov). The approved plan is
`PLAN.md`; the rules are `CLAUDE.md`. Sessions: Green Lantern #1 (14–21 Nov), its log in Master-Repo
`log/green-lantern-1.md`.

## Where it stands (21 Nov)
- **Stage 0 (setup): done and pushed (15 Nov).**
  - It holds template v3 copied in (first at `f7ae723`), then template T0 (`9aac63d`, John merged ASIMKARD/Pull-List-template#12): the v9-frame guard's clock is pinned to each reference's captured day.
  - T0 brought four files: `test/layout/lib.js`, `test/layout/ref/capture-frame.js`, `test/layout/47-frame-v9.test.js` and `BUILD-NOTES.md`. Every other template file is identical to template `main` `9aac63d`, apart from this tracker's own docs.
  - **T1 + T2 copied in (21 Nov),** from template `b9a0128` (John merged ASIMKARD/Pull-List-template#13). Before the copy, every changed file in this repo was checked identical to template T0. The 23 files that aren't this repo's own docs were taken as they are:
    - `app.js`, `tools/build.py`, `tools/build_workbook.py`, `schema/dataset.schema.json`;
    - `BUILD-NOTES.md`, `FEATURE-INVENTORY.md`;
    - the tests and fixtures, including the new `9m-scoped-core` and three `broken/corefor-*` cases;
    - the generated files.
    `CLAUDE.md` takes the template's visibility-list lines. The rebuilt `data.js` is byte for byte the template's (v52, `88308c019615`).
  - The harness gives 1765 assertions (38 suites) and the layout suite 470, with 0 failed in both. Template T0 also gave 1720, so the +45 is T1 + T2's own.
  - **Since stage 2's sub-era 1 (21 Nov) the data is the tracker's own:**
    - `franchise.key` `green-lantern`, with rows in `data/eras/`;
    - the interim icons (an emerald "GL" monogram, until stage 8);
    - `FEATURE-INVENTORY.md` dropped;
    - the starter's generated `data.js` removed before the first build, so the version started at v1.
- **Stage 1 (arc spine): approved by John, 20 Nov.** Revised with the Grand Comics Database's dates (17 Nov) and John's decisions of 18–20 Nov. The research folder is merged: ASIMKARD/Research-Repo#6, `a43c300` (21 Nov).
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
  1. **Done (20–21 Nov): John approved the stage-1 order** and merged Research-Repo#6 (`a43c300`).
  2. **Done (21 Nov): T1 + T2 merged as template `b9a0128` and copied into this repo** (see Stage 0 above). The record of the build follows.
     - **Before the merge:** it was open as ASIMKARD/Pull-List-template#13 (21 Nov). John held it for two changes, now made: a chosen character's picks show at every depth, and a character with no picks doesn't scope. Template branch `claude/awesome-brahmagupta-89pq1z` at `f61f2e9`; harness 1765, layout 470, 0 failed. John merges after his check.
     - **Once John merged it:** copy the changed template files into this repo and record the template commit here and in `CLAUDE.md`. The files: `app.js`, `tools/build.py`, `tools/build_workbook.py`, `schema/dataset.schema.json`, `BUILD-NOTES.md`, `CLAUDE.md`'s visibility list, the tests and fixtures. Then rebuild and run both suites.
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
  3. **Stage 2, sub-era by sub-era (started 21 Nov).** Each sub-era's report goes to John, and its rows are committed only after he approves it (John, 21 Nov).
     - **The research:** Research-Repo `sessions/2026-11-14-green-lantern/`, branch `claude/awesome-brahmagupta-89pq1z` at `d4ae921` (no pull request yet).
       - `appearances.py`: presence, graded by the plan's written rule.
       - `stage2.py`: the sub-era's rows in this repo's layout, from stage 1's approved order. It builds them with this repo's `tools/build.py` and checks the order read back.
       - `verify_order.py --subset`: the independent pass.
       - `report_stage2.py`: the report and the phone page.
       - `rebuild_check_stage2.sh`: the offline rebuild check.
     - **Sub-era 1, Rebirth: approved and committed (21 Nov).** Report: `change-report-stage2-rebirth.md`, plus the phone page.
       - 40 rows: Green Lantern: Rebirth #1–6, Green Lantern (2005) #1–20, Ion #1–12, Guy Gardner: Collateral Damage #1–2.
       - The order equals stage 1's; independent pass 40 checked, 0 mismatches.
       - Rebuilds offline, 10 of 10 files identical.
     - **John's answers (21 Nov):**
       - the per-Lantern picks take arcs rated 5 only ("5 only");
       - the interim icons are used until stage 8 ("Use them").
     - **The commit's steps** (sub-era 1; later sub-eras need only step 1's data files and step 4):
       1. copy `stage2/dataset.json` over `dataset.json`, `stage2/data/eras/` into `data/eras/`, and `stage2/icons/*.png` into `icons/`;
       2. delete the starter's generated `data.js`, so the first build is v1 and the starter's five demo ids aren't treated as saved progress (they lived under the key `starter`);
       3. `git rm FEATURE-INVENTORY.md`; the docs test allows it once the key isn't `starter`; update `CLAUDE.md`'s repo map;
       4. `python3 tools/build.py`, `--check`, the gate, both suites.

       Done: built v1 (`5e2e702217ef`), 40 rows; the gate passed with 0 warnings. Its data is the same as the build the order checks read, apart from the build hash (the icons count in it).
     - **Sub-era 1's commit:** `2e89122`, CI green.
     - **Sub-era 2, the Sinestro Corps War: approved (John, 22 Nov) and committed.**
       - 8 rows: Green Lantern (2005) #21–28; ★ #21–25.
       - The order equals stage 1's; independent pass 48 / 0 mismatches. Sub-era 1's committed file is byte for byte the draft's.
       - Research-Repo `c241ee9`.
       - Tried in a scratch copy: gate 0 warnings, harness 1764, layout 470, 0 failed.
       - No questions.
       - Built v2 (`1bd4f87756fb`, the same hash as the build the checks read); gate 0 warnings.
     - **Per-Lantern picks (John, 22 Nov):** threshold 5 stays. For a Lantern left with few picks (Simon Baz, Jessica Cruz), propose their best arcs by hand, with sources, in that sub-era's report for John to approve (`stage2-decisions.json`, `corefor.hand_picks`).
     - **Sub-era 2's commit:** `813e1c6`, CI green.
     - **Sub-era 3, Secret Origin to Agent Orange: approved by John (22 Nov) and committed after T7.** Built v4 (`c3e542ff1537`); 62 rows in stage 1's order; gate 0 warnings; harness 1764, layout 472, 0 failed.
       - 14 rows: Green Lantern (2005) #29–42.
       - The order equals stage 1's; independent pass 62 / 0 mismatches.
       - ★: Secret Origin (#29–35) and Agent Orange (#39–42).
       - Research-Repo `43c88bd`.
       - **The trial in a scratch copy:** gate 0 warnings, harness 1764, layout 470 with 6 failed.
         - `10-sweep` finds Settings → Mark range's end select (`#bulkTo`) cut off by its section at 320 px (9 px; 46 px with large text) and at 360 px with large text (6 px).
         - A select is as wide as its longest option, and "Secret Origin to Agent Orange" (29 characters) is the longest sub-era name so far. Later names run to 40.
         - The cause is the template's CSS: `.erasel` has no `max-width`, and `.sgrp` keeps "through" and the select on one line.
       - **John chose template change T7 (22 Nov), now ASIMKARD/Pull-List-template#14** (`8fbcc32`, CI green on the push and the PR).
         - `.erasel` and `.sgrp` take `min-width: 0; max-width: 100%`.
         - `10-sweep`'s long-era check now covers every control on the List and in Settings. It was written first and fails on the old CSS.
         - Template harness 1765, layout 472, 0 failed. Sub-eras 1–3 with the fix: `10-sweep` 313, 0 failed.
       - **T7 merged (John, 22 Nov) as template `d5c1585`, and copied in.** Its three files (`styles.css`, `test/layout/10-sweep.test.js`, `BUILD-NOTES.md`) were checked identical to the template's before T7, then taken as they are. The rebuilt data is unchanged.
       - **The steps for sub-era 3** (step 1 is done):
         1. copy the template's `styles.css`, `test/layout/10-sweep.test.js` and `BUILD-NOTES.md` into this repo, and record the template commit here and in `CLAUDE.md`;
         2. copy `stage2/dataset.json` and `stage2/data/eras/5020-secret-origin.json` in (Research-Repo `f397095`);
         3. build, `--check`, the gate, both suites (layout expected 472); commit and push.
     - **Sub-era 3's commit:** `b4a1c27`, CI green.
     - **Sub-era 4, Blackest Night: approved (John, 23 Nov) and committed.** Built v5 (`ed20ba5dc2af`); 72 rows in stage 1's order; gate 0 warnings.
       - 10 rows: Green Lantern (2005) #43–52.
       - The order equals stage 1's; independent pass 72 / 0 mismatches. Sub-eras 1–3's committed files are byte for byte the draft's.
       - ★: the nine Blackest Night chapters. #49 is Tales of the Corps, rated 4.
       - Research-Repo `ff0dc1a`.
       - Tried in a scratch copy: build v5, gate 0 warnings, harness 1764, layout 472, 0 failed.
       - No questions.
     - **Sub-era 4's commit:** `e2791b8`, CI green.
     - **Sub-era 5, Brightest Day: approved (John, 23 Nov) and committed.** Built v6 (`0a55aca6d4df`); 82 rows in stage 1's order; gate 0 warnings.
       - 10 rows: Green Lantern (2005) #53–62, the New Guardians arc, all on the CORE path.
       - The order equals stage 1's; independent pass 82 / 0 mismatches.
       - #61 has no presence: Atrocitus' story, with Hal on the cover only (rev 3976104). It's a note, not a question.
       - Research-Repo `f97aa26`.
       - Tried in a scratch copy: build v6, gate 0 warnings, harness 1764, layout 472, 0 failed.
       - No questions.
     - **Sub-era 5's commit:** `bd70645`, CI green.
     - **Sub-era 6, War of the Green Lanterns: approved (John, 23 Nov) and committed, with event-timeline versions counted.**
       - 11 rows: Green Lantern (2005) #63–67 (★), then Flashpoint: Abin Sur #1–3 and Flashpoint: Hal Jordan #1–3.
       - The order equals stage 1's; independent pass 93 / 0 mismatches.
       - **The question:** whether event-timeline versions count in presence. Hal Jordan (Flashpoint Timeline) leads Flashpoint: Hal Jordan, and only New Earth and Prime Earth versions count today. 12 stage-2 rows depend on it: 5 here, Futures End #1, Future State #1–2.
       - Research-Repo `73e141f`.
       - Tried in a scratch copy: build v7, gate 0 warnings, harness 1764, layout 472, 0 failed.
       - **John's answer: "Count them".** `stage2.py` now counts the timeline class (`stage2-decisions.json`, `presence`), taking the best grade. Sub-eras 1–5 have no timeline matches, and their committed files are still byte for byte the draft's.
       - Flashpoint: Hal Jordan #1–3 show Hal (major); Abin Sur #2 Hal (minor); Abin Sur #1 Green Arrow (cameo). Abin Sur #3 has none of the ten.
     - **Next: sub-era 7, The New 52: to the First Lantern** (22 stage-2 rows). Run `stage2.py new-52` with `GL_REPO` at this branch's latest pushed commit.

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
  - Stage 1's order approved; John merged Research-Repo#6 (`a43c300`).
  - #13 held for two changes:
    - the depths must nest with a character chosen (a bug);
    - John's decision: "if none of the chosen characters has any core picks (for Green Lantern: Green Arrow, the Indigo Tribe, the Star Sapphires), ★ and Barebones fall back to the overall core, as with no character chosen. With several chosen, only those with picks count."
  - Both merged (Research-Repo#6, template #13): "Copy T1 + T2 into Green-Lantern, record the template commit, and start stage 2. Send each sub-era's report to me before its rows are committed."
  - Sub-era 1 (Rebirth), question form:
    - per-Lantern picks, "5 only": a Lantern's picks are the CORE-path issues they're in, plus their lead arcs rated 5;
    - the interim icons, "Use them";
    - "Approved: commit".
- **22 Nov:**
  - Sub-era 2 (the Sinestro Corps War): "Approved: commit".
  - "On per-Lantern picks: keep 5 only, and for a Lantern left with few picks (Simon Baz, Jessica Cruz), propose their best arcs by hand, with sources, in that sub-era's report for me to approve."
  - The Mark range fix: "Template change T7". Sub-era 3: "Approved: commit after fix".
  - T7 merged (#14, `d5c1585`). "T6 after stage 2's sub-eras is fine, but it must be merged before go-live v1."
- **23 Nov:**
  - sub-eras 4 (Blackest Night), 5 (Brightest Day) and 6 (War of the Green Lanterns): "Approved: commit";
  - event-timeline versions in presence (Flashpoint, Futures End, Future State): "Count them". Counterparts from other worlds stay listed, not counted.
- **20 Nov:**
  - Answers: New Guardians #20 before Red Lanterns #20; for T6, Hal Jordan and the GLC: Rebirth #1 just before Green Lanterns: Rebirth #1.
  - T6's design note approved, with the four recommendations.
  - A fix: Green Lantern (2005) #48 comes before Blackest Night #5 (wrongly given the Group A rule).
  - The reading step (`CLAUDE.md`, "Green Lantern's own rules").

## Decided, not yet built
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
- **T6** (John, 18 Nov): a row placed after or before another issue by a cited note, keeping its true date; Publication order ignores it; a placement that crosses its own series isn't applied but listed. The design note (`t6-design.md` in the Research-Repo session folder) also gives a clean release order. **Approved, 20 Nov**, with its four recommendations: "between A and B" lands nearest the row's own date; the release date is `date.order` with a citation; "before the epilogue of" places the row before the whole issue; the "Placed after …" line shows. Its own template PR, after T1 + T2. **When (John, 22 Nov):** after stage 2's sub-eras, and merged before go-live v1.

## Stages (from `PLAN.md`)
| # | Stage | State |
|---|---|---|
| 0 | Setup | done and pushed (15 Nov) |
| 1 | Arc spine | approved (20 Nov); Research-Repo#6 merged (`a43c300`, 21 Nov) |
| 2 | Core spine (goes live as v1) | sub-eras 1–6 committed (21–23 Nov); 7 to go; then T6, merged before go-live v1 |
| 3 | Green Lantern Corps and New Guardians | — |
| 4 | Spectrum spin-offs | — |
| 5 | Canonical events, with T3 | — |
| 6 | Pre-2004 landmarks | — |
| 7 | Elseworlds (ALT) | — |
| 8 | The look, then the signature skin's deploy | — |
