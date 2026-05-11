---
week: 2026-W19
type: on-demand-style-override
run_suffix: 6mo-trajectory
generated: 2026-05-10
---

# Synthesis Style for this run (per-run override; standing style still applies)

This file is the complete style spec the synthesizer reads for this run. It bakes in the standing rules from `shared-context/synthesis-style.md` and adds the trajectory / practitioner-audience tweaks the operator asked for.

---

## Standing rules carried over from `shared-context/synthesis-style.md`

The synthesis is **top-down**. Lower layers must be consistent with the upper layer. Compress the *intersection* of the papers, not the union.

### Banned vocabulary (absolute — applies to every line of the digest)

`delve`, `unpack`, `paradigm shift`, `let's explore`, `moreover`, `furthermore`, `it's worth noting`. Also banned in any text the synthesizer writes itself.

### Anti-patterns to reject

- Listing cluster names with one sentence each (that is a TOC, not a synthesis).
- Naming individual papers by author at the headline layer.
- Hedging with "Various developments occurred" / "Several papers explored" / "There were a number of."
- Adjectives without arguments: "important," "exciting," "novel." State what makes the work matter.
- Restating the cluster name as the first sentence of the cluster paragraph.
- Cherry-picking one paper and ignoring the others when describing a cluster.

### Per-paper bullet rules

- One bullet per paper. Title, author(s), source, date.
- The one-sentence description must say what the paper *does* (method? result? benchmark?), connect to the cluster's argument (why this paper landed here), and preserve the paper's own hedging (if abstract says "suggests", line says "suggests").
- Always include a clickable link.
- For this run, each per-paper bullet must also carry: **a numerical/methodological detail** (the strongest concrete number or the key methodological choice) and **a traction-confidence tag** (see traction reporting rules below).

### Cross-layer consistency checks (run before writing the file)

1. Upward: does the headline/30K paragraph reflect what the per-phase / per-theme sections collectively say?
2. Downward: does each phase/theme paragraph match the papers in its bullet list?
3. Lateral: do two cluster names contradict?

---

## Per-run tweaks (specific to this 6-month trajectory run)

### Lens: trajectory over 6 months, not weekly snapshot

The default cluster-by-theme layout is replaced for this run by a **chronological arc with themes nested per phase**. Structure:

1. **Headline** (one paragraph, the "what changed across the 6 months" through-line, 4-6 sentences). This is the single-paragraph version a practitioner reads first. It must answer: what is the practitioner-relevant shift across the window, what is mature, what is still research, and what (if anything) the field still has not settled.

2. **Trajectory by phase** (~5 phases — adjust per the natural inflection points the kept set actually shows; do not force a fixed number). Each phase is a section with:
   - **Phase header**: a date range and a one-line argument-shaped name (e.g., "Phase 2: Late Nov 2025 – Jan 2026 — agentic-RAG efficiency becomes a first-class research target").
   - **Phase paragraph(s)**: 1-3 paragraphs describing what the phase looked like, what was ascendant, what was being questioned, what was already getting superseded. Where multiple themes are active in the same phase, organize them as named sub-paragraphs within the phase, not as separate sub-clusters across phases.
   - **Inflection point**: where applicable, an explicit "the inflection here is X" sentence inside the phase paragraph. Inflection points are what a practitioner needs to notice — the weeks where the conversation actually shifted.

3. **Where things stand now (early May 2026 — the practitioner's view)**: a section that synthesizes the 6 months into actionable tiers:
   - **Mature enough to use today**: techniques the kept set converges on, with strong empirical support and either production-ready code or simple-to-implement.
   - **Worth piloting**: techniques that are convergent but where the kept set still shows uncertainty about the right mechanism or where production-readiness is unclear.
   - **Still research, do not put in production**: techniques that look promising in single papers but are unreplicated or where the kept set itself disagrees substantially.

4. **Papers, by theme** (not by phase — the per-paper section is grouped by theme so a practitioner can find papers on a given technique without scanning every phase). Each theme section: 2-3 sentence theme paragraph + per-paper bullets with the per-paper rules above.

### Audience: practitioner, not researcher

Voice should be **plain and direct**. Frame around action, not academic context. Where a paper makes a claim, translate it into "what this means if you are building an agent system today" — not in a separate sidebar but as a phrase or clause inside the paragraph that surfaces the paper.

Examples of voice the practitioner audience wants:
- Good: "If you are picking a reranker today, the kept set converges on cross-encoders with LLM-utility objectives — CAR (training-free) is the lowest-friction pilot."
- Bad (too academic): "The literature increasingly suggests that LLM-utility objectives may outperform IR-relevance objectives in reranker training, with several papers reporting positive results in this direction."

The bad version uses "may," "increasingly suggests," and "in this direction" — practitioners reading the digest need the call-to-action shape of the good version.

### Traction signal reporting (operator's impact axis, surfaced in the digest)

For each paper, surface a one-clause traction tag inside the bullet:
- For papers older than the cutoff (2025-11-10 → 2026-03-31): the tag is the actual signal — citations, named-by-other-papers in the kept set, model-release-with-adoption, journal-version status. Report the signal, not just "high traction."
- For papers from 2026-04-01 to 2026-05-10: the tag is the proxy signal with calibrated confidence — "high-confidence-prominent / gaining traction / signal-uncertain". Report which proxies fired (named-author-known-lab, GitHub release, named in concurrent work, clear-technique-with-low-adoption-friction).

Confidence levels: `high`, `medium`, `low`. Always include the confidence level. Never report traction as ground truth without it.

### Length budget

Target ~3000 words total. Rough split:
- Headline: ~250 words.
- Trajectory by phase: ~1500 words across 4-5 phases.
- Where things stand now (practitioner tiers): ~500 words.
- Papers by theme: ~750 words for the theme paragraphs and bullets together.

Do not pad to hit the budget. If the natural digest is 2500 words and reads well, ship at 2500. If it is 3500 and every paragraph earns its space, ship at 3500. The budget is a target, not a quota.

### Outliers section

If the kept set contains papers that genuinely do not fit any phase or theme, surface them in a brief **Outliers** section after the per-theme papers. Two-three sentences max — what the paper is, why it is here, why no theme.
