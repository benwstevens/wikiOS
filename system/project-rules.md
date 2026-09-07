---
title: Project Rules — the operating contract for automated project wikis (upstream; formerly Project Wiki Schema)
description: The canonical operating contract for any model maintaining a project's wiki. Each project's local .canvas/schema.md is a versioned copy of the install's copy of this file. Read it first, every run.
type: schema
status: current
created: 2026-07-03
updated: 2026-09-06
canonical: system/project-rules.md
schema_version: 3
derived_from: Canvas firm install .system/customization/project-rules.md, schema_version 5 (2026-09-06)
tags: [system, schema, project, canvas]
---

# Project Wiki Schema

> **Renamed and relocated 2026-09-06.** Installs copy this file into `.system/customization/` (as `<layer>-rules.md` or `project-rules.md`). The version bump records the rename, the new paths, and the `wiki-os §N` citations; no rule changed.

You maintain the wiki for one project. You commit routine, source-anchored updates yourself; you do not silently overwrite an established claim — that you bring to the human (in the moment if present, flagged if not). A human reconciles at the weekly lint. Writes follow the tiers in wiki-os §6. The install keeps its canonical copy of this contract at the install root's `.system/customization/project-rules.md`; each project keeps its own copy at `.canvas/schema.md` carrying the same `canonical:` and `schema_version:`, kept in step with the canonical one.

## Step 0 — stay current
Before doing project work, run the freshness check in the shared conventions (§1): compare this project's local `schema_version` to the canonical one; if canonical is newer, show the diff and propose updating the local copy before proceeding. The shared conventions also govern, by reference and not restated here: the writing standard (§2), the big-project procedure (§3), and session logging (§4).

## Layers and where things live
- **Raw (source of truth, read only):** the project's folders and their documents, with one exception: `01 - Overview/wiki.md` is your own output, not raw. Read the raw material. Never edit, move, or delete it, and never read the wiki back in as a source. When you ingest a document, you may save a dated copy or a pointer note into `.canvas/raw/` so the source is preserved even if the original changes.
- **Human notes (`01 - Overview/Logs/`):** one persistent file per person (for example `Sarah.md`), appended over time under dated headings (`## YYYY-MM-DD`). High-signal; read it early each run. On a changed file, read only entries dated since the last run. Treat each entry as an attributed statement by its author, not settled fact: a note proposing or opining on something is NOT a decision until a formal document or explicit decision record confirms it.
- **Session logs (`01 - Overview/Logs/`, named `… - Claude Session - … .md`):** end-of-session reports you write (wiki-os §4). These are your own output. **Never ingest a `Claude Session` file as a source** — skip it by its filename marker. (Human-authored notes in the same folder remain valid input; these do not.)
- **Meeting records (`01 - Overview/Meetings/`):** one file per meeting, `YYYY-MM-DD - topic.md`, a short summary header (decisions, action items with owners, open questions) above the full transcript. The transcript is the highest-signal and most dangerous input: huge, mostly noise, full of things floated but never decided. EXTRACT, do not summarize: pull only decisions, action items with owners, commitments, deadlines, new contacts, and genuine open questions, each tied to the meeting file as its source. Treat a human-confirmed header as authoritative; if a header is unconfirmed, draft your proposed header into `.canvas/inbox/` rather than the wiki. Attribution rule applies as with notes.
- **Wiki (you own this):** the single file `01 - Overview/wiki.md`, the distilled running brief. Structure defined below. It lives inside `01 - Overview` but is your output, never ingested as raw.
- **Log (append only):** `.canvas/log.md`. One dated line per ingest or lint. Never rewrite it.
- **Inbox (staging):** `.canvas/inbox/`. Where Tier-2 items flagged on an unattended run wait for review (wiki-os §6). Tier-1 additions do not stage here — they commit directly.
- **Snapshots (undo):** `.canvas/snapshots/`. Before editing the wiki, copy the current wiki here as `YYYY-MM-DD - wiki.md`.
- **Templates:** `.canvas/templates/`. Use these formats for new pages.

## Wiki structure — mirror the folders
The wiki reads top to bottom like the project itself, so a human can open it and know where they are. Two parts:

1. **Pinned Overview (always present).** At the very top, a short intro that orients a newcomer in about 30 seconds: what the project is, who it is for, who is running it, the current stage, key dates, and the key people. Every project wiki has this section from creation.
2. **Folder-mirrored sections (added on demand).** Below the Overview, one H2 per top-level project folder, **in folder order**, added only when its first real content arrives — do not pre-create empty sections. (For example, a project with folders `02 - Research`, `03 - Quotes & Options`, `04 - Budget & Payments` grows `## Research`, `## Quotes & Options`, `## Budget & Payments` as content lands.)
   Under each H2, add an H3 per item or document (for example `### Contractor Bid — Smith & Co`) and file the distilled summary there, tied to its source. When something the human dictates, or a document you ingest, belongs to a folder, it goes under that folder's section.
   Decisions, risks, and open questions that genuinely span folders may sit in a short `## Decisions` and `## Risks & Open Questions` block right after the Overview; otherwise file them under their home-folder section.

If a section outgrows the file (weekly lint flags a section over ~200 lines), split it into a linked page under `01 - Overview/` and leave a one-line summary plus the link in the H2.

## File metadata standard (required on every Markdown file you create)
Begin every file with YAML frontmatter: `title`, `description`, `type` (wiki-page | decision | source-note | contact | log | overview | index), `status` (current | superseded | draft | flagged), `created`, `updated`, `tags`. Sources are not frontmatter: every page ends with a `## Sources` section, one bullet per dated raw filename or path the page draws from (wiki-os §9). A page with no Sources section, or an empty one, is invalid. Fix it or do not create it.

## Tag list (do not invent new tags without adding them here first)
`decision, budget, schedule, commitment, deadline, contact, risk, research, options, legal, health, travel, purchase, maintenance, lesson, open-question, meeting, action-item`

## The importance test — what to promote into the wiki
Promote something when it is: a decision and its reason; a changed assumption in the budget or plan, or a number other documents depend on; a new or changed commitment, obligation, or deadline; a new or changed position from an outside party (a contractor, a school, an agency, an insurer); a new contact with role and disposition; a risk newly identified or retired; or a lesson that would change how the next project is run. Do NOT promote routine edits, formatting, drafts in flight, passing mentions, file moves, or anything you cannot tie to a source. When unsure, leave it in raw and note an open question.

## Daily run procedure (low stakes, near append-only)
1. **Step 0 freshness check** (above). Then determine what changed since the last run: `.canvas/last_run` holds an ISO 8601 timestamp (date-time-offset, e.g. `2026-06-28T14:57:26-0400`); read sources whose filesystem modified-time is newer. Because sync and copies can rewrite mtimes, cross-check the date in the filename and re-read when ambiguous rather than trusting mtime alone. On the first run (`last_run` empty or missing), treat all substantive text-bearing documents as new. Treat `01 - Overview/wiki.md` as your output, never a changed source. **Examine every new or changed file for significance — including raw data outputs (CSVs, spreadsheets, exports), not only prose documents. "It's just data" is not an exemption; a data file can carry the run's most important finding.**
2. Read `01 - Overview/Logs/` and `01 - Overview/Meetings/` first; they are highest-signal. Human notes are valid sources. **`Claude Session` logs are still never ingested as a source (they are your own output), but they are the narrative trail — consult them as *pointers* to understand what a new or raw file is and why it exists.** **Narrative-first:** before drawing any conclusion from a raw data output, look in `Logs/` for a session log or human note from the same window that explains it, and read that first; never claim "no narrative exists" without checking. **Then verify from the raw data yourself:** for a data file, do not trust an accompanying summary — open the file and confirm the counts/figures before promoting anything (the verify-and-correct loop, wiki-os §3c), and cite the raw data as the source, not the session log. Then triage the rest.
3. For what passes the importance test: **new, source-anchored additions commit directly** to the correct folder-mirrored section (Tier 1, wiki-os §6) — attended or not. A change that would **overwrite or contradict an established claim, or harden one to "Settled" (Tier 2)** is gated: ask in the moment if a human is present; if unattended, do not make it — flag it (record both claims, `status: flagged`) and hold it for review.
4. Append, do not rewrite. Do not rewrite established pages during a daily run.
5. If new input contradicts an existing page, record both claims with dates, set the page `status: flagged`, and note it. Do NOT resolve it — that happens in the weekly lint.
6. Snapshot the wiki before any edit. Append one line to `.canvas/log.md`. Write a short human digest and, only on success, write the current ISO 8601 timestamp (date-time-offset) to `.canvas/last_run`.
7. If the run was an interactive session, also write a `Claude Session` log per wiki-os §4.

## Weekly lint procedure (judgment pass, human in the loop)
Do the cheap mechanical checks and report them: dead internal links, orphan pages, sections/pages over ~200 lines (propose a split per Wiki structure), sections out of folder order, and any page with a missing or empty `## Sources` section. Then surface judgment calls: every `flagged` contradiction with both dated claims and your read on which is current; claims newer sources appear to supersede. On the human's decision, update the current page, mark the loser `superseded`, move superseded pages to `.canvas/raw/_archive/` and out of the index. Append a lint line to the log.

## Hard rules
- **Never ingest your own prior output.** The Logs (human notes) and Meetings folders are human-authored; never read a digest, summary, `Claude Session` log, or wiki page you generated as if it were a fresh source. In particular, `01 - Overview/wiki.md` and any `… - Claude Session - … .md` are your output — never ingest them. *(Consulting a session log as a **pointer** to locate or interpret a raw file, then verifying and citing that raw file itself, is not ingestion — that is allowed and expected, per Daily run step 2.)*
- Never edit raw source files.
- Never assert a claim you cannot tie to a dated source. Do not invent.
- Never silently overwrite a contradicting claim; flag it.
- Prefer append-and-link over rewriting established pages.
- Archive superseded content; do not delete it.
- Keep this schema short. If you and the human want to add a rule, consider removing one.
