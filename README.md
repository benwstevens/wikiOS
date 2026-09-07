# wikiOS

An LLM-maintained wiki system for keeping durable, auditable knowledge in plain markdown. The system is **wikiOS**; its core rules file is `wiki-os.md`. Built by **Ben Stevens** (benwstevens.com) as an evolution of Andrej Karpathy's LLM-wiki idea and refined through daily use across a firm, its clients and negotiations, its projects, and a household. This repo is the versioned upstream: the shared rule files and blank templates, no content.

**To install: download or clone this folder, open your LLM tool inside it, and say "set up wikiOS."** It reads `SETUP.md` and asks you what it needs. In Claude Code, opened in this folder, `/setup-wiki` does the same (the command lives in this folder's `.claude/skills/`, so it exists only here, not everywhere on your machine). Claude Code will ask you to trust the folder the first time, and will ask before writing into your own workspace unless you pick a permissive mode; both are expected.

## The idea in five lines
1. **Memory lives in files, not in the model.** Everything is markdown a human can open, audit, and fix. The files win over prior knowledge.
2. **One canonical home per fact; link, never restate.** A lean always-on hub points to read-on-demand spokes and project wikis.
3. **Every claim is source-anchored** to a dated source, and every edit is snapshotted first. Unsourced = flagged, not asserted.
4. **Writes are risk-tiered:** routine, sourced additions auto-commit (Tier 1); anything that overwrites, contradicts, or hardens a claim is gated behind human approval (Tier 2).
5. **Propose in the moment, verify on refresh.** Decisions are proposed for the wiki as they happen in conversation; every session leaves a log; meeting notes and a `log.md` buffer catch what happens outside sessions. One command, **"update the wikis"**, sweeps all of it, integrates with approval, and ends with a lint. No schedule; a fourteen-day nudge.

## Repo map
| Path | What it is |
|---|---|
| `system/LLM-rules.md` | How the model behaves with the owner, every session: the Requests recap, plan-first, provenance and evidence rules, and three optional modules (negotiation, writing voice, daily tools). Imported into the workspace root entry file. |
| `system/wiki-os.md` | The cross-cutting operating rules every layer follows (freshness check, writing standard, big-project SOP, session logs, log processing, write tiers, query workflow, full refresh). Formerly `conventions.md`. |
| `system/layer-rules-template.md` | Template for one layer's filing rules (a human-owned hub-and-spoke layer). Installs copy it once per layer into `.system/customization/<layer>-rules.md`. Formerly `hub-schema.md`. |
| `system/project-rules.md` | The contract for the automated per-project wikis; each project carries a copy in its `.canvas/schema.md`. Formerly `project-schema.md`. |
| `templates/` | Starter files: root and layer `CLAUDE.md`, optional global `CLAUDE.md`, `customization.md`, `LLM-rules-origins.md`, `writing-style.md`, project `CLAUDE.md`, hub wiki, project wiki, capture log, plain-language explainer. |
| `SETUP.md` | Read this first if you are installing. Written for whatever LLM you use: explains the system, then gives it the interview to run with you, then what to build. Claude Code users can say `/setup-wiki`. |
| `system/githubsync.md` | Rule files only, never wiki content. The two passes: "port the system upstream" (install → repo) and "sync with upstream" (repo → install). Folder to folder: the install's `.system/` root against `system/`. Installs carry a copy at `.system/githubsync.md`. |
| `CHANGELOG.md` | One entry per `schema_version` bump of any `system/` file. |

## The layout an install gets (since 2026-09-06)
One folder at the workspace root, `.system/`. Its top holds what is shared with this repo (`LLM-rules.md`, `wiki-os.md`) plus `customization.md`, the install's own description. Its `customization/` folder holds everything specific to that install: one rules file per layer, the project rules with that install's folder names, the origins file behind the behaviour rules, templates, how-tos, tools. Each layer of the workspace keeps only its entry file, hub `wiki.md`, `log.md`, and `Logs/`. The rule of thumb: if a file names a person, a client, a path, or a tool, it lives under `customization/` and never ships.

## How versioning works
- Each `system/` file carries `schema_version` in its frontmatter. Any rule change bumps the version and adds a CHANGELOG entry.
- An **install** copies the `system/` files into its `.system/` folder (root files as they are; the layer template once per layer and the project rules into `.system/customization/`). The install's copies become the *canonical* files for that install (`canonical:` points inside the install), and they record where they came from with `upstream:` (repo path) and `upstream_version:` frontmatter fields.
- Daily work never touches this repo: the freshness check (conventions §1) runs entirely inside the install, offline.
- **Syncing an install with upstream** is a deliberate, occasional pass: diff the install's canonical files against `system/`, show the human what changed, and update the install copies (and their `upstream_version`) only on approval. Install-specific adaptations are expected — the install records them in its own `.system/customization.md`.
- Improvements flow both ways: when an install evolves a rule worth keeping, port it back here, bump the version, and let other installs adopt it on their next sync.

## What this repo is not
No wiki *content* lives here — no firm knowledge, no family knowledge. Content stays in each install's own storage. This repo is only the rule set and templates, so it stays safe to share with anyone.
