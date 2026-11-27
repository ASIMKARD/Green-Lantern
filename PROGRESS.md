# Green Lantern — progress

Built on Pull-List-template v3: copied at template `f7ae723`, then template T0 at `9aac63d` (15 Nov 2026), then T1 + T2 at `b9a0128` (21 Nov), then T7 at `d5c1585` (22 Nov), then T6 at `e21c338` (27 Nov). The approved plan is
`PLAN.md`; the rules are `CLAUDE.md`. Sessions: Green Lantern #1 (14–26 Nov) and Green Lantern #2 (26 Nov on), their logs in Master-Repo
`log/green-lantern-1.md` and `log/green-lantern-2.md`.

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
     - **Sub-era 6's commit:** `0cad433`, CI green.
     - **Sub-era 7, The New 52: to the First Lantern: approved (John, 23 Nov) and committed.** Built v8 (`2e8726b1e99e`); 115 rows in stage 1's order; gate 0 warnings.
       - 22 rows: Green Lantern (2011) #1–20, #0 and Annual #1.
       - The order equals stage 1's; independent pass 115 / 0 mismatches.
       - One numbering exception, as in stage 1: #0 after #12, flagged `SPECIAL_NUMBERING`.
       - ★: Rise of the Third Army and The End. They are already Simon Baz's picks, so no hand-picks are needed.
       - Research-Repo `ff1694a`; it rebuilds offline, 16 of 16 (its commit message says 17 by mistake).
       - Tried in a scratch copy: build v8, gate 0 warnings, harness 1764, layout 472, 0 failed.
       - No questions.
     - **Sub-era 7's commit:** `f314550`, CI green.
     - **Sub-era 8, Lights Out to Godhead: approved (John, 23 Nov) and committed.** Built v9 (`75494e07735f`); 142 rows in stage 1's order; gate 0 warnings.
       - 27 rows: Green Lantern (2011) #21–40, #23.1–23.4, Annuals #2–3, and Green Lantern: Futures End #1.
       - The order equals stage 1's; independent pass 142 / 0 mismatches.
       - No ★: stage 1 rated none of it Barebones.
       - #23.2 has no presence: Mongul's origin, with Hal on the cover only (rev 3837118).
       - Research-Repo `2e740c4`; it rebuilds offline, 17 of 17.
       - Tried in a scratch copy: build v9, gate 0 warnings, harness 1764, layout 472, 0 failed.
       - No questions.
     - **Sub-era 8's commit:** `e0327c8`, CI green.
     - **Sub-era 9, Renegade and the Lost Army: approved (John, 25 Nov) and committed.** Built v10 (`c9a1ff56bc0b`); 155 rows in stage 1's order; gate 0 warnings.
       - 13 rows: Green Lantern (2011) #41–52 and Annual #4. Hal alone; no ★.
       - The order equals stage 1's; independent pass 155 / 0 mismatches.
       - Research-Repo `c27e613`; it rebuilds offline, 18 of 18.
       - Tried in a scratch copy: build v10, gate 0 warnings, harness 1764, layout 472, 0 failed.
       - No questions.
     - **Sub-era 9's commit:** `f722963`, CI green.
     - **Sub-era 10, Hal Jordan and the Corps; Green Lanterns: approved (John, 25 Nov: "Approved: commit now") and committed.** Built v11 (`49f0dc8d2369`); 265 rows in stage 1's order; gate 0 warnings.
       - 110 rows: Green Lanterns: Rebirth #1, Green Lanterns (2016) #1–57 and Annual #1, Hal Jordan and the GLC: Rebirth #1 and #1–50.
       - The order equals stage 1's; independent pass 265 / 0 mismatches. No ★, so no picks at threshold 5.
       - Green Lanterns #26 has no presence: Rami's and Volthoom's origin (rev 3985444).
       - Research-Repo `d67714a`; it rebuilds offline, 19 of 19, twice.
       - Tried in a scratch copy: build v11, gate 0 warnings, harness 1764, layout 472, 0 failed.
       - **Simon Baz's and Jessica Cruz's hand-picks (John, 22 Nov) are not proposed yet.**
         - The DC Database has no reading list for either.
         - John allowed the critic and review hosts on 25 Nov (environment "1"). The session's safety check then refused the fetch twice, by script and through the web-reading tool.
         - Nothing is proposed from search summaries or memory. John decides how to go on.
       - **John's answer on the hand-picks: "I'll name the arcs".** He named them (Green Lanterns (2016): A Day in the Life #15, Ghosts of the Past #44–47, The First Ring #22–26, The Phantom Lantern #9–14; Comic Book Roundup critic averages weighted by review count). **Applied in their own change (built v12, `de68cf002a93`):**
         - 14 rows each: Green Lanterns #10–15, #22–25 and #44–47.
         - #9 (both cameos) and #26 (neither in it) can't be picks and are listed.
         - The tracker now has 23 picks for Simon and 15 for Jessica.
         - The source is John's reading of Comic Book Roundup (26 Nov); this session didn't fetch it.
     - **The picks' commit:** `137f9b3`, CI green.
     - **Sub-era 11, The Green Lantern and Far Sector: approved after one fix (John, 26 Nov) and committed.** Built v13 (`30c1a0f55b3e`); 304 rows in stage 1's order; gate 0 warnings.
       - 39 rows: The Green Lantern (2019) #1–12 and Annual #1, Blackstars #1–3, Far Sector #1–12, Season Two #1–10, the 80th Anniversary Special.
       - The order equals stage 1's; independent pass 304 / 0 mismatches.
       - ★: 33 rows (Hal's Morrison run, and Far Sector for Jo).
       - 26 counterpart lines from other worlds are listed, not counted.
       - Research-Repo `22efa48`; it rebuilds offline, 20 of 20.
       - Tried in a scratch copy: build v13, gate 0 warnings, harness 1764, layout 472, 0 failed.
       - **John's fix:** Season Two #10 loses Guy Gardner's cameo.
         - Guy's only line there is "Guy Gardner's Counterpart", linked to the generic Guy Gardner page (a disambiguation), so it's another world's counterpart.
         - A link with no reality now counts only through the DC Database's redirect. 29 such lines are now listed, not counted; only this tag changed.
       - **John's check:** every presence tag on every row built comes from a New Earth, Prime Earth or event-timeline link. 783 tags on 304 rows, 0 failures. It fails on the old rule (Season Two #10's Guy).
     - **John's standing rule (26 Nov):**
       - commit a sub-era without asking when its report has the order equal to stage 1's, the independent pass at 0 mismatches and no questions;
       - still ask about questions, decisions and every template PR;
       - stop before the go-live PR, so all of stage 2 can be checked in one pass (`CLAUDE.md`).
     - **Sub-era 12, Future State and Infinite Frontier: committed without asking (John's 26 Nov rule; a clean report).**
       - 18 rows: Future State: Green Lantern #1–2, Season Two #11–12, Green Lantern (2021) #1–12 and Annual #1, Dark Crisis: Worlds Without a Justice League – Green Lantern #1.
       - The order equals stage 1's; independent pass 322 / 0 mismatches; presence check 853 tags, 0 failures.
       - No ★. Built v14 (`fad370f7dadb`); gate 0 warnings.
       - **Notes:**
         - Future State's Lanterns count under the timeline rule.
         - Dark Crisis' dream-world Kyle is listed as another world's.
         - Jessica leads only the one-issue Annual (rated 2), so no hand-pick is proposed.
         - The Annual's placement note waits for T6.
     - **Sub-era 12's commit:** `8903ef5`, CI green.
     - **John's instructions (26 Nov)** (`CLAUDE.md`): back to back; commit clean sub-eras (up to three together) without waiting; three checks in every report; questions batched (four, or the end of stage 2); stop before the go-live PR.
       - The three checks are `stage2_checks.py`, in every sub-era's report, with every sub-era in its own section of `change-report-stage2.md`.
       - **Over stage 2:** 381 of 381 rows match their saved pages; every collection difference has its reason; 2 plain-text entries.
     - **Sub-era 13, Dawn of DC to today: approved (John's answers, 26 Nov) and committed.** Built v15 (`d056649cfacb`): 382 rows, 381 issues and the gap note; gate 0 warnings.
       - 59 rows: Green Lantern (2023) #1–40, War Journal #1–12, Knight Terrors: Green Lantern #1–2, and five one-shots and specials.
       - The order equals stage 1's; independent pass 381 / 0; presence check 1,026 / 0. No ★.
       - War Journal #1–2's credits are read from their pages (listed under an untitled story 2).
       - The Absolute Green Lantern gap note and legend line follow the approved plan.
       - The current status was checked 26 Nov: Green Lantern #41's page appeared as a stub; #42–43, Training Day and Lanterns have none.
       - Research-Repo `080c2f5`; it rebuilds offline, 23 of 23.
       - Tried in a scratch copy with all 13 sub-eras: v15, gate 0 warnings, harness 1764, layout 472, 0 failed.
       - **John's answers:**
         - Green Lantern (2023) #41: "Hold it, and check its page again in the pass before go-live: add it then if the page lists the story, on-sale date and appearances." It is recorded in `stage2-decisions.json` (`before_go_live`).
         - The gap note: June 2025, after Green Lantern (2023) #22.
   - **Stage 2 is complete: 13 sub-eras, 381 issues and one gap note** (21–26 Nov).
     - All 381 rows match their saved pages, and the presence check gives 1,026 tags, 0 failures.
     - `change-report-stage2.md` (Research-Repo) has every sub-era in its own section, for John's one-pass check.
   - **T6: done (Green Lantern #2, 26–27 Nov).**
     - **The template PR:** ASIMKARD/Pull-List-template#15 (`6d05dd8`), merged by John on 27 Nov as `e21c338`.
       - Harness 1844 and layout 490 in the template, 0 failed.
       - 32 bugs put back, each caught.
       - Five calls beyond the design, listed in the PR for John: a placed row must be in its target's era; gap notes keep their place in the release order; Table view leaves the line out; the order-date columns and the About copy; `date.order` beside `date.onsale` fails.
     - **Copied in (27 Nov):** every code file T6 changed was first checked identical to template `d5c1585`, then taken as it is from `e21c338`:
       - `app.js`, `styles.css`, `tools/build.py`, `tools/build_workbook.py`, `schema/dataset.schema.json`, `BUILD-NOTES.md`;
       - the tests and fixtures, including the new `9n-placement` and 11 `broken/` cases.

       `CLAUDE.md` takes the template's T6 data rule and records `e21c338`.
     - **Applied (Research-Repo `sessions/2026-11-26-green-lantern-2/`: `t6_apply.py`, `t6-placements.json`):**
       - **`date.order` on all 359 rows the DC Database leaves undated.** Each takes the ordering date stage 1 used: 358 from the GCD record (cited from the cached API response) and 1 from John's DC.com citation (the World's Finest Special). The 22 rows with a DC Database on-sale date keep it.
       - **`place` on two rows:**
         - Hal Jordan and the GLC: Rebirth #1, just before Green Lanterns: Rebirth #1 (John, 20 Nov);
         - Green Lantern (2021) Annual #1, just before #5 (the note says between #2 and #5; T6's first choice puts it nearest its own date).
       - Nothing else in the data changed (checked row by row).
     - **Built v16 (`4958a2209566`).** `--check` is fresh, and the gate gives 0 failures and 0 warnings. Harness 1843 and layout 490, 0 failed.
     - **`t6_check.py` → `t6-check.json`:** the order rebuilt from stage 1's approved order with the two placements equals the build, 381 of 381.
       - Each placed row sits just before its target, in its era.
       - Every issue has a release date.
       - Publication order has 0 neighbouring pairs in one cover month against their release dates (3 before T6), with 12 rows moved.
       - The Absolute gap note stays after Green Lantern (2023) #22 in both orders.
       - On the build before T6 the check fails: the reading order, both placements, and 359 rows undated.
     - **Wait for their stage:**
       - Blackest Night #0, after Green Lantern (2005) #43 at stage 5, replacing its `sortDate`;
       - Tales of the GLC: Guy Gardner #1, before Green Lantern Corps (2025) #13 at stage 3.
     - **Listed, not applied:**
       - Green Lanterns (2016) #14 and #50, which cross their own series;
       - the hedged Green Lantern Corps (2025) #1–3 note.
   - **T6's design** (approved 20 Nov), with four recommendations (`t6-design.md`):
     - "between A and B" lands nearest the row's own date;
     - the release date is `date.order` with a citation;
     - "before the epilogue of" places a row before the whole issue;
     - the "Placed after …" line shows.

   - **Next: the pass before go-live** (Green Lantern #2):
     - Check Green Lantern (2023) #41's page again and add it if it is complete (John, 26 Nov).
     - Check the current status again.
     - Stop before the go-live PR for John's one-pass check of all of stage 2.
       - **Fixed:** `stage2.py` lists a sub-era's volumes in reading order. Ordering them by first cover date left ties to Python's set order, which changes run to run.
       - **Done in sub-era 13:** Green Lantern: War Journal #1–2's credits were read from their pages (listed under an untitled story 2).

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
  - sub-eras 4 (Blackest Night), 5 (Brightest Day), 6 (War of the Green Lanterns), 7 (The New 52) and 8 (Lights Out to Godhead): "Approved: commit";
  - event-timeline versions in presence (Flashpoint, Futures End, Future State): "Count them". Counterparts from other worlds stay listed, not counted.
- **26 Nov:**
  - sub-era 11: "Commit after one fix": Season Two #10 loses Guy Gardner's cameo (a counterpart linked to the generic Guy Gardner page); add a check that every presence tag comes from a main-world or event-timeline link, and run it on all committed rows;
  - the standing rule for stage 2's sub-eras (`CLAUDE.md`, "Green Lantern's own rules");
  - the end-of-stage-2 form: Green Lantern (2023) #41 is held, to be checked again in the pass before go-live; the gap note sits in June 2025;
  - later the same day, five instructions: the fix (already made); work back to back, committing clean sub-eras (up to three together) without waiting; three checks in every sub-era report; questions together at four or the end of stage 2; stop before the go-live PR.
- **25 Nov:**
  - sub-era 9 (Renegade and the Lost Army): "Approved: commit";
  - adding seven hosts to environment "1" for the hand-picks' sources (approved);
  - sub-era 10: "Approved: commit now", the hand-picks to follow as a separate, reported change;
  - the hand-picks' sources: "I'll name the arcs". He named them: A Day in the Life (#15), Ghosts of the Past (#44–47), The First Ring (#22–26) and The Phantom Lantern (#9–14), "the four highest-rated arcs by Comic Book Roundup's critic averages, weighted by review count". "Record them as my decision with that source."
- **20 Nov:**
  - Answers: New Guardians #20 before Red Lanterns #20; for T6, Hal Jordan and the GLC: Rebirth #1 just before Green Lanterns: Rebirth #1.
  - T6's design note approved, with the four recommendations.
  - A fix: Green Lantern (2005) #48 comes before Blackest Night #5 (wrongly given the Group A rule).
  - The reading step (`CLAUDE.md`, "Green Lantern's own rules").
- **26 Nov (Green Lantern #2):**
  - Question form: the Master-Repo log and archive for Green Lantern #2 are approved.
  - The session's five steps:
    1. T6 with his four choices, as a template PR with bug-back proofs, pasted to him before he merges;
    2. after the merge, copy it in and apply the placements whose issues are in the tracker, plus the release order from the GCD dates. The rest wait for their stage; Green Lanterns #14 and #50 and the hedged Green Lantern Corps (2025) #1–3 note stay listed;
    3. the pass before go-live (Green Lantern (2023) #41's page, the current status);
    4. a Research-Repo PR for stage 2's work;
    5. stop before the go-live PR and send its summary.
- **27 Nov:** John merged T6, ASIMKARD/Pull-List-template#15, as `e21c338`.

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
| 2 | Core spine (goes live as v1) | **all 13 sub-eras committed (21–26 Nov)**; T6 merged (`e21c338`) and applied (27 Nov); next the pass before go-live; stop before the go-live PR |
| 3 | Green Lantern Corps and New Guardians | — |
| 4 | Spectrum spin-offs | — |
| 5 | Canonical events, with T3 | — |
| 6 | Pre-2004 landmarks | — |
| 7 | Elseworlds (ALT) | — |
| 8 | The look, then the signature skin's deploy | — |
