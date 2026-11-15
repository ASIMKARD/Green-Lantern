# Green Lantern — progress

Built on Pull-List-template v3, copied at template `f7ae723` (15 Nov 2026). The approved plan is
`PLAN.md`; the rules are `CLAUDE.md`. Sessions: Green Lantern #1 (14–15 Nov), its log in Master-Repo
`log/green-lantern-1.md`.

## Where it stands
- **Stage 0 (setup): built and tested, committed locally, not pushed (15 Nov).**
  - Harness: 1720 assertions, 0 failed.
  - Layout suite: 468 assertions, 2 failed, both in the template's `47-frame-v9`. The cause is in the template, and today's date sets it off:
    - the sig-v9 fixture's "finish by" line is worked out from today;
    - its reference was recorded on 28 Oct, when it read "finish by Jan 2027", 107 px wide;
    - since 14 or 15 Nov it reads "Feb 2027", 107.7 px wide (measured with Chromium's clock pinned to each date).
  - The template's CI was green on 13 Nov (`f7ae723`). It will fail on its next push, as will any tracker that runs the guard.
  - **The fix is a template change, waiting for John:** pin the clock in the v9-frame measurement to the reference's `captured` date. Stage 0 is pushed once it is green.
  - The template is copied in with fresh history.
  - Green Lantern's own `README.md`, `CLAUDE.md`, `PROGRESS.md` and `PLAN.md` are written.
  - The data is still the template's starter demo (`franchise.key` `starter`), so CI runs green until stage 2 replaces it.
  - **The template's `FEATURE-INVENTORY.md` stays too, until stage 2.** The docs test expects it while the key is `starter`. Stage 2 drops it when the key becomes `green-lantern`.
- **Stage 1 (arc spine): researched; the change report is waiting for John (15 Nov).**
  - Research-Repo `sessions/2026-11-14-green-lantern/`, pushed (`da65eda`), PR ASIMKARD/Research-Repo#5.
  - The spine is 168 arcs over 714 issues, in 13 sub-eras (ranks 5000–5120) and 6 bands:
    - the report: `change-report-stage1.md` and `.json`;
    - the data: `arc-spine.json`;
    - the phone page: `arc-spine.html`.
  - T1's design note is `t1-design.md`, which also covers the date bug (T0).
- **Where the next step begins:**
  1. **John:** approve the stage-1 report (or change it) and T1's design (with or without T2), and decide T0.
  2. **T0, then T1, on the template's branch:**
     - T0 first: pin the clock in `test/layout/ref/capture-frame.js` `measureAll`, and its use in `test/layout/47-frame-v9.test.js`, to the reference's `captured` date.
     - Then T1: `schema/dataset.schema.json` (`rows[].coreFor`), `tools/build.py` (validation, `issueCoreFor`), `app.js` (`HAS.coreFor`, ★ and Barebones scoped to the chosen Lanterns), `tools/build_workbook.py` (four columns), and tests in `20-build`, a new `9m-scoped-core`, `9f-visibility` and `24-workbook`.
  3. **Then stage 0 is pushed here** once the template fix is copied in and both suites are green.
  4. **Stage 2 starts** with `dataset.json`:
     - the franchise is `green-lantern`, and `FEATURE-INVENTORY.md` is dropped;
     - the approved eras, periods and arcs from `arc-spine.json` go in;
     - then the rows of sub-era 5000 (Rebirth) in `data/eras/5000-rebirth.json`, with presence graded from each issue page's Appearances section.

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
