# Relevance Criteria

What counts as in-scope vs out-of-scope when filtering the candidate papers fetched each week. The `paper-relevance-filter` skill applies these rules; you own this file.

The criteria below are deliberately defaults — a starting point you'll tune as you read a few weeks of digests. After 2-3 runs you'll see which classes of paper keep getting kept-but-irrelevant or dropped-but-actually-wanted; refine accordingly.

---

## What "in scope" means by default

A paper is in scope if it meets **all** of:

1. **Primary research, methods, or rigorous benchmark.** Empirical results, novel methods, or systematic evaluations.
2. **Substantive abstract.** The abstract states what was done and what was found — not just what will be discussed.
3. **Aligned with watchlist intent**, not just keyword surface match. (Use the watchlist's keywords to find candidates; use this criteria file to decide whether the candidate fits the *intent* behind those keywords.)

A paper is out of scope if **any** of:

- It is a perspective / commentary / editorial without new data or method.
- It is a press release, news item, or PR-shaped abstract.
- It mentions a watchlist keyword only in passing (single mention, paper's main subject is elsewhere).
- It is a book chapter or workshop summary.

## Keep with caveat

These pass but get tagged in the digest:

- **Review article on a watchlist topic** → KEEP, tag `[review]`. Useful for orientation; the synthesis layer should mention but not over-weight.
- **Methods paper without empirical evaluation** → KEEP, tag `[methods-only]`. Treat as a signal of where the field is going, not where it has arrived.
- **Preprint with a journal version already in PubMed** → KEEP the journal version, tag the preprint as `[also: preprint <doi>]`.
- **Journal version of a preprint we already covered** → KEEP, tag `[journal version of preprint covered YYYY-WW]`. Do not re-summarize substantively.

## Hard exclusions (always drop, regardless of keyword match)

- Retracted papers (PubMed flags these — drop immediately, log in dropped list).
- Predatory-journal venues. Not auto-detectable; if you build a list later, add it here.
- Papers in a language whose abstract is not English. (Drop, log; user can add a translator step later if this matters.)

---

## Look-alike traps for common watchlist terms

These are the cases where the keyword filter is most likely to over-fire. Add to this list as you spot patterns in dropped papers.

| Keyword                       | False-positive class                                         | What to do                                              |
| ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------- |
| "transformer"                 | Electrical-grid transformer engineering papers                | Drop unless paper is about ML / sequence models         |
| "attention"                   | Cognitive-psychology / neuroscience attention studies        | Drop unless paper is about ML attention / transformers  |
| "diffusion"                   | Physical diffusion (gas, drug delivery)                      | Drop unless paper is about generative models            |
| "agent"                       | Pharmaceutical agent (a drug) / chemical agent               | Drop unless paper is about software agents              |
| "embedding"                   | Surgical embedding (tissue), polymer embedding               | Drop unless paper is about ML embeddings                |
| "regression"                  | Disease regression (clinical sense)                          | Keep only if statistical-method context                  |
| "model"                       | Animal model (mouse model) / disease model                   | Heavy false-positive class — require second keyword     |

---

## Required minimums

- **For methods papers**: abstract must name the benchmark or the dataset evaluated on. Otherwise → REVIEW, not KEEP.
- **For benchmark papers**: abstract must name the size of the benchmark (number of items / patients / samples). Otherwise → REVIEW.
- **For review articles**: abstract must name the timeframe covered or the number of studies surveyed. Otherwise → DROP (it's a magazine piece, not a review).

---

## How the filter combines this with the watchlist

The relevance filter scores each paper on three axes:

1. **Match strength** — how strongly the watchlist keywords appear in title + abstract.
2. **Criteria fit** — how well the paper meets the rules above (in-scope / out-of-scope / required minimums).
3. **Novelty** — not already covered in the last 4 weeks.

A paper needs both a decent keyword match *and* a decent criteria fit. A strong keyword match in an out-of-scope paper drops. A weak keyword match in a perfect-fit paper still drops (the watchlist is the gate).

For details and the score-to-decision thresholds, see the `paper-relevance-filter` skill.

---

## Tuning loop

After each weekly digest, scan the dropped-papers section in `{YYYY-WW}-papers.md`:

- A paper you'd actually want to read got dropped → tighten the relevant criterion (probably a required minimum that's too strict) or add a watchlist keyword that would have caught it.
- A paper you wouldn't want to read got kept → either the watchlist keyword is too broad (add a phrase qualifier) or this file's exclusions need a new entry.

The goal is to drift toward "every dropped paper looks like an obvious drop, every kept paper looks like an obvious keep" within ~3-4 weeks of running.
