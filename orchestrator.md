# papersynthesis — Orchestrator

This is the local control file for the weekly literature-scan project. It is the only place absolute paths live. The agents that run this project (`literature-scan-coach` as the entry point, `paper-synthesizer` as its worker) are path-agnostic and live in the shareable Claude Code agents repo; this file tells you how to invoke them correctly against this folder.

The recommended way to start a session is to paste one of the prompts in `prompts/` — see `prompts/README.md` for the menu. The prompts set project context and explicitly invoke `literature-scan-coach`, which then routes to the right workflow.

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

The clean invocation. Open Claude Code in the project folder and paste a prompt:

```
cd /Users/kushaldsouza/Documents/Thinking/papersynthesis
claude
# then paste prompts/weekly.md (or prompts/kickoff.md if you want to decide the run type from your follow-up)
```

What happens:

1. The `literature-scan-coach` agent runs its pre-flight check (confirms `orchestrator.md`, `shared-context/watchlist.md`, `shared-context/source-registry.md`, and `ops/paper-synthesizer/` are visible).
2. It detects intent (WEEKLY / CATCH_UP / ON_DEMAND / RE_SYNTHESIZE / OUT_OF_SCOPE) from your prompt.
3. For a weekly run, it computes the window (today minus 7 days through yesterday, inclusive) and ISO week tag.
4. It spawns the `paper-synthesizer` subagent with explicit per-run parameters (window, week tag, run type).
5. The subagent reads watchlist + source-registry + relevance-criteria + synthesis-style + last-4-weeks digests, fetches bioRxiv + medRxiv + PubMed + arXiv, filters, clusters, synthesizes, and writes the two digest files + cache.
6. The coach surfaces back the digest path, kept/dropped counts, the 30,000-ft preview, and any warnings.

### Catch-up runs

Use `prompts/catchup.md` and fill in `N`. The coach runs N independent passes oldest-first so each newer pass has the prior digests as historical context.

### On-demand thematic queries

Use `prompts/on-demand.md` and fill in topic + window. The coach writes a one-shot per-week override file and runs the subagent against it; the persistent watchlist is not modified.

### Re-synthesize after editing criteria

Use `prompts/re-synthesize.md`. The coach skips fetches and re-runs filter + cluster + synthesis from the `.cache/` JSON, so you can see what your relevance-criteria or synthesis-style edits actually changed.

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
├── prompts/                             # paste-and-go session kickoff prompts
│   ├── README.md                        # menu of prompts
│   ├── kickoff.md                       # generic entry; coach decides intent from follow-up
│   ├── weekly.md                        # standard Monday weekly run
│   ├── catchup.md                       # back-fill N missed weeks (oldest-first)
│   ├── on-demand.md                     # off-cadence thematic question
│   └── re-synthesize.md                 # re-render an existing digest from cache
├── shared-context/
│   ├── watchlist.md                     # persistent keywords (you own this)
│   ├── source-registry.md               # bioRxiv/medRxiv/PubMed/arXiv endpoints + query notes
│   ├── synthesis-style.md               # how the layered digest is structured
│   └── relevance-criteria.md            # keep/drop rules for the relevance filter
├── ops/
│   └── paper-synthesizer/
│       ├── {YYYY-WW}-digest.md          # the synthesized report
│       ├── {YYYY-WW}-papers.md          # the full filtered paper list
│       ├── overrides/{YYYY-WW}.md       # per-week keyword overrides (optional)
│       └── .cache/{YYYY-WW}-{src}.json  # raw fetches
├── inbox/                               # ad-hoc paper drops (out-of-scope for v1 agents)
└── archive/                             # older digests, manual move only
```

---

## Agents + skills (lives in the shareable repo)

| Component                    | Path                                                                                            |
| ---------------------------- | ----------------------------------------------------------------------------------------------- |
| `literature-scan-coach`      | `~/Documents/Projects/claude/agents/literature-scan-coach.md` (entry point — invoked by prompts)|
| `paper-synthesizer`          | `~/Documents/Projects/claude/agents/paper-synthesizer.md` (worker, spawned by the coach)        |
| `fetch-preprint-recent`      | `~/Documents/Projects/claude/skills/fetch-preprint-recent/`                                     |
| `fetch-pubmed-recent`        | `~/Documents/Projects/claude/skills/fetch-pubmed-recent/`                                       |
| `fetch-arxiv-recent`         | `~/Documents/Projects/claude/skills/fetch-arxiv-recent/`                                        |
| `paper-relevance-filter`     | `~/Documents/Projects/claude/skills/paper-relevance-filter/`                                    |
| `paper-cluster-by-theme`     | `~/Documents/Projects/claude/skills/paper-cluster-by-theme/`                                    |
| `layered-reasoning`          | `~/Documents/Projects/claude/skills/layered-reasoning/` (existing, used for synthesis)          |

For Claude Code to discover these at runtime, they must be in `~/.claude/agents/` and `~/.claude/skills/` — not just the source-of-truth git repo at `~/Documents/Projects/claude/`. Three install options, in order of preference:

- **Plugin install** (cleanest): `/plugin install thinking-frameworks-skills` from the lyndonkl/claude marketplace.
- **Symlink** (always-current): `ln -s ~/Documents/Projects/claude/agents/literature-scan-coach.md ~/.claude/agents/literature-scan-coach.md` and equivalent for `paper-synthesizer.md` and the five skills folders.
- **Copy** (manual): `cp` after each merge.

The agents and skills are intentionally portable — no absolute paths, no machine-specific assumptions. They work for anyone who clones the agent repo and writes their own orchestrator pointing at their own project folder.

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
