# Green Lantern — the approved plan (John, 15 Nov 2026)

## Context
- **What:** a new Green Lantern reading-order tracker in `ASIMKARD/Green-Lantern`, which today holds only a README.
- **Base:** Pull-List-template v3 (`main` `f7ae723`).
- **Rules:**
  - The spec is Master-Repo `starter/specs/in-progress/Green-Lantern-Tracker-Spec.md` (locked). Where it predates v3, STANDARDS and the template win.
  - It is the first build made to the Essential/Complete Event Standard.
  - Every date is fetched from the DC Database API and cited.
  - Absolute Green Lantern stays out, with a cross-reference note.
  - Each stage ends with a change report John approves before its rows are committed.
  - Read-only: the template, Master-Repo (except this session's log and archive), Absolute. Research-Repo is add-only.

**Checked while planning (read-only):**
- The DC Database API answers here. Python's default client gets 403, so the fetchers send a plain user agent.
- The newest issues are Green Lantern (2023) #40 (Dec 2026, "First Light" part 1) and Green Lantern Corps (2025) #22 (Jan 2027, part 2). Tales of the Green Lantern Corps: Guy Gardner #1 is cover-dated Jul 2026.
- The DC Database has no page yet for a *Lanterns* comic or for Tales of the GLC: Training Day. Stage 1 checks again, and DC's own announcements too.
- There is no Indigo Tribe or Star Sapphire series. Both appear only inside other books (Tales of the Corps, GLC arcs).
- Absolute Green Lantern is in Absolute v10 as 19 rows (`absolute-green-lantern-2025-N`).

## Decisions John made (14 Nov, question forms)
1. **Master-Repo:** this session may add `log/green-lantern-1.md` and `archive/code/green-lantern-1.md`, with one PR that merges itself.
2. **Template T1** (per-Lantern CORE and workbook columns) is done from GL before stage 2, as a template branch and a PR John merges. The exact change is shown to him before the first template edit.
3. **Events:** drafted in GL first, then sent to the template as one PR at the end of stage 5, with the hashes checked equal.
4. **Going live:** after stage 2, then after every stage.
5. **Workbook:** generated.
6. **Reports:** pasteable markdown, the full report in Research-Repo, and a private Artifact page for the phone.
7. **Indigo Tribe and Star Sapphires** are Appearances chips. Tracks exist only where a series does (Red, Orange, Sinestro).
8. **Collected In** goes in each arc's ⓘ blurb, with no template change (no T4).
9. **T3, cross-tracker progress for shared issues (John, 14 Nov):**
   - its own template PR, approved by John first like T1, and built at stage 5;
   - separate from the optional T2;
   - recorded in GL `PROGRESS.md` (at stage 0) and in the first log entry.

   Design below, in "T3".

## 1. The seven Lanterns, and each one's CORE
**What the template does today**
- `characters: [{id, name}]`, and each row has `presence: [{who, grade: major|minor|cameo}]`.
- One chip per character under Filters → Characters → Appearances. Several chips combine as OR, and strands combine with characters as AND.
- The default counts major and minor appearances; "Include cameos" adds cameos.
- It is a browse filter: the banners count the filtered view, marked "filtered". The build rejects an unknown `who` or a bad grade.

**What it lacks**
- **Per-Lantern CORE.** `core` is one true/false per row, drawn as ★. The depth tier (Barebones is the core path) can't be scoped to a character.
- **Lead only.** Major and minor are counted the same, so "John Stewart-centric" can't be told apart from "John appears".
- **Workbook columns.** The Reading Order sheet has no presence, importance or strand columns.
- **Collected In** and **digital availability.** There are no fields for them, and rows and arcs refuse unknown keys.

**The data**
- Characters: `hal-jordan`, `john-stewart`, `guy-gardner`, `kyle-rayner`, `simon-baz`, `jessica-cruz`, `jo-mullein`, and `green-arrow` (the spec's presence flag for Hard-Traveling Heroes).
- Grades come from each issue page's Appearances section, by one written rule:
  - **Featured** → major;
  - **on panel elsewhere** → minor;
  - **marked cameo, or only in a flashback** → cameo;
  - **mentioned only** → no tag.
- CORE and landmark rows are checked by hand.

**Template change T1 (approved route: from GL, before stage 2).**
- **Data:** `coreFor: [character]` on rows. The build checks that each name is a character the row has as major or minor.
- **App:** with a Lantern chip on, ★ and the Barebones depth show that Lantern's picks; with none, the overall CORE.
- **Workbook:** Presence, Importance and Strands columns in the Reading Order sheet.
- **How it's built:** through the capability map, with a 9f visibility row and tests, and with each new check proved by putting the bug back.
- **Where:** template branch `claude/awesome-brahmagupta-89pq1z`. Template `PROGRESS.md` is updated, and John merges the PR. GL then copies the changed files and records the template commit.
- **Optional T2, a "Lead only" appearance step,** is offered with T1's design note, for John to take or leave.
- **Until T1 lands,** the per-Lantern picks wait in the stage reports, because the schema refuses `coreFor`.

## 2. Canonical events
**What the template does today**
- `events/` in the template is the master and holds no events yet.
- The tracker lists `events: [{id, era, arc}]`. Chapters merge on `issueId`, and the tracker's own row wins.
- A chapter is Essential when it is `core`, when it is tagged `green-lantern` (`franchise.eventRelevance`), or when the tracker already has it.
- Each built event carries the sha256 of its file, but nothing compares that with the template's copy.

**Proposal**
- Draft each event in Research-Repo (`sessions/2026-11-14-green-lantern/events/`).
- On approval, commit it to the tracker's `events/<id>.json` and propose the same bytes to the template's `events/` in one template PR at the end of stage 5. Nothing reaches the template before that PR.
- A stage-5 check confirms that the tracker's and the template's hashes match.

**GL keeps its own rows** for every chapter it cares about: the Blackest Night minis and the GL and GLC chapters. Those rows carry the Lantern presence and the arc's depth.
- The event files list the tie-ins with no presence. A Batman or Flash tracker would refuse an unknown `who`.
- Each event names its own arc and depth, so Complete-only tie-ins follow the depth filter rather than the build's default, the broadest depth.

## T3 — cross-tracker progress for shared issues (stage 5; design note before the template PR)
**The rule (John):**
- An issue marked read or skipped in any tracker counts in every tracker that has the same `issueId`.
- Each tracker writes only its own storage. It reads the others' saves on asimkard.github.io and never writes them.

**How a tracker finds the others' saves**
- All trackers share one origin, so in one browser they share one localStorage.
- **Publishing:** each T3 tracker also keeps, in its own namespace, `<key>:v3:shared`: `{v:1, name, m: {issueId: [state, time]}}`.
  - It is keyed by `issueId`, so a migrated tracker whose ids are old sort keys still matches.
  - It is written with the existing 400 ms save and flushed on `pagehide`.
- **Reading:** at boot, a tracker lists every key ending in `:v3:shared` other than its own, keeps only the `issueId`s it has, and builds an overlay.
- **Refreshing:** the overlay is rebuilt on the `storage` event (another tab changed something) and when the page is shown again.
- **Never read:** other trackers' native progress keys. A tracker without T3 contributes nothing until it is updated.

**When two disagree**
- **Proposed: the latest mark wins,** by its time, across every tracker, unmarking included. So unmarking in one tracker clears the mark everywhere.
- On a tie: read > skipped > reading > unread.
- **The alternative John can pick in the note:** "read always wins", where unmarking needs doing in each tracker.
- **What the reader sees:** a row counted from elsewhere shows its state with an accessible note, "read in Absolute". Progress, time left and finish-by count it.

**Undo, Clear all, backups and sync codes**
- **Undo** restores this tracker's own previous marks and its shared entries. It can't change another tracker's.
- **Clear all** clears only this tracker's progress and its shared entries. The confirmation says that rows read in other trackers stay counted. Undo restores.
- **Backups, copy-codes, `#sync=` links and the QR** carry only this tracker's own marks.
  - The backup and copy-code gain per-mark times, optional and tolerant: older codes import with the import time.
  - The compact QR is unchanged.
  - Merge and Replace never write another tracker's keys.
- **Settings → Sync:** a status line, "Counting progress from: Absolute (N shared issues)". It is shown only when another tracker's save shares an issue, decided by a capability computed at boot.

**Limits**
- The shared indexes count against the origin's single ~5 MB localStorage quota: about 30 KB per 1,000 rows.
- A failed write never breaks the tracker's own save.

**Tests**
- **jsdom:** merge and tie rules, Undo, Clear all, backup and sync round trips, and a spy proving no write outside the tracker's own namespace.
- **Chromium (`test/layout/`):**
  - two fixture trackers with different keys, served on one origin at `/a/` and `/b/`, sharing one event;
  - mark in A and see it in B (reload and live `storage` event); unmark in B and see it clear in A;
  - Clear all in A leaves B's keys byte-identical;
  - each worker controls only its own scope.
- **Unchanged:** Absolute's own skin and every existing tracker stay unchanged until each is updated. 47-frame-v9 and the rest stay green.

**iPhone test (sent with the PR)**
1. **Safari, two tabs.** Open trackers A and B, which share an issue. Mark it in A, switch to B: it should show read, "read in A". Unmark it in B, return to A: it should be unread.
2. **Two home-screen apps.** Add A and B to the Home Screen, mark the issue in A's app, open B's app, and read Settings → Sync's status line. iOS may give each home-screen app separate storage, in which case B sees nothing. The fallback is the copy-code or QR.
3. **Safari against a home-screen app:** the same check.

The test needs two T3 trackers sharing an `issueId` on the site. That is a real pair once a second tracker carries T3, or a small test pair deployed for the purpose; where it goes is John's call in the design note.

## 3. Workbook and the stage-1 review
- **Workbook:** the recommendation is to generate it (`deliverables.workbook` left on). It costs nothing, `--check` covers it, and the spec asked for Excel.
- **Change reports:**
  - Each one is markdown text, short enough to paste into the Master Chat.
  - The full report is `change-report-<stage>.md` and `.json` in the Research-Repo session folder.
  - Optionally there is also a private Artifact page that reads well on a phone: sub-eras as sections, and for each arc its issue range, dates, writer and artist, collection and source.
- **Stage 1 reviews the arc spine:**
  - the sub-eras, each arc with its exact issue range, a one-line blurb, importance and depth, and its source pages;
  - and the period bands and era ranks.

## 4. The look (stage 8; mock-ups before any build)
- An emerald signature skin on the x frame (`franchise.signature.frame: "x"`). Pull stays the X-Men copy, untouched.
- **Spectrum options** (red, orange, yellow, green, blue, indigo, violet) as a swatch row, the template's swatch pattern. This is a new Look setting, so it needs template change **T5**:
  - token-only blocks;
  - contrast in 40-look for every skin × paper × 64 eras;
  - a capability row and a row in the visibility suite.
- **Mock-ups:** an Artifact page with 2–3 emerald directions at 390 px (landing, an era open, rows, Reading, Settings → Look) and the seven swatches. They are built from the template's real tokens, and contrast is measured, not eyeballed.
- **Icons:** original emerald icons (no DC emblem artwork), shown with the first go-live.

## 5. The stages
Every stage follows the same loop:
1. Research in Research-Repo `sessions/2026-11-14-green-lantern/`, using copies of Absolute's `fetch_dcdb.py`, `fetch_lists.py` and `extract.py` extended with Appearances, run with `python3 -I` and with the cache committed.
2. Write a draft and the change report.
3. John approves.
4. The rows go into `data/eras/<rank>-<era>.json`.
5. Run `build.py`, the gate, the harness and the layout suite, all green, and report the counts.
6. Commit, push, update the Master-Repo log, and update `PROGRESS.md`.

**How rows are written**
- **Dates:** `date: {cover, onsale only when the page states it, source: "DC Database, \"Green Lantern Vol 4 1\" (rev N, fetched 2026-11-DD)"}`.
- **Credits:** writer and artist from every issue page (`strictCredits` on).
- **`issueId`:** e.g. `green-lantern-2005-1`, `green-lantern-2011-23-1`, `green-lantern-corps-2006-annual-1`. Titles name the volume: "Green Lantern (2005) #1".

| # | Stage | Contents | Rows (est.) |
|---|---|---|---|
| 0 | Setup | Template copied into GL with fresh history; GL README, CLAUDE.md and PROGRESS.md; still the starter data, so CI is green | 0 |
| 1 | Arc spine | Sub-eras from Rebirth (2004) to today, every arc with its issue range; current status checked | ~150 arcs |
| 2 | Core spine | GL: Rebirth; GL 2005, 2011, 2021 and 2023; Green Lanterns; Hal Jordan and the GLC; The Green Lantern and Season Two; Far Sector; War Journal; Ion; the Flashpoint GL minis; specials. One report per sub-era | ~370 |
| 3 | Corps | GLC 2006, 2011 and 2025; Recharge; Emerald Warriors; New Guardians; Lost Army; Edge of Oblivion; War of the GLs: Aftermath | ~200 |
| 4 | Spectrum | Red Lanterns, Larfleeze and its Christmas special, Sinestro (2014), Tales of the Sinestro Corps, Rage of the Red Lanterns, Tales of the Corps | ~90 |
| 5 | Events (+ T3) | T3's design note → John's approval → template PR → GL copies it; then Sinestro Corps War, Blackest Night (every line-wide tie-in), Brightest Day, War of the GLs, Wrath of the First Lantern; to verify: Rise of the Third Army, Lights Out, Godhead, Uprising, Starbreaker Supremacy, First Light | ~200 new |
| 6 | Landmarks | Showcase #22–24, Sinestro's and Guy's debuts, Hard-Traveling Heroes incl. #87, Tygers and the Moore shorts, Emerald Dawn, Ganthet's Tale, Emerald Twilight, Kyle's debut, others verified | ~50 |
| 7 | Elseworlds (ALT) | Earth One, Evil's Might, Dragon Lord, 1001 Emerald Nights, Willworld, the 2002 Brightest Day, Blackest Night, and others verified | ~30 |
| 8 | Look and deploy | Mock-ups, T5, the signature skin, icons | — |

**Total about 950 rows (850–1,150).**

**Structure**
- **Bands are the eras of the DC line;** eras are the sub-eras.
  - Modern eras take ranks from 5000, spaced 10.
  - The landmark eras take 4600–4900, spaced 100, so the later growth back to 1959 slots in without renumbering.
  - Elseworlds is the last era, rank 9000.
- **Strands (tracks):** Green Lantern, Corps, Red Lanterns, Larfleeze, Sinestro. Each issue has one home strand, its publication.
- **Characters:**
  - the seven Lanterns;
  - Green Arrow;
  - the Indigo Tribe and the Star Sapphires as groups, graded by the same rule.
- **Types:** MAIN, SOLO, MINI, SPIN-OFF and EVENT (Pull's colours), plus LANDMARK.
- **Landmarks** are Optional except the CORE turning points. A reader can start at Rebirth with "Mandatory only".
- **Absolute Green Lantern:**
  - a GAPNOTE row in the current sub-era: "Absolute Green Lantern (2025–) is in the Absolute tracker · asimkard.github.io/Absolute/";
  - plus a legend line;
  - no template change.
- **Line-wide DC events** (Final Crisis, Forever Evil, DC K.O. …) are not GL canonical events. Their GL issues sit in the spine with a note.

**Sessions: about 8 (6–10).**
- GL #1: setup and stage 1.
- GL #2–3: stage 2.
- GL #4: stages 3–4.
- GL #5–6: stage 5 and T3.
- GL #7: stages 6–7.
- GL #8: stage 8.
- Plus template work for T1 and T5, unless it goes into Template #6.

## 6. Going live
- **Recommended:** the first deploy after stage 2 (v1, shared skins, Pull by default). After that, each stage's PR goes live when John merges it (v2, v3 …).
- **Before each go-live PR,** the branch's `data.js` is rebuilt against `main`'s, so the version rises by one per deploy and starts at v1.
- **After the first merge,** John turns on Pages (main, root): asimkard.github.io/Green-Lantern/. Then every file is verified live by hash, ~100 s after the push.

## This session (Green Lantern #1)
1. After approval: open Master-Repo `log/green-lantern-1.md` and `archive/code/green-lantern-1.md` (the archive written by a script that never prints transcript text). They go on branch `claude/awesome-brahmagupta-89pq1z` from the latest `main`, with one PR that merges itself.
2. Stage 0 in GL on `claude/awesome-brahmagupta-89pq1z`: run `npm ci`, `build --check`, the gate and both suites, commit and push. Update the log.
3. Stage 1 research and the arc-spine change report: markdown in chat, the full `.md` and `.json` in Research-Repo, and an Artifact page. Commit the Research-Repo session folder and push it to its session branch, with one PR per stage for John to merge, as Absolute's sessions did. Update the log.
4. Write T1's design note (the exact schema, build, app and workbook change) to go with the stage-1 report. **Stop for John's review of both.**
5. If the session runs long, stop after a finished step and write in `PROGRESS.md` where the next one begins.

**Next sessions:** T1 in the template (PR) → stage 2, sub-era by sub-era → go-live v1 (GL PR; John turns on Pages) → stages 3–4 → T3 (design note, John's approval, template PR) with stage 5 → stages 6–8, each going live on merge.

**Recording T3:** GL `PROGRESS.md` (written at stage 0) gets a "Decided, not yet built" section naming T3 and its stage. The first Master-Repo log entry records it as John's decision of 14 Nov, in his words.

## Verification (each stage)
- `python3 tools/build.py --check`, `python3 tools/verify_gate.py`, `node test/run.js` and `npm run test:layout`: 0 failures, with the counts reported.
- Spec checks, run from the session folder:
  - one home strand per issue;
  - presence names only the eight characters;
  - every chapter has its role and relevance;
  - no issue claimed twice by an event and its series;
  - every date has a DC Database citation, with no derived or recalled dates.
- At go-live, every file is verified live by hash.
