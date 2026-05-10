# papersynthesis

Weekly compressor of new biology / clinical / CS / ML research, scoped to your keyword watchlist.

Each Monday: 1 digest, 2-5 thematic clusters, ≤25 papers worth your attention, and direct links to the originals. Filtered against bioRxiv, medRxiv, PubMed, and arXiv for the prior 7 days. Synthesized using layered reasoning (30K → 3K → 300 ft).

The project is run by two agents in the shareable Claude Code agents repo: `literature-scan-coach` is the entry point (intent detection + spawning), `paper-synthesizer` is the worker that fetches, filters, clusters, and writes the digest. You don't invoke `paper-synthesizer` directly — the coach does.

## Quick start

1. Open this folder, edit `shared-context/watchlist.md`, and replace the placeholder keywords with the topics you actually care about.
2. Skim `shared-context/relevance-criteria.md` and `shared-context/source-registry.md` (especially the arXiv categories block) and adjust to taste.
3. Make sure the `literature-scan-coach` and `paper-synthesizer` agents are installed where Claude Code can find them — see the "Agents + skills" section in `orchestrator.md` for plugin / symlink / copy options.
4. Run the weekly digest:
   ```
   cd /Users/kushaldsouza/Documents/Thinking/papersynthesis
   claude
   # paste prompts/weekly.md (or prompts/kickoff.md if you'd like to decide the run type from your follow-up)
   ```
5. The digest will land at `ops/paper-synthesizer/{YYYY-WW}-digest.md`. The full filtered paper list lives next to it as `{YYYY-WW}-papers.md`.

For other run types (catch-up, on-demand thematic, re-synthesize from cache) see `prompts/README.md`. For everything else — cadence, folder map, agent install — see `orchestrator.md`.

## Recent digests

<!-- the agent appends one line here per run, newest first -->

_(none yet)_
