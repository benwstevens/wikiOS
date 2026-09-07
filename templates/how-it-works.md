---
title: <Install Name> Wiki System (How It Works)
description: Plain-language explainer of the wiki system for humans. Carries no rules of its own.
type: wiki-page
status: draft
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
tags: [system, conventions]
---
# <Install Name> Wiki System (How It Works)
> **This is the plain-language explainer, written for humans.** The operative rules a model must follow live in the schema files: the workspace root's `.system/` folder: `wiki-os.md` (cross-cutting rules), `LLM-rules.md` (how the model behaves with the owner), and `customization/<layer>-rules.md` (this layer's rules). This page exists to be read for understanding; it does not carry rules of its own.

This workspace keeps memory in editable markdown that a human can audit and fix, rather than in a model's training or hidden memory. The files win: when a model's prior knowledge conflicts with what is written here, it defers to the files and flags the conflict, and it labels general knowledge as general knowledge rather than stating it as an established fact.

## Two kinds of file
- **Knowledge files** (the wikis and their linked references) hold content and can be as long as the content needs.
- **Schema files** (`.canvas/schema.md`) hold behavioral instructions for maintaining the wiki and are kept short, around 500 to 600 words, because they compete for a model's instruction-following budget.

## Always-on versus retrieved
The hub (`wiki.md`) is a lean always-on core, aimed at 500 to 1000 words: who and what, governing principles, and an index. Depth lives in spoke wikis and linked files that are read on demand, not loaded every time.

## Hub versus project wikis
- **Project wikis** are the automated layer. They update from changed files in their project folder and carry the live state for that project.
- **The hub layer** is human-owned and deliberately edited. It is propose before changing positions: a model may propose an edit and show what changed and why, but a human approves it. No automation rewrites it on a schedule.

## Source-anchoring and status
Every claim should trace to a dated source. An unsourced assertion is a flag for a human, not a fact to state confidently. A position does not harden into "Settled" until a human confirms it.

## Snapshots
Before any edit is applied to a wiki, the current file is copied to `.canvas/snapshots/` dated `YYYY-MM-DD`. That is the undo button.

## Capture log and processing
Week-to-week notes are captured raw in `log.md` at the layer root, then integrated into the wiki by **"update the wikis"**, the one refresh command: it also sweeps session logs and meeting notes, routes each item to its one canonical home, shows a before/after diff, writes only after approval, and ends with a lint. Project notes do not go in this log; they live in each project's `01 - Overview/Logs/`, read by that project's own ingest.

## The daily refresh
Saying **"update the wikis"** refreshes everything: every live project's ingest pulls changed files into its project wiki, the log buffer is processed, and the model reports a digest of what was added and what was flagged.

## Sources
- <dated source, one per bullet>
