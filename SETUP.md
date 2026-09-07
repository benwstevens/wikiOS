# wikiOS — SETUP: point your LLM at this folder

## For the person

*This section is for you. Everything after the next heading is instructions to the AI, and you never need to read it.*

**Before anything else: what you need.** wikiOS works with an AI tool that runs on your computer and can read and write files in a folder. Today that means Claude Code or Cursor, or a similar tool. If you use ChatGPT or Claude in a web browser, it cannot reach your folders, so this is not for you yet. It also needs a folder where your actual work lives (your documents, notes, and projects), which is a different folder from this one. Cost: the tool's own subscription; wikiOS adds no fee. It runs only when you talk to it, so there is no background usage. To remove it later, delete the `.system/` folder and the few `wiki.md`, `log.md`, and `CLAUDE.md` files it added; your own files are untouched.

**Why bother.** An LLM forgets everything between conversations, and what it does remember it keeps somewhere you cannot see. wikiOS gives it a memory you own: a set of ordinary text files, in your own folders, that it reads at the start of every session and maintains as you work. So the model shows up already knowing your clients, your projects, your decisions, and how you like things done. Every fact on every page says where it came from and when, so you can check it. Every change is copied first, so you can undo it. And because it is all plain text, you can open any page yourself, read it, fix it, or search it, with or without the model.

**Two things to know before you start.** First, every rule in wikiOS is a rule the AI reads and follows; none of it is a lock. What keeps you safe is that every fact it writes names its source, so you can check it; it copies every page before changing it, so you can undo it; and every session leaves a log, so you can trace it. Second, the wiki is not an inventory of your files. Many of your files are drafts, duplicates, or noise, and the AI does not summarise them all. A page holds the decisions and facts you have vetted, and a file earns a line only when it carries one.

**What happens next.** Download or clone this folder, open your LLM tool (Claude Code, Cursor, or similar) inside it, and say "set up wikiOS." The model reads this file and asks you what it needs. (In Claude Code the `/setup-wiki` command does the same, but only while you are in this folder; it is a project skill, not something installed on your machine.) Budget an hour for the conversation and a few days of ordinary use before wikiOS feels like yours. The AI will ask you about ten short rounds of questions, two or three at a time, and read everything back before it builds. Pages are ordinary text files; if you have never met markdown, the note at the very end of this file explains it in a paragraph.

## Where this comes from

wikiOS was built by **Ben Stevens** (benwstevens.com), who runs a small real-estate development advisory and has used it every working day since mid-2026 for his firm's knowledge, his clients and negotiations, his projects, his family's records, and his writing. It began as an evolution of **Andrej Karpathy's LLM-wiki idea**: keep your raw sources, let the model maintain a wiki over them, and lint the wiki for drift instead of trusting the model's memory. Ben's early experience matched what others reported: after about sixty days the wiki went stale in places and overconfident in others, asserting as settled things nobody had decided. Most of what is in these files is the response to that, worked out one correction at a time: every claim tied to a dated source, a copy taken before anything is overwritten, a hard line between a fact (written directly) and a position (asked about first), a log of every session, and one periodic command that re-reads everything and lints it. Each rule carries the date it was adopted and, in the origin install, the incident behind it.

wikiOS's shared files are versioned here. The core rules file is named `wiki-os.md` after the system; the system is wikiOS, the file is one of its four root files. Anyone's install can adopt improvements, and improvements flow back. Nothing of Ben's content is in this repo, only rules and blank templates.

---

## For the model

**If you are the model:** everything from here to the vocabulary at the end is addressed to you. Read this whole file, then `system/LLM-rules.md` and `system/wiki-os.md`. Then run the interview in Part B, a few questions at a time, writing the answers into the user's `customization.md` as you go so nothing is lost if the session ends. Then build what Part C describes. Do not skip questions because you can guess the answers; the point of the interview is that the user hears the choices. One exception to `LLM-rules.md` during the interview: skip the **Requests** recap at the end of each round. The round *is* the questions; repeating them underneath is noise. The recap rule applies again once the system is built.

## Part A. What wikiOS is

**In plain words.** A folder of ordinary markdown pages that your LLM maintains under written rules. There is one always-on hub page per area of your life or work, pointing to subject pages that are read only when needed. Every claim on a page names the dated source it came from. Before the model changes any page it saves a dated copy. Facts and notes it writes directly; positions, contradictions, and anything on a hub page it proposes and waits for your yes. Every working session ends with a short log. Meeting notes and stray thoughts have a place to land. **The wiki is not an inventory.** It does not summarise every file in the folders; many files are drafts, duplicates, or noise. A page holds vetted decisions and facts, each traceable to its source, and a file earns a line in the wiki only when it carries one of those. Keeping the pages small and true is the whole point, and it is why the model proposes rather than ingests wholesale. And one command, **"update the wikis"**, re-reads everything since last time, proposes what the pages should say, and checks them for contradictions. Nothing runs on a timer.

**Be honest with the user about one thing.** Every control in wikiOS is a rule the model reads and follows. None of it is a lock. The safety comes from three things that do not depend on the model's obedience in the moment: the sources it must cite (so anything can be checked), the snapshots it must take (so anything can be undone), and the session logs (so anything can be traced). Say this plainly during setup; people responsible for someone else's data will ask.

A **layer** is one top-level folder with its own privacy rule. Most people need one. Someone with work and private life in the same workspace needs two with a wall between them. The origin install has three: a private firm folder, a shareable firm folder, and a household folder.

---

## Part B. The interview

Ask in this order, two or three questions at a time, in plain language. Give a default for every question so the user can say "default." Do not look at the user's folders until round 4 asks permission. Write each answer into `customization.md` as it lands.

### 1. What this is for
- **Ask this first, in these words:** "Are you setting this up for a whole company, for your own projects at a company, for your personal life, for a single piece of work such as a book, a course, a research topic, or a codebase, or some combination?" The answer decides how many folders (layers) there will be and who else will ever open them. *(Default: one area.)*
- Does anyone else run sessions in any part of it, or will any folder be shared with a team or a client? *(Default: no.)* A shared folder becomes a shared layer where nothing candid lives.
- How should the files refer to you? *(First name is fine.)* The workspace is named after its folder unless the user wants something else; do not ask them to name "the install," which means nothing to a newcomer.

### 2. Your files, your tool, and how much I may do unasked
- **The tool.** You can usually see which tool you are running in; confirm it rather than asking: "I'm running in Claude Code, so I can load the rules with one line in your entry file." (Cursor reads `.cursorrules` or `AGENTS.md`; if the tool cannot import a file, the rules get pasted into the entry file and `customization.md` notes that the two must be kept in step.)
- **The folder that holds their work.** The folder you are in now is the wikiOS download, not their files. Ask: "Where does your actual work live: your documents, notes, and projects? Drag that folder into the chat, or paste its path, so I know where to set up." If it syncs through Dropbox, iCloud, OneDrive, or Google Drive, tell them to mark that folder "available offline" so files are not fetched one at a time.
- **Anything already there.** If that folder already has a `CLAUDE.md`, or the tool has a global config, say so and promise to show what you would add and merge it, never replace it.
- **How much I may do without asking.** Most tools have a setting for this. In Claude Code it is the Mode menu at the bottom of the chat: *Manual* asks before every change; *Accept edits* lets file edits through and asks for anything else; *Auto* lets the model decide; *Plan* makes a plan before changing anything. There is also a bypass setting that turns off all asking; do not use it. Recommend, in this order: Manual for the first week, while the user watches what the model does and sees that it takes a snapshot and asks before changing a position, as the rules require; then Accept edits or Auto for everyday wiki work, once that trust is earned; Plan for any big job. Be clear that the wikiOS rules are rules the model follows, not locks, which is exactly why the first week is spent watching.
- **Outside this workspace.** Will the model be used for other work on this machine? If yes, offer `templates/CLAUDE-global.md` for the tool's global config, merged with whatever is already there, so the way the model answers (the Requests list, the writing rules) applies everywhere.

### 3. What you are working on, and the shape of a page
This is the round that decides whether the wiki holds together. Explain before asking, in this order: **"We are going to set up a wiki for each individual project, client, or matter you have. The shape of that wiki depends on what you are working on."** A wiki about a home renovation, a lawsuit, a sales account, a research topic, and a family member's schooling do not want the same headings. If pages are added before a shape is agreed, the notes come in disjointed and no later pass fixes that. So:

- **Ask: "What are you actually working on, day to day? Describe the two or three kinds of thing you would want pages about."** Listen for whether there is *one consistent kind of thing* (every page is a client account; every page is a case; every page is a property) or *several kinds* (clients and also internal subjects; renovations and also finances).
- **Then show the shapes from the original author's files** and ask which the user recognises. Four are shipped in `templates/`, generalised from pages that have been in daily use for months:
  - `templates/matter-page.md`: one client, deal, case, engagement, or other ongoing thing with people and a timeline. Sections: how this file is organised, people, backstory, major milestones, current status, full history, sources.
  - `templates/domain-page.md`: a subject rather than a matter, with no cast and no chronology. Sections: how this file is organised, where it stands, positions, dynamics and reads, open questions, index, sources.
  - `templates/project-wiki.md`: a thing with a start and an end, whose page mirrors the project's own folders.
  - `templates/wiki-hub.md`: the short always-on page for an area, two or three sentences per subject with a link.
- **Agree the shape or shapes before moving on.** One kind of work usually means one template plus the hub. Several kinds mean a template per kind, named for the kind ("account page," "case page," "property page"), each adapted from a shipped one by renaming or dropping sections. Write the agreed shapes into `customization.md` under Pages; they become that layer's rules file's template section. Do not invent a third structure during setup; adapt a shipped one, and let use show what is missing.

### 4. Your existing folders, and how wikiOS lays over them
Assume the person already has a folder tree. Do not ask them to name folders; **read the tree and propose.** Open the round by asking permission in these words or close to them: **"Ok, now I'm ready to help you set up the system. I'm going to scan your folders under <the path from step 2>, two or three levels deep, so I can propose where the wikis and their subjects go. Does that work?"** On yes, list the folders under the path from step 2 (folders only, no files; skip anything that is obviously photos, downloads, archives, or application data) and show the user a short map. Then propose, and let them edit:

- **Which existing folder is each area from step 1.** For one area, the workspace itself is the layer. For work and personal side by side, point at the two folders that already hold them; if they are mixed together in one folder, say so and ask whether to separate them now or leave the wall for later.
- **Which existing folders become the subjects (spokes)** under each area, shaped by step 3: if every page is a client account, the client folders are the subjects, plus whatever internal folders exist (pricing, hiring, finances); if it is a household, the folders for home, money, health, school. Five to ten. Folders that do not fit any subject are left alone and simply not wikied; folders that are archives are named as such so the refresh skips them.
- **Which subjects already have real material** (the model can see this) and which are empty; empty ones get a placeholder page and nothing else.
- **Say plainly that the scan is not an ingest.** Close to these words: "I'm mapping folders, not reading files. wikiOS does not summarise everything you have; a lot of it will be drafts or noise. The wikis hold the decisions and facts we vet, and a file gets a line only when it carries one."
- **Nothing moves (unless the user asks).** Say so: "Nothing moves. I add wiki pages and a log; I do not rename or reorganise anything, unless you ask me to." wikiOS adds a `wiki.md` to the folders that become subjects and a hub `wiki.md`, `log.md`, and `Logs/` at each layer's root. If the user does want to reorganise, that is a separate job, planned first (wiki-os §3), not part of setup.

- **Projects, from the same scan.** If the tree shows things with a start and an end (a build, a case, a renovation, a book), say what pattern they already follow and propose it as the project layout: the stage folders they move through *(default if none exist: Planning, Active, Completed, plus an Archive the refresh skips)*, what one project folder contains *(default: Overview, Research, Options, Budget, Execution, Records)*, and the tag words for project entries *(show the shipped list; ask which words are wrong for this work)*. If there are no projects, say so and skip.

Only if the workspace is empty: propose the subjects from the answers in step 3 and create the folders.

Two small settings while here: hub word cap *(default: 800 to 1200 words)*, and whether pages carry status tags (Settled, Open) or say their uncertainty in prose *(default: prose only)*.

### 5. Privacy
Two plain questions.
- "Is there a wall between anything in your folders that the wikis must never mix? For example personal versus company material, or HR files versus what employees may see, or one client versus another. If so, point those things out." *(Each wall becomes a privacy rule in the folders on either side of it, and decides which folder may read which: the private side may read the shared side, never the reverse.)*
- "Is there anything you never want the AI to see at all?" Then the honest answer: "Not giving a folder a wiki does not stop me reading it if it sits under the folder we set up. The strong fix is to move that material outside this folder altogether. The weaker fix is a rule in `customization.md` telling me to ignore it, which I will follow, but it is a rule, not a lock." *(Also say plainly, not only if asked: the AI vendor sees whatever a session shows it, and the sync provider already holds the files; wikiOS adds no other destination.)*

### 6. Key files: what the model must read before certain tasks
Ask: "Are there documents you would want the model to read every time before it does a certain kind of work?" Examples from the origin install: a negotiation-principles file before any deal conversation; a legal style guide before drafting a contract; a voice guide before drafting anything under the owner's name; a how-to before touching a spreadsheet model. For each: the file, and the trigger ("before X, read Y"). These go into `customization.md` under **Key files**, and the model treats each as a standing instruction. The author's own key files, for context: negotiation rules, a writing-style guide, a task list and a meeting list. If the user wants the writing guide, start `customization/writing-style.md` from the template and explain the capture loop (after they send something you drafted, keep their final and the lesson). If the user has none yet but wants one (a voice guide, a house style, a set of principles), do not write it during setup: record it as an open item in the hub's Open questions and in `customization.md`, so the refresh keeps surfacing it until it is built. Otherwise leave the section with one example line so they know where it goes.

### 7. How the model should behave
One question, in the model's own voice, with examples so it is answerable: "There are already rules about how I should behave with you, baked into `LLM-rules.md`. You can read them, and we can edit them or I can suggest changes as we go. Is there anything I should keep in mind for now? People often say things like: ask before you touch anything in a certain folder; keep answers short; never use a particular word; always show me the before and after when you propose a change." *(Record any answer as the first entry in `customization/LLM-rules-origins.md`; if it should govern every session, propose the one-line version for `LLM-rules.md`. Mark any module the user does not want as switched off in `customization.md`; the three optional modules are negotiation and deals, writing in the owner's voice, daily files and tools.)*

### 8. Engines: processes you run again and again
Ask: "Is there a job you do repeatedly that has the same steps each time?" A research sweep across many sources, a reader panel on a draft, a comps pull, a weekly digest. Each becomes an **engine**: its own folder with a plain-language `workflow.md` (what it does, what can go wrong), a `plan.md`, its inputs and outputs, and a `Logs/` folder; the model runs it the same way each time and the outputs are never treated as canonical facts until a person has looked at them. Record the list in `customization.md` under **Engines**, even if it is empty. Do not build engines during setup; note them and build the first one when the user asks. If the user has none but wants one, record it as an open item in the hub's Open questions and in `customization.md`, so it comes back up at the next refresh rather than being forgotten.

### 9. Meetings and notes: how new information reaches the wikis
This is the main way the wikis grow, so give it its own round. Ask, close to these words: "A big part of growing the wiki will be my notes from your meetings and calls. Do you type those out, use a transcript service, or dictate? Where do they get saved, and should that be one place or a folder per project? Anything I should know about how they arrive, such as a recorder that mixes up who said what?" *(The answers go into `customization.md` under Meeting notes, with the location per project or one place, and into a how-to under `customization/howtos/` for the tool and its quirks. These notes are what "update the wikis" reads as its main inflow, wiki-os §8 step 3. If the user has no habit yet, propose one: one file per meeting, named with the date and topic, saved in the project's or matter's folder, and the model summarises it into the wiki at the next conversation or refresh.)*

### 10. The upkeep, explained once, then confirm
Tell the user, in these words or close to them: *"Here's how we stay up to date. I'll make a log of each conversation we have. You'll have meeting transcripts or notes saved where we agreed in the last round. You may also make separate notes in a project's `log.md`. All of this is good information for the wikis. I'll ask you about adding basic information during each conversation or after each meeting. But once a week or so, you'll want me to do a scan across the whole system. That does two things: first, it makes sure everything important has been incorporated (not every file; only the decisions and facts worth keeping), and if something is an important decision or viewpoint, I'll confirm it's actually your view before adding it. Then, after I add it, I check the wikis against each other to make sure there aren't any conflicts. The way you kick this off is by saying **'update the wikis'**. Anything you want to change about that?"* Then read `customization.md` back in full, take corrections, and build.

---

## Part C. What to build

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
    history/              decision records and, in history/Logs/, system-level session logs
  <Layer folder>/         one per layer: CLAUDE.md, wiki.md (the hub), log.md (a buffer), Logs/
    <Spoke folder>/       one per subject: wiki.md and the files it covers
    Projects/ ...         if the layer runs projects; each project has its own hidden .canvas/ folder
```

**How the entry file works.** Claude Code loads `CLAUDE.md` from the working directory and every folder above it, and a line reading `@.system/LLM-rules.md` pulls that file in at launch. So the behaviour rules are active from the first message. Cursor reads `.cursorrules` or `AGENTS.md`; other tools have their own. If the user's tool has no import, paste the rules file's body into the entry file and note in `customization.md` that the two must be kept in step.

**What a page looks like.** Frontmatter (a block of `field: value` lines between `---` markers: title, description, type, status, dates, tags), then the body in plain sentences with headings, then a `## Sources` section at the bottom with one bullet per dated source. Links are ordinary markdown links to other files by relative path. `templates/wiki-hub.md`, `templates/matter-page.md`, `templates/domain-page.md`, and `templates/project-wiki.md` are finished examples.

1. `.system/` in the user's work folder (the repo's `system/` folder is the source; the install's copy is the hidden `.system/`). Into it: `LLM-rules.md`, `wiki-os.md`, and `githubsync.md` copied unchanged (record each `schema_version` as the install's `upstream_version`); `customization.md` from `templates/customization.md` with every answer filled in; and the folder `customization/` holding one `<layer>-rules.md` per layer (from `system/layer-rules-template.md`, differences filled), `project-rules.md` (from `system/project-rules.md`, folder names and tags filled), `LLM-rules-origins.md` (blank template), `writing-style.md` if that module is on, `templates/` (the hub, matter, domain, and project page templates, adapted as agreed in step 3; project layout from step 4), and empty `howtos/` and `tools/`. Beside `customization/`, not inside it: `snapshots/<layer>/`, `state/`, and `history/` with a `Logs/` folder in it.
2. The root entry file from `templates/CLAUDE-root.md` with the import line, and one entry file per layer from `templates/CLAUDE-layer.md`, each stating the layer's privacy rule.
3. Per layer: a hub `wiki.md` (`status: draft`, seeded from the interview, under the word cap), spoke folders with stub `wiki.md` files, `log.md` from `templates/log.md`, and `Logs/`.
4. The project folder template if projects are on. Each project carries a hidden `.canvas/` folder (its own small copy of the machinery): `schema.md` copied from `customization/project-rules.md`, `CLAUDE.md` from `templates/CLAUDE-project.md`, and empty `log.md`, `inbox/`, `raw/`, `snapshots/`, `templates/`.
5. `templates/CLAUDE-global.md` into the tool's global config, only if the user said yes in step 2.
6. A first session log in `.system/history/Logs/` recording the setup, with every decision and every default the user accepted.

**First-run checklist, done with the user watching:** open a fresh session at the workspace root and confirm the entry file and `LLM-rules.md` loaded (in Claude Code, `/context` lists them under Memory files). Drop one test note in a layer's `log.md`. Add one test meeting note. If projects are on, create one test project from the template and put a document in it. Say **"update the wikis"** and confirm it reads the project, the note, and the buffer, proposes entries, and ends with a lint. End the session and confirm a log landed. Then delete the test material.

**What to say at the end.** Where the three root files are and that `customization.md` is theirs to edit; that everything under `customization/` is theirs and never ships; the one command, run every week or two, and the reminder if two weeks pass; the permission mode chosen and how to change it; and that the first week is for watching what the model does and correcting it, because every correction becomes a dated line in the origins file and, if it should govern every session, a proposed line in `LLM-rules.md`.

---

## Vocabulary, for the person reading over the model's shoulder

**Layer:** one top-level folder with its own privacy rule. **Hub:** a layer's always-on `wiki.md`. **Spoke:** a subject folder with its own `wiki.md`. **Matter page:** the page about one client, deal, case, or ongoing matter. **Project:** a folder with a start and an end that carries its own copy of the project rules. **Ingest:** read a folder's new files and propose what the wiki should say about them. **Snapshot:** a dated copy of a page taken before it is changed. **Lint:** a check for contradictions, stale sections, and broken links. **Frontmatter:** the `field: value` block at the top of a file. **Tier 1 / Tier 2:** written directly / asked about first. **Engine:** a repeatable multi-step job with its own folder and written steps. **Key file:** a document the model must read before a named kind of task. **§:** section; "wiki-os §6" is section 6 of `wiki-os.md`.

## A note on markdown, for whoever wants it

**What a "wiki" page is.** Just a text file. Each page is a file ending in `.md`, written in **markdown**, which is ordinary text with a few light conventions: a line starting with `#` is a heading, a line starting with `-` is a bullet, `**bold**` is bold, and a link is `[words](path/to/file.md)`. That is nearly all of it, and you do not have to learn it, because the model writes the pages; you read them. They open in anything that opens text: Notepad or TextEdit, Word, your phone's notes app. If you want them to look nice, free editors made for markdown show the headings and links formatted: **Obsidian** and **Typora** are the common ones on Mac and Windows, **iA Writer** on Mac and iPhone, and VS Code if you already have it. None of this is programming. It is the same kind of file a README on a website is.

