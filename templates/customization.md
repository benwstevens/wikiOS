---
title: Customization — this install
description: What is specific to <owner>'s <install name>. The layers and their privacy walls, the project conventions, the enabled modules, the install-specific rules that never ship upstream, and the versions last synced with the repo. Hub for the customization/ folder.
type: install-profile
status: current
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
tags: [system, install, customization]
---

# Customization — this install

Root files in `.system/` (`LLM-rules.md`, `wiki-os.md`) carry the same rules as the upstream repo. Everything here and under `customization/` is this install's. If a root file turns out to name something specific to this install, that is a bug: move the line here.

## The install
- **Owner:** <name>. **Root:** <path>. **Tool:** <Claude Code / other>; the root entry file imports `LLM-rules.md`.
- **Names and titles to get exactly right:** <list>.
- **Upstream:** the `wikiOS` repo. Sync is a deliberate pass, never automatic (`.system/githubsync.md`; rule files only).

## Layers and privacy walls
| Layer | Folder | What it holds | Rules file | Wall |
|---|---|---|---|---|
| <name> | `<folder>/` | <one line> | `customization/<layer>-rules.md` | <who sees it; what it may read> |

Each layer keeps only `CLAUDE.md`, `wiki.md`, `log.md`, and `Logs/`. Each layer's `CLAUDE.md` carries its own folder map and shorthand.

## Projects
- Lifecycle folders: <e.g. `Projects/01 - Planning/`, `02 - Active/`, `03 - Completed/`>; the template lives at <path>.
- Project folder template: <section list>.
- Tags: <list, or "shipped default">.
- Every project's `.canvas/schema.md` is a copy of `customization/project-rules.md` and points its `canonical:` there.

## Tool and permission mode
- **Tool:** <Claude Code / Cursor / other>. **Entry file:** <CLAUDE.md with the `@.system/LLM-rules.md` import / pasted body>.
- **Permission mode:** <e.g. Accept edits for everyday wiki work; Plan for big jobs; Manual while learning>. Changed by <where the setting lives>.
- **Sync:** <Dropbox / iCloud / OneDrive / none>; workspace marked available offline: <yes/no>.

## Key files: read these before the named task
| Before doing this | Read this |
|---|---|
| <e.g. any negotiation or deal conversation> | <`<layer>/Negotiation/wiki.md`> |
| <e.g. drafting a contract or legal letter> | <the legal style guide> |
| <e.g. drafting anything under the owner's name> | `customization/writing-style.md` |

## Engines: repeatable processes
| Engine | What it does | Where |
|---|---|---|
| <name> | <one line> | <`<layer>/Engines/<name>/`, with workflow.md, plan.md, Logs/> |
(None yet is a fine answer. Build the first one when the owner asks; outputs are never canonical until a person has looked at them.)

## Modules enabled
<which optional sections of `LLM-rules.md` are on; which are switched off here and why. The shared file is never edited.>

## Install-specific rules (never ship upstream)
- <rules that name a person, client, tool, or path>

## What is in `customization/`
- `<layer>-rules.md` files; `project-rules.md`; `LLM-rules-origins.md`; `writing-style.md` (if on); `templates/`; `howtos/`; `tools/`.

## Versions
| File | Version | Upstream file | Upstream version at last sync |
|---|---|---|---|
| `LLM-rules.md` | | `system/LLM-rules.md` | |
| `wiki-os.md` | | `system/wiki-os.md` | |
| `customization/<layer>-rules.md` | | `system/layer-rules-template.md` | |
| `customization/project-rules.md` | | `system/project-rules.md` | |

## Divergences from upstream (by design)
- <list>

## History
`.system/history/` holds the dated decision records, plans, and system-level session logs, starting with the setup session.
