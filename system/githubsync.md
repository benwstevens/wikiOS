---
title: GitHub sync — how an install and the upstream repo exchange rule files
description: The two deliberate, human-approved passes. "Port the system upstream" carries a generalizable rule change from an install's .system/ into the repo's system/. "Sync with upstream" brings repo improvements back into an install. Never automatic; daily work never depends on the repo.
type: rules
status: current
created: 2026-07-03
updated: 2026-09-06
canonical: system/githubsync.md
schema_version: 1
tags: [system, sync]
---

# GitHub sync — keeping an install's rule files and the upstream repo in step

**This file is about rule files only.** It has nothing to do with wiki content, session logs, meeting notes, or the "update the wikis" refresh (wiki-os §8). It describes the occasional, by-hand pass that moves a changed rule between an install's `.system/` and the GitHub repo.

This file is itself one of the shared root files: an install keeps a byte-identical copy at `.system/githubsync.md`, so a session inside the workspace knows the procedure without opening the repo. The shared root files are `LLM-rules.md`, `wiki-os.md`, and `githubsync.md`; `customization.md` is the install's own.

Rules evolve fastest in the Canvas install. They flow in two deliberate, human-approved passes — never automatically. Both are things you say to the model in a session that can reach both the repo and the install in question.

```
an install's .system/  ──"port the system upstream"──▶  repo system/  ──"sync with upstream"──▶  other installs' .system/
(rules evolve here)                                (versioned master)                   (adopt on approval)
```

## Pass 1 — "port the system upstream" (Canvas → repo)

**When:** any time a Canvas canonical file gets a `schema_version` bump (the existing mechanism already forces that on every rule change), or on a periodic sweep.

**How Claude runs it:**
1. Read the Versions table in the install's `.system/customization.md`. Diff the install's `.system/LLM-rules.md`, `.system/wiki-os.md`, and `.system/githubsync.md` against the same names under `system/` (these should differ only in naming), and the files under `.system/customization/` against `system/layer-rules-template.md` and `system/project-rules.md`. Any install file whose `schema_version` is higher than the `upstream_version` it records has changes to consider.
2. For each change, classify it:
   - **Generalizable** (a better rule any install would want) → port it into the matching `system/` file in de-branded language, bump that file's `schema_version`, add a CHANGELOG entry.
   - **Install-specific** (folder names, privacy routing, named tools) → do not port; it belongs under the install's `customization/` and in the divergences list of its `customization.md`.
3. Update the Versions table in the install's `customization.md` and the `upstream_version` frontmatter of each synced file.
4. Show all diffs; the human approves; commit with a message naming the source change; push.

## Pass 2 — "sync with upstream" (repo → an install)

**When:** after a port, or whenever you want — the family install keeps working on its own copies regardless. Monthly is plenty.

**How Claude runs it:**
1. In the install, read each `.system/` rules file's `upstream_version` frontmatter (also summarised in `customization.md`). Compare against the repo `system/` files' `schema_version`. (Run `git pull` first if the repo has a remote.)
2. For each file where upstream is newer: read the CHANGELOG entries in between, show the diff, and propose an updated install copy that **preserves the install's recorded adaptations** (listed in its `customization.md`; anything under `customization/` is by definition the install's own).
3. On approval: snapshot the old copy into the install's `.system/snapshots/`, write the new one, bump its `schema_version`, set `upstream_version` to the adopted repo version.
4. Done — no further steps needed for projects. Each project's local `.canvas/schema.md` catches up automatically through the existing **Step 0 freshness check** the next time that project runs.

## What keeps this safe
- **Nothing syncs silently.** Both passes are propose-diff-approve, same as every other gated write in the system.
- **Divergence is visible, not forbidden.** Each install's `customization.md` records intentional differences, so a diff never "corrects" an adaptation by accident.
- **Daily work never depends on the repo.** Installs are self-canonical; if the repo is unreachable, nothing breaks.
