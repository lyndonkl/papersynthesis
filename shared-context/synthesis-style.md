# Synthesis Style

How the agent applies layered reasoning to a week of papers. The `layered-reasoning` skill describes the *technique*; this file describes how to apply it to *this specific use case*.

The reader of the digest has three different questions on different days. The three layers serve those three questions, in this order:

| Layer       | The reader's question                            | The unit of writing      |
| ----------- | ------------------------------------------------ | ------------------------ |
| 30,000 ft   | "What did you find across all the papers?"       | The week                 |
| 3,000 ft    | "What were the themes? Tell me by topic."        | The cluster              |
| 300 ft      | "Show me the actual papers."                     | The individual paper     |

The synthesis is **top-down**. Write 30K first, then 3K per cluster, then 300 ft per paper. The lower layers must be consistent with the upper layer (a cluster summary cannot contradict the week's headline; a paper line cannot contradict its cluster's argument).

---

## Layer 1 — 30,000 ft: What did you find across all the papers?

This is one paragraph (3-5 sentences) that answers, for someone who reads only this paragraph: **what changed in the field this week?**

The 30K paragraph is the hardest to write because it requires actually thinking. The temptation is to write a list of cluster names or a headline per paper. Both fail. The 30K must compress the *intersection* of the papers, not the union.

### Questions to answer (in order)

1. **What is the through-line across the kept papers?** If you had to describe what the field collectively did this week in one sentence, what is it? (If no through-line exists — a genuinely scattered week — say so. Honesty here is more useful than fake coherence.)
2. **What did NOT change?** What is the field still stuck on / still not doing / still disagreeing about? This is high-information; the absence of progress is itself a signal.
3. **What's the continuity from prior weeks?** Reference last week's digest by week-tag if a thread is continuing. ("Continuing from 2026-18, the convergence on X is now joined by…")
4. **What's the disagreement, if any?** When two clusters argue against each other, surface it here.

### Patterns

**Good 30K paragraph:**

> This week the field's protein-design work tightened around a single claim: structure-conditioned generation outperforms sequence-only baselines, with three independent groups reporting it (cluster 1). What did not change: nobody is yet showing this on out-of-distribution targets, where AlphaFold remains the only data point. Continuing from 2026-18, the single-cell foundation-model thread now publishes benchmarks alongside weights (cluster 2) — the benchmark-vs-leaderboard discussion from two weeks ago is implicitly being answered. The week's tension: cluster 1's papers disagree on the magnitude of the structure-conditioning gain, with one group (P5) reporting half the effect of the other two.

Notice: it tells you what to take away in sentence 1, what's still open in sentence 2, what's continuing in sentence 3, and where the disagreement is in sentence 4. A reader who reads only this paragraph leaves with a defensible mental model of the week.

**Bad 30K paragraph (this is a list, not a synthesis):**

> This week we saw papers on protein design, single-cell methods, and CRISPR. Three protein design papers came out, including one from DeepMind. There was also a benchmark paper. The single-cell papers focused on foundation models.

Notice: this is a TOC, not an argument. It does not compress; it just summarizes the cluster names. Reject anything that reads like this.

### Anti-patterns to reject

- Listing cluster names with one sentence each. (That's the 3K layer.)
- Naming individual papers by author. (That's the 300 ft layer.)
- Hedging with "Various developments occurred" / "Several papers explored" / "There were a number of." If you find yourself writing these, you have not actually synthesized — restart with the through-line question.
- Adjectives without arguments: "important," "exciting," "novel." Useless. State what makes the work matter.
- Banned vocabulary: delve, unpack, paradigm shift, let's explore, moreover, furthermore, it's worth noting.

### When the week is genuinely scattered

If there is no through-line — kept papers are 4 papers in 4 unrelated areas — say that:

> This week was scattered. No single thread runs across the kept papers; instead, four independent updates worth tracking individually (see clusters). Notably absent: any new work on [recurring theme from prior weeks].

This is honest and high-information. The reader knows to skip to 3K rather than expecting a synthesis.

---

## Layer 2 — 3,000 ft: What were the themes?

For each cluster from `paper-cluster-by-theme`, write 2-3 sentences that answer: **what does this cluster of papers collectively argue?**

The cluster name is itself argument-shaped (per the cluster skill). The 3K paragraph elaborates that argument. It must:

1. **State the cluster's collective claim.** ("Three papers this week converge on X.")
2. **Cite the strongest 1-2 papers inline by reference.** Inline links are fine; numbered references are fine; just point at the actual papers.
3. **Surface the tension if any.** ("P5 disagrees on magnitude; reports 12% gain vs the others' 24%.") If the cluster's `tension` field is non-null, this sentence is required.
4. **Tag continuity** if the cluster name appeared in any of the last 4 digests: `[continuing from 2026-17]`. This goes in the cluster header, not the paragraph.

### Pattern

```markdown
### Cluster 1: Protein design moves toward sequence+structure conditioning [continuing from 2026-18]

Three independent groups report that adding structural context at training time outperforms sequence-only
baselines on standard benchmarks. The strongest result is from [Smith et al.](url), who show a 24% RMSD
improvement on the CASP holdout. The key tension: [P5](url) reports only ~12% gain on the same benchmark,
attributing it to a difference in negative-sample mining — worth tracking whether the field converges on
P5's protocol or the others'.
```

### Anti-patterns

- Restating the cluster name as the first sentence. (Repetitive — the reader just read the header.)
- Writing one sentence per paper in the cluster. (That's the 300 ft layer.)
- Naming the cluster's topic without naming its argument. ("This cluster is about protein design." Useless.)
- Cherry-picking one paper and ignoring the others. If a cluster has 5 papers, the 3K paragraph should reflect what the *cluster* says, not what one paper says.

---

## Layer 3 — 300 ft: Show me the actual papers

For each paper in each cluster, one bullet:

```
- **{Title}** — {first author et al.}, {source}, {YYYY-MM-DD}. {one sentence on what it does and why it
  belongs in this cluster.} → [link]({url})
```

The one-sentence description must:
1. Say what the paper *does* (method? result? benchmark? review?), not what it's about.
2. Connect to the cluster's argument — i.e., why this paper landed here. ("Reports the 24% gain that anchors the cluster claim.")
3. Preserve the paper's own hedging. If the abstract says "suggests," the line says "suggests" — never upgrade to "shows" or "proves."

### Pattern

```markdown
- **Structure-Conditioned Protein Generation at Scale** — Smith et al., bioRxiv, 2026-05-07. Reports a 24%
  RMSD improvement on CASP15 holdout when conditioning on a coarse structural prior at training time;
  this is the result that anchors the cluster's claim. → [link](https://www.biorxiv.org/content/10.1101/2026.05.07.123456v1)
```

### Anti-patterns

- "This paper discusses X." (Vacuous.)
- Re-summarizing the abstract in 4 sentences. (One sentence — let the link do the rest.)
- Skipping the link. (The whole point is that the user can drill in.)
- Decorating with "interesting" / "notable" / "exciting." Either the cluster sentence already explains why it matters, or it doesn't belong here.

---

## Cross-layer consistency checks (run before writing the file)

Before saving the digest, verify:

1. **Upward**: does the 30K paragraph reflect what the clusters collectively say? If you added a sentence to 30K that no cluster supports, either delete the sentence or check whether you missed a cluster.
2. **Downward**: does each cluster's 3K paragraph match the papers in its 300 ft list? If a cluster paragraph claims "three papers converge on X" but only two of the three actually argue X, fix the paragraph or move the third paper.
3. **Lateral**: do two cluster names contradict (one says X is settled, another says X is debated)? Either rename one or surface the tension explicitly in the 30K layer.

If any check fails, the synthesis is not ready. Fix before writing.

---

## Worked example (compressed)

Imagine a week where 12 papers were kept, clustered into 3 themes:

```markdown
# Week 2026-19 Paper Digest

## 30,000 ft — What changed in the field this week
The headline is convergence in protein design: three independent groups now report that
structure-conditioned generation beats sequence-only baselines (cluster 1), with one
notable disagreement on magnitude. What did not move: out-of-distribution evaluation —
none of the three reports addressed it, and AlphaFold remains the lone data point there.
Continuing from 2026-18, the single-cell foundation-model thread now publishes benchmarks
alongside weights (cluster 2). One outlier: a cryo-EM segmentation paper that doesn't fit
either thread but is methodologically clean (cluster 3).

## 3,000 ft — By theme

### Cluster 1: Protein design moves toward sequence+structure conditioning [continuing from 2026-18]
Three independent groups report structure-conditioned generation outperforms sequence-only
baselines. Smith et al. anchor with a 24% RMSD improvement on CASP15; Park et al. and Liu
et al. report similar directions on different benchmarks. P5 (Liu et al.) shows ~12%, half
the others' magnitude — they attribute it to negative-sample mining differences.

### Cluster 2: Single-cell foundation models start releasing benchmarks, not just weights [continuing from 2026-17]
Two papers release evaluation suites alongside the model. This continues last month's
discussion of leaderboard inflation — the implicit answer here is "publish your eval set."

### Cluster 3: Cryo-EM segmentation
One paper, but methodologically distinct from anything in clusters 1 or 2. Worth tracking
in case a thread emerges next month.

## 300 ft — Papers, by cluster

### Cluster 1: Protein design moves toward sequence+structure conditioning
- **Structure-Conditioned Protein Generation at Scale** — Smith et al., bioRxiv, 2026-05-07.
  Reports a 24% RMSD improvement on CASP15 holdout when conditioning on a coarse structural
  prior at training time; this is the result that anchors the cluster's claim.
  → [link](https://www.biorxiv.org/content/10.1101/2026.05.07.123456v1)
- **Joint Sequence-Structure Diffusion for Inverse Folding** — Park et al., PubMed, 2026-05-08.
  Independently reports the same direction on a different benchmark; weaker baseline so the
  absolute number is harder to compare. → [link](https://pubmed.ncbi.nlm.nih.gov/39000001/)
- **Limits of Structure Conditioning** — Liu et al., bioRxiv, 2026-05-09. Same direction, half
  the magnitude (12% vs 24%); attributes the difference to negative-sample mining. The cluster's
  open question. → [link](https://www.biorxiv.org/content/10.1101/2026.05.09.222222v1)

### Cluster 2: Single-cell foundation models start releasing benchmarks, not just weights
- ...

## Notes for next week
- Watch for the journal version of Smith et al. — preprint version was light on ablations.
- If Liu et al.'s negative-sample protocol gets adopted, the magnitude question may resolve.
- Cluster 3 (cryo-EM) is one paper for now; flag if a second appears next week.

## Full list
See `2026-19-papers.md` for the unsynthesized table of every kept paper.
```

The reader who reads only the 30K paragraph leaves with the field's state. The reader who reads 30K + 3K leaves with the per-theme picture. The reader who drills in to 300 ft sees the actual papers and can click through. Each layer is independently useful — that is the test.
