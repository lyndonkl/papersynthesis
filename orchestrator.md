# papersynthesis — Orchestrator

This is the local control file for the weekly paper-synthesis project. It is the only place absolute paths live. The `paper-synthesizer` agent (in the shareable Claude Code agents repo) is path-agnostic; this file tells you how to invoke it correctly against this folder.

---

## What this project is

Each Monday morning, scan bioRxiv, medRxiv, and PubMed for papers posted in the prior 7 days that match the persistent keyword watchlist (with optional per-week overrides), filter for relevance, cluster by theme, and write a layered-reasoning synthesis with paper links. Maintain historical context across weeks.

Output for week `YYYY-WW`:
- `ops/paper-synthesizer/{YYYY-WW}-digest.md` — synthesized layered report (the thing you read)
- `ops/paper-synthesizer/{YYYY-WW}-papers.md` — full filtered paper list with rationale
- `ops/paper-synthesizer/.cache/{YYYY-WW}-{source}.json` — raw fetch results (debugging only)

---

## Project root (this machine)

```
/Users/kushaldsouza/Documents/Thinking/papersynthesis
```

This is the working directory the agent must be invoked in. The agent never resolves this itself — that is this orchestrator's job. If this folder ever moves, edit only this file.

---

## How to run the weekly digest

The clean invocation. Run from anywhere:

```
cd /Users/kushaldsouza/Documents/Thinking/papersynthesis
claude
> Run the paper-synthesizer agent for this week.
```

The agent will:

1. Confirm `orchestrator.md`, `shared-context/watchlist.md`, and `ops/paper-synthesizer/` are visible in the cwd.
2. Compute the window (today minus 7 days through yesterday, inclusive) and ISO week tag.
3. Read watchlist, source-registry, relevance-criteria, synthesis-style, this-week's overrides if any, and the last 4 weekly digests.
4. Fetch bioRxiv + medRxiv + PubMed for the window.
5. Filter, cluster, synthesize.
6. Write the two digest files + the cache.
7. Report path + counts + top-3 highlights.

### Catch-up runs

If you missed weeks, ask:

> Run paper-synthesizer for the last 3 weeks, oldest first.

The agent runs N independent passes so each newer pass has the prior digests as historical context.

### Per-week overrides

Want to add or remove a keyword for one specific week without editing the watchlist? Drop a file at:

```
ops/paper-synthesizer/overrides/{YYYY-WW}.md
```

Format:

```markdown
---
week: 2026-19
add:
  - "neural ODE"
  - "graph neural network OR GNN"
exclude:
  - "alphafold"   # too noisy this week, all of bioRxiv is on it
note: "Skipping AlphaFold spam this week."
---
```

The orchestrator reads this; the agent applies `(watchlist ∪ add) - exclude` for that week.

---

## How to update the watchlist

Edit `shared-context/watchlist.md` directly. The agent never edits it. The agent may *suggest* edits in the "Notes for next week" section of a digest — those are advisory; you decide.

---

## Folder map

```
papersynthesis/
├── README.md                            # plain-English overview, recent digests index
├── orchestrator.md                      # this file
├── design-decisions.md                  # why these choices
├── shared-context/
│   ├── watchlist.md                     # persistent keywords (you own this)
│   ├── source-registry.md               # bioRxiv/medRxiv/PubMed endpoints + query notes
│   ├── synthesis-style.md               # how the layered digest is structured
│   └── relevance-criteria.md            # keep/drop rules for the relevance filter
├── ops/
│   └── paper-synthesizer/
│       ├── {YYYY-WW}-digest.md          # the synthesized report
│       ├── {YYYY-WW}-papers.md          # the full filtered paper list
│       ├── overrides/{YYYY-WW}.md       # per-week keyword overrides (optional)
│       └── .cache/{YYYY-WW}-{src}.json  # raw fetches
├── inbox/                               # ad-hoc paper drops (out-of-scope for v1 agent)
└── archive/                             # older digests, manual move only
```

---

## Agent + skills (lives in the shareable repo)

| Component                  | Path                                                                                            |
| -------------------------- | ----------------------------------------------------------------------------------------------- |
| `paper-synthesizer` agent  | `~/Documents/Projects/claude/agents/paper-synthesizer.md`                                       |
| `fetch-preprint-recent`    | `~/Documents/Projects/claude/skills/fetch-preprint-recent/`                                     |
| `fetch-pubmed-recent`      | `~/Documents/Projects/claude/skills/fetch-pubmed-recent/`                                       |
| `paper-relevance-filter`   | `~/Documents/Projects/claude/skills/paper-relevance-filter/`                                    |
| `paper-cluster-by-theme`   | `~/Documents/Projects/claude/skills/paper-cluster-by-theme/`                                    |
| `layered-reasoning`        | `~/Documents/Projects/claude/skills/layered-reasoning/` (existing, used for synthesis)          |

The agent and skills are intentionally portable — no absolute paths, no machine-specific assumptions. They work for anyone who clones the agent repo and writes their own orchestrator pointing at their own project folder.

---

## Cadence

**Monday morning, weekly.** Lookback = the prior 7 days (Mon-of-this-week minus 7 → Sun-of-prior-week).

If you run on a non-Monday, the agent treats the invocation date as the window endpoint and computes the window backwards from there. Acceptable for catch-up; not how you'd normally use it.

---

## What lives where

- **The watchlist**: `shared-context/watchlist.md`. You own it. The agent reads it.
- **What "in-scope" means**: `shared-context/relevance-criteria.md`. You own it. The agent applies it.
- **The endpoints + query templates**: `shared-context/source-registry.md`. The agent uses it; you only edit when an endpoint changes.
- **The output style**: `shared-context/synthesis-style.md`. The agent renders to it.
- **The history**: `ops/paper-synthesizer/*-digest.md`. The agent appends weekly; never deletes.
- **The cache**: `ops/paper-synthesizer/.cache/`. Disposable; the agent regenerates.
- **The overrides for a single week**: `ops/paper-synthesizer/overrides/{YYYY-WW}.md`. You write it before the run; the agent reads it during the run.

---

## What this orchestrator never does

- It does not fetch papers.
- It does not write digests.
- It does not edit `shared-context/`.

It is a control file. The agent does the work.
