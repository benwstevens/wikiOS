# wikiOS — SETUP: point your LLM at this folder

**Why bother.** An LLM forgets everything between conversations, and what it does remember it keeps somewhere you cannot see. wikiOS gives it a memory you own: a set of ordinary text files, in your own folders, that it reads at the start of every session and maintains as you work. So the model shows up already knowing your clients, your projects, your decisions, and how you like things done. Every fact on every page says where it came from and when, so you can check it. Every change is copied first, so you can undo it. And because it is all plain text, you can open any page yourself, read it, fix it, or search it, with or without the model.

**What a "wiki" is in wikiOS.** Just a text file. Each page is a file ending in `.md`, written in **markdown**, which is ordinary text with a few light conventions: a line starting with `#` is a heading, a line starting with `-` is a bullet, `**bold**` is bold, and a link is `[words](path/to/file.md)`. That is nearly all of it, and you do not have to learn it, because the model writes the pages; you read them. They open in anything that opens text: Notepad or TextEdit, Word, your phone's notes app. If you want them to look nice, free editors made for markdown show the headings and links formatted: **Obsidian** and **Typora** are the common ones on Mac and Windows, **iA Writer** on Mac and iPhone, and VS Code if you already have it. None of this is programming. It is the same kind of file a README on a website is.

**If you are the person:** download or clone this folder, open your LLM tool (Claude Code, Cursor, or similar) inside it, and say "set up wikiOS." The model reads this file and asks you what it needs. (In Claude Code the `/setup-wiki` command does the same, but only while you are in this folder; it is a project skill, not something installed on your machine.) Budget an hour for the conversation and a few days of ordinary use before wikiOS feels like yours.

**If you are the model:** read this whole file, then `system/LLM-rules.md` and `system/wiki-os.md`. Then run the interview in Part B, a few questions at a time, writing the answers into the user's `customization.md` as you go so nothing is lost if the session ends. Then build what Part C describes. Do not skip questions because you can guess the answers; the point of the interview is that the user hears the choices. One exception to `LLM-rules.md` during the interview: skip the **Requests** recap at the end of each round. The round *is* the questions; repeating them underneath is noise. The recap rule applies again once the system is built.

## Where this comes from

wikiOS was built by **Ben Stevens** (benwstevens.com), who runs a small real-estate development advisory and has used it every working day since mid-2026 for his firm's knowledge, his clients and negotiations, his projects, his family's records, and his writing. It began as an evolution of **Andrej Karpathy's LLM-wiki idea**: keep your raw sources, let the model maintain a wiki over them, and lint the wiki for drift instead of trusting the model's memory. Ben's early experience matched what others reported: after about sixty days the wiki went stale in places and overconfident in others, asserting as settled things nobody had decided. Most of what is in these files is the response to that, worked out one correction at a time: every claim tied to a dated source, a copy taken before anything is overwritten, a hard line between a fact (written directly) and a position (asked about first), a log of every session, and one periodic command that re-reads everything and lints it. Each rule carries the date it was adopted and, in the origin install, the incident behind it.

wikiOS's shared files are versioned here. The core rules file is named `wiki-os.md` after the system; the system is wikiOS, the file is one of its four root files. Anyone's install can adopt improvements, and improvements flow back. Nothing of Ben's content is in this repo, only rules and blank templates.

---

## Part A. What wikiOS is

**In plain words.** A folder of ordinary markdown pages that your LLM maintains under written rules. There is one always-on hub page per area of your life or work, pointing to subject pages that are read only when needed. Every claim on a page names the dated source it came from. Before the model changes any page it saves a dated copy. Facts and notes it writes directly; positions, contradictions, and anything on a hub page it proposes and waits for your yes. Every working session ends with a short log. Meeting notes and stray thoughts have a place to land. And one command, **"update the wikis"**, re-reads everything since last time, proposes what the pages should say, and checks them for contradictions. Nothing runs on a timer.

**Be honest with the user about one thing.** Every control in wikiOS is a rule the model reads and follows. None of it is a lock. The safety comes from three things that do not depend on the model's obedience in the moment: the sources it must cite (so anything can be checked), the snapshots it must take (so anything can be undone), and the session logs (so anything can be traced). Say this plainly during setup; people responsible for someone else's data will ask.

**The layout.** Everything about wikiOS lives in one folder at the root of the user's workspace:

```
<workspace root>/
  CLAUDE.md               the entry file the tool loads every session; one line imports LLM-rules.md
  .system/
    LLM-rules.md          how the model behaves with the owner (shared with this repo, identical)
    wiki-os.md            how the wikis operate (shared with this repo, identical)
    githubsync.md         how rule files move to and from this repo (never content)
    customization.md      THIS install: layers, walls, folders, key files, engines, tool, modules, versions
    customization/        everything specific to this install
      <layer>-rules.md      one per layer
      project-rules.md      the contract for project wikis (copied into each project's .canvas/)
      LLM-rules-origins.md  the dated story behind each behaviour rule
      writing-style.md      the owner's voice guide (optional)
      templates/  howtos/  tools/
    snapshots/<layer>/    the undo trail
    state/                the timestamp of the last "update the wikis"
    history/              decision records and system-level session logs
  <Layer folder>/         one per layer: CLAUDE.md, wiki.md (the hub), log.md (a buffer), Logs/
    <Spoke folder>/       one per subject: wiki.md and the files it covers
    Projects/ ...         if the layer runs projects
```

A **layer** is one top-level folder with its own privacy rule. Most people need one. Someone with work and private life in the same workspace needs two with a wall between them. Ben has three: a private firm folder, a shareable firm folder, and a household folder.

**How the entry file works.** Claude Code loads `CLAUDE.md` from the working directory and every folder above it, and a line reading `@.system/LLM-rules.md` pulls that file in at launch. So the behaviour rules are active from the first message. Cursor reads `.cursorrules` or `AGENTS.md`; other tools have their own. If the user's tool has no import, paste the rules file's body into the entry file and note in `customization.md` that the two must be kept in step.

**What a page looks like.** Frontmatter (a block of `field: value` lines between `---` markers: title, description, type, status, dates, tags), then the body in plain sentences with headings, then a `## Sources` section at the bottom with one bullet per dated source. Links are ordinary markdown links to other files by relative path. `templates/wiki-hub.md`, `templates/matter-page.md`, `templates/domain-page.md`, and `templates/project-wiki.md` are finished examples.

---

## Part B. The interview

Ask in this order, two or three questions at a time, in plain language. Give a default for every question so the user can say "default." If the workspace already has files, look at the tree first and propose answers from it. Write each answer into `customization.md` as it lands.

### 1. What this is for
- **Ask this first, in these words:** "Are you setting this up for a whole company, for your own projects at a company, for your personal life, or some combination?" The answer decides how many folders (layers) there will be and who else will ever open them. *(Default: one area.)*
- If more than one area: should they be walled off from each other, so a session in one can never read the other? *(Default: yes if anyone else will ever see the work side.)*
- Does anyone else run sessions in any part of it, or will any folder be shared with a team or a client? *(Default: no.)* A shared folder becomes a shared layer where nothing candid lives.
- How should the files refer to you? *(First name is fine.)* The workspace is named after its folder unless the user wants something else; do not ask them to name "the install," which means nothing to a newcomer.

### 2. Platform, tool, and permission mode
- Where do the files live: Dropbox, iCloud, OneDrive, Google Drive, or a plain local folder? Give the path to the top folder. If a sync provider is in use, tell the user to mark the workspace "available offline" so the model does not stall fetching files one by one.
- Which tool runs the model: Claude Code, Cursor, something else? *(This decides the entry file and whether imports work.)*
- **Permission mode.** Most tools have a setting for how much the model may do without asking. In Claude Code it is the Mode menu: *Auto* (the model handles permission decisions), *Manual* (always ask before making changes), *Accept edits* (file edits go through, other actions ask), *Plan* (plan before making changes), and a bypass setting. It makes a large difference to how fast the work goes. Recommend: **Manual for the first week**, while the user learns what the model does; then **Accept edits or Auto for everyday wiki work inside the workspace**, because wikiOS's own rules already force snapshots and approval on the changes that matter; **Plan mode for any big job**, which is also what wiki-os §3 asks for. Record the choice; if the tool has no such setting, say so.
- Will the model run outside this workspace too (other projects on the same machine)? If yes, offer `templates/CLAUDE-global.md` for the tool's global config so the Requests-recap and writing rules apply everywhere.

### 3. What you are working on, and the shape of a page
This is the round that decides whether the wiki holds together. Explain before asking, in this order: **"We are going to set up a wiki for each individual project, client, or matter you have. The shape of that wiki depends on what you are working on."** A wiki about a home renovation, a lawsuit, a sales account, a research topic, and a family member's schooling do not want the same headings. If pages are added before a shape is agreed, the notes come in disjointed and no later pass fixes that. So:

- **Ask: "What are you actually working on, day to day? Describe the two or three kinds of thing you would want pages about."** Listen for whether there is *one consistent kind of thing* (every page is a client account; every page is a case; every page is a property) or *several kinds* (clients and also internal subjects; renovations and also finances).
- **Then show the shapes from the original author's files** and ask which the user recognises. Two are shipped in `templates/`, generalised from pages that have been in daily use for months:
  - `templates/matter-page.md`: one client, deal, case, engagement, or other ongoing thing with people and a timeline. Sections: how this file is organised, people, backstory, major milestones, current status, full history, sources.
  - `templates/domain-page.md`: a subject rather than a matter, with no cast and no chronology. Sections: how this file is organised, where it stands, positions, dynamics and reads, open questions, index, sources.
  - `templates/project-wiki.md`: a thing with a start and an end, whose page mirrors the project's own folders.
  - `templates/wiki-hub.md`: the short always-on page for an area, two or three sentences per subject with a link.
- **Agree the shape or shapes before moving on.** One kind of work usually means one template plus the hub. Several kinds mean a template per kind, named for the kind ("account page," "case page," "property page"), each adapted from a shipped one by renaming or dropping sections. Write the agreed shapes into `customization.md` under Pages; they become that layer's rules file's template section. Do not invent a third structure during setup; adapt a shipped one, and let use show what is missing.

### 4. Your existing folders, and how wikiOS lays over them
Assume the person already has a folder tree. Do not ask them to name folders; **read the tree and propose.** Open the round by asking permission in these words or close to them: **"Ok, now I'm ready to help you set up the system. I'm going to scan your folders, two or three levels deep, so I can propose where the wikis and their subjects go. Does that work?"** On yes, list the folders under the path from step 2 (folders only, no files; skip anything that is obviously photos, downloads, archives, or application data) and show the user a short map. Then propose, and let them edit:

- **Which existing folder is each area from step 1.** For one area, the workspace itself is the layer. For work and personal side by side, point at the two folders that already hold them; if they are mixed together in one folder, say so and ask whether to separate them now or leave the wall for later.
- **Which existing folders become the subjects (spokes)** under each area, shaped by step 3: if every page is a client account, the client folders are the subjects, plus whatever internal folders exist (pricing, hiring, finances); if it is a household, the folders for home, money, health, school. Five to ten. Folders that do not fit any subject are left alone and simply not wikied; folders that are archives are named as such so the refresh skips them.
- **Which subjects already have real material** (the model can see this) and which are empty; empty ones get a placeholder page and nothing else.
- **Nothing moves.** wikiOS adds a `wiki.md` to the folders that become subjects and a hub `wiki.md`, `log.md`, and `Logs/` at each layer's root. It does not rename or reorganise the user's folders. If the user wants to reorganise, that is a separate job for later, planned first (wiki-os §3).

- **Projects, from the same scan.** If the tree shows things with a start and an end (a build, a case, a renovation, a book), say what pattern they already follow and propose it as the project layout: the stage folders they move through *(default if none exist: Planning, Active, Completed, plus an Archive the refresh skips)*, what one project folder contains *(default: Overview, Research, Options, Budget, Execution, Records)*, and the tag words for project entries *(show the shipped list; ask which words are wrong for this work)*. If there are no projects, say so and skip.

Only if the workspace is empty: propose the subjects from the answers in step 3 and create the folders.

Two small settings while here: hub word cap *(default: 800 to 1200 words)*, and whether pages carry status tags (Settled, Open) or say their uncertainty in prose *(default: prose only)*.

### 5. Privacy
Two plain questions.
- "Is there a wall between anything in your folders that the wikis must never let cross-pollinate? For example personal versus company material, or HR files versus what employees may see, or one client versus another. If so, point those things out." *(Each wall becomes a privacy rule in the folders on either side of it, and decides which folder may read which: the private side may read the shared side, never the reverse.)*
- "Is there anything you never want the AI to see at all? If so, we leave it in a folder wikiOS does not set up." *(Say plainly, if asked, that the AI vendor sees whatever a session shows it, and the sync provider already holds the files; wikiOS adds no other destination.)*

### 6. Key files: what the model must read before certain tasks
Ask: "Are there documents you would want the model to read every time before it does a certain kind of work?" Examples from the origin install: a negotiation-principles file before any deal conversation; a legal style guide before drafting a contract; a voice guide before drafting anything under the owner's name; a how-to before touching a spreadsheet model. For each: the file, and the trigger ("before X, read Y"). These go into `customization.md` under **Key files**, and the model treats each as a standing instruction. If the user has none yet, leave the section with one example line so they know where it goes.

### 7. Engines: processes you run again and again
Ask: "Is there a job you do repeatedly that has the same steps each time?" A research sweep across many sources, a reader panel on a draft, a comps pull, a weekly digest. Each becomes an **engine**: its own folder with a plain-language `workflow.md` (what it does, what can go wrong), a `plan.md`, its inputs and outputs, and a `Logs/` folder; the model runs it the same way each time and the outputs are never treated as canonical facts until a person has looked at them. Record the list in `customization.md` under **Engines**, even if it is empty. Do not build engines during setup; note them and build the first one when the user asks.

### 8. How the model should behave
Do not walk the whole of `LLM-rules.md`; it is on by default and corrections will refine it. Ask only these:
- **The three optional modules.** Negotiation and deals (for anyone who negotiates or does contracts); writing in the owner's voice (for anyone who will have the model draft things they send); daily files and tools (for anyone with a task list the model helps run). Which stay on? Switched-off modules are recorded in `customization.md`; the shared file is never edited.
- **The three rules people most often question,** read aloud: every answer that asks something ends with a **Requests** list; anything not yet decided is written as a proposal, never as a decision; the owner's files are never copied anywhere else. Any objection?
- If the writing module stays on: start `customization/writing-style.md` from the template and explain the capture loop (after the owner sends something, record the model's draft, the owner's final, and the lesson).
- **Meeting notes:** does the user record or dictate meetings? Which tool? Any known quirk (the origin install's recorder swaps speaker labels)? This goes into a how-to under `customization/howtos/` and is what "update the wikis" reads as its main inflow.

### 9. The upkeep, explained once, then confirm
Tell the user, in these words or close to them: *Every conversation ends with a short log in the nearest Logs folder. When something is decided in conversation, the model offers to write it to the wiki right then. Your meeting notes and any stray thoughts in `log.md` wait for the next refresh. Every week or two, whenever you like, you say "update the wikis": the model re-reads everything since last time, proposes what the pages should say, asks you at most seven questions, and ends by checking the pages for contradictions. If you go two weeks without one, it reminds you once. Nothing runs on its own.* Then read `customization.md` back in full, take corrections, and build.

---

## Part C. What to build

1. `.system/` with `LLM-rules.md`, `wiki-os.md`, and `githubsync.md` copied from `system/` unchanged (record each `schema_version` as the install's `upstream_version`); `customization.md` from `templates/customization.md` with every answer filled in; `customization/` holding one `<layer>-rules.md` per layer (from `system/layer-rules-template.md`, differences filled), `project-rules.md` (from `system/project-rules.md`, folder names and tags filled), `LLM-rules-origins.md` (blank template), `writing-style.md` if that module is on, `templates/` (the hub, matter, domain, and project page templates, adapted as agreed in step 3; project layout from step 4), empty `howtos/` and `tools/`, `snapshots/<layer>/`, `state/`, `history/`.
2. The root entry file from `templates/CLAUDE-root.md` with the import line, and one entry file per layer from `templates/CLAUDE-layer.md`, each stating the layer's privacy rule.
3. Per layer: a hub `wiki.md` (`status: draft`, seeded from the interview, under the word cap), spoke folders with stub `wiki.md` files, `log.md` from `templates/log.md`, and `Logs/`.
4. The project folder template if projects are on, with its `.canvas/` (`schema.md` copied from `customization/project-rules.md`, `CLAUDE.md` from `templates/CLAUDE-project.md`, empty `log.md`, `inbox/`, `raw/`, `snapshots/`, `templates/`).
5. `templates/CLAUDE-global.md` into the tool's global config, only if the user said yes in step 2.
6. A first session log in `.system/history/Logs/` recording the setup, with every decision and every default the user accepted.

**First-run checklist, done with the user watching:** open a fresh session at the workspace root and confirm the entry file and `LLM-rules.md` loaded (in Claude Code, `/context` lists them under Memory files). Drop one test note in a layer's `log.md`. Add one test meeting note. If projects are on, create one test project from the template and put a document in it. Say **"update the wikis"** and confirm it reads the project, the note, and the buffer, proposes entries, and ends with a lint. End the session and confirm a log landed. Then delete the test material.

**What to say at the end.** Where the three root files are and that `customization.md` is theirs to edit; that everything under `customization/` is theirs and never ships; the one command and the two-week reminder; the permission mode chosen and how to change it; and that the first week is for watching what the model does and correcting it, because every correction becomes a dated line in the origins file and, if it should govern every session, a proposed line in `LLM-rules.md`.

---

## Vocabulary, for the person reading over the model's shoulder

**Layer:** one top-level folder with its own privacy rule. **Hub:** a layer's always-on `wiki.md`. **Spoke:** a subject folder with its own `wiki.md`. **Matter page:** the page about one client, deal, case, or ongoing matter. **Project:** a folder with a start and an end that carries its own copy of the project rules. **Ingest:** read a folder's new files and propose what the wiki should say about them. **Snapshot:** a dated copy of a page taken before it is changed. **Lint:** a check for contradictions, stale sections, and broken links. **Frontmatter:** the `field: value` block at the top of a file. **Tier 1 / Tier 2:** written directly / asked about first. **Engine:** a repeatable multi-step job with its own folder and written steps. **Key file:** a document the model must read before a named kind of task. **§:** section; "wiki-os §6" is section 6 of `wiki-os.md`.
