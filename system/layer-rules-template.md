---
title: Layer Rules — template for one layer's filing rules (upstream; formerly Hub Layer Wiki Schema)
description: How to maintain a human-owned hub-and-spoke wiki layer. Human-owned, propose before changing positions for the hub, source-anchored, one canonical home per fact. Installs copy and adapt this file.
type: schema
status: current
created: 2026-07-03
updated: 2026-09-06
canonical: system/layer-rules-template.md
schema_version: 8
derived_from: Canvas firm install corporate-rules.md v12 / public-rules.md v3 / family-rules.md v2 (2026-09-06)
tags: [system, schema, hub, canvas]
---

# Layer rules — template (formerly Hub Layer Wiki Schema)

> **Renamed and relocated 2026-09-06.** Installs copy this file into `.system/customization/` (as `<layer>-rules.md` or `project-rules.md`). v5 recorded the rename and new paths. v6 (2026-09-06, after a lint) removes the standing rules and the six-step log routine that every layer shared; they now live once in wiki-os §9 and §5, and this file carries only a layer's differences.

This governs a human-owned wiki layer: one always-on hub plus read-on-demand spokes. The cross-cutting rules — how to write, how to run big projects, how to log sessions, the freshness check, the write tiers — live once in this layer's `.system/wiki-os.md`; read that alongside this file. This schema covers only what is specific to maintaining the hub layer.

## The model
One lean, always-on hub (`wiki.md` at the layer root) points to many read-on-demand spoke wikis (each spoke folder's `wiki.md`), each the single canonical owner of its domain. The standing rules every human-owned layer shares are wiki-os §9; the Rules section below holds only what this layer sets for itself.

## Rules — this layer's differences
- **Privacy.** If the install declares this layer private, never share its contents or copy them into any shared space. If the install has a shared layer, shared facts live once there and this layer points down to them (reach direction: private may read shared, never the reverse).
- **Hub cap:** <e.g. 800 to 1200 words>. Keep the hub lean; push depth into spokes.
- **Status tags:** <none, uncertainty in prose only (recommended); or the tag set this layer uses, human-verified>.
- **Snapshots:** `.system/snapshots/<layer>/`.

## File structure — fixed section templates
Pages in a hub layer grow by accretion: new facts get appended wherever there is room, so a page's current state ends up buried under superseded reads, and single paragraphs run past 4,000 characters. The fix is that every substantive page uses one of a small number of **fixed section structures**, so a reader always knows where to look.

Two templates cover most hub layers. An install may rename or extend them, but should keep the set small and fixed.

**Template A — matter pages.** Anything about a specific counterparty, deal, case, or ongoing matter.

    0. How this file is organised
    1. Where it stands     — true right now; rewritten in place, never accretes
    2. Positions           — what the owner decided, each dated. Adopted only.
    3. People              — role in THIS matter; link out for the standing profile
    4. History             — newest first; never silently rewritten
    5. Dynamics            — the candid read. Nothing here is a commitment.
    6. Open questions      — and what would settle each
    7. Documents           — where everything else lives
    ## Sources

**Template B — domain spokes.** A subject area rather than a matter.

    0. How this file is organised
    1. Where it stands
    2. Positions
    3. Dynamics & reads
    4. Open questions
    5. Index
    ## Sources

- **History and People stay out of Template B.** A domain has no chronology or cast. Do not scaffold empty versions — forcing sections is what makes structure feel bureaucratic. Where a domain genuinely carries a chronology, it graduates to its own page listed in Index.
- **A Template B page with no Dynamics at all is a signal**, not a gap: it is probably a reference document rather than a spoke. Flag it rather than forcing the template.
- **Cite sections by name, never by number.** Headings may carry numbers for the eye, but every reference — in-page and cross-page — uses the name. Numbers break every pointer the moment a section is added, and they break silently.
- **When a section graduates to its own page, grep for references to it by name as well as by number**, and repoint them in the same pass. Name-based pointers are the ones a number sweep misses.
- **Readability is the only length test.** There is no word cap on a section. Content graduates to its own page when it is genuinely a separate subject, not to hit a number. The lean-hub target above is the one exception and still stands.
- **One idea per paragraph, roughly 80 words, and no line over 600 characters.**
- **Budget for the template's own overhead when applying this to a capped hub.** The "How this file is organised" section costs roughly 100–130 words. A hub already near the top of its word cap will exceed it on conversion. Decide deliberately: cut hub content to fit, or raise the cap — but never blow it silently. The origin install hit exactly this and chose to raise the cap, which is why the lean-hub target above is 800–1200 rather than the 500–1000 it was before Template B existed.

## Restructuring an existing page — verify mechanically
Converting an accreted page to a template is a presentation change: **no fact may change and no content may be lost.** If something looks wrong, stale, or self-contradictory, leave it and flag it — a conversion is exactly when things vanish unnoticed.

- **Snapshot first**, then write, then **diff the output against the snapshot mechanically** — hard tokens (money, percentages, dates, times, quoted strings) plus per-chunk word coverage. Do not rely on re-reading. In the origin install's pilot, a careful human re-read passed a draft that had silently dropped seven passages, including a whole decision block with its probability estimates; the mechanical diff caught all seven.
- **When the diff reports a loss, restore the wording and re-run.** Do not rationalise a low-coverage chunk as "captured in substance."
- **Never promote a proposal into a Positions section during a conversion.** Positions holds only what the owner adopted. Promotion is a separate, deliberate act. This is the failure mode that matters most, and it is the one a mechanical diff cannot catch.
- Splitting a very long paragraph is an editing judgement, not a mechanical reflow — you are deciding what was one idea and what was four. Where a split is genuinely ambiguous, keep the sentences together.

## Capture buffer
`log.md` at the layer root`. Emptied by **"update the wikis"** (wiki-os §8 step 4). "Process the logs" and its aliases are retired (2026-09-07).

## How this fits the rest of the install
- `.system/wiki-os.md` — the cross-cutting rules shared by every layer. Linked, not restated here.
- `.system/customization/project-rules.md` — the canonical schema for the **automated per-project wikis** in the install's projects area. That is a different layer with its own machinery; this hub schema does not govern it.
- The install's *How It Works* page is the plain-language explainer for humans. This schema is the operative rulebook; the explainer carries no rules of its own.
