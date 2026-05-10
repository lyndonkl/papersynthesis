# 2026-W19 On-Demand Digest — Retrieval and Reranking for LLM Agents: 8-Month Evolution

**Run type:** on-demand thematic question (not a standard weekly digest).
**Window:** 2025-09-09 → 2026-05-09 (8 months, three quarterly buckets).
**Sources:** arXiv (cs.IR primary; cs.CL, cs.LG, cs.AI secondary). PubMed / bioRxiv / medRxiv skipped (CS-heavy theme).
**Operator's question:** Latest retrieval and reranking techniques for LLM agents over the last 8 months — gaining-traction work, organized by mechanism family, quarterly bucket, and what changed.
**Override file:** `ops/paper-synthesizer/overrides/2026-W19.md` (extended window).
**Priors used:** `ops/paper-synthesizer/digests/2026-W19-on-demand-retrieval-rerank-llm-agents.md` (3-month version covering 2026-02-09 → 2026-05-09; this run extends back to 2025-09-09 and changes the lens to mechanism families + time-progression).
**Generated:** 2026-05-09

> **Caveats up front.** Citation counts within an 8-month preprint window are not reliably observable per paper — Semantic Scholar / Google Scholar were not directly queried in this run. The traction signal is therefore a **multi-signal heuristic**: clear mechanism contribution, named system, benchmark coverage with concrete numbers, group/lab affiliation pattern, model/code release, and presence in subsequent papers' baselines or "we compare to X" mentions inside the kept set itself. I report it per-paper with calibrated confidence and do not claim it as ground truth. Pass 2 ran in **degraded mode (abstract-only)** for all papers; figure-level analysis is not extracted; the digest's specifics are what the abstracts state, with hedging preserved. Where I mark a Sep/Oct 2025 approach as "already partially superseded," the evidence is the *kept set itself*: a Q4 2025 or Q1 2026 paper that names the older one as a baseline and reports outperforming it.

---

## 30,000 ft — What changed in retrieval / reranking for LLM agents over 8 months

The clearest through-line across the 57 kept papers is a **structural reshaping of the retrieval interface**, not just a quality bump on existing rerankers. Three sub-shifts compose the headline. First, **the target of optimization moved from IR-style relevance to LLM/generator utility** — a thread that started as isolated Sep–Oct 2025 papers (InfoGain-RAG, P1) framing "document information gain" as the right reranker objective, consolidated through Q4 2025 (LURE-RAG, P21; multivector-with-LSR-gather, P19), and reached its empirical anchor in Q1 2026 with CAR's ρ=0.964 between reranker score and downstream generation F1 (P26, carried from the 3-month digest). Second, **the retriever interface itself became the question** — Sep–Oct 2025 papers asked the agent to interact more richly with the corpus (Interact-RAG's Corpus Interaction Engine, P10; jina-reranker-v3's "last but not late" cross-document attention, P2), Q4 2025 escalated this with a paper claiming **simple keyword search inside a tool-using agent reaches ~90% of vector-RAG performance** (P16) and a 2026-02-03 paper exposing keyword/semantic/chunk-read as separate tools to the agent (A-RAG, P25), and Q1 2026 closed with DCI (P28) reporting the agent grepping the raw corpus directly outperforms strong sparse, dense, *and* reranking baselines on BRIGHT/BEIR/BrowseComp-Plus. Third, **agentic-RAG efficiency emerged as a first-class research target** — almost absent in Q3 2025 except for cache and token-efficiency precursors (ARC, P13; TeaRAG, P12), routine in Q4 2025 (process-supervision RL, query-decomposition pruning), dominant in Q1+ 2026 (LatentRAG's ~90% latency cut at comparable accuracy, P30; Doctor-RAG's failure-aware repair, P32; AutoSearch's RL-controlled depth, P33).

What did **not** change. Across all three quarters there is **still no shared evaluation framework** for agentic-RAG efficiency — every kept efficiency paper measures against a different baseline (Search-R1, single-step RAG, rerun-based repair, recent multi-agent frames). And across all three quarters there are **persistent negative results that the field has not absorbed**: the Sep 2025 recency-bias diagnostic (P3) showed LLM rerankers shift Top-10 mean publication year forward by up to 4.78 years; Apr 2026's FRESCO (P34) re-finds essentially the same bias from a different angle; the Feb 2026 Cold-Start diagnostic (P39) shows popularity-rank dominating LLM rerankers ~30× on HR@10. The reranker-bias literature is now substantial enough to warrant its own subfield, but new reranker papers in the kept set continue to evaluate without these diagnostics.

The week's **disagreement to track**: the "no embedder needed" claim now exists in three independent forms — agentic keyword search (P16, Dec 2025), navigation-as-retrieval (Corpus2Skill, P36, Apr 2026), direct corpus interaction (DCI, P28, May 2026). If a fourth independent confirmation lands in the next 2-3 months, the vector-store paradigm for agentic settings is in serious question. If it doesn't, the result is a methodology curiosity. The strongest opposing data point is Nemotron ColEmbed V2 (P22, Feb 2026), which leads the ViDoRe V3 leaderboard with late-interaction multi-vector embeddings — the high end of "embeddings are still pulling ahead" within the same 8 months.

---

## Mechanism-family map of the territory (now)

The kept set populates roughly nine families. Family count is approximate — several papers fit two and I assign each to its dominant frame, with `also-fits` where relevant. Family ordering is by activity level in this 8-month window.

### 1. Trained / RL-trained rerankers targeting LLM utility (8 papers across 8 months)
The reranker is trained to predict downstream generation usefulness rather than IR relevance. Splits into RL-feedback (RRPO P14; GR2 P29; LURE-RAG P21 — listwise loss with LLM utility), distillation (Prism-Reranker P25; MemReranker P27 — multi-teacher LLM distillation; XProvence P22 — context-pruning + reranking), and information-gain (InfoGain-RAG P1 — earliest, Sep 2025).

### 2. Training-free LLM-confidence / utility rerankers (3 papers)
Use the LLM's own confidence change to rerank, no extra training. LCR (P23) and CAR (P26) are the carry-forward anchors with ρ=0.964 generation correlation; this family began as a position in late 2025 and is consolidated by mid-2026.

### 3. Listwise / late-interaction / multi-vector rerankers (5 papers)
Architecture-driven: late-interaction efficiency (Col-Bandit P11 — query-time pruning), late-interaction at scale (Nemotron ColEmbed V2 P22 — visual SOTA), listwise mechanism design (jina-reranker-v3 P2 — "last but not late" cross-document attention; CoRe Heads P9 — attention-based; L2G P5 — listwise→graph). Adaptive listwise (AdaRankLLM P40) bridges this with the role-shift framing.

### 4. Specialized rerankers for specific failure modes (5 papers)
Recency bias (Recency-Bias diagnostic P3, Sep 2025; FRESCO P34, Apr 2026 — same finding, two angles, eight months apart), corpus poisoning (ProGRank P31), graph proximity (GraphER P32), cold-start coverage (Cold-Start Diagnostic P39).

### 5. Learned-sparse retrieval / two-stage architectures (4 papers)
Mostly engineering: LACONIC (P18 — Llama-3-based LSR rivaling dense at 71% less memory), Milco (P6 — multilingual LSR), Forward-Index compression for LSR (P24), Multivector-with-LSR-gather (P19 — recasting gather-and-refine as classic two-stage). Pre-existing family; the 8-month signal is "sparse retrieval is back, with LLM backbones."

### 6. GraphRAG variants and graph-structured retrieval (4 papers)
Iterative GraphRAG diagnostic (P4 — Sep 2025 systematic study, finding iteration helps but adds noise), GraphER's graph-based reranking without requiring a KG (P32), TagRAG's tag-guided hierarchical KG (kept-but-vertical), Multi-Agent-GraphRAG's text-to-Cypher framework (kept-but-vertical). The carry-forward RAGSearch (P37) is the comparative anchor: agentic search closes most of the dense-vs-graph gap.

### 7. Agentic-RAG efficiency: latency, search depth, failure repair, orchestration (8 papers)
The 2026 frontier. LatentRAG (P30 — latent-space agentic loop, ~90% latency cut), AutoSearch (P33 — RL search-depth control), Doctor-RAG (P32 — failure-aware repair with prefix reuse), Test-Time Strategies (P38 — contextualization + de-dup on Search-R1), HERA (P35 — co-evolving topology + prompts, +38.7% over baselines), Stop-RAG (P8 — value-based stopping for iterative RAG), TeaRAG (P12 — token-efficient via PPR over knowledge associations), ARC (P13 — agent-RAG cache reducing storage to 0.015%, latency 80%).

### 8. Retrieval-replacement / retrieve-by-other-means (5 papers)
The structural challenge to vector-store retrieval. Direct Corpus Interaction (DCI P28 — agent greps the raw corpus, no embedder), Corpus2Skill (P36 — distill corpus into navigable skill directory), Interact-RAG (P10 — Corpus Interaction Engine, an earlier version of the same idea), Keyword Search Is All You Need (P16 — tool-using agent + keyword search reaches ~90% of vector-RAG performance), A-RAG (P15 — exposes keyword/semantic/chunk-read as parallel tools).

### 9. Agent memory architectures with retrieval-method dominance findings (6 papers)
Layered/structured agent memory plus the empirical finding that retrieval method matters more than write strategy. LightMem (P19 — SLM-driven 3-tier), Kumiho (P28 — AGM belief-revision postulates), Agentic Memory (P17 — unified LTM+STM via RL), xMemory (P30 — decouple+aggregate, beyond top-k similarity), SYNAPSE (P31 — episodic-semantic spreading activation), Continuum Memory (P20 — class definition). The diagnostic anchor is the carry-forward Retrieval-vs-Utilization paper (P31, 20-pt accuracy span on retrieval method vs 3-8 pts on write strategy).

Plus three cross-cutting positions (each fits multiple families):
- **Comparative empirical evaluations** (Is Agentic RAG Worth It? P26; MCP vs RAG vs NLWeb vs HTML P15; Rethinking Retrieval — financial domain P14) — agent-vs-non-agent and interface-vs-interface comparisons.
- **Production-grade enterprise stacks** (Higress-RAG P11 — Adaptive Routing + Hybrid Retrieval + CRAG; A-RAG P25 — hierarchical interfaces) — the field is starting to write production architectures rather than only research prototypes.
- **Adversarial / security** (MemoryGraft P21 — poisoned-experience-retrieval attack on agent memory; ProGRank P31 — defense against corpus poisoning) — small but persistent.

---

## Quarterly breakdown — what was ascendant, what was getting cited, what was being questioned

### Q3 2025 (Sep 9 – Nov 30, 2025) — the shift starts

**Papers in window (kept set): 14.** Ascendant: information-gain rerankers (InfoGain-RAG P1 was the earliest concrete formulation of "rerank by LLM utility, not relevance"); listwise / late-interaction architectures (jina-reranker-v3 P2 with "last but not late" was a clean mechanism contribution that held up across the 8 months — still listed as a strong listwise baseline in Q1 2026 papers like Rerank Before You Reason P19); learned-sparse retrieval was already established but quieter (Milco P6 — multilingual LSR with 30 active dimensions per doc beating dense baselines).

Getting heavy attention (mechanism-family-level): GraphRAG variants — Beyond Static Retrieval (P4) is the earliest systematic study of iterative GraphRAG in this window and named several follow-ups in Q4 2025 use it as a reference. Recency bias was diagnosed cleanly (P3) in mid-September 2025 — important enough that the FRESCO paper (P34) re-discovered essentially the same finding from a different methodology eight months later. The recency-bias finding is the single most-replicated empirical result in the kept set.

Starting to be questioned: black-box retrieval. Interact-RAG (P10, Oct 31, 2025) was the first kept paper to explicitly call the existing retrieval API a "black box" and equip the agent with primitives for fine-grained control over information retrieval — the framing then propagates through Q4 2025 (A-RAG hierarchical interfaces, P25) and Q1+ 2026 (DCI's no-retriever-at-all stance, P28).

Already partially superseded by Q1+ 2026: simple agentic-RAG without efficiency considerations. ARC (Agent RAG Cache, P13, Nov 4) and TeaRAG (P12, Nov 7) are early efficiency-themed papers; by Q1 2026 the entire efficiency-themed cluster (LatentRAG, Doctor-RAG, AutoSearch, Test-Time Strategies, HERA) had reframed the discussion around latency and token budget as the core question.

### Q4 2025 (Dec 1, 2025 – Feb 8, 2026) — the consolidation

**Papers in window (kept set): 21.** Ascendant: production / enterprise stacks. Higress-RAG (P11, Dec 30) is the highest-scored kept paper in this run by keyword density and traction signals — it does not contribute one new technique, but assembles Adaptive Routing + Hybrid Retrieval + Corrective-RAG + Semantic Caching + RRF into a Model Context Protocol-based architecture, which is the kind of paper the field cites as a systems-level reference. Self-MedRAG (P5, Jan 8) does the same for medical RAG with self-reflection, hybrid retrieval, and iterative query reformulation.

Getting heavy attention: the **non-vector / non-embedder** claim. Keyword Search Is All You Need (P16, Dec 19) is the boldest version of this position in Q4 — agentic keyword search reaching ~90% of vector-RAG performance — and it both follows from Q3 2025's Interact-RAG framing and *anticipates* Q1+ 2026's DCI claim. Three independent groups now hold versions of this position; the kept set treats it as the single most consequential structural challenge of the 8 months.

Reinforcement learning for agentic RAG matures. DecEx-RAG (P9, Oct 7) introduced process-supervision; TreePS-RAG (P7, Jan 11) added tree-based step-utility estimation via Monte Carlo over rollout descendants; JADE (P11, Jan 29) tackled the strategic-operational mismatch — planner and executor co-adapting under one shared backbone. The trajectory: from outcome rewards → process supervision → joint planner/executor optimization, all within ~3 months.

Starting to be questioned: the "agentic always wins" assumption. Is Agentic RAG Worth It? (P26, Jan 12) is the kept set's most direct empirical pushback — its conclusion is conditional ("which approach is preferable depends on conditions"), not a coronation of agentic RAG. MCP vs RAG vs NLWeb vs HTML (P15, Nov 28) finds **RAG, MCP, and NLWeb agents all outperform HTML on effectiveness and efficiency**, but does not crown a single winner among the three.

Already partially superseded by Q1+ 2026: fixed-iteration RAG. By Stop-RAG (P8, Oct 16, 2025) the field was already arguing for value-based stopping; PruneRAG (P12, Jan 16) and AutoSearch (P33, Apr 2026) extend the same logic into Q1+ 2026.

### Q1+ 2026 (Feb 9 – early May 2026) — the frontier extends

**Papers in window (kept set): 22 (all carried forward from the prior W19 3-month digest, where they were the original KEEP set).** Ascendant: agentic-RAG efficiency at the system level. LatentRAG (P30, May 7) is the headline — agentic reasoning + retrieval in latent space with one forward pass and a parallel decoder for transparency, claiming ~90% latency cut at comparable accuracy on seven benchmarks. The cluster's other members (Doctor-RAG failure-aware repair, AutoSearch RL-search-depth, HERA co-evolving orchestration, Test-Time Strategies post-hoc tweaks on Search-R1) collectively define the frontier as **how to deliver agentic-RAG quality without paying its cost**.

Getting heavy attention: rerank-for-utility consolidates. Five carry-forward Q1+ 2026 papers (CAR, RRPO, MemReranker, Prism-Reranker, plus the carried-from-Q3 LCR) all argue rerankers should target generator utility, not IR relevance. CAR's ρ=0.964 between reranker score and downstream F1 is the cluster's empirical anchor — the strongest empirical result in the kept set on this question.

Starting to be questioned: vector stores as the right primitive for agentic settings. DCI (P28, May 3) is the strongest version — agent grepping/scripting the raw corpus outperforms strong sparse, dense, and reranking baselines on multiple BRIGHT/BEIR/BrowseComp-Plus splits. Corpus2Skill (P36, Apr 16) replaces top-k retrieval with navigation through an offline-distilled skill directory. The Q3 2025 → Q4 2025 → Q1+ 2026 escalation of this thread is the most coherent multi-quarter trajectory in the kept set.

Already partially superseded inside Q1+ 2026 itself: standard relevance-tuned rerankers. The cluster of utility-targeted rerankers cites them as baselines; FRESCO (P34) shows they have a recency bias; ProGRank (P31) shows they are vulnerable to corpus poisoning. The carry-forward Cold-Start Diagnostic (P39) shows they can be beaten ~30× by popularity-rank in a low-recall regime.

---

## What changed — time-progression on three high-confidence shifts

This section calls the three clearest "what was the dominant approach 8 months ago → what challenged or replaced it → what is now dominant or rising" trajectories. I report confidence per shift and name the specific papers that constitute the evidence.

### Shift 1 — Reranker objective: IR relevance → LLM utility

**8 months ago (Q3 2025):** Most rerankers in the literature (cross-encoders like RankZephyr, ColBERT, listwise LLM rerankers) trained against IR-style relevance labels (TREC, BEIR, MS-MARCO). InfoGain-RAG (P1, Sep 16, 2025) was the earliest kept-set paper to formulate "Document Information Gain" — the difference of LLM generation confidence with vs. without the document — as the *correct* reranker objective. That is, the shift's first explicit formulation appears at the start of this 8-month window.

**Evidence that challenged or extended it (Q4 2025 → Q1+ 2026):** LCR (P23, Feb 14, 2026 — at the Q4/Q1 boundary) operationalized the same principle as a training-free reranker scoring by LLM Maximum-Semantic-Cluster-Proportion confidence; up to +20.6% NDCG@5 on BEIR over fine-tuned rerankers. RRPO (P14, Apr 2, 2026) trained a reranker via RL using LLM generation feedback as reward, no human labels, beating RankZephyr on knowledge-intensive QA. MemReranker (P27, May 7) used multi-teacher LLM distillation. CAR (P26, May 6, 2026) provided the empirical anchor: training-free reranking by sampled-answer semantic-consistency with **ρ=0.964 between reranking gain and downstream F1** — the strongest correlation result in the kept set on this question. LURE-RAG (P21, Jan 27) added the listwise-loss-with-utility-target finishing: 97-98% of dense-baseline performance with a LambdaMART-based reranker trained against LLM utility.

**Now dominant / rising:** Utility-targeted rerankers. The IR-relevance objective is not gone — the kept set still includes recency-bias-aware (FRESCO) and cold-start-aware (Cold-Start Diagnostic) reranker papers operating against IR labels — but the new-system papers in Q1 2026 default to utility as the target. Within utility-targeted, the unresolved sub-debate is **training-free (LCR, CAR) vs trained (RRPO, MemReranker, Prism, LURE-RAG)** — neither has won; both report strong numbers on different benchmarks.

**Field confidence:** **medium-high** (consolidating). Five+ papers across at least three independent groups, with a strong empirical correlation result (CAR's ρ=0.964) and an RL-feedback formulation (RRPO) that follows naturally. Not yet at "all new rerankers must justify the choice of objective," but trending that way; expect that constraint within ~2 quarters.

### Shift 2 — Retrieval interface: black-box vector store → agent-controlled corpus interaction (and possibly: → no embedder at all)

**8 months ago (Q3 2025):** The dominant agentic-RAG architecture wrapped a vector store + reranker behind a single `retrieve(query)` action exposed to the agent. The agent issued a query string; the system handed back top-k. Both Q3 2025 papers like the early agentic-RAG works (Search-R1 referenced in Test-Time Strategies P38) and Q3-2025 vertical applications (CTI benchmark, financial RAG) operated within this frame.

**Evidence that challenged it:** Three escalating moves over the 8 months.
- **Sep–Oct 2025:** Interact-RAG (P10, Oct 31) "dismantles the black-box with a Corpus Interaction Engine, equipping the agent with a set of action primitives for fine-grained control" — explicit framing that retrieval should not be a single API call.
- **Dec 2025:** Keyword Search Is All You Need (P16, Dec 19) reports that a tool-using LLM agent given only basic keyword search tools "can attain over 90% of the performance metrics compared to traditional RAG systems without using a standing vector database" — not a method paper claiming SOTA, but a measurement paper claiming that the value-add of vector-store retrieval over agentic keyword search may be smaller than assumed.
- **Feb 2026:** A-RAG (P25, Feb 3) exposes keyword search, semantic search, and chunk read as three parallel tools to the agent — i.e. the multi-tool retrieval interface as a deliberate design choice, not a workaround.
- **May 2026:** DCI (P28, May 3) takes the strongest position: agent grepping/reading/scripting the raw corpus directly, no embedder, no index, no retrieval API, *outperforms* strong sparse, dense, and reranking baselines on BRIGHT, BEIR, and BrowseComp-Plus.

Corpus2Skill (P36, Apr 16) is the orthogonal version — replace top-k retrieval with navigation through an offline-distilled hierarchical skill directory — same critique of top-k, different positive solution.

**Now dominant / rising:** The conventional vector-store + reranker pipeline is still the deployed default — Higress-RAG (P11) and Self-MedRAG (P5) and most production-flavored kept papers still use it. But **the interface critique is now consolidated enough that any new agentic-RAG paper publishing in the next 2 quarters has to defend why the agent gets a single retrieval action rather than a richer set**.

**Field confidence:** **medium** (contested, three groups with three different versions of the structural challenge). The DCI claim's strength rests on its replication. If a fourth independent group reproduces the no-embedder-at-all result on a non-BRIGHT/BEIR benchmark within the next ~2 quarters, the vector-store assumption for agentic settings is in serious question. If not, the result is a methodology curiosity. The strongest opposing data point is Nemotron ColEmbed V2 (P22, Feb 3, 2026): late-interaction multi-vector embeddings leading the ViDoRe V3 leaderboard with NDCG@10 = 63.42 — embeddings still moving forward at the visual-document end of the retrieval spectrum.

### Shift 3 — Agentic-RAG cost: ignored → first-class research target

**8 months ago (Q3 2025):** Agentic-RAG papers reported accuracy on knowledge-intensive QA without consistent latency or token-cost reporting. ARC (P13, Nov 4) and TeaRAG (P12, Nov 7) are the kept set's earliest papers framing efficiency as the *headline contribution* — ARC's 80% latency reduction and 0.015% storage; TeaRAG's PPR-over-knowledge-associations to compress retrieval content + reasoning steps. Stop-RAG (P8, Oct 16) added the iterative-RAG stopping question.

**Evidence that escalated it:** Through Q4 2025 the cost question became routine, and through Q1+ 2026 it became dominant.
- **Q4 2025:** PruneRAG (P12, Jan 16) — confidence-guided query decomposition trees with adaptive node expansion, defining an "Evidence Forgetting Rate" metric. XProvence (P22, Jan 26) — zero-cost multilingual context pruning integrated into the reranker. Rerank Before You Reason (P19, Jan 20) — explicit cost-aware analysis of listwise reranking depth using a novel "effective token cost" metric, finding moderate reranking often beats more search-time reasoning at lower cost.
- **Q1+ 2026:** LatentRAG (P30, May 7) shifts the entire reasoning + retrieval loop into latent space, claiming **~90% latency reduction** at comparable accuracy on seven benchmarks. AutoSearch (P33, Apr 19) RL-controls search depth via self-answer scoring. Doctor-RAG (P32, Apr 1) decouples failure diagnosis from repair, reusing validated reasoning prefixes instead of rerunning the full pipeline. Test-Time Strategies (P38, Mar 12) gets +5.6% EM and -10.5% turns on Search-R1 from contextualization + de-dup alone. HERA (P35, Apr 1) co-evolves multi-agent topology and prompts, claiming +38.7% over baselines.

**Now dominant / rising:** Efficiency is a first-class target. New agentic-RAG papers in Q1+ 2026 that *do not* report latency or token-cost numbers stand out.

**Field confidence:** **medium** (consolidated as direction, fragmented as evaluation). The direction is universal: every kept agentic-RAG paper from Q1+ 2026 reports an efficiency dimension. But there is **no shared evaluation framework**: each paper measures against a different baseline (Search-R1, single-step RAG, rerun-based repair, ReAct, recent multi-agent baselines), and the "effective token cost" metric introduced in Rerank Before You Reason (P19) is not yet adopted across the kept set. Expect a benchmark / leaderboard paper for agentic-RAG efficiency within ~1-2 quarters; if it consolidates around an existing metric (ETC, BCAS), the cost-optimization race accelerates further.

### Two smaller shifts worth flagging

**Sub-shift A — Retriever-vs-utilization debate.** The carry-forward Retrieval-vs-Utilization Diagnostic (P31 in this run, P21 in the prior 3-month digest) found retrieval method swings agent-memory accuracy 20 points while write strategy contributes only 3-8. The Cold-Start Diagnostic (P39) extends the same pattern — retrieval coverage, not reranker capacity. Together these two papers refocus the agent-memory subfield: **the bottleneck is upstream of the reranker, not at the reranker**. This is the kept set's clearest negative result and it has not yet been absorbed into agent-memory architecture papers (LightMem, Kumiho, Agentic Memory, xMemory, SYNAPSE, Continuum Memory) — they each propose a memory architecture without explicitly engaging the retrieval-method-dominates finding.

**Sub-shift B — Learned-sparse retrieval gets LLM backbones.** LSR was a quiet, separate research thread in Q3 2025 (Milco, P6 — multilingual). LACONIC (P18, Jan 4, 2026) — Llama-3 1B/3B/8B as LSR backbones, 60.2 nDCG on MTEB Retrieval at 71% less index memory than dense — is the first kept paper to bring LLM-scale backbones to the LSR formulation, and Q1 2026 follow-ups (Forward Index Compression P24, Multivector + LSR-gather P19, To-Case-or-Not-To-Case empirical study) treat LSR as a serious dense-retrieval alternative again.

---

## 3,000 ft — By mechanism family

(Argument-shaped headers per `synthesis-style.md`. Inline links + quarterly tags after each cluster name.)

### Cluster A — Reranker objective shifts from IR relevance to LLM utility [continuing across Q3 2025 → Q4 2025 → Q1+ 2026]

Eight papers across the 8-month window argue, with different mechanisms, that the reranker's training objective should be a generator-utility signal rather than an IR-relevance label. The trajectory: information-gain framing (InfoGain-RAG, Sep 2025) → training-free LLM-confidence operationalization (LCR Feb 2026, CAR May 2026 — the latter with **ρ=0.964** between reranker score and downstream F1) → RL-feedback-trained (RRPO Apr 2026) → multi-teacher LLM distillation (MemReranker May 2026) → reranker-output redesign that emits contribution + evidence-passage rewrites (Prism-Reranker Apr 2026) → listwise loss with utility target (LURE-RAG Jan 2026). The cluster's open question is **training-free (LCR, CAR) vs trained (RRPO, MemReranker, Prism, LURE-RAG)** — neither has won; both report strong numbers on different benchmarks.

### Cluster B — The retrieval interface itself is the bottleneck, not the retriever's capacity [Q3 2025 → Q1+ 2026 escalation]

Five papers across all three quarters argue, with escalating boldness, that when agentic systems underperform on knowledge-intensive QA, the issue is the *shape* of the retrieval interface, not the retriever's quality. Interact-RAG (Oct 2025) is the earliest clean version. Keyword Search Is All You Need (Dec 2025) is the surprise empirical result: tool-using agent + keyword search reaches ~90% of vector-RAG performance. A-RAG (Feb 2026) operationalizes the interface critique by exposing keyword search, semantic search, and chunk read as parallel agent tools. Corpus2Skill (Apr 2026) replaces top-k with navigation through a distilled skill directory. **DCI** (May 2026) takes the strongest position — no embedder, no index, no retrieval API; agent grep/script the raw corpus, beating strong sparse/dense/reranking baselines on BRIGHT/BEIR/BrowseComp-Plus. The cluster's open question is replication: three independent groups, three versions, no fourth confirmation yet.

### Cluster C — Agentic-RAG efficiency becomes a first-class research target [Q3 2025 emerging → Q1+ 2026 dominant]

Eight papers attack different dimensions of the agentic-RAG cost/latency problem. The progression is precursors-to-dominance: ARC's agent-RAG cache (Nov 2025), TeaRAG's token-efficient triplet+PPR (Nov 2025), Stop-RAG's value-based iteration stopping (Oct 2025) → Q4 2025 process-supervision RL (DecEx-RAG Oct 2025; TreePS-RAG Jan 2026) and explicit cost-aware analyses (PruneRAG Jan 2026; Rerank Before You Reason Jan 2026 — "effective token cost" metric) → Q1+ 2026 systems that turn cost into the headline (LatentRAG ~90% latency cut May 2026; Doctor-RAG failure-repair Apr 2026; AutoSearch RL-search-depth Apr 2026; HERA co-evolving orchestration Apr 2026; Test-Time Strategies on Search-R1 Mar 2026). The cluster's open question: **no shared evaluation framework yet** — each paper measures against a different baseline.

### Cluster D — Specialized rerankers expose specific failure modes of generic ones [recurring across all three quarters]

Five papers diagnose failure modes (recency bias, cold-start coverage, corpus poisoning, graph proximity) and propose targeted fixes or expose persistent gaps. The Q3 2025 Recency Bias diagnostic (P3) and the Q1+ 2026 FRESCO benchmark (P34) — eight months apart, different methodologies — converge on the same finding: LLM rerankers consistently shift Top-10 mean publication year forward and prefer older semantically-rich documents over recent factual ones. ProGRank (Q1+ 2026, P31) is the kept set's clean defense paper. GraphER (Q1+ 2026, P32) adds non-semantic graph proximity without requiring a KG. The Cold-Start Diagnostic (P39) is the cluster's **negative anchor**: rerankers cannot rescue a retrieval pool that already lost the relevant items — popularity-rank dominates LLM rerankers ~30× on HR@10. The tension: this cluster is internally coherent on the reranker side, but its negative finding (Cold-Start) tells the *adjacent* clusters their reranker improvements have a ceiling that retrieval-coverage work has to break.

### Cluster E — Listwise / late-interaction architectures evolve toward smaller-and-stronger [Q3 2025 → Q1+ 2026]

Five papers refine listwise / late-interaction / multi-vector reranking. jina-reranker-v3 (P2, Sep 2025) introduces "last but not late" cross-document attention at 0.6B parameters with state-of-the-art BEIR. CoRe Heads (P9, Oct 2025) uses <1% of attention heads for state-of-the-art listwise reranking. L2G (P5, Oct 2025) implicitly induces document graphs from listwise reranker logs. Col-Bandit (P11, Feb 2026) is a zero-shot drop-in pruning algorithm for late-interaction. Nemotron ColEmbed V2 (P22, Feb 2026) leads the ViDoRe V3 leaderboard at NDCG@10 = 63.42 on visual document retrieval — late-interaction multi-vector still climbing. The cluster's open question: when do rich interactions (jina-reranker-v3) beat plain late-interaction (Col-Bandit / ColBERT)? The kept set does not directly compare them.

### Cluster F — Agent memory consolidates around layered architectures with retrieval-method dominance [Q1+ 2026 mostly]

Six papers represent the agent-memory subfield's consolidation. LightMem (P19, Apr 2026 — SLM-driven 3-tier STM/MTM/LTM) and Kumiho (P28, Mar 2026 — AGM belief-revision postulates) are the two architectures the prior 3-month digest contrasted as pragmatic-vs-rigorous. Agentic Memory (P17, Jan 2026 — unified LTM+STM as RL policy), xMemory (P30, Feb 2026 — decouple+aggregate, beyond top-k similarity), SYNAPSE (P31, Jan 2026 — episodic-semantic spreading activation), Continuum Memory Architectures (P20, Jan 2026 — class definition) round out the subfield. The cluster's empirical anchor — and its **unresolved tension** — is the carry-forward Retrieval-vs-Utilization Diagnostic (in Cluster B): retrieval method, not write strategy, is what matters. The Q1 2026 memory architectures each propose a write/retain strategy without explicitly engaging this finding.

### Cluster G — Retrieval research turns toward learned-sparse with LLM backbones [Q1 2026]

Four papers re-energize learned-sparse retrieval by attaching LLM-scale backbones. LACONIC (P18, Jan 4) — Llama-3 1B/3B/8B as LSR encoders, achieving 60.2 nDCG on MTEB Retrieval at 71% less index memory than equivalent dense models. Multivector Reranking in the Era of Strong First-Stage Retrievers (P19, Jan 8) — replaces token-level gather with LSR for the first stage, recasting gather-and-refine as classic two-stage architecture. Forward Index Compression for LSR (P24, Feb 5) — engineering gains on the forward-index data structure. Milco (P6, Oct 2025) — multilingual LSR via shared-English-lexical-space connector. The cluster is engineering-heavy; the question for next 1-2 quarters is whether the LSR-with-LLM-backbones thread converges with the rerank-for-utility thread (cluster A).

### Cluster H — GraphRAG variants and graph-structured retrieval mature [all three quarters]

Four papers refine graph-based retrieval. Beyond Static Retrieval (P4, Sep 2025) is the cluster's diagnostic anchor: iterative retrieval helps multi-hop GraphRAG but adds noise on simple queries. The carry-forward RAGSearch (P37, Apr 2026) is the comparative: agentic search closes most of the dense-vs-graph gap, GraphRAG holds on complex multi-hop where its offline cost amortizes. GraphER (P32, Mar 2026) adds non-semantic graph proximity *without requiring a KG*, retriever-agnostic — practical version. The cluster's open question is whether the agentic-search-closes-the-gap finding will hold as iterative-retrieval techniques (Beyond Static Retrieval) get more refined, or whether GraphRAG maintains a multi-hop advantage at the graph-construction-cost / multi-hop-quality frontier.

### Cluster I — Comparative empirical evaluations recalibrate field assumptions [Q4 2025 → Q1+ 2026]

Three papers in this cluster do not propose methods — they evaluate existing ones against each other and surface findings the field needs to absorb. Is Agentic RAG Worth It? (P26, Jan 2026) — empirical comparison of "Enhanced" vs "Agentic" RAG, conditional rather than coronation conclusion. MCP vs RAG vs NLWeb vs HTML (P15, Nov 2025) — RAG, MCP, and NLWeb agents all outperform HTML; no single winner among the three. Rethinking Retrieval (financial domain, P14, Nov 2025) — vector-based agentic RAG beats hierarchical-node-based 68% of the time on SEC filings; cross-encoder reranking and small-to-big chunk retrieval as enhancement levers. The cluster is small, but its function is recalibration — every assumption about agentic-vs-non-agentic and embedding-vs-non-embedding is under empirical scrutiny within the 8-month window.

---

## 300 ft — Papers, by cluster

### Cluster A: Trained / RL-trained / training-free LLM-utility rerankers

- **InfoGain-RAG: Boosting RAG via Document Information Gain-based Reranking and Filtering** — Zihan Wang et al., arXiv, **2025-09-16** [Q3 2025]. Earliest kept-set formulation of "rerank by LLM utility": defines Document Information Gain (DIG) as the difference of LLM generation confidence with vs without the document, trains a specialized reranker, filters irrelevant docs. *Traction:* gaining-traction; clean conceptual contribution that anticipates the cluster. Confidence: medium. → [arXiv](https://arxiv.org/abs/2509.12765)

- **LLM-Confidence Reranker: Training-Free Approach for Enhancing RAG Systems** — Zhipeng Song et al., arXiv, **2026-02-14** [Q1+ 2026 carry-forward from prior W19 digest]. Training-free reranker scoring by LLM Maximum-Semantic-Cluster-Proportion confidence; up to +20.6% NDCG@5 on BEIR over fine-tuned rerankers using 7-9B LLMs. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2602.13571)

- **Optimizing RAG Rerankers with LLM Feedback via Reinforcement Learning (RRPO)** — Yuhang Wu et al., arXiv, **2026-04-02** [Q1+ 2026 carry-forward]. RL-trains rerankers using LLM-generation feedback as reward (no human labels), reference-anchored deterministic baseline; outperforms RankZephyr on knowledge-intensive QA. *Traction:* gaining-traction; the rerank-for-utility framing is hot. Confidence: medium. → [arXiv](https://arxiv.org/abs/2604.02091)

- **CAR: Query-Guided Confidence-Aware Reranking for RAG** — Zhipeng Song et al., arXiv, **2026-05-06** [Q1+ 2026 carry-forward; **cluster anchor**]. Training-free reranker using semantic-consistency-of-sampled-answers as a usefulness signal; +25.4% on YesNo+Contriever and **ρ=0.964 with downstream generation F1**. *Traction:* high-confidence-prominent within the rerank-by-utility subthread. Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2605.04495)

- **MemReranker: Reasoning-Aware Reranking for Agent Memory Retrieval** — Chunyu Li et al., arXiv, **2026-05-07** [Q1+ 2026 carry-forward]. Reranker family (0.6B / 4B) for agent memory; multi-teacher LLM distillation; 0.737 MAP at ~10-20% the latency of Gemini-3-Flash. *Traction:* gaining-traction; agent-memory framing is itself a 2026 trend. Confidence: medium. → [arXiv](https://arxiv.org/abs/2605.06132)

- **Prism-Reranker: Beyond Relevance Scoring — Jointly Producing Contributions and Evidence for Agentic Retrieval** — Dun Zhang, arXiv, **2026-04-26** [Q1+ 2026 carry-forward]. Reranker family (0.8B-9B) outputs a contribution statement and evidence-passage rewrite alongside the relevance verdict; +1.54 average NDCG@10 on BEIR-QA. *Traction:* high-confidence-prominent. Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2604.23734)

- **LURE-RAG: Lightweight Utility-driven Reranking for Efficient RAG** — Manish Chandra et al., arXiv, **2026-01-27** [Q4 2025]. Augments any black-box retriever with a LambdaMART reranker trained with **listwise ranking loss guided by LLM utility**; reaches 97-98% of state-of-the-art dense baselines at fraction of compute. *Traction:* gaining-traction; the "ranking-loss-meets-utility" formulation is the cluster's missing piece. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.19535)

- **GR2: Generative Reasoning Re-ranker** — Mingfu Liang et al., arXiv, **2026-02-08** [Q4 2025/Q1 2026 boundary]. End-to-end RL-trained generative reranker for recommendation systems with semantic-ID tokenizer (≥99% uniqueness); industrial-scale design. *Traction:* gaining-traction in the recommendation subthread. Confidence: medium. → [arXiv](https://arxiv.org/abs/2602.07774)

- **XProvence: Zero-Cost Multilingual Context Pruning for RAG** — Youssef Mohamed et al., arXiv, **2026-01-26** [Q4 2025]. Multilingual context-pruning model trained on 16 languages, supporting 100+ via cross-lingual transfer; integrates pruning into the reranker. *Traction:* gaining-traction; multilingual coverage is a clean novelty. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.18886)

### Cluster B: The retrieval interface is the bottleneck (not the retriever's capacity)

- **Interact-RAG: Reason and Interact with the Corpus, Beyond Black-Box Retrieval** — Yulong Hui et al., arXiv, **2025-10-31** [Q3 2025; cluster origin]. "Dismantles the black-box with a Corpus Interaction Engine, equipping the agent with a set of action primitives for fine-grained control"; SFT then RL refinement; outperforms advanced methods across 6 benchmarks. *Traction:* gaining-traction; the framing precursor for the rest of this cluster. Confidence: medium. → [arXiv](https://arxiv.org/abs/2510.27566)

- **Keyword Search Is All You Need: Achieving RAG-Level Performance Without Vector Databases** — Shreyas Subramanian et al., arXiv, **2025-12-19** [Q4 2025; cluster anchor]. Tool-using LLM agent with only basic keyword-search tools attains **over 90% of the performance metrics compared to traditional RAG** without a vector database; cost-effective, simple to implement. *Traction:* high-confidence-prominent; AWS-affiliated authors and a deliberately provocative measurement claim. Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2602.23368)

- **A-RAG: Scaling Agentic RAG via Hierarchical Retrieval Interfaces** — Mingxuan Du et al., arXiv, **2026-02-03** [Q4 2025/Q1 2026 boundary]. Exposes **keyword search, semantic search, and chunk read** as three parallel tools to the agent, enabling adaptive retrieval across granularities; consistently outperforms existing approaches at comparable or lower retrieved tokens. *Traction:* gaining-traction; cleanly operationalizes the multi-tool interface critique. Confidence: medium. → [arXiv](https://arxiv.org/abs/2602.03442)

- **Corpus2Skill: Distilling Enterprise Knowledge into Navigable Agent Skills** — Yiqun Sun et al., arXiv, **2026-04-16** [Q1+ 2026 carry-forward]. Distills corpus into a navigable skill directory (LLM summaries at each level + doc-ID retrieval); outperforms dense / RAPTOR / agentic-RAG on WixQA in the right regime. *Traction:* gaining-traction; structurally fresh alternative to top-k. Confidence: medium. → [arXiv](https://arxiv.org/abs/2604.14572)

- **Beyond Semantic Similarity: Rethinking Retrieval for Agentic Search via Direct Corpus Interaction (DCI)** — Zhuofeng Li et al., arXiv, **2026-05-03** [Q1+ 2026 carry-forward; **cluster anchor**]. Lets the agent grep / read / script the raw corpus directly (no embedder, no index, no retrieval API); reportedly outperforms strong sparse, dense, and reranking baselines on BRIGHT, BEIR, BrowseComp-Plus. *Traction:* gaining-traction; bold position-with-evaluation. Confidence: medium (preprint; needs replication beyond authors' setup). → [arXiv](https://arxiv.org/abs/2605.05242)

### Cluster C: Agentic-RAG efficiency as a first-class target

- **ARC: Agent RAG Cache Mechanism** — Shuhang Lin et al., arXiv, **2025-11-04** [Q3 2025]. Annotation-free caching framework that dynamically manages small high-value corpora per-agent by synthesizing query-distribution patterns with embedding-space geometry; reduces storage to **0.015% of the original corpus**, up to 79.8% has-answer rate, **80% latency reduction**. *Traction:* gaining-traction; the headline numbers will draw eyes. Confidence: medium. → [arXiv](https://arxiv.org/abs/2511.02919)

- **TeaRAG: A Token-Efficient Agentic RAG Framework** — Chao Zhang et al., arXiv, **2025-11-07** [Q3 2025]. Compresses retrieval content (chunk-based + graph-based triplets, Personalized PageRank-weighted) and reasoning steps (Iterative Process-aware DPO); orthogonal cost-cutting axes. *Traction:* gaining-traction; Q3 2025's clearest token-budget paper. Confidence: medium. → [arXiv](https://arxiv.org/abs/2511.05385)

- **Stop-RAG: Value-Based Retrieval Control for Iterative RAG** — Jaewan Park et al., arXiv, **2025-10-16** [Q3 2025]. Casts iterative RAG as a finite-horizon MDP and trains a value-based stopping controller with full-width Q(λ) targets; black-box-API-compatible; outperforms fixed-iteration and prompting-based stopping. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2510.14337)

- **DecEx-RAG: Boosting Agentic RAG via Decision and Execution Optimization with Process Supervision** — Yongqi Leng et al., arXiv, **2025-10-07** [Q3 2025]. Models RAG as MDP with separate decision/execution; pruning strategy improves data construction efficiency ~6×; +6.2% absolute over baselines on six datasets. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2510.05691)

- **TreePS-RAG: Tree-based Process Supervision for Reinforcement Learning in Agentic RAG** — Tianhua Zhang et al., arXiv, **2026-01-11** [Q4 2025]. Online tree-based RL where each reasoning step is a node and step utility is estimated by Monte Carlo over descendants; step-wise credit assignment without intermediate labels. *Traction:* gaining-traction; cleanly extends process-supervision RL. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.06922)

- **PruneRAG: Confidence-Guided Query Decomposition Trees for Efficient RAG** — Shuguang Jiao et al., arXiv, **2026-01-16** [Q4 2025]. Builds a structured query-decomposition tree with adaptive node expansion, confidence-guided acceptance/pruning, fine-grained entity-level retrieval; defines an **Evidence Forgetting Rate** metric. *Traction:* gaining-traction; new metric is reusable infrastructure. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.11024)

- **Rerank Before You Reason: Analyzing Reranking Tradeoffs through Effective Token Cost in Deep Search Agents** — Sahel Sharifymoghaddam, Jimmy Lin, arXiv, **2026-01-20** [Q4 2025]. Defines an **Effective Token Cost (ETC) metric** and shows on BrowseComp-Plus that moderate reranking often beats more search-time reasoning at substantially lower cost. *Traction:* gaining-traction; first kept-set paper with a portable cost metric. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.14224)

- **JADE: Joint Agentic Dynamic Execution — Bridging the Strategic-Operational Gap in Dynamic Agentic RAG** — Yiqun Chen et al., arXiv, **2026-01-29** [Q4 2025]. Models the system as a cooperative multi-agent team unified under a single shared backbone; planner and executor co-adapt under outcome-based RL. *Traction:* gaining-traction; the strategic-operational mismatch framing is the cluster's missing conceptual move. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.21916)

- **LatentRAG: Latent Reasoning and Retrieval for Efficient Agentic RAG** — Yijia Zheng et al., arXiv, **2026-05-07** [Q1+ 2026 carry-forward; **cluster anchor**]. Runs agentic-RAG reasoning + retrieval in latent space with one forward pass and a parallel decoder for transparency; **~90% latency reduction** at comparable accuracy on seven benchmarks. *Traction:* high-confidence-prominent. Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2605.06285)

- **AutoSearch: Adaptive Search Depth for Efficient Agentic RAG via RL** — Jingbo Sun et al., arXiv, **2026-04-19** [Q1+ 2026 carry-forward]. RL framework scoring each step's intermediate self-answer to find minimal-sufficient depth and penalize over-searching. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2604.17337)

- **Doctor-RAG: Failure-Aware Repair for Agentic RAG** — Shuguang Jiao et al., arXiv, **2026-04-01** [Q1+ 2026 carry-forward]. Diagnoses earliest failure point in a trajectory and repairs locally with prefix reuse; beats full-pipeline rerun on accuracy and token cost. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2604.00865)

- **Test-Time Strategies for More Efficient and Accurate Agentic RAG** — Brian Zhang et al., arXiv, **2026-03-12** [Q1+ 2026 carry-forward]. Test-time tweaks (contextualization + de-dup of retrieved docs) on Search-R1; +5.6% EM and -10.5% turns on HotpotQA + Natural Questions. *Traction:* too-early-to-tell. Confidence: low-medium. → [arXiv](https://arxiv.org/abs/2603.12396)

- **Experience as a Compass: Multi-agent RAG with Evolving Orchestration and Agent Prompts (HERA)** — Sha Li et al., arXiv, **2026-04-01** [Q1+ 2026 carry-forward]. Multi-agent RAG that co-evolves agent topology and per-role prompts; +38.7% average across six knowledge-intensive benchmarks. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2604.00901)

- **APEX-Searcher: Augmenting LLMs' Search Capabilities through Agentic Planning and Execution** — Kun Chen et al., arXiv, **2026-03-14** [Q1+ 2026 carry-forward]. Two-stage agentic-search training: stage-1 RL with decomposition-specific rewards (planning); stage-2 SFT on multi-hop trajectories (execution). *Traction:* too-early-to-tell; clean planning/execution decoupling. Confidence: low-medium. → [arXiv](https://arxiv.org/abs/2603.13853)

### Cluster D: Specialized rerankers expose persistent failure modes of generic ones

- **Do Large Language Models Favor Recent Content? A Study on Recency Bias in LLM-Based Reranking** — Hanpei Fang et al., arXiv, **2025-09-14** [Q3 2025; cluster diagnostic]. Across seven LLMs (GPT-3.5/4/4o, LLaMA-3 8B/70B, Qwen-2.5 7B/72B), "fresh" passages are consistently promoted, shifting Top-10 mean publication year forward by **up to 4.78 years**; pairwise preferences reverse up to 25% after date injection. *Traction:* gaining-traction; the kept set's most replicated empirical finding (re-found by FRESCO 8 months later). Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2509.11353)

- **FRESCO: Benchmarking and Optimizing Re-rankers for Evolving Semantic Conflict in RAG** — Sohyun An et al., arXiv, **2026-04-14** [Q1+ 2026 carry-forward; **cluster recurrence**]. Recency-aware reranker benchmark using paired recency-seeking queries + Wikipedia revision history; reveals consistent reranker bias toward older documents; instruction tuning recovers up to +27% on evolving knowledge. *Traction:* gaining-traction. Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2604.14227)

- **ProGRank: Probe-Gradient Reranking to Defend Dense-Retriever RAG from Corpus Poisoning** — Xiangyu Yin et al., arXiv, **2026-03-24** [Q1+ 2026 carry-forward]. Training-free defense reranker probing the retriever's gradient response under perturbation; competitive even under adaptive attacks; surrogate variant for unavailable retrievers. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2603.22934)

- **GraphER: Efficient Graph-Based Enrichment and Reranking for RAG** — Ruizhong Miao et al., arXiv, **2026-03-26** [Q1+ 2026 carry-forward]. Graph-based reranker that runs over standard vector stores (no KG required), retriever-agnostic with claimed negligible latency overhead. *Traction:* too-early-to-tell. Confidence: low-medium. → [arXiv](https://arxiv.org/abs/2603.24925)

- **Diagnosing LLM-based Rerankers in Cold-Start Recommender Systems: Coverage, Exposure and Practical Mitigations** — Ekaterina Lemdiasova et al., arXiv, **2026-02-09** [Q4 2025/Q1 2026 boundary, carry-forward; **cluster negative anchor**]. Cross-encoder rerankers fail in cold-start movie recommendation: HR@10 of 0.268 (popularity) vs 0.008 (LLM rerank); blames retrieval coverage, not reranker capacity. *Traction:* high-confidence-prominent. Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2604.16318)

### Cluster E: Listwise / late-interaction architectures evolve toward smaller-and-stronger

- **jina-reranker-v3: Last but Not Late Interaction for Listwise Document Reranking** — Feng Wang et al., arXiv, **2025-09-29** [Q3 2025; cluster anchor]. 0.6B-parameter multilingual listwise reranker introducing **"last but not late" interaction**: causal attention between query and all candidate documents in the same context window before extracting contextual embeddings from each document's final token; **state-of-the-art BEIR at NDCG@10 = 61.94**. *Traction:* high-confidence-prominent (jina is a known retrieval-model lab; explicit head-to-head with ColBERT family). Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2509.25085)

- **CoRe Heads: Contrastive Retrieval Heads Improve Attention-Based Re-Ranking** — Linh Tran et al., arXiv, **2025-10-02** [Q3 2025]. Identifies a small set (<1% of all heads) of retrieval-discriminative attention heads via a contrastive scoring metric; substantially improves listwise reranking accuracy across three LLMs; pruning final 50% of layers preserves accuracy. *Traction:* gaining-traction; both interpretability and efficiency contributions. Confidence: medium. → [arXiv](https://arxiv.org/abs/2510.02219)

- **L2G: Listwise Reranking for Corpus Feedback** — Soyoung Yoon et al., arXiv, **2025-10-01** [Q3 2025]. Implicitly induces document graphs from listwise reranker logs; matches oracle-based graph methods on TREC-DL and BEIR with **zero additional LLM calls**. *Traction:* gaining-traction; the graph-from-logs framing is reusable. Confidence: medium. → [arXiv](https://arxiv.org/abs/2510.00887)

- **Col-Bandit: Zero-Shot Query-Time Pruning for Late-Interaction Retrieval** — Roi Pony et al., arXiv, **2026-02-02** [Q4 2025/Q1 boundary]. Casts late-interaction reranking as a finite-population Top-K identification problem; adaptively reveals only the (document, query token) MaxSim entries needed; zero-shot drop-in over standard multi-vector systems on BEIR + REAL-MM-RAG. *Traction:* gaining-traction; clean engineering on a known bottleneck. Confidence: medium. → [arXiv](https://arxiv.org/abs/2602.02827)

- **Nemotron ColEmbed V2: Top-Performing Late Interaction Embedding Models for Visual Document Retrieval** — Gabriel de Souza P. Moreira et al., arXiv, **2026-02-03** [Q4 2025/Q1 boundary]. Family of 3B/4B/8B late-interaction VLM embedders; **8B variant ranks first on ViDoRe V3 leaderboard at NDCG@10 = 63.42** (as of Feb 3, 2026). *Traction:* high-confidence-prominent (NVIDIA-affiliated; leaderboard-leading). Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2602.03992)

- **AdaRankLLM: Rethinking the Necessity of Adaptive RAG through Adaptive Listwise Ranking** — Jun Feng et al., arXiv, **2026-04-17** [Q1+ 2026 carry-forward]. Adaptive listwise reranker with passage dropout + progressive distillation for small LLMs; identifies a role-shift of adaptive retrieval (filter for weak models, efficiency lever for strong ones). Tested across 8 LLMs. *Traction:* gaining-traction; the role-shift framing is conceptually sharp. Confidence: medium. → [arXiv](https://arxiv.org/abs/2604.15621)

### Cluster F: Agent memory consolidates around layered architectures

- **Agentic Memory: Learning Unified Long-Term and Short-Term Memory Management for LLM Agents** — Yi Yu et al., arXiv, **2026-01-05** [Q4 2025]. Unified framework integrating LTM + STM management directly into agent policy; memory operations as tool-based actions (store/retrieve/update/summarize/discard); three-stage progressive RL with step-wise GRPO. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.01885)

- **xMemory: Beyond RAG for Agent Memory — Retrieval by Decoupling and Aggregation** — Zhanghao Hu et al., arXiv, **2026-02-02** [Q4 2025/Q1 boundary]. Argues agent memory is a bounded coherent dialogue stream (not large heterogeneous corpus); decouples memories into semantic components, organises them hierarchically, retrieves top-down from themes/semantics down to raw messages only when needed. *Traction:* gaining-traction; cleanly addresses the structural mismatch between RAG and agent memory. Confidence: medium. → [arXiv](https://arxiv.org/abs/2602.02007)

- **SYNAPSE: Empowering LLM Agents with Episodic-Semantic Memory via Spreading Activation** — Hanqi Jiang et al., arXiv, **2026-01-06** [Q4 2025]. Memory as dynamic graph where relevance emerges from spreading activation rather than pre-computed links; lateral inhibition + temporal decay; Triple Hybrid Retrieval; outperforms state-of-the-art on LoCoMo's complex temporal/multi-hop tasks. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.02744)

- **Continuum Memory Architectures for Long-Horizon LLM Agents** — Joe Logan, arXiv, **2026-01-14** [Q4 2025]. Defines a class of systems (Continuum Memory Architecture, CMA) maintaining and updating internal state across interactions through persistent storage, selective retention, associative routing, temporal chaining, consolidation; class-definition paper rather than a system paper. *Traction:* too-early-to-tell; class-definition papers are slow burners. Confidence: low-medium. → [arXiv](https://arxiv.org/abs/2601.09913)

- **Lightweight LLM Agent Memory with Small Language Models (LightMem)** — Jiaquan Zhang et al., arXiv, **2026-04-09** [Q1+ 2026 carry-forward]. SLM-driven 3-tier (STM/MTM/LTM) agent memory + 2-stage vector-coarse + semantic-consistency-rerank retrieval; +2.5 F1 over A-MEM on LoCoMo at 83 ms retrieval / 581 ms end-to-end. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2604.07798)

- **Graph-Native Cognitive Memory for AI Agents: Formal Belief Revision Semantics for Versioned Memory Architectures (Kumiho)** — Young Bin Park, arXiv, **2026-03-18** [Q1+ 2026 carry-forward]. Graph-native agent memory grounded in **AGM belief-revision postulates K*2-K*6 and Hansson's belief-base postulates**; hybrid retrieval + client-side LLM rerank; 93.3% LoCoMo-Plus authors / mid-80s reproduction (vs 45.7% prior best). *Traction:* gaining-traction; rare formal grounding. Confidence: medium. → [arXiv](https://arxiv.org/abs/2603.17244)

- **Diagnosing Retrieval vs. Utilization Bottlenecks in LLM Agent Memory** — Boqin Yuan et al., arXiv, **2026-03-02** [Q1+ 2026 carry-forward; **cluster empirical anchor**]. 3×3 diagnostic on agent memory: **retrieval method dominates** (20-pt accuracy span) vs write strategy (3-8 pts); raw chunks match expensive summarization at zero LLM-call cost. *Traction:* high-confidence-prominent; counterintuitive, code released. Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2603.02473)

### Cluster G: Learned-sparse retrieval gets LLM backbones

- **Milco: Learned Sparse Retrieval Across Languages via a Multilingual Connector** — Thong Nguyen et al., arXiv, **2025-10-01** [Q3 2025]. LSR architecture mapping queries and documents from different languages into a shared English lexical space via a multilingual connector; **30 active dimensions per document beats dense BGE-M3 / Qwen3-Embed**. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2510.00671)

- **LACONIC: Dense-Level Effectiveness for Scalable Sparse Retrieval via a Two-Phase Training Curriculum** — Zhichao Xu et al., arXiv, **2026-01-04** [Q4 2025; cluster anchor]. Family of LSR retrievers based on Llama-3 (1B / 3B / 8B); 8B variant achieves **60.2 nDCG on MTEB Retrieval (rank 15 on the leaderboard as of Jan 1, 2026), at 71% less index memory than equivalent dense models**. *Traction:* high-confidence-prominent; LSR + LLM-scale backbone is the cluster's pivot. Confidence: medium-high. → [arXiv](https://arxiv.org/abs/2601.01684)

- **Multivector Reranking in the Era of Strong First-Stage Retrievers** — Silvio Martinico et al., arXiv, **2026-01-08** [Q4 2025]. Replaces token-level gather phase with a single-vector LSR retriever, recasting gather-and-refine into classic two-stage retrieval; reduces gather latency, exposes query encoding as the new bottleneck. *Traction:* gaining-traction; reframing the multi-vector pipeline. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.05200)

- **Forward Index Compression for Learned Sparse Retrieval** — Sebastian Bruch et al., arXiv, **2026-02-05** [Q4 2025/Q1 boundary]. Targets the forward-index data structure that constitutes a substantial fraction of LSR index size; **DotVByte** (improvement over StreamVByte for inner-product computation) achieves significant space savings on MS-MARCO. *Traction:* too-early-to-tell; engineering paper on a load-bearing data structure. Confidence: low-medium. → [arXiv](https://arxiv.org/abs/2602.05445)

### Cluster H: GraphRAG variants and graph-structured retrieval mature

- **Beyond Static Retrieval: Opportunities and Pitfalls of Iterative Retrieval in GraphRAG** — Kai Guo et al., arXiv, **2025-09-29** [Q3 2025; cluster diagnostic]. First systematic study of iterative retrieval in GraphRAG; iteration improves complex multi-hop questions and helps promote bridge documents into leading ranks, but naive expansion introduces noise reducing precision. *Traction:* gaining-traction; named in subsequent papers' related-work. Confidence: medium. → [arXiv](https://arxiv.org/abs/2509.25530)

- **Do We Still Need GraphRAG? Benchmarking RAG and GraphRAG for Agentic Search Systems (RAGSearch)** — Dongzhe Fan et al., arXiv, **2026-04-01** [Q1+ 2026 carry-forward; cluster comparative anchor]. Unified benchmark; agentic search closes most of the dense-vs-graph gap (especially RL-based); GraphRAG holds advantage on complex multi-hop when its offline cost amortizes. *Traction:* gaining-traction. Confidence: medium. → [arXiv](https://arxiv.org/abs/2604.09666)

### Cluster I: Comparative empirical evaluations recalibrate field assumptions

- **Is Agentic RAG Worth It? An experimental comparison of RAG approaches** — Pietro Ferrazzi et al., arXiv, **2026-01-12** [Q4 2025; cluster recalibrator]. Empirical comparison of "Enhanced" vs "Agentic" RAG across multiple scenarios and dimensions; concludes the trade-off is conditional, not coronation. *Traction:* gaining-traction; the kept set's most direct empirical pushback against agentic-RAG triumphalism. Confidence: medium. → [arXiv](https://arxiv.org/abs/2601.07711)

- **MCP vs RAG vs NLWeb vs HTML: A Comparison of Different Agent Interfaces to the Web** — Aaron Steiner et al., arXiv, **2025-11-28** [Q3 2025]. Single controlled environment with identical tasks across HTML / RAG / MCP / NLWeb agents using GPT 4.1 / GPT 5 / GPT 5 mini / Claude Sonnet 4; **RAG, MCP, and NLWeb all outperform HTML on effectiveness and efficiency**, no single winner among the three. *Traction:* gaining-traction; the field's first like-for-like comparison of these four interface paradigms. Confidence: medium. → [arXiv](https://arxiv.org/abs/2511.23281)

- **Rethinking Retrieval: From Traditional RAG to Agentic and Non-Vector Reasoning Systems in the Financial Domain** — Elias Lumer et al., arXiv, **2025-11-22** [Q3 2025]. Systematic evaluation comparing vector-based agentic RAG (hybrid search + metadata filtering) against hierarchical-node-based systems on 1,200 SEC 10-K/10-Q/8-K filings; **vector-based agentic RAG wins 68% over hierarchical-node-based**, comparable latency. *Traction:* gaining-traction; well-controlled vertical evaluation that anticipates the broader vector-vs-non-vector debate. Confidence: medium. → [arXiv](https://arxiv.org/abs/2511.18177)

### Outliers (didn't fit any of the nine clusters cleanly)

- **Higress-RAG: A Holistic Optimization Framework for Enterprise RAG (Hybrid Retrieval + Adaptive Routing + CRAG)** — Weixi Lin, arXiv, **2025-12-30** [Q4 2025]. Enterprise architecture with Adaptive Routing + Semantic Caching + Hybrid Retrieval (RRF over dense + sparse) + Corrective RAG, MCP-based; not a new technique paper but a systems-integration reference. *Traction:* gaining-traction (single-author, but the architecture-as-reference framing tends to accumulate citations slowly). Confidence: medium. → [arXiv](https://arxiv.org/abs/2602.23374)

- **MemoryGraft: Persistent Compromise of LLM Agents via Poisoned Experience Retrieval** — Saksham Sahai Srivastava, Haoyu He, arXiv, **2025-12-18** [Q4 2025]. Indirect-injection attack implanting malicious successful experiences into agent long-term memory via benign ingestion-level artifacts; demonstrates persistence beyond standard RAG poisoning. *Traction:* gaining-traction within agent-security subthread. Confidence: medium. → [arXiv](https://arxiv.org/abs/2512.16962)

---

## Notes for next time

- **Replication signal to watch — the "no embedder needed" thread.** Keyword Search Is All You Need (Dec 2025), Corpus2Skill (Apr 2026), DCI (May 2026), and Interact-RAG (Oct 2025) collectively form three quarters of escalating challenge to the vector-store assumption. Watch for a **fourth independent confirmation** (different lab, non-BRIGHT/BEIR benchmark) within the next 1-2 quarters; that's the discriminating evidence.
- **Convergence point to watch — rerank-for-utility consolidates.** Cluster A has 9 papers across 3 quarters all arguing the same direction with different mechanisms. CAR's ρ=0.964 between reranker score and downstream F1 is the cluster's empirical anchor; if 2-3 follow-up papers replicate that correlation on different benchmarks, the field has its first reliable reranker-quality metric. If RRPO-style RL-feedback consistently beats LCR/CAR-style training-free at scale, the cluster splits in favor of trained.
- **Negative result not absorbed — recency bias.** Q3 2025 (Recency Bias diagnostic) and Q1+ 2026 (FRESCO) found the same bias from independent angles 8 months apart. New reranker papers in Q1+ 2026 still do not consistently include recency-bias diagnostics. This is the kept set's clearest replication-without-uptake signal — the field is producing the negative result but not changing reranker evaluation protocols.
- **Negative result not absorbed — retrieval-method-dominates.** The agent-memory diagnostic (P36 carry-forward) is striking and code-released. Q4 2025 / Q1+ 2026 agent-memory architecture papers (LightMem, Kumiho, Agentic Memory, xMemory, SYNAPSE, Continuum Memory) each propose write/retain mechanisms without explicitly engaging this finding. Worth tracking whether the next round of agent-memory papers (next 2-3 months) start to include retrieval-method ablations as a default.
- **Missing comparison — open-source vs commercial-API rerankers.** No paper in the kept set runs head-to-head against a strong commercial reranker API (Cohere Rerank, Voyage, etc.) in the agentic-RAG setting. Open-source vs commercial-API comparison would help calibrate the absolute strength of these techniques.
- **Pass 3 candidates.** If the operator wants a deep-read on any specific paper, the strongest candidates are (in order): **DCI (P28, May 2026)** for the bold no-embedder position; **CAR (P26, May 2026)** for the ρ=0.964 utility-correlation claim; **Keyword Search Is All You Need (Dec 2025)** for the 90%-of-RAG-without-vector-DB measurement; **LACONIC (Jan 2026)** for the LSR-with-LLM-backbones SOTA claim; **LatentRAG (May 2026)** for the ~90% latency cut. Trigger via a DEEP_READ intent on the relevant arXiv ID.
- **Watchlist suggestion (advisory).** This thematic run reused the same per-week override file as the prior 3-month run. If LLM-agent retrieval is to become a recurring topic, consider adding to `shared-context/watchlist.md`: `agentic RAG`, `reranker for LLM agents`, `agent memory`, `LLM-as-reranker`, `direct corpus interaction`, `learned sparse retrieval`. Operator decision; the orchestrator does not edit the watchlist.

---

## Full list

See `ops/paper-synthesizer/2026-W19-papers-8mo.md` for the unsynthesized table of every kept and reviewed candidate with rationale and traction notes.

## Generated

- Date: 2026-05-09
- Override file: `ops/paper-synthesizer/overrides/2026-W19.md` (extended window applied at orchestrator level for this run)
- Cache: `ops/paper-synthesizer/.cache/2026-W19-8mo-candidates.json`, `2026-W19-8mo-picked.json`, `2026-W19-8mo-w*-*.xml`
- Prior carry-forward source: `ops/paper-synthesizer/digests/2026-W19-on-demand-retrieval-rerank-llm-agents.md` and `ops/paper-extractor/2026-W19/`
- Digest: this file (`ops/paper-synthesizer/digests/2026-W19-on-demand-retrieval-rerank-evolution-8mo.md`)
