# 2026-W19 On-Demand Digest — Retrieval and Re-ranking Techniques for LLM Agents

**Run type:** on-demand thematic question (not a standard weekly digest).
**Window:** 2026-02-09 → 2026-05-09 (3 months).
**Source:** arXiv (cs.IR primary; cs.CL, cs.LG, cs.AI secondary). PubMed / bioRxiv / medRxiv skipped (off-theme).
**Operator's question:** Latest retrieval and re-ranking techniques for LLM agents — papers from the last 3 months that are highly cited or gaining traction.
**Override file:** `ops/paper-synthesizer/overrides/2026-W19.md`
**Generated:** 2026-05-09

> **Caveats up front.** Citation counts within a 3-month preprint window are not directly observable; the per-paper traction signal is calibrated heuristically (clear-technique-contribution + named-system + benchmark-coverage + group-affiliation). I report it as a calibrated confidence, not as ground truth. Pass 2 ran in degraded mode — abstract-only — so figure-level analysis and reference triage were not extracted; the digest's specifics are what the abstracts state, with hedging preserved.

---

## 30,000 ft — What changed in retrieval / rerank for LLM agents over the last 3 months

The clearest through-line across the kept papers is that the **target of optimization is moving from IR-style relevance to LLM-utility**, both for rerankers (cluster 1, five papers) and for retrieval interfaces themselves (cluster 4, four papers). The boldest version of this shift comes from cluster 4: a position-with-evaluation paper that eliminates the embedder, vector index, and retrieval API entirely and lets the agent grep the corpus directly — and reports outperforming strong sparse, dense, and reranking baselines on multiple BRIGHT/BEIR datasets (DCI, P23). What did *not* change: there is no shared evaluation framework for agentic-RAG efficiency yet, so the six papers in cluster 3 each measure latency / search-depth / failure-cost / orchestration against different baselines. A second negative finding worth flagging — the Cold-Start LLM-Reranker Diagnostic (cluster 2) shows popularity-rank dominating LLM rerankers ~30x on HR@10 in a recommender-system cold-start setting, and locates the bottleneck at retrieval coverage, not reranker capacity. Continuity: this is the project's first run, so there is no prior digest to anchor against; future runs in this thread should track whether the rerank-for-utility cluster consolidates around training-free (LCR, CAR) or trained (RRPO) approaches, and whether the "no-retriever-at-all" position from DCI replicates beyond its authors' setup.

---

## 3,000 ft — By theme

### Cluster 1: Rerankers shift their target from IR relevance to downstream LLM utility

Five papers in this 3-month window argue that the conventional reranker objective (does this document match the query?) is the wrong objective for RAG, and that the right objective is some form of generator-utility signal. CAR (P5) and LCR (P3) operationalize this with LLM-confidence change — training-free, plug-and-play. RRPO (P4) does the same via RL on LLM feedback as the reward. MemReranker (P1) and Prism-Reranker (P2) push the same conclusion through reranker design: distillation from LLM judges, and reranker outputs that emit a contribution + evidence-passage rewrite the agent can directly consume. The five papers agree on the diagnosis and disagree only on the mechanism.

**Tension within the cluster.** Training-free (LCR, CAR) vs trained (RRPO, MemReranker, Prism) splits the cluster on method but not on direction. Whether the training-free shortcut suffices at scale, or whether RL/distillation is needed for production use, is unresolved.

### Cluster 2: Specialized rerankers fill gaps the generic ones miss — recency, robustness, listwise adaptation, graph proximity

Five papers in the window each surface a specific failure mode of generic rerankers and offer a targeted fix. FRESCO (P12) finds rerankers prefer older, semantically-rich documents over recent factual ones; instruction tuning recovers up to +27% on evolving knowledge. AdaRankLLM (P17) shows adaptive listwise reranking shifts role with model strength (filter for weak, efficiency for strong). GraphER (P7) adds non-semantic graph proximity without requiring a knowledge graph. ProGRank (P15) is a retriever-side training-free defense against corpus poisoning. The Cold-Start Diagnostic (P9) is the cluster's negative result: rerankers can fail badly when retrieval coverage is poor, with popularity-rank dominating LLM rerankers by ~30x in cold-start movie recommendation.

**Tension within the cluster.** The Cold-Start paper's finding (popularity-beats-LLM-reranker) sits in tension with the cluster's other papers, which all assume the reranker is the right place to fix retrieval problems. The Cold-Start authors locate the bottleneck upstream — at retrieval coverage. The cluster as a whole supports both readings: rerankers have specialized failure modes worth fixing AND rerankers cannot rescue a retrieval pool that already lost the relevant items.

### Cluster 3: Agentic-RAG efficiency is the 2026 frontier — latency, search depth, failure repair, orchestration

Six papers attack the cost/latency penalty of multi-step agentic RAG. LatentRAG (P18) is the most aggressive: shift the entire reasoning + retrieval loop into latent space, claiming ~90% latency reduction at comparable accuracy. AutoSearch (P27) trains an RL agent to find the minimal-sufficient search depth via self-answer scoring. Doctor-RAG (P35) decouples failure diagnosis from repair, reusing validated reasoning prefixes instead of rerunning the pipeline. Test-Time Strategies (P44) gets +5.6% EM and -10.5% turns on Search-R1 with two test-time-only modules. APEX-Searcher (P43) decomposes training into RL-for-planning + SFT-for-execution to escape sparse-reward issues. HERA (P34) co-evolves multi-agent topology and per-role prompts, claiming +38.7% over recent baselines.

**Tension within the cluster.** These papers attack different dimensions of the same overall budget (latency, search depth, failure cost, orchestration cost) — they are complementary rather than contradictory. The open question they collectively raise: what does an agentic-RAG efficiency benchmark look like, given that each paper measures against a different baseline (Search-R1, single-step RAG, rerun-based repair, recent multi-agent baselines)? No common evaluation framework yet exists across these efficiency dimensions.

### Cluster 4: The retrieval interface itself is the bottleneck — not the retriever's capacity

Five papers in different ways argue the same provocative claim: when agentic systems underperform on knowledge-intensive QA, the failure is rarely the retriever's quality and almost always the retrieval interface's shape. DCI (P23) takes the most extreme stance — let the agent grep the raw corpus directly, no embedder, no index, no retrieval API — and claims to outperform strong sparse, dense, and reranking baselines on BRIGHT, BEIR, BrowseComp-Plus. Corpus2Skill (P22) replaces top-k retrieval with navigation through an offline-distilled hierarchical skill directory, outperforming dense retrieval / RAPTOR / agentic-RAG on enterprise QA. RAGSearch (P24) finds that agentic search itself substantially closes the gap between dense RAG and GraphRAG. The Retrieval-vs-Utilization Diagnostic (P21) for agent memory finds retrieval method swings accuracy 20 points while write-strategy contributes only 3-8. The Cold-Start Diagnostic (P9, best-fit in cluster 2) blames retrieval coverage, not reranker capacity.

**Tension within the cluster.** DCI's no-retriever-at-all claim is the cluster's strongest version of the argument and also its most fragile — if it replicates beyond the authors' setup, the implications for the vector-store paradigm are large. Corpus2Skill's pre-compiled skill tree is the opposite extreme: a heavy offline cost to make serve-time navigation fast. RAGSearch's framing — agentic search compensates for lack of explicit graph structure — is the cluster's most cautious reading: not 'embeddings are wrong' but 'the interaction loop matters more than the retriever architecture.'

### Cluster 5: Agent memory consolidates around layered architectures with formal or empirical anchors

Three papers represent the agent-memory subfield's slow consolidation in this window. LightMem (P20) proposes a layered (STM/MTM/LTM) architecture driven by small language models, with a two-stage vector-coarse-then-rerank retrieval, claiming +2.5 F1 over A-MEM on LoCoMo at 83 ms retrieval / 581 ms end-to-end. Kumiho (P41) brings unusual formal grounding — proves AGM belief-revision postulates K*2-K*6 and Hansson's belief-base postulates over a property-graph memory — and achieves 93.3% on LoCoMo-Plus (mid-80s on independent reproduction, still well above the 45.7% prior best). The Retrieval-vs-Utilization Diagnostic (P21, best-fit in cluster 4) provides the cluster's empirical anchor: retrieval method, not write strategy, is what matters.

**Tension within the cluster.** The two architectures in this cluster represent different design philosophies: LightMem leans pragmatic (SLM-driven, latency-budgeted) and Kumiho leans rigorous (AGM-grounded, graph-native). Both report on LoCoMo so their numbers can be compared, but they answer different questions — LightMem on efficient retrieval, Kumiho on principled belief revision. The cluster's open question is whether the field will converge on a unified framework or maintain these two design philosophies as legitimate alternatives.

### Outliers (notable papers that don't form a thematic argument)

- **Quantifying the Accuracy and Cost Impact of Design Decisions in Budget-Constrained Agentic LLM Search** — Measurement harness paper — provides reproducible budget-constrained evaluation setup rather than a method or new finding. Too cross-cutting for any single cluster (its findings inform every efficiency-themed paper in cluster 3 plus the rerank papers in cluster 1).
- **A Reference Architecture for Agentic Hybrid Retrieval in Dataset Search** — Software-architecture-style paper for dataset search; explicit governance tactics and 7-variant evaluation framework. Architecture papers don't fit argument-shaped clusters cleanly — they describe a design space rather than argue a position.
- **AgenticOCR: Parsing Only What You Need for Efficient Retrieval-Augmented Generation** — Multimodal-RAG primitive — proposes OCR-as-third-RAG-block. Sits between retrieval and reranking conceptually but is multimodal-document-specific, and the only multimodal-focused paper in the kept set.

---

## 300 ft — Papers, by cluster

### Cluster 1: Rerankers shift their target from IR relevance to downstream LLM utility

- **MemReranker: Reasoning-Aware Reranking for Agent Memory Retrieval** — Chunyu Li et al., arXiv, 2026-05-07.
  Reranker family (0.6B / 4B) for agent memory; multi-teacher LLM distillation; 0.737 MAP at ~10-20% the latency of Gemini-3-Flash.
  *Traction:* gaining-traction: clear technical contribution and quantified comparison with frontier models; the agent-memory framing is itself a 2026 trend. Confidence: medium (preprint posted 2026-05-07; too recent for citations to materialize).
  → [arXiv](https://arxiv.org/abs/2605.06132)

- **Prism-Reranker: Beyond Relevance Scoring -- Jointly Producing Contributions and Evidence for Agentic Retrieval** — Dun Zhang, arXiv, 2026-04-26.
  Reranker family (0.8B-9B) that outputs a contribution statement and an evidence-passage rewrite alongside the relevance verdict; +1.54 average NDCG@10 on BEIR-QA when applied to Qwen3-Reranker-4B.
  *Traction:* high-confidence-prominent: targets a specific, well-known agentic-RAG pain point (token-waste from full-document context); single-author preprint but model release lowers adoption friction. Confidence: medium-high.
  → [arXiv](https://arxiv.org/abs/2604.23734)

- **LLM-Confidence Reranker: A Training-Free Approach for Enhancing Retrieval-Augmented Generation Systems** — Zhipeng Song et al., arXiv, 2026-02-14.
  Training-free reranker that scores by LLM Maximum-Semantic-Cluster-Proportion confidence; up to +20.6% NDCG@5 on BEIR over fine-tuned rerankers using 7-9B LLMs.
  *Traction:* gaining-traction: appealing zero-training premise and large reported headline number, but 'up to' qualifier on the lift means the average gain is smaller. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2602.13571)

- **Optimizing RAG Rerankers with LLM Feedback via Reinforcement Learning** — Yuhang Wu et al., arXiv, 2026-04-02.
  RL-trains rerankers using LLM-generation feedback as the reward (no human labels), with a reference-anchored deterministic baseline; outperforms RankZephyr on knowledge-intensive QA.
  *Traction:* gaining-traction: the rerank-for-utility-not-relevance framing is a hot subthread in RAG; alignment-via-RL is well-trodden technique territory transferred to a new locus. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2604.02091)

- **CAR: Query-Guided Confidence-Aware Reranking for Retrieval-Augmented Generation** — Zhipeng Song et al., arXiv, 2026-05-06.
  Training-free reranker that uses semantic-consistency-of-sampled-answers as a usefulness signal; +25.4% on YesNo + Contriever and ρ=0.964 with downstream generation F1.
  *Traction:* high-confidence-prominent within the 'rerank-by-utility' subthread: ρ=0.964 with downstream F1 is a strong empirical anchor that should attract follow-up replication. Confidence: medium-high.
  → [arXiv](https://arxiv.org/abs/2605.04495)

### Cluster 2: Specialized rerankers fill gaps the generic ones miss — recency, robustness, listwise adaptation, graph proximity

- **FRESCO: Benchmarking and Optimizing Re-rankers for Evolving Semantic Conflict in Retrieval-Augmented Generation** — Sohyun An et al., arXiv, 2026-04-14.
  Recency-aware reranker benchmark using paired recency-seeking queries + Wikipedia revision history; reveals a consistent reranker bias toward older docs; instruction tuning recovers up to +27% on evolving knowledge.
  *Traction:* gaining-traction: temporally-aware retrieval is an underexplored gap that production RAG hits constantly; benchmark + recipe is a complete contribution. Confidence: medium-high.
  → [arXiv](https://arxiv.org/abs/2604.14227)

- **Rethinking the Necessity of Adaptive Retrieval-Augmented Generation through the Lens of Adaptive Listwise Ranking** — Jun Feng et al., arXiv, 2026-04-17.
  Adaptive listwise reranker with passage dropout + progressive distillation for small LLMs; identifies a role-shift of adaptive retrieval (filter for weak models, efficiency lever for strong ones).
  *Traction:* gaining-traction: the role-shift framing is an important conceptual sharpening for the adaptive-RAG literature; tested across 8 LLMs adds breadth. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2604.15621)

- **GraphER: An Efficient Graph-Based Enrichment and Reranking Method for Retrieval-Augmented Generation** — Ruizhong Miao et al., arXiv, 2026-03-26.
  Graph-based reranker that runs over standard vector stores (no KG required), retriever-agnostic with claimed negligible latency overhead.
  *Traction:* too-early-to-tell: useful technique with a clean integration story for production RAG, but the abstract's empirical claim ('demonstrates effectiveness') is hedged. Confidence: low-medium.
  → [arXiv](https://arxiv.org/abs/2603.24925)

- **ProGRank: Probe-Gradient Reranking to Defend Dense-Retriever RAG from Corpus Poisoning** — Xiangyu Yin et al., arXiv, 2026-03-24.
  Training-free defense reranker that probes the retriever's gradient response under perturbation; competitive even under adaptive attacks, with a surrogate variant for unavailable retrievers.
  *Traction:* gaining-traction: corpus poisoning is a rising concern for production RAG; the retriever-side training-free design is uniquely deployable. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2603.22934)

- **Diagnosing LLM-based Rerankers in Cold-Start Recommender Systems: Coverage, Exposure and Practical Mitigations** — Ekaterina Lemdiasova et al., arXiv, 2026-02-09.
  Cross-encoder rerankers fail in cold-start movie recommendation: HR@10 of 0.268 (popularity) vs 0.008 (LLM rerank); blames retrieval coverage, not reranker capacity.
  *Traction:* high-confidence-prominent within the 'rerankers don't help in low-recall regime' subthread; honest, well-controlled negative result with full code release. Confidence: medium-high.
  → [arXiv](https://arxiv.org/abs/2604.16318)

### Cluster 3: Agentic-RAG efficiency is the 2026 frontier — latency, search depth, failure repair, orchestration

- **LatentRAG: Latent Reasoning and Retrieval for Efficient Agentic RAG** — Yijia Zheng et al., arXiv, 2026-05-07.
  Runs agentic-RAG reasoning + retrieval in latent space (one forward pass), with a parallel decoder for transparency; ~90% latency reduction at comparable accuracy on seven benchmarks.
  *Traction:* high-confidence-prominent: ~90% latency cut on agentic RAG is a headline-worthy result; latent-reasoning is a 2026-year theme. Confidence: medium-high.
  → [arXiv](https://arxiv.org/abs/2605.06285)

- **AutoSearch: Adaptive Search Depth for Efficient Agentic RAG via Reinforcement Learning** — Jingbo Sun et al., arXiv, 2026-04-19.
  RL framework for agentic-RAG search-depth control: scores each step's intermediate self-answer to find minimal-sufficient depth and penalize over-searching.
  *Traction:* gaining-traction: search-depth control is a practical bottleneck many agentic-RAG deployments hit; clean operationalization. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2604.17337)

- **Doctor-RAG: Failure-Aware Repair for Agentic Retrieval-Augmented Generation** — Shuguang Jiao et al., arXiv, 2026-04-01.
  Failure-aware repair for agentic RAG: diagnoses earliest failure point in a trajectory, repairs locally with prefix reuse; beats full-pipeline rerun on accuracy and token cost.
  *Traction:* gaining-traction: practical pain point for production agentic-RAG; the diagnose-vs-repair separation is a clean conceptual move. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2604.00865)

- **Test-Time Strategies for More Efficient and Accurate Agentic RAG** — Brian Zhang et al., arXiv, 2026-03-12.
  Test-time tweaks (contextualization + de-dup of retrieved docs) on Search-R1; +5.6% EM and -10.5% turns on HotpotQA + Natural Questions.
  *Traction:* too-early-to-tell: pure test-time engineering on a recent baseline; modest but real lift. Confidence: low-medium.
  → [arXiv](https://arxiv.org/abs/2603.12396)

- **APEX-Searcher: Augmenting LLMs' Search Capabilities through Agentic Planning and Execution** — Kun Chen et al., arXiv, 2026-03-14.
  Two-stage agentic-search training: stage-1 RL with decomposition-specific rewards (planning); stage-2 SFT on multi-hop trajectories (execution).
  *Traction:* too-early-to-tell: RL-then-SFT recipes are technique-heavy; quantitative claims would be sharper with concrete benchmark numbers in the abstract. Confidence: low-medium.
  → [arXiv](https://arxiv.org/abs/2603.13853)

- **Experience as a Compass: Multi-agent RAG with Evolving Orchestration and Agent Prompts** — Sha Li et al., arXiv, 2026-04-01.
  Multi-agent RAG that co-evolves agent topology (reward-guided sampling) and per-role prompts (dual-axis credit assignment); +38.7% average across six knowledge-intensive benchmarks.
  *Traction:* gaining-traction: 38.7% headline lift will draw eyes; orchestration-evolution is a less-explored angle than agent-evolution alone. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2604.00901)

### Cluster 4: The retrieval interface itself is the bottleneck — not the retriever's capacity

- **Beyond Semantic Similarity: Rethinking Retrieval for Agentic Search via Direct Corpus Interaction** — Zhuofeng Li et al., arXiv, 2026-05-03.
  Lets the agent grep / read / script the raw corpus directly (no embedder, no index, no retrieval API); reportedly outperforms strong sparse, dense, and reranking baselines on BRIGHT, BEIR, BrowseComp-Plus.
  *Traction:* gaining-traction: bold position-with-evaluation; if the claim replicates, it is a structural challenge to the entire vector-store paradigm for agentic settings. Confidence: medium (preprint; needs replication beyond authors' setup).
  → [arXiv](https://arxiv.org/abs/2605.05242)

- **Don't Retrieve, Navigate: Distilling Enterprise Knowledge into Navigable Agent Skills for QA and RAG** — Yiqun Sun et al., arXiv, 2026-04-16.
  Distills corpus into a navigable skill directory (LLM summaries at each level + doc-ID retrieval); outperforms dense / RAPTOR / agentic-RAG on WixQA, with single-domain corpora as the right regime.
  *Traction:* gaining-traction: a structurally fresh alternative to top-k retrieval; the regime-characterization is honest about scope. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2604.14572)

- **Do We Still Need GraphRAG? Benchmarking RAG and GraphRAG for Agentic Search Systems** — Dongzhe Fan et al., arXiv, 2026-04-01.
  Unified benchmark of dense-RAG vs GraphRAG under agentic search; agentic search closes most of the dense-vs-graph gap (especially RL-based); GraphRAG holds advantage on complex multi-hop when its offline cost amortizes.
  *Traction:* gaining-traction: addresses a question many production teams are quietly asking; comparative-benchmark papers tend to accumulate citations slowly but durably. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2604.09666)

- **Diagnosing Retrieval vs. Utilization Bottlenecks in LLM Agent Memory** — Boqin Yuan et al., arXiv, 2026-03-02.
  3x3 diagnostic on agent memory: retrieval method dominates (20-pt accuracy span) vs write strategy (3-8 pts); raw chunks match expensive summarization at zero LLM-call cost.
  *Traction:* high-confidence-prominent: sharp, counterintuitive finding with publicly released code; this is the kind of negative-result paper that recalibrates field priorities. Confidence: medium-high.
  → [arXiv](https://arxiv.org/abs/2603.02473)

### Cluster 5: Agent memory consolidates around layered architectures with formal or empirical anchors

- **Lightweight LLM Agent Memory with Small Language Models** — Jiaquan Zhang et al., arXiv, 2026-04-09.
  SLM-driven 3-tier (STM/MTM/LTM) agent memory + 2-stage vector-coarse + semantic-consistency-rerank retrieval; +2.5 F1 over A-MEM on LoCoMo at 83 ms retrieval / 581 ms end-to-end.
  *Traction:* gaining-traction: efficiency-first agent-memory work is a clear thread; LightMem's framing is clean. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2604.07798)

- **Graph-Native Cognitive Memory for AI Agents: Formal Belief Revision Semantics for Versioned Memory Architectures** — Young Bin Park, arXiv, 2026-03-18.
  Graph-native agent memory grounded in AGM belief-revision postulates with hybrid retrieval + client-side LLM rerank; 93.3% LoCoMo-Plus authors / mid-80s reproduction (vs 45.7% prior best).
  *Traction:* gaining-traction: rare degree of formal grounding in this subfield; honest reporting of authors-vs-reproduction gap. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2603.17244)

### Outliers

- **Quantifying the Accuracy and Cost Impact of Design Decisions in Budget-Constrained Agentic LLM Search** — Kyle McCleary et al., arXiv, 2026-03-09.
  Measurement harness for budget-constrained agentic search across 6 LLMs and 3 QA benchmarks; hybrid lexical+dense + lightweight rerank dominates the cost-accuracy frontier; deeper search caps quickly.
  *Traction:* too-early-to-tell: measurement papers are slow-burning influence (cited as the harness rather than a method); concrete budget-aware finding is useful. Confidence: low-medium.
  → [arXiv](https://arxiv.org/abs/2603.08877)

- **A Reference Architecture for Agentic Hybrid Retrieval in Dataset Search** — Riccardo Terrenzi et al., arXiv, 2026-03-28.
  Reference architecture for agentic hybrid retrieval in dataset search (BM25 + dense + RRF + LLM-agent rerank + offline pseudo-query metadata expansion); ReAct vs multi-agent horizontal architectures compared with explicit governance tactics.
  *Traction:* too-early-to-tell: architecture papers attract slower, durable citation patterns; the explicit governance framing is unusual and may be picked up by the LLM-ops community. Confidence: low-medium.
  → [arXiv](https://arxiv.org/abs/2604.16394)

- **AgenticOCR: Parsing Only What You Need for Efficient Retrieval-Augmented Generation** — Zhengren Wang et al., arXiv, 2026-02-27.
  Query-driven OCR module for visual-RAG that recognizes only regions of interest, sitting alongside embedding + reranking; claims expert-level performance on long visual documents.
  *Traction:* gaining-traction: visual-RAG is an active subthread, OpenDataLab affiliation lends credibility, code+models released. Confidence: medium.
  → [arXiv](https://arxiv.org/abs/2602.24134)

---

## Notes for next time

- **Replication signal to watch.** DCI (P23, cluster 4) makes the strongest provocative claim: agentic search without any embedder or retrieval API outperforms strong sparse / dense / reranking baselines. If this replicates in a follow-up paper from a different group within the next 3 months, the field's vector-store assumption is in serious question. If it does not replicate, the result becomes a methodology curiosity. Worth a re-scan of cs.IR / cs.CL in 6-8 weeks for follow-ups.

- **Convergence point to watch.** Cluster 1 has five papers all arguing the same direction (rerank-for-utility, not relevance) but with different mechanisms. Do they converge on a small number of dominant approaches over the next 3 months? CAR's ρ=0.964 between ranking gain and downstream F1 is the empirical anchor most likely to drive replication.

- **Missing comparison.** No paper in the kept set runs head-to-head against a strong commercial reranker API (Cohere Rerank, Voyage, etc.) in the agentic-RAG setting. Open-source vs commercial-API comparison would help calibrate the absolute strength of these techniques.

- **Watchlist suggestion (advisory).** This thematic run was driven by a per-week override file; the watchlist itself remained focused on life-sciences. If LLM-agent retrieval is to become a recurring topic, consider adding to `shared-context/watchlist.md`: `agentic RAG`, `reranker for LLM agents`, `agent memory`, `LLM-as-reranker`. Operator decision; the orchestrator does not edit the watchlist.

- **Pass 3 candidates.** If the operator wants a deep-read on any specific paper, the strongest candidates are: DCI (P23) for the bold position; CAR (P5) for the ρ=0.964 utility-correlation claim; LatentRAG (P18) for the ~90% latency-cut claim; Cold-Start Diagnostic (P9) for the rigorous negative result. Trigger via a DEEP_READ intent on the relevant arxiv ID.

---

## Full list

See `ops/paper-synthesizer/2026-W19-papers.md` for the unsynthesized table of every kept, reviewed, and dropped paper with rationale.
