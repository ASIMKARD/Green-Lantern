# Green Lantern — progress

Built on Pull-List-template v3, copied at template `f7ae723` (15 Nov 2026). The approved plan is
`PLAN.md`; the rules are `CLAUDE.md`. Sessions: Green Lantern #1 (14–15 Nov), its log in Master-Repo
`log/green-lantern-1.md`.

## Where it stands (15 Nov)
- **Stage 0 (setup):** committed on this branch (`59ab9d3` and later), **not pushed yet.**
  - **Why:** the template's v9-frame guard (`47-frame-v9`) failed on the date. John approved the fix as template T0, [ASIMKARD/Pull-List-template#12](https://github.com/ASIMKARD/Pull-List-template/pull/12) (CI green, waiting for his merge).
  - **When T0 is merged:**
    1. copy its three files: `test/layout/lib.js`, `test/layout/ref/capture-frame.js` and `test/layout/47-frame-v9.test.js`;
    2. also its `BUILD-NOTES.md` change;
    3. record the template commit here;
    4. run `node test/run.js` and `npm run test:layout` (expect 1720 and 470, 0 failed);
    5. push this branch and update the Master-Repo log.
- **Stage 1 (arc spine): revised after John's review (15 Nov).**
  - **Where:** Research-Repo `sessions/2026-11-14-green-lantern/`.
  - **The spine:** `spine.py` → `arc-spine-v2.json`.
  - **The built order:** `stage1_order.py BUILD_DIR` → `stage1.dataset.draft.json`, built with this repo's `tools/build.py` → `stage1-order.json`.
  - **The independent pass:** `verify_order.py BUILD_DIR` → `verify-order.json`.
  - **The report:** `report2.py` → `change-report-stage1.md`, `.json` and `arc-spine.html`.
- **Next steps, in order:**
  1. **John approves the revised stage-1 report,** including its same-month order questions.
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

## Decided, not yet built
- **T1:** per-Lantern CORE and the workbook columns. A template PR before stage 2; the design note comes with the stage-1 report.
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
- **Optional T2,** "Lead only" appearances, is offered with T1's design note.

## Stages (from `PLAN.md`)
| # | Stage | State |
|---|---|---|
| 0 | Setup | done (15 Nov) |
| 1 | Arc spine | report sent to John (15 Nov) |
| 2 | Core spine (goes live as v1) | — |
| 3 | Green Lantern Corps and New Guardians | — |
| 4 | Spectrum spin-offs | — |
| 5 | Canonical events, with T3 | — |
| 6 | Pre-2004 landmarks | — |
| 7 | Elseworlds (ALT) | — |
| 8 | The look, then the signature skin's deploy | — |
