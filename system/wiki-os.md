---
title: Wiki OS — the operating conventions every layer follows (upstream)
description: The single canonical home for the cross-cutting rules every layer and project of an install follows — how to write, how to run big projects, how to log sessions, how the wikis are refreshed, and how rules files keep themselves current. Install specifics live in customization.md. Installs copy this file and descend from it; they never restate it.
type: schema
status: current
created: 2026-07-03
updated: 2026-09-07
canonical: system/wiki-os.md
schema_version: 12
derived_from: the origin install's .system/wiki-os.md, schema_version 18 (2026-09-07); bodies are identical
tags: [system, schema, conventions]
---

*(The block above this heading is machine bookkeeping for section 1's freshness check. Readers can skip it.)*

# Wiki OS — the operating conventions every layer follows

This file is the one home for the rules that apply across every layer of an install. Any rules file, a layer's or a project's, links here instead of copying these rules, so a single change here updates the whole system at once. One home per fact; link, never restate.

**How to read this file.** The § sign means section: "wiki-os §6" is section 6 of this file, and other files cite it that way. "The owner" is the person whose workspace this is; "the model" is whatever LLM is doing the work. **Words used here:** a *layer* is one top-level folder with its own privacy rule (a firm's private folder, a shared folder, a household folder); a *hub* is the layer's always-on `wiki.md`; a *spoke* is a subject folder with its own `wiki.md`; a *matter page* is the page about one client, deal, case, or other ongoing matter; its *current-state block* is the section that says where the matter stands right now and its *history* is the dated record beneath; a *hub one-liner* is the two or three sentences the hub gives each spoke or matter; a *project* is a folder with a start and an end that carries its own copy of the project rules; to *ingest* a folder is to read its new files and propose what the wiki should say about them; a *snapshot* is a dated copy of a page taken before it is changed; a *lint* is a check for contradictions and broken links; to *scaffold* a page is to write its headings with a note that says the content is missing; *frontmatter* is the block of `field: value` lines between `---` markers at the top of a file.

**Read `customization.md` alongside this file.** It describes this particular install: its layers and their privacy walls, its project lifecycle folders, its page templates and their section names, its tools, and any install-specific rules. Several rules below say "the layer," "the project folders," "the matter page," or "the install's tool"; `customization.md` says what those are here. This file never names them itself, so it stays identical to the upstream copy.

**Reach direction (the privacy wall).** Where an install has private and shared layers, a private layer may read a shared layer's files, but a model working in a shared layer must never have to read anything inside a private one. Rules files are not content, so this file and its siblings sit above every layer. Which layers are private and which are shared: `customization.md`.

## 1. Staying current — the freshness check (Step 0 of any run)

Every rules file carries two fields in its frontmatter:
- `canonical:` — the path of the master copy this file descends from. The master copies themselves (the files in `.system/`) point at their own path; the check below is for the copies, chiefly each project's `.canvas/schema.md`.
- `schema_version:` — a whole number, raised whenever this master copy's rules change. It counts this install's edits; the separate `upstream_version:` records which repo version was last adopted, so the two numbers are not meant to match.

Before doing project work, the model runs **Step 0**: open the master copy and compare `schema_version`. If the canonical version is higher than the local copy's, show the owner a short diff of what changed and propose updating the local copy; once approved, proceed under the new rules. If the canonical file cannot be read, run on the local copy and say plainly that the rules could not be verified. Never silently run on stale rules, and never silently overwrite a local copy without showing the change first. (Read-only questions skip Step 0; it protects edits, not answers.)

The install's canonical files may themselves descend from the upstream repository: they carry `upstream:` and `upstream_version:` in their frontmatter, and the version numbers are summarised in `customization.md`. Crossing that boundary in either direction is the separate, occasional, human-approved pass described in `githubsync.md`; a daily run never depends on the repo and works offline on the install's own files.

## 2. Writing standard — readable from start to finish

Every wiki and reference must be readable by a person with no prior context. The test: a stranger, or the owner six months from now, opening the file cold should come away actually understanding the subject. This **onboarding test** governs all wiki writing.

- Write in plain, complete sentences, not shorthand or cryptic fragments. Each entry should carry enough context to stand on its own.
- Lean is still required — verbosity burns the always-on token budget — but lean means *fewer words*, never *less meaning*. Compress the wording; never drop the context a reader needs to follow it.
- Prefer plain language over jargon. When a technical term is unavoidable, define it once at its canonical home and link to it.
- Rule of thumb: if you would not understand a line after six months away from it, rewrite it.

**Meeting and call entries, and only those, are bullets, not narrative (owner adopted 2026-07-29).** Ordinary pages stay in plain complete sentences; this rule is about the entry that records what happened in a meeting. A wiki entry recording a meeting, call, or negotiation captures **the moves, the decisions, and the crises** — what changed a position, what got decided, what nearly broke, what the other side conceded. Write it as a short bulleted list, one move per bullet, with a bolded lead. **Do not write it as narrative prose.** Prose accounts of meetings have run long and read slowly; someone scanning for the moment a concession landed should not have to read a transcript to find it.

- **The full account belongs in the session log (§4), not in the wiki.** The wiki entry carries only what moved.
- **Where a session log exists, the entry names it by filename**, so the detail is one click away and the bullets can be trimmed hard without losing anything. This is the same index-to-detail pattern the file structures already use: the entry is the index, the log holds the record.
- This governs the *form* of a meeting entry. It does not relax the provenance rules — every un-adopted read still carries its own marker, bullets included.

## 3. Big-project standard procedure

A **big project** is any multi-step process we set out to run together — a research sweep, a system change, a build, a migration. Whenever one begins, do all three of the following in the appropriate project folder.

**a. Write and keep a `plan.md`.** Create it at the start and update it frequently as work proceeds. It is both the audit trail — what we set out to do and where we are — and crash protection: on a long task the context limit may be reached, and a current `plan.md` lets any later session resume exactly where work stopped.

**b. Write a plain-language `workflow.md` before kicking off.** Explain the workflow at roughly a sixth-grade reading level, so the owner fully understands what we are about to do before we do it. Then list the likely points of failure and sort the fixes into two buckets: *practical to implement* (do these) and *not worth the added complexity* (name them and consciously accept them). The owner reads this before we start and can stop us if a step sounds wrong.

**c. Build in a verify-and-correct loop.** Producing facts is not the same as producing *correct* facts. After each result, step back and check it against reality before trusting or acting on it — and loop until it holds.
- *Cautionary anchor — the fire station.* A search once reported that a town was about to build a fire station. On a call to offer help, the station turned out to have stood for 13 years, and the person who answered was sitting inside it. Surfaced data can be flatly wrong.
- *Model to emulate — the book-distiller script* (a program from the origin install that turns books into summaries). Write code, look at the real output, judge whether it is right, fix it, regenerate, and loop — until it is right. That cycle is the standard for any job that generates facts or artifacts.

## 4. Log every session

At the end of essentially any working session, write a short report capturing what happened. This closes the gap where useful context used to evaporate between sessions: every session is captured when it happens, and the §8 refresh verifies that anything important reached the wiki, so nothing is lost.

**These logs are the narrative trail the next ingest depends on — not optional housekeeping.** Most new files (data outputs, deliverables, exports) are produced inside a working session; the log is what explains them to a later run that sees only the files. So if a session produced or changed any files, its log must say what they are and why. A later ingest is expected to consult these logs as *pointers* to interpret new files — while still never ingesting them as sources and always verifying from the underlying file itself. An unlogged session that leaves files behind forces the next run to guess, which is exactly the failure this system exists to prevent.

- **Where.** For work inside a project, the project's `01 - Overview/Logs/` folder. For any other work, a `Logs/` folder in the folder where the work happened (create it if it does not exist).
- **Filename:** `YYYY-MM-DD HHMMam/pm - Claude Session - <description>.md` — applies to every kind of session, whichever tool runs it.
- **Contents:** a plain report of what we did, what changed, what was decided, and anything left open.
- **Propose the wiki update in the moment.** When a decision, a milestone, a changed position, or a new durable fact lands in conversation, say so then: name the line and its canonical home and offer to write it. On the owner's yes, write it (snapshot, source-anchored to the conversation date). The log records what was written and what was left unwritten, so the §8 refresh can verify the first and catch the second.
- **Never defer the log behind a pending confirmation (owner adopted 2026-08-05).** Write it before the session goes idle, with what is known, and amend later if the answer arrives. Do not end a session saying "tell me when it's sent and I'll write the log" — the confirmation often never comes, the session idles, and the work vanishes from the record along with any corrections the log was carrying. Where a fact is still unsettled, write the log and mark that fact open. *(The originating case is in the install's `customization/LLM-rules-origins.md`, under this rule's name.)*
- **These reports are the model's own output, not a source.** The project ingest (§8 step 1) must never read a `Claude Session` report back in as fresh input — that would be ingesting its own output and would create an echo loop. The `Claude Session` filename marker is what lets the ingest skip them. Human-authored notes in the same `Logs/` folder remain valid input; these do not.

## 5. The capture buffer (`log.md`)

Each human-owned layer keeps a `log.md` at its root for notes made outside a session: a thought on the phone, a line dictated between meetings. It is a buffer, never a second canonical home; nothing in it is authoritative until integrated into a wiki and approved. It is emptied by §8 step 4. There is no separate command for the buffer; every integration runs through **"update the wikis"** (§8). In practice most decisions never touch the buffer: they are proposed and written during the conversation itself (§4) and verified by the §8 sweep.

## 6. Write policy — write facts directly, ask before changing positions

Writes are risk-tiered. The line between the tiers: **a fact or a note is written directly; a position needs the owner's approval.**

- **Tier 1 — write directly.** New, source-anchored facts and notes: a document's summary, a new fact from a meeting note, a query finding (§7), an index refresh, a session log. Write these, snapshot, and log them. No approval needed. What keeps this safe is source-anchoring (every claim cites a source, so nothing is uncheckable) and snapshots (every change has an undo).
- **Tier 2 — ask first.** Anything that states or changes a *position* (what the owner has decided, believes, or will do), overwrites or contradicts an established claim, hardens a claim to "Settled," or edits a layer's hub. **When the owner is in the session, ask in the moment:** "the wiki says X (source A); this says Y (source B): overwrite, keep both flagged, or leave it?" **When the owner is not present, never do it silently:** record both claims with dates, mark the page `status: flagged`, and hold it for the next session or the next refresh (§8).

The §8 lint is the standing audit; "that response smells wrong" is the on-demand one.

## 7. Querying the wiki

When asked a question of the wiki:

1. Read the relevant index/catalog first to find the right pages, then open them.
2. Answer **with citations** to the source pages or files. If the wiki cannot support a claim, say so — an unsourced answer is a flag, not a fact.
3. If the answer is itself new and worth keeping (a comparison, an analysis, a connection you found), **file it back into the wiki** in its canonical home (Tier 1: sourced, written, logged). Explorations should compound, not vanish into chat. The answer can take whatever form the question needs — a page, a table, a chart — but the durable version lands in the wiki.
## 8. Updating the wikis — the one refresh command

**In plain words: nothing runs on a timer. The owner says "update the wikis" when they want to, roughly every week or two, and answers up to seven questions. That is the whole upkeep.**

**Trigger: "update the wikis."** It runs when the owner says so, and only then. There is no schedule and no frequency target: an unattended scheduled run, tried once, only prepared review queues that nobody read. **The nudge:** at the start of a session in the workspace, if the `.system/state/<layer>.last_update` marker (the timestamp the last refresh wrote) is older than fourteen days, say so in one line and offer to run the refresh. The nudge is a sentence, not a run; never run it unasked.

The refresh reads every inflow since the last update, in order, then lints. Facts and notes are written directly; positions and changes to established claims are asked about, or flagged if the owner is not present (§6).

1. **Project ingests.** Every live project under the install's project lifecycle folders (named in `customization.md`): run its ingest (its `.canvas/schema.md`, Step 0 first), pulling changed or new source files into the project wiki. Skip the archive and dead-project subfolders the install designates, and everything inside them; a project moved there is retired from the refresh. Skip a project with nothing changed since its `.canvas/last_run`.
2. **Session logs.** Every `Claude Session` log across the layer newer than the marker, wherever it sits: layer root, spoke, matter, project, or any other folder. The writing sessions propose and write as they go (§4), so this step is mostly verification: confirm the claimed writes reached their targets, and catch what was left unwritten.
   - **Pointer, never source.** A session log says what happened and which files it touched; it is the model's own output and is never quoted into a wiki as evidence. Open the underlying artifact, verify the fact there, and cite the artifact. This is the §4 rule applied, and it is what keeps the step from becoming the echo loop §4 warns about. The project ingest in step 1 still skips these files entirely.
   - **The bar: big things only.** An item qualifies if it is a decision the owner adopted, a position that changed, a new durable fact, or an artifact a wiki should point at and does not. Explicitly out: file moves, formatting, session mechanics, and anything the writing session already integrated. Most logs yield nothing, and that is the expected result.
   - **One decisions file, capped at seven.** A plain list of questions for the owner; the pass does all the reading and tracing and parks anything it is not allowed to decide alone. Rank by consequence and give every question a recommended answer. Anything that did not make the cut is listed as considered-and-not-raised, never silently dropped. If more than seven qualify, carry the surplus to the next pass.
   - **Every question carries its substance inline, in the chat message, not just the file.** A question that proposes replacing text shows the actual before and after; a question about items names the items. The review-queue file holds the full record; the chat ask must stand alone. This applies to any pass that puts questions to the owner.
   - **The cap is for routine passes, not a catch-up.** A backlog sweep covering weeks or months is a different job: drop the cap and group the questions by theme.
3. **Meeting notes.** Every new note of a meeting or call since the marker, wherever it landed: a project's `Meetings/`, a matter's source folder, a spoke's `Logs/`, or the owner's dictation. Recorded, dictated, or typed, these are the main inflow for the owner-owned layers. Read the whole note, never only its summary. Extract decisions, commitments, deadlines, new contacts, changed positions, and genuine open questions, each tied to the note as its source, and propose the entries: the matter page's history as bullets (§2), its current-state block rewritten in place, the hub one-liner (section names per the install's templates, `customization.md`). Human-authored notes are valid sources. A note's own speaker labels and summary are not trusted until checked against its body; the install names its recording tool and that tool's quirks in `customization/howtos/`.
4. **The capture buffers (§5).** For each layer's `log.md`: for each entry decide wiki-worthy or noise; find the single canonical home; snapshot the target; show the before/after diff with a one-line reason; write on approval; move the entry to the log's Integrated section.
5. **Lint, always, as the last step,** over the pages touched since the last update plus every hub, and each live project's own lint procedure (project rules). Look for: two homes for one fact (make one a link); a hub one-liner that disagrees with its spoke's current state; a current-state block older than the newest history entry beneath it; a number, tactic, or position without its proposed-or-adopted marker; dead internal links; a page with a missing or empty `## Sources` section. Report the mechanical findings; put the judgment calls into the same decisions file as step 2, under the same cap. This is the audit §6 relies on.
6. **Digest, then mark.** Report per project what was added and flagged; what the session-log and meeting-note sweeps surfaced and what they deliberately did not raise; what the buffers integrated; what the lint found. Then, and only then, write the current ISO 8601 timestamp to `.system/state/<layer>.last_update`, so an interrupted run re-reads rather than skips.

The refresh never touches the upstream repo. Moving rule changes to and from the repo is `githubsync.md`, a separate, occasional pass.

## 9. Standing rules for every human-owned layer

These apply to every hub-and-spoke layer. A layer's own rules file states only what differs for that layer: its privacy rule, hub word cap, snapshot path, log path, whether it uses status tags, and its page templates.

- **One canonical home per fact; link, never restate.** If two pages need the same fact, one owns it and the other links to it. If you find yourself restating another page's content, stop and replace it with a link. This is the whole point of the system.
- **Human-owned.** New facts and notes are written directly (Tier 1); positions, contradictions of established claims, and hub edits are proposed, shown with what changed and why, and written only on the owner's approval (Tier 2, §6). Nothing rewrites these pages on a timer; the model writes only inside a session the owner started. New pages are born `status: draft` and await review.
- **Source-anchor every claim** to a dated source. An unsourced assertion is a flag for the owner, not an established fact. Do not import facts from other projects, prior conversations, or general knowledge as if established here; label general knowledge as such. Sources sit in a `## Sources` section at the bottom of the page, one bullet per source, never in a `sources:` frontmatter line (universal since 2026-09-06; frontmatter lines had grown past 4,000 characters on mature files, and one convention beats two). A page with no Sources section, or an empty one, is invalid.
- **Do not fabricate.** Where a page has little real source material, scaffold it (section headers plus `STATUS: scaffold, populate from source`) rather than inventing figures, dates, or agreements. An empty sourced section is correct; a plausible invented one is a failure.
- **Uncertainty in prose.** Express genuine uncertainty plainly (leaning, undecided, not yet papered) and flag what is unverified. Never let a tentative note harden into a settled conviction. A position does not become "Settled" until the owner confirms it. Whether a layer also uses status tags is set by its rules file.
- **Snapshot before overwriting** any pre-existing file: copy it into `.system/snapshots/<layer>/` dated `YYYY-MM-DD` first. That is the undo button. **Name the snapshot so it cannot collide:** date, then the page's folder or title, then the file name, then what the edit was (`2026-09-06 - Finances spoke wiki (pre-sources-footer).md`). A layer holds many files named `wiki.md`; a snapshot named only by file name is overwritten by the next one and the undo trail is gone. Snapshots do the job of version history because most owners will never use git or GitHub; the folder is the whole system, and it has to carry its own undo.
- **The files win.** The only authoritative sources are the files in the layer and what the owner says. When prior knowledge conflicts with the files, defer to the files and flag the conflict.
- **Capture, then integrate.** Notes made outside a session drop raw into the layer's `log.md`, never filed at capture time. The log is a buffer, never a second canonical home. Facts become authoritative only once integrated into a wiki and approved (§5, §8 step 4; in practice most decisions are proposed in-session, §4, and verified by the §8 sweep).
- **Keep the hub lean** so it can serve as always-on context; push depth into spokes and reference rather than inline. The cap is set per layer.
- **Promote a spoke when a topic earns it.** When a set of distinct sub-topics grows large enough to merit independent treatment, create a spoke or sub-wiki and link it into the hub, so the primary wiki does not become long or convoluted. If a sub-wiki grows its own cluster of pages, give it its own folder with its `wiki.md` as the entry point.

---

*This file holds the cross-cutting conventions and, in §9, the standing rules every human-owned layer shares. Each layer's own rules file carries only that layer's differences.*
