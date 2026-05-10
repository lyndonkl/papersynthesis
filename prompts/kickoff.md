I'm working in the papersynthesis literature-scan project. The current working directory is the project root and contains:

- `orchestrator.md` — the project's orchestrator agent definition (also installed at `~/.claude/agents/papersynthesis-orchestrator.md` so the Agent tool can spawn it)
- `shared-context/watchlist.md` — my persistent keyword watchlist (life sciences + CS / ML)
- `shared-context/source-registry.md` — bioRxiv / medRxiv / PubMed / arXiv endpoints + the arXiv categories I want queried
- `shared-context/relevance-criteria.md` — keep / drop rules for filtering
- `shared-context/synthesis-style.md` — Pass A within-paper + Pass B across-papers layered-digest rendering rules
- `ops/paper-extractor/` — per-paper extraction notes (Pass 1 + Pass 2; appended Pass 3 only on explicit deep-read)
- `ops/paper-synthesizer/` — weekly digests, per-paper Pass A summaries, and a `.cache/` of raw fetches
- `ops/paper-synthesizer/overrides/{YYYY-WW}.md` — optional per-week keyword overrides

Use the Agent tool with `subagent_type=papersynthesis-orchestrator` to spawn the project's orchestrator and hand this session over to it. Pass it the project context above. The orchestrator will:

- run its pre-flight check on the project files
- detect intent from my follow-up message (or ask if ambiguous)
- fan out subagents per stage — `literature-scan-coach` (search-only), `paper-extractor` × N (Pass 1 + Pass 2), `paper-synthesizer` × N (Pass A per paper) and × 1 (Pass B across papers)
- exchange context between stages and surface back a single combined report

Wait for me to tell you which run I want before doing any fetches or spawning extraction subagents.
