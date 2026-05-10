# papersynthesis

A weekly literature-scan project that produces a tight, layered digest of new biology + clinical + CS / ML research scoped to a keyword watchlist you control.

Each Monday: 1 digest, 2-5 thematic clusters, ≤25 papers worth your attention, direct links to the originals, plus per-paper structured extraction notes you can drill into. Filtered against bioRxiv, medRxiv, PubMed, and arXiv for the prior 7 days. Synthesized using layered reasoning (30K → 3K → 300 ft).

## Architecture (at a glance)

You invoke a single agent — `papersynthesis-orchestrator` (defined in this repo at `orchestrator.md`). It owns the project's context and fans out subagents per stage:

```
            papersynthesis-orchestrator (this project's agent — entry point, owns context exchange)
                          │
            ┌─────────────┼──────────────────────────┐
            ▼             ▼                          ▼
       Stage 1        Stage 2 + 4              Stage 5 + 6
       Search         Extract                  Synthesize

  literature-     paper-extractor       paper-synthesizer
  scan-coach      × N (per paper)       × N per paper (Pass A)
  (search-only)   Pass 1 every paper    × 1 across papers (Pass B)
                  Pass 2 only on KEEPs

  returns:        appends to            writes per-paper summaries
  paper records   ops/paper-extractor/  + the weekly digest
```

- **`papersynthesis-orchestrator`** — defined in this repo at `orchestrator.md`. Project-specific entry point. Reads project context (watchlist, source-registry, relevance-criteria, synthesis-style, last-4-weeks digests), runs pre-flight, fans out subagents, exchanges context between stages, surfaces the final report.
- **`literature-scan-coach`** — generic search/retrieve subagent. Invoked by the orchestrator in search-only mode: fetches bioRxiv / medRxiv / PubMed / arXiv, dedupes, returns the paper-records list.
- **`paper-extractor`** — per-paper structured-extraction worker, spawned in parallel. Applies a Three-Pass + Five-Cs reading methodology *internally* (questions are the agent's checklist; they're not asked of you). Pass 1 inspectional on every paper; Pass 2 content-grasp on relevance-filter KEEPs; Pass 3 only on explicit operator request.
- **`paper-synthesizer`** — synthesis worker, spawned in two modes by the orchestrator. Pass A: per-paper, in parallel — translates each extraction into a reader-friendly summary (lighten cognitive load, preserve hedging). Pass B: one invocation across all per-paper outputs — clusters by theme and writes the layered weekly digest.

`papersynthesis-orchestrator` lives in this repo (project-specific). The other three agents and the supporting skills are domain-neutral and live in the [`lyndonkl/claude`](https://github.com/lyndonkl/claude) repo.

---

## Run this yourself

These steps assume you're starting from scratch on a new machine.

### 1. Prerequisites

- **Claude Code** installed and signed in. ([install instructions](https://docs.claude.com/en/docs/claude-code))
- Git, with a GitHub account if you plan to clone over HTTPS.

### 2. Install the agents and skills

The pipeline depends on four agents and a dozen-plus skills that live in [`lyndonkl/claude`](https://github.com/lyndonkl/claude). Pick one of the three install paths.

**Option A — Plugin install (recommended).** Adds the agents and skills to your global `~/.claude/` directory automatically:

```bash
# Inside any Claude Code session
/plugin marketplace add lyndonkl/claude
/plugin install thinking-frameworks-skills
```

**Option B — Symlink (always-current with the source repo).** Useful if you want updates the moment you `git pull`:

```bash
git clone https://github.com/lyndonkl/claude.git ~/Documents/Projects/claude
mkdir -p ~/.claude/agents ~/.claude/skills

# Agents
for a in literature-scan-coach paper-extractor paper-synthesizer skill-creator; do
  ln -sf ~/Documents/Projects/claude/agents/$a.md ~/.claude/agents/$a.md
done

# Skills (symlink the whole skills directory in one shot, or pick a subset)
ln -sf ~/Documents/Projects/claude/skills/* ~/.claude/skills/
```

**Option C — Copy (manual).** Simplest, but you'll need to re-copy after upstream changes:

```bash
git clone https://github.com/lyndonkl/claude.git
cd claude
cp -rf agents/* ~/.claude/agents/
cp -rf skills/* ~/.claude/skills/
```

After any of the three options, verify with:

```bash
ls ~/.claude/agents/ | grep -E "literature-scan-coach|paper-extractor|paper-synthesizer"
ls ~/.claude/skills/ | grep -E "paper-three-pass-extraction|fetch-arxiv-recent"
```

You should see all three agents and the two named skills.

### 3. Clone this project

```bash
git clone https://github.com/lyndonkl/papersynthesis.git
cd papersynthesis
```

### 4. Install the project's orchestrator as an agent

This project ships its own orchestrator agent at `orchestrator.md` (project root). It's the entry point — the prompts in `prompts/` invoke it. For Claude Code to discover it as an agent, you need it in `~/.claude/agents/`. Two options:

**Symlink (always-current with the repo).** Best if you `git pull` periodically:

```bash
mkdir -p ~/.claude/agents
ln -sf "$(pwd)/orchestrator.md" ~/.claude/agents/papersynthesis-orchestrator.md
```

**Copy.** Simpler, but you'll need to re-copy after any changes:

```bash
mkdir -p ~/.claude/agents
cp orchestrator.md ~/.claude/agents/papersynthesis-orchestrator.md
```

The agent's YAML `name` field is `papersynthesis-orchestrator`, which is what Claude Code uses internally. The filename should match.

Verify with:

```bash
ls ~/.claude/agents/papersynthesis-orchestrator.md
```

You should see the file (or symlink). After this step, the orchestrator agent is invocable from any Claude Code session, but it expects the working directory to be this project root — see Step 6.

### 5. Configure

Three files live under `shared-context/`. You **must** edit at least the watchlist; the others have sensible defaults you can tune later.

```
shared-context/watchlist.md          # required: your keyword watchlist
shared-context/source-registry.md     # the four source endpoints + arXiv category list
shared-context/relevance-criteria.md  # keep / drop rules
shared-context/synthesis-style.md     # how the layered digest is rendered
```

Open `shared-context/watchlist.md` and replace the placeholder keywords with topics you actually want to track. Single keywords match with word boundaries; multi-word phrases match as contiguous substrings; weights are optional (`keyword :: 0.8`).

If your interests are CS / ML-leaning, skim the arXiv category list in `source-registry.md` (default is `cs.LG, cs.CL, cs.CV, cs.AI, cs.NE, stat.ML`) and adjust if your watchlist drifts (e.g., add `q-bio.QM` for computational biology).

### 6. Run the weekly digest

Always start Claude Code from inside the project root so the working directory matches the agents' relative paths:

```bash
cd papersynthesis    # from wherever you cloned it
claude
```

Then paste the contents of `prompts/kickoff.md` as your first message. It hands you off to the `papersynthesis-orchestrator` agent installed in Step 4. The orchestrator runs the pipeline:

- pre-flight check on the project files
- spawns `literature-scan-coach` (search-only) and gets the paper-records list back
- spawns `paper-extractor` Pass 1 in parallel, one subagent per paper
- applies the relevance filter on Pass 1 outputs
- spawns `paper-extractor` Pass 2 in parallel for KEEPs
- spawns `paper-synthesizer` Pass A in parallel, one per kept paper (per-paper translation)
- spawns one `paper-synthesizer` Pass B (across all per-paper outputs → clustered weekly digest)
- reports back: digest path, kept / dropped counts, the 30K-ft preview paragraph, any warnings

Outputs land at:

- `ops/paper-synthesizer/{YYYY-WW}-digest.md` — the digest you read
- `ops/paper-synthesizer/{YYYY-WW}-papers.md` — the full filtered paper list with rationale
- `ops/paper-synthesizer/{YYYY-WW}/per-paper/{slug}.md` — per-paper Pass A translated summaries
- `ops/paper-extractor/{YYYY-WW}/{slug}.md` — per-paper extraction notes (Pass 1 + Pass 2)

### 7. Other run types

The kickoff prompt is the only one you need. After it hands the session over to the orchestrator, describe what you want in plain English:

- "Run the weekly paper digest." → WEEKLY
- "Catch me up on the last 3 weeks." → CATCH_UP (oldest-first; non-negotiable)
- "What's new on diffusion models in the last 14 days?" → ON_DEMAND
- "Re-run last week from cache. I just edited the relevance criteria." → RE_SYNTHESIZE
- "Deep-read the Smith et al. paper from week 19." → DEEP_READ

The orchestrator detects intent and routes the pipeline accordingly.

---

## Where to learn more

- `orchestrator.md` — full system map, folder layout, agent / skill table, cadence rules
- `design-decisions.md` — why this project is shaped the way it is (sources, cadence, three-stage pipeline rationale, what's not in v1)
- `prompts/README.md` — the prompt menu + how to use them
- `shared-context/synthesis-style.md` — the rendering rules the synthesizer follows; edit this to change the digest's voice
- [`lyndonkl/claude`](https://github.com/lyndonkl/claude) — the agents + skills source repo; agent files document each pipeline stage in detail

---

## Recent digests

<!-- the agent appends one line here per run, newest first -->

_(none yet)_
