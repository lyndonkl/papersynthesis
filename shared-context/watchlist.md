# Watchlist

Persistent keywords for the weekly paper digest. The agent reads this every run. You own it; the agent never edits it (it may *suggest* edits in the digest's "Notes for next week" section — those are advisory).

## Format

Each line under `## keywords` is one keyword or phrase. The agent matches:

- Multi-word phrases ("protein language model") as contiguous substrings.
- Single words ("crispr") with word boundaries — so "crispr" doesn't match "crisper".

Comments (`#`) and blank lines are ignored.

You may also use a simple OR-group with `|`: `gnn|graph neural network` matches if either appears.

To weight a keyword (the agent uses weights when scoring relevance), append ` :: <0.0-1.0>`. Default is 1.0.

```
single-cell :: 0.8        # broad term — slightly down-weight
spatial transcriptomics    # default 1.0
```

---

## keywords

<!-- TODO: replace these placeholders with the topics you actually care about. -->
<!-- Examples below; delete or keep as starting points. -->

# protein design
# protein language model
# AlphaFold
# CRISPR base editing
# single-cell foundation model
# spatial transcriptomics
# diffusion model for biology
# benchmark for biological foundation models

---

## Notes

- A focused watchlist (5-15 keywords) produces sharper digests. Broader (30+) means you'll need either tighter `relevance-criteria.md` or per-week overrides to manage volume.
- If 3+ weeks running you keep <3 papers per week, the agent will flag it. That usually means a keyword needs broadening or the criteria are too strict.
- If a keyword keeps producing dropped papers (look-alike traps), tighten it with a phrase or add the look-alike to the criteria's exclusion list.
