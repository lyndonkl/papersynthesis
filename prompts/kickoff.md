# Kickoff prompt — generic entry to the literature-scan project

Paste this as your first message to start any literature-scan session. Use it when you haven't yet decided whether you want a weekly run, a catch-up, or a thematic query — the coach will detect intent from your next message.

---

I'm working in my literature-scan project. The current working directory is the project root and contains:

- `orchestrator.md` — system map for the project
- `shared-context/watchlist.md` — my persistent keyword watchlist (life sciences + CS / ML)
- `shared-context/source-registry.md` — bioRxiv / medRxiv / PubMed / arXiv endpoints, plus the arXiv categories I want queried
- `shared-context/relevance-criteria.md` — keep / drop rules for filtering
- `shared-context/synthesis-style.md` — how the layered digest should be written
- `ops/paper-synthesizer/` — where weekly digests get written; subfolder `.cache/` holds raw fetch responses
- `ops/paper-synthesizer/overrides/{YYYY-WW}.md` — optional per-week keyword overrides

Read `orchestrator.md` first, then invoke the `literature-scan-coach` agent. The coach handles intent detection, window computation, and spawning the `paper-synthesizer` subagent for each run.

I'll tell you in my next message what I want done — a regular weekly run, a multi-week catch-up, an on-demand thematic question, or a re-synthesize from cache. Wait for that message before doing anything that fetches.
