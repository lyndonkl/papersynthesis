---
week: 2026-W19
type: on-demand
run_suffix: 6mo-trajectory
window_from: 2025-11-10
window_to: 2026-05-10
theme: "Latest retrieval and re-ranking techniques for LLM agents — 6-month trajectory"
generated: 2026-05-10
---

# Topic for this run

This run replaces the standing watchlist (which is placeholder-only). The synthesizer reads this file as the complete topic statement.

## What the operator wants

Latest retrieval techniques and re-ranking techniques for **LLM agents** — papers from the prior 6 months (2025-11-10 → 2026-05-10), with the digest framed as a **trajectory across the 6-month window** for a **practitioner building an LLM-agent system right now**.

## Approved query list (8 queries — verbatim, do not modify)

1. `"retrieval-augmented generation" OR RAG OR "agentic RAG"`
2. `"agentic search" OR "agent retrieval" OR "tool-augmented retrieval" OR "search agent"`
3. `"neural reranker" OR "cross-encoder" OR "listwise reranking" OR "LLM reranker"`
4. `"dense passage retrieval" OR "dense retrieval" OR "embedding model" retrieval OR "bi-encoder"`
5. `"hybrid retrieval" OR "BM25" reranking OR "sparse-dense" retrieval OR SPLADE`
6. `"long-context retrieval" OR "long-context RAG" OR "retrieval" "long context" OR "needle in a haystack"`
7. `"GraphRAG" OR "graph retrieval" OR "knowledge graph" RAG OR "structured retrieval"`
8. `"retrieval" benchmark OR BEIR OR MTEB OR "RAG benchmark" OR "retrieval evaluation"`

## In scope

- Methods, systems, evaluations for retrieval, reranking, and retrieval-interfaces in the context of LLM agents (RAG agents, tool-using agents, search agents).
- Empirical results, novel methods, rigorous benchmarks, comparative evaluations.
- Both training-based and training-free approaches.
- Both academic and industry preprints; both single-paper contributions and systems papers.

## Out of scope (operator-excluded — drop unless borderline)

- Multimodal / vision-language retrieval (no image/video retrieval — text only).
- Pure information-retrieval theory papers without an LLM connection.
- Recommender systems (the LLM-reranker-for-recommendation cluster is out unless it teaches something general about reranker design).
- Agent memory papers as such (memory architecture / belief revision / write strategies). Memory papers that are *about retrieval-method dominance over write strategy* are in.
- Code / repo retrieval (specific to code search; the general retrieval insights might generalize but are not the operator's question).
- Standard scope rules from `shared-context/relevance-criteria.md` apply on top: primary research / methods / rigorous benchmarks; substantive abstracts; no commentary / press releases / book chapters / non-English abstracts.

## Impact axis (folded into the relevance filter)

Citation-weighted, **lenient on recency**. Apply on top of in-scope/out-of-scope content filter.

- **Cutoff date: early April 2026** (~2026-04-01).
- Papers **older than the cutoff** (2025-11-10 → 2026-03-31): need a real citation/traction signal to clear the bar — concrete citations, follow-up papers in the kept set citing them, journal-version-of-preprint status, demonstrable adoption (named system widely referenced, model release with adoption signal).
- Papers **from the last ~6 weeks** (2026-04-01 → 2026-05-10): can ride on **traction proxies** — GitHub stars on associated code, secondary blog/social mentions, named-author or known-lab pattern, clear technique contribution that the field is likely to adopt, presence in concurrent work as a named approach. Citations within this window are not directly observable; treat traction proxies as legitimate signal but report confidence per paper.
- The traction signal is a **soft modifier** to the score, not a hard gate. A paper with weak traction but strong on-topic content can still be KEEP if the operator's question (latest techniques for practitioners) is best answered by including it. Always report traction with calibrated confidence in the per-paper line.

## Sources for queries

- **arXiv**: primary. Categories for **this run**: `cs.CL`, `cs.IR`, `cs.LG`, `cs.AI` (cs.IR added per run; cs.CV / cs.NE / stat.ML dropped). Pass these category set explicitly per query.
- **PubMed**: included for completeness — expected near-zero results. Empty result is normal, not a failure.
- **bioRxiv / medRxiv**: included for completeness — expected near-zero results. Empty result is normal, not a failure.

## Digest shape

- **Lens**: Trajectory across the 6-month window. Establish a chronological arc: what the field looked like in mid-November 2025, what shifted through Q1 2026, where it stands as of early May 2026. Identify inflection points. Themes nest *inside* the timeline — i.e., per-quarter (or finer-grained) sections each contain the per-theme narrative for that slice.
- **Audience**: A practitioner building an LLM-agent system right now. Frame everything around: what's mature enough to use today, what's worth piloting, what's still research and not production-ready.
- **Length**: ~3000 words. Themes get real paragraphs (not bullet lists). Per-paper bullets carry methods and numbers.
- The standard `shared-context/synthesis-style.md` voice rules apply (banned words: delve, unpack, paradigm shift, let's explore, moreover, furthermore, it's worth noting). The layered-reasoning altitudes (30K / 3K / 300 ft) translate to: **Headline** = the 6-month through-line and what to act on now; **Trajectory by phase** = the chronological arc with themes nested per phase; **Papers** = per-paper bullets grouped by theme/phase, each with methods and numbers.
