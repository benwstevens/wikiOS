# Start here

<!-- Template: copy to the workspace root as CLAUDE.md (or the entry file your tool reads) and fill the placeholders. Keep it short: it points, it does not restate. The @ line below imports the behaviour rules into every session. -->

This workspace is <owner>'s <install name>, kept as LLM-maintained wikis. The system that runs them lives in one folder, **`.system/`**.

@.system/LLM-rules.md

*(If the import above did not load, you will not know the rule about ending a response with a Requests section. In that case read `.system/LLM-rules.md` now, before anything else.)*

- **`.system/LLM-rules.md`** (imported above, always on): how to work with <owner>.
- **`.system/wiki-os.md`**: how the wikis operate. Read it before maintaining any wiki: freshness check (§1), writing standard (§2), big-project SOP (§3), session logs (§4), the capture buffer (§5), write policy, facts written directly and positions asked about (§6), query workflow (§7), **"update the wikis"** (§8), the one refresh command, which ends with a lint.
- **`.system/customization.md`**: everything specific to this install. The layers and their privacy walls, project conventions, enabled modules, install-specific rules. Read it when a task touches projects, tools, or anything owner-specific.

**The layers.** <one line per layer: folder, what it is, who sees it; state which layers never read into each other>. Each layer's own `CLAUDE.md` carries its folder map and shorthand; its rules file is under `.system/customization/`.

**To answer a question:** find the relevant hub `wiki.md`, then the spoke, and answer with citations (wiki-os §7). A read-only question skips the rule ceremony. **To work on a project:** read its `.canvas/schema.md` first. **At the end of a session:** write a session log (wiki-os §4). **At the start of one:** if any `.system/state/*.last_update` marker is older than fourteen days, say so in one line and offer "update the wikis"; never run it unasked (wiki-os §8).

**The system's upstream** is the `wikiOS` repo; say "sync with upstream" to adopt improvements (`.system/githubsync.md`; rule files only, never wiki content). **How the system got this shape:** `.system/history/`.
