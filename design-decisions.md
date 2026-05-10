# Design Decisions

Why this project is shaped the way it is. Useful when you (or future-you) wonder "why didn't we just…"

## Sources: bioRxiv + medRxiv + PubMed + arXiv

bioRxiv covers life sciences preprints; medRxiv covers clinical / health-sciences preprints (same operator, same API shape, different endpoint). PubMed is where the published version eventually lands. arXiv covers CS / ML / stats / math / physics / quantitative-biology preprints — the watchlist crosses domains, so the CS-side coverage is necessary, not optional.

Reading all four sources gets you both the earliest signal (preprint) and the validated version (PubMed) for life-sciences work, plus full CS / ML coverage that bioRxiv and PubMed barely touch.

The arXiv category set is operator-controlled in `shared-context/source-registry.md`. The default is CS / ML focused (`cs.LG, cs.CL, cs.CV, cs.AI, cs.NE, stat.ML`) — adjust upward (q-bio, math, physics) when the watchlist drifts that way, or set to `null` to scan all of arXiv when the keyword filter is tight enough to handle the noise.

## Cadence: Monday morning, 7-day lookback

Monday morning means the digest is ready when you start the work week. The 7-day lookback is the cleanest unit — bioRxiv posts mostly Mon-Thu, PubMed indexes daily, and a 7-day window catches one full posting cycle without overlap.

Friday-evening cadence (the trend-scout pattern) was the alternative. Monday won because:
- A literature scan benefits from being read at the start of the week, not the end.
- Friday-evening output competes with weekend reading; Monday output competes with email.
- A weekend buffer means the bioRxiv mirror is fully populated by run time.

## Keyword watchlist + per-week overrides

A persistent watchlist preserves intent across weeks. Per-week overrides are a release valve when the field is saturated with a single topic (e.g., a major model release week) without polluting the standing list.

Considered but rejected:
- **Multiple named topic groups** (e.g., "protein-design", "single-cell" as separate digests). Adds setup cost; you can simulate this later by adding subject-area hints in cluster naming. Easy to upgrade to if needed.
- **Fully fresh keywords every week**. Loses historical continuity; the "is this topic continuing?" tag depends on stable keywords.

## Layered-reasoning synthesis (30K / 3K / 300 ft)

A weekly digest needs to serve three reading modes:
- "What changed this week?" → 30K
- "Tell me by topic" → 3K
- "Show me the actual papers" → 300 ft

Layered reasoning gives all three from one synthesis pass without copy-paste between sections. It also forces the writer (the agent) to commit to a top-line argument before listing papers, which is the part that actually saves the reader time.

## Cluster-by-theme as a hard step

Without clustering, a digest is a list. Lists do not compress. The clustering step forces the agent to answer "what are these papers collectively saying?" before describing any individual paper — and that's the question worth answering.

Clusters are *argument-shaped*, not topic-shaped. "Protein design" is a topic. "Protein design moves toward sequence+structure conditioning" is a theme. The latter is what makes a digest useful.

## Historical context = last 4 weeks

Reading every prior digest is too expensive (and there's a long tail of stale topics). Reading only this week loses continuity. Four weeks is enough to:
- Catch a preprint → journal-version migration
- Tag a continuing thread without false-positives from a one-week reappearance
- Notice watchlist drift (3+ weeks of <3 papers = watchlist too narrow)

If a topic stops appearing for 5+ weeks and then returns, the agent will treat it as new — that's fine; that's actually the right call most of the time.

## Cap at 25 kept papers per week

A weekly digest the user won't read is worse than no digest. 25 papers, distributed across 2-5 clusters, is roughly the upper bound of what fits on one screen and still gives the synthesis layer something to say per cluster. When the field genuinely produces more, the right move is to raise the relevance bar, not pad the digest.

## Two agents: literature-scan-coach (entry) + paper-synthesizer (worker)

Originally this project shipped only `paper-synthesizer` (the worker) plus a static `orchestrator.md` documentation file. That worked but forced the operator to manually compute the window, remember the catch-up loop ordering rule (oldest-first so historical context is consistent), and decide which run type to invoke.

`literature-scan-coach` is a real orchestrator agent — single entry point, runs the pre-flight check, detects intent (WEEKLY / CATCH_UP / ON_DEMAND / RE_SYNTHESIZE / OUT_OF_SCOPE), computes parameters, and spawns `paper-synthesizer` per run with explicit framing. The split keeps each agent's job small: the coach owns *what to do*, the synthesizer owns *do it*. New paper-related agents (e.g., a single-paper deep-dive) can be added later without changing the operator's UX — the coach picks them up as new intents.

## Agents path-agnostic; orchestrator file owns "where"

`literature-scan-coach`, `paper-synthesizer`, and the five supporting skills are in a shareable repo. They contain no absolute paths and no machine-specific assumptions. Anyone can clone them and point them at their own project.

This local `orchestrator.md` is the only file that knows where this project lives on disk. If you ever move the folder, you edit one file. If you ever clone this for a second domain (e.g., "papersynthesis-economics"), you copy the structure and write a second orchestrator — no agent changes.

## What's not in v1

- **Inbox processing**: dropping a single PDF or URL into `inbox/` to get an ad-hoc analysis. Out of scope; the existing `domain-research-health-science` skill handles single-paper critique well enough already.
- **PDF parsing**: the agent reads abstracts, not full text. If a paper is critical, you click through to read it.
- **Slack / email delivery**: the digest is a markdown file. You read it where you read your other notes.
- **Multiple watchlists / topic groups**: discussed above.
- **Auto-execution on a schedule**: the agent is invoked on demand. If you want true Monday automation, wire it up via `/schedule` or a cron once you trust the output.

These are easy to add later; none of them are baked in as assumptions, so adding them won't require restructuring.
