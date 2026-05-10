# Kickoff prompt — hand the session over to the project's orchestrator

This is the only prompt you usually need. Paste it as your first message in a Claude Code session that you've started from inside this project's root folder.

It does three things:

1. Sets the working-context for Claude (you're in the papersynthesis project; here's where the watchlist, source-registry, criteria, style, and prior outputs live).
2. Spawns the `papersynthesis-orchestrator` subagent and hands the conversation off to it.
3. Stops there — the orchestrator will then ask you (in plain English) what kind of run you want, or detect intent from your follow-up message ("run the weekly digest", "catch me up on 3 weeks", "what's new on diffusion models", "re-run last week from cache", "deep-read the Smith paper from week 19", etc.).

Make sure you've run Step 4 of the README (install `papersynthesis-orchestrator` to `~/.claude/agents/`) at least once on this machine. Otherwise the Agent tool will not find the orchestrator.

---

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
