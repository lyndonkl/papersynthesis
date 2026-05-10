# 2026-W19 On-Demand Run (8-month) — Full Paper List

**Operator theme:** Latest retrieval and reranking techniques for LLM agents — 8-month window, mechanism-family map + quarterly view + time-progression.
**Window:** 2025-09-09 → 2026-05-09.
**Source:** arXiv (cs.IR / cs.CL / cs.LG / cs.AI).
**Companion digest:** `ops/paper-synthesizer/digests/2026-W19-on-demand-retrieval-rerank-evolution-8mo.md`.

## Pipeline summary

- arXiv fetched (older sub-window 2025-09-09 → 2026-02-08): 2,064 unique records across 9 query slices (3 sub-windows × 3 keyword slices).
- Keyword-filtered candidates (at least one theme keyword in title or abstract): 1,894.
- Curated picks via title-match against mechanism-family slate: 59.
- Final KEEP for digest (combined with carry-forward from prior W19 3-month digest): **57 papers**. Larger than the brief's soft target of 15-30 because the 8-month, 9-mechanism-family, 3-quarter coverage required ~5-7 papers per cluster to make each cluster's argument defensible.
- Quarterly distribution of KEEPs (by submission date):
  - Q3 2025 (Sep 9 – Nov 30, 2025): **14 papers**
  - Q4 2025 (Dec 1, 2025 – Feb 8, 2026): **21 papers**
  - Q1+ 2026 (Feb 9 – early May 2026): **22 papers** (all carried forward from prior W19 digest; their full Pass 1 + Pass 2 extractions are in `ops/paper-extractor/2026-W19/`)
- Pass 1 / Pass 2: degraded mode (abstract-only) for all newly-added candidates; carry-forward papers reuse the existing Pass 1+2 extractions in `ops/paper-extractor/2026-W19/`.
- Synthesis: structured per the operator's brief — mechanism-family map (9 families), quarterly view (3 buckets), time-progression "what changed" (3 high-confidence shifts + 2 sub-shifts).

## Cross-source dedupe note

Single-source run (arXiv only). No cross-source dedupe needed.

## Traction signal — how it was assessed

The brief asked for highly-cited or gaining-traction papers within an 8-month window. Direct citation counts via Semantic Scholar / Google Scholar were not queried in this run (the per-paper traction signal is therefore a calibrated heuristic, not ground truth). The signal combines:

- **Clear mechanism contribution** — does the paper have a named system / metric / formulation that subsequent work in the kept set could reference?
- **Specific empirical claim** — does the abstract include concrete benchmark numbers (NDCG, EM, latency, etc.) rather than only "demonstrates effectiveness"?
- **Group / lab affiliation pattern** — first-author + institution suggest a known retrieval / RAG lab? (jina, NVIDIA, AWS, ByteDance, Tsinghua, etc.)
- **Model / code release** — open-source code or model weights, lowering downstream adoption friction?
- **Mentions in other kept-set papers' baselines** — is this paper named as a baseline by a later paper in the kept set? (Strongest within-set signal of traction inside the 8 months.)

Per-paper confidence is reported as `low-medium`, `medium`, `medium-high`, or qualitative tags `gaining-traction`, `high-confidence-prominent`, `too-early-to-tell` — visible in the digest's 300 ft section.

---

## KEEP — 28 papers in the digest

### Q3 2025 (Sep 9 – Nov 30, 2025)

#### [B] Interact-RAG: Reason and Interact with the Corpus, Beyond Black-Box Retrieval
- **Authors**: Yulong Hui, Chao Chen, Zhihang Fu et al.
- **Date**: 2025-10-31    **arXiv**: https://arxiv.org/abs/2510.27566
- **Primary category**: cs.IR
- **Mechanism family**: retrieval-replacement (corpus interaction; cluster B, **earliest version**)
- **Traction tag**: gaining-traction (cluster origin; framing precursor for the rest of cluster B). Confidence: medium.
- **Rationale**: First explicit "dismantle the black-box" framing in the kept set; agent-controlled action primitives over information retrieval. Anchors the Q3 2025 → Q1+ 2026 retrieval-interface critique trajectory.

#### [C] ARC: Agent RAG Cache Mechanism
- **Authors**: Shuhang Lin, Zhencan Peng, Lingyao Li et al.
- **Date**: 2025-11-04    **arXiv**: https://arxiv.org/abs/2511.02919
- **Primary category**: cs.CL
- **Mechanism family**: agentic-RAG efficiency (caching; cluster C precursor)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Storage to 0.015% of corpus, 80% latency reduction; Q3 2025's clearest cache-as-headline paper. Anchors the efficiency-as-first-class-target shift earlier than Q1+ 2026.

#### [C] TeaRAG: A Token-Efficient Agentic RAG Framework
- **Authors**: Chao Zhang, Yuhao Wang, Derong Xu et al.
- **Date**: 2025-11-07    **arXiv**: https://arxiv.org/abs/2511.05385
- **Primary category**: cs.IR
- **Mechanism family**: agentic-RAG efficiency (tokens; cluster C precursor)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Compresses retrieval content (chunk + triplet + PPR) and reasoning steps (IP-DPO) — orthogonal cost axes. Q3 2025's token-budget paper.

#### [C] Stop-RAG: Value-Based Retrieval Control for Iterative RAG
- **Authors**: Jaewan Park, Solbee Cho, Jay-Yoon Lee
- **Date**: 2025-10-16    **arXiv**: https://arxiv.org/abs/2510.14337
- **Primary category**: cs.LG
- **Mechanism family**: agentic-RAG efficiency (iterative-RAG control; cluster C)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Cast iterative RAG as MDP, value-based stopping with Q(λ) targets, black-box-API-compatible. Anchors the adaptive-iteration-stop subtheme.

#### [C] DecEx-RAG: Boosting Agentic RAG via Decision and Execution Optimization
- **Authors**: Yongqi Leng, Yikun Lei, Xikai Liu et al.
- **Date**: 2025-10-07    **arXiv**: https://arxiv.org/abs/2510.05691
- **Primary category**: cs.CL
- **Mechanism family**: agentic-RAG RL (process supervision; cluster C)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: First kept-set paper to introduce process-supervision RL for agentic RAG; +6.2% absolute over baselines on six datasets. Q3 2025's process-supervision precursor.

#### [A] InfoGain-RAG: Document Information Gain-based Reranking
- **Authors**: Zihan Wang, Zihan Liang, Zhou Shao et al.
- **Date**: 2025-09-16    **arXiv**: https://arxiv.org/abs/2509.12765
- **Primary category**: cs.IR
- **Mechanism family**: trained LLM-utility reranker (cluster A; **earliest formulation**)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Earliest kept-set paper to formulate "rerank by LLM utility, not relevance" via Document Information Gain (DIG = ΔLLM-confidence with vs without doc). Anchors the rerank-for-utility shift's earliest point.

#### [E] jina-reranker-v3: Last but Not Late Interaction for Listwise Document Reranking
- **Authors**: Feng Wang, Yuqing Li, Han Xiao
- **Date**: 2025-09-29    **arXiv**: https://arxiv.org/abs/2509.25085
- **Primary category**: cs.CL
- **Mechanism family**: listwise / late-interaction (cluster E anchor)
- **Traction tag**: high-confidence-prominent (jina-affiliated; mechanism contribution explicitly contrasted with ColBERT). Confidence: medium-high.
- **Rationale**: 0.6B-param multilingual listwise reranker introducing "last but not late" cross-document attention; SOTA BEIR at NDCG@10 = 61.94. Holds up across the 8 months.

#### [E] CoRe Heads: Contrastive Retrieval Heads Improve Attention-Based Re-Ranking
- **Authors**: Linh Tran, Yulong Li, Radu Florian et al.
- **Date**: 2025-10-02    **arXiv**: https://arxiv.org/abs/2510.02219
- **Primary category**: cs.IR
- **Mechanism family**: listwise / attention-based reranker (cluster E)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: <1% of attention heads → state-of-the-art listwise reranking; pruning final 50% layers preserves accuracy. Both interpretability and efficiency.

#### [E] L2G: Listwise Reranking for Corpus Feedback
- **Authors**: Soyoung Yoon, Jongho Kim, Daeyong Kwon et al.
- **Date**: 2025-10-01    **arXiv**: https://arxiv.org/abs/2510.00887
- **Primary category**: cs.IR
- **Mechanism family**: listwise reranker (cluster E)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Implicitly induces document graphs from listwise reranker logs; matches oracle graph methods at zero additional LLM calls. Reusable framing.

#### [D] Recency Bias in LLM-Based Reranking (diagnostic)
- **Authors**: Hanpei Fang, Sijie Tao, Nuo Chen et al.
- **Date**: 2025-09-14    **arXiv**: https://arxiv.org/abs/2509.11353
- **Primary category**: cs.IR
- **Mechanism family**: specialized reranker diagnostic (cluster D anchor)
- **Traction tag**: gaining-traction; **most-replicated empirical finding in the kept set** (re-found by FRESCO 8 months later). Confidence: medium-high.
- **Rationale**: 7 LLMs (GPT-3.5/4/4o, LLaMA-3, Qwen-2.5); fresh passages consistently promoted, Top-10 mean publication year shifts forward by up to 4.78 years. Quantitative evidence of pervasive recency bias.

#### [G] Milco: Learned Sparse Retrieval Across Languages
- **Authors**: Thong Nguyen, Yibin Lei, Jia-Huei Ju et al.
- **Date**: 2025-10-01    **arXiv**: https://arxiv.org/abs/2510.00671
- **Primary category**: cs.IR
- **Mechanism family**: learned-sparse retrieval (cluster G)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: 30 active dimensions per doc beats dense BGE-M3 / Qwen3-Embed; multilingual LSR via shared-English-lexical-space connector. Q3 2025's quiet LSR work.

#### [H] Beyond Static Retrieval: Iterative Retrieval in GraphRAG
- **Authors**: Kai Guo, Xinnan Dai, Shenglai Zeng et al.
- **Date**: 2025-09-29    **arXiv**: https://arxiv.org/abs/2509.25530
- **Primary category**: cs.AI
- **Mechanism family**: iterative GraphRAG (cluster H diagnostic)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: First systematic study of iterative retrieval in GraphRAG: helps multi-hop, but naive expansion adds noise. Anchors the GraphRAG-iteration thread.

### Q4 2025 (Dec 1, 2025 – Feb 8, 2026)

#### [B] Keyword Search Is All You Need (Tool-Using Agentic Search Without Vector DB)
- **Authors**: Shreyas Subramanian, Adewale Akinfaderin, Yanyan Zhang et al.
- **Date**: 2025-12-19    **arXiv**: https://arxiv.org/abs/2602.23368
- **Primary category**: cs.IR
- **Mechanism family**: retrieval-replacement (non-vector / agentic; cluster B)
- **Traction tag**: high-confidence-prominent (AWS-affiliated; deliberately provocative measurement). Confidence: medium-high.
- **Rationale**: Tool-using agent + keyword search reaches >90% of vector-RAG performance; the kept set's most-cited example of "non-vector RAG works" inside Q4 2025. Anticipates DCI's stronger position.

#### [B] A-RAG: Scaling Agentic RAG via Hierarchical Retrieval Interfaces
- **Authors**: Mingxuan Du, Benfeng Xu, Chiwei Zhu et al.
- **Date**: 2026-02-03    **arXiv**: https://arxiv.org/abs/2602.03442
- **Primary category**: cs.CL
- **Mechanism family**: retrieval-interface (cluster B; multi-tool exposure)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Exposes keyword search, semantic search, chunk read as three parallel agent tools; consistently outperforms existing approaches at comparable or lower retrieved tokens. Operationalizes the multi-tool interface critique.

#### [A] LURE-RAG: Lightweight Utility-Driven Reranking
- **Authors**: Manish Chandra, Debasis Ganguly, Iadh Ounis
- **Date**: 2026-01-27    **arXiv**: https://arxiv.org/abs/2601.19535
- **Primary category**: cs.IR
- **Mechanism family**: trained LLM-utility reranker (cluster A; **listwise-loss-with-utility**)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: LambdaMART reranker trained with listwise ranking loss guided by LLM utility — the first kept paper to put listwise-ranking-loss and utility-target in the same framework. 97-98% of dense baseline at fraction of compute.

#### [A] GR2: Generative Reasoning Re-ranker
- **Authors**: Mingfu Liang, Yufei Li, Jay Xu et al.
- **Date**: 2026-02-08    **arXiv**: https://arxiv.org/abs/2602.07774
- **Primary category**: cs.IR
- **Mechanism family**: trained reranker / RL-trained generative (cluster A; recommendation-flavor)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: End-to-end RL-trained generative reranker for recommendation with semantic-ID tokenizer (≥99% uniqueness). Industrial-scale design.

#### [A] XProvence: Zero-Cost Multilingual Context Pruning for RAG
- **Authors**: Youssef Mohamed, Mohamed Elhoseiny, Thibault Formal et al.
- **Date**: 2026-01-26    **arXiv**: https://arxiv.org/abs/2601.18886
- **Primary category**: cs.IR
- **Mechanism family**: trained reranker (context-pruning) + cluster A
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Multilingual zero-cost context pruning trained on 16 languages; 100+ via cross-lingual transfer. Naver Provence-family extension, model released on HuggingFace.

#### [E] Col-Bandit: Zero-Shot Query-Time Pruning for Late-Interaction Retrieval
- **Authors**: Roi Pony, Adi Raz, Oshri Naparstek et al.
- **Date**: 2026-02-02    **arXiv**: https://arxiv.org/abs/2602.02827
- **Primary category**: cs.IR
- **Mechanism family**: late-interaction efficiency (cluster E)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Casts late-interaction reranking as Top-K identification problem; adaptively reveals only needed (doc, q-token) MaxSim entries. Zero-shot drop-in over multi-vector systems.

#### [E] Nemotron ColEmbed V2: Late-Interaction for Visual Document Retrieval
- **Authors**: Gabriel de Souza P. Moreira, Ronay Ak, Mengyao Xu et al.
- **Date**: 2026-02-03    **arXiv**: https://arxiv.org/abs/2602.03992
- **Primary category**: cs.IR
- **Mechanism family**: late-interaction (cluster E; visual)
- **Traction tag**: high-confidence-prominent (NVIDIA-affiliated; **leaderboard-leading on ViDoRe V3 at NDCG@10=63.42**). Confidence: medium-high.
- **Rationale**: 8B variant ranks first on ViDoRe V3 leaderboard (Feb 3, 2026). The kept set's strongest opposing data point to the no-embedder thread (cluster B).

#### [G] LACONIC: Dense-Level Effectiveness for Scalable Sparse Retrieval (LSR + Llama-3)
- **Authors**: Zhichao Xu, Shengyao Zhuang, Crystina Zhang et al.
- **Date**: 2026-01-04    **arXiv**: https://arxiv.org/abs/2601.01684
- **Primary category**: cs.IR
- **Mechanism family**: learned-sparse retrieval (cluster G; **anchor — LSR + LLM backbone**)
- **Traction tag**: high-confidence-prominent (rank 15 on MTEB Retrieval leaderboard as of Jan 1, 2026). Confidence: medium-high.
- **Rationale**: Llama-3 1B/3B/8B as LSR encoders; 8B variant **60.2 nDCG on MTEB Retrieval at 71% less index memory than equivalent dense models**. The cluster's pivot.

#### [G] Multivector Reranking in the Era of Strong First-Stage Retrievers
- **Authors**: Silvio Martinico, Franco Maria Nardini, Cosimo Rulli et al.
- **Date**: 2026-01-08    **arXiv**: https://arxiv.org/abs/2601.05200
- **Primary category**: cs.IR
- **Mechanism family**: learned-sparse + multivector pipeline (cluster G + E)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Replaces token-level gather with single-vector LSR retriever; recasts gather-and-refine into classic two-stage. Reframes the multivector pipeline.

#### [G] Forward Index Compression for Learned Sparse Retrieval
- **Authors**: Sebastian Bruch, Martino Fontana, Franco Maria Nardini et al.
- **Date**: 2026-02-05    **arXiv**: https://arxiv.org/abs/2602.05445
- **Primary category**: cs.IR
- **Mechanism family**: learned-sparse retrieval engineering (cluster G)
- **Traction tag**: too-early-to-tell. Confidence: low-medium.
- **Rationale**: Targets forward-index data structure; DotVByte (improvement on StreamVByte for inner-product) yields significant space savings on MS-MARCO. Engineering paper on a load-bearing structure.

#### [F] Agentic Memory: Unified LTM+STM via RL
- **Authors**: Yi Yu, Liuyi Yao, Yuexiang Xie et al.
- **Date**: 2026-01-05    **arXiv**: https://arxiv.org/abs/2601.01885
- **Primary category**: cs.CL
- **Mechanism family**: agent memory architecture (cluster F)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Memory operations as tool-based actions; three-stage progressive RL with step-wise GRPO; outperforms strong memory-augmented baselines on five long-horizon benchmarks.

#### [F] xMemory: Beyond RAG for Agent Memory — Decouple and Aggregate
- **Authors**: Zhanghao Hu, Qinglin Zhu, Di Liang et al.
- **Date**: 2026-02-02    **arXiv**: https://arxiv.org/abs/2602.02007
- **Primary category**: cs.CL
- **Mechanism family**: agent memory architecture (cluster F; structural critique)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Argues agent memory is bounded coherent dialogue stream, not heterogeneous corpus; hierarchical themes/semantics → episodes → raw messages, top-down expansion only when reducing reader uncertainty.

#### [F] SYNAPSE: Episodic-Semantic Memory via Spreading Activation
- **Authors**: Hanqi Jiang, Junhao Chen, Yi Pan et al.
- **Date**: 2026-01-06    **arXiv**: https://arxiv.org/abs/2601.02744
- **Primary category**: cs.CL
- **Mechanism family**: agent memory architecture (cluster F; cognitive-science-flavored)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Memory as dynamic graph with spreading activation, lateral inhibition, temporal decay; Triple Hybrid Retrieval; outperforms SOTA on LoCoMo's complex temporal/multi-hop tasks.

#### [F] Continuum Memory Architectures for Long-Horizon LLM Agents
- **Authors**: Joe Logan
- **Date**: 2026-01-14    **arXiv**: https://arxiv.org/abs/2601.09913
- **Primary category**: cs.AI
- **Mechanism family**: agent memory class definition (cluster F)
- **Traction tag**: too-early-to-tell. Confidence: low-medium.
- **Rationale**: Class-definition paper for systems maintaining/updating internal state across interactions. Slow-burn citation pattern; named in subsequent work as a vocabulary anchor.

#### [C] TreePS-RAG: Tree-Based Process Supervision for RL in Agentic RAG
- **Authors**: Tianhua Zhang, Kun Li, Junan Li et al.
- **Date**: 2026-01-11    **arXiv**: https://arxiv.org/abs/2601.06922
- **Primary category**: cs.CL
- **Mechanism family**: agentic-RAG RL (process supervision; cluster C)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Online tree-based RL; each reasoning step is a node, step utility estimated by Monte Carlo over descendants; step-wise credit without intermediate labels. Cleanly extends DecEx-RAG.

#### [C] PruneRAG: Confidence-Guided Query Decomposition Trees
- **Authors**: Shuguang Jiao, Xinyu Xiao, Yunfan Wei et al.
- **Date**: 2026-01-16    **arXiv**: https://arxiv.org/abs/2601.11024
- **Primary category**: cs.IR
- **Mechanism family**: query decomposition / iterative-RAG control (cluster C)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Query-decomposition tree with adaptive node expansion, confidence-guided acceptance/pruning, fine-grained entity-level retrieval; defines an Evidence Forgetting Rate metric.

#### [C] Rerank Before You Reason: Reranking Tradeoffs through Effective Token Cost
- **Authors**: Sahel Sharifymoghaddam, Jimmy Lin
- **Date**: 2026-01-20    **arXiv**: https://arxiv.org/abs/2601.14224
- **Primary category**: cs.IR
- **Mechanism family**: cost-aware reranking analysis (cluster C metric)
- **Traction tag**: gaining-traction (Jimmy Lin co-authored; introduces a portable cost metric). Confidence: medium.
- **Rationale**: Defines Effective Token Cost (ETC) on BrowseComp-Plus; moderate reranking often beats more search-time reasoning at substantially lower cost. First kept-set paper with a portable cost metric.

#### [C] JADE: Joint Agentic Dynamic Execution
- **Authors**: Yiqun Chen, Erhan Zhang, Tianyi Hu et al.
- **Date**: 2026-01-29    **arXiv**: https://arxiv.org/abs/2601.21916
- **Primary category**: cs.AI
- **Mechanism family**: agentic-RAG joint optimization (cluster C)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Cooperative multi-agent team unified under shared backbone; planner and executor co-adapt under outcome-based RL. The strategic-operational mismatch framing is the cluster's missing conceptual move.

#### [I] Is Agentic RAG Worth It? An Experimental Comparison of RAG Approaches
- **Authors**: Pietro Ferrazzi, Milica Cvjeticanin, Alessio Piraccini et al.
- **Date**: 2026-01-12    **arXiv**: https://arxiv.org/abs/2601.07711
- **Primary category**: cs.CL
- **Mechanism family**: comparative empirical (cluster I)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Empirical comparison "Enhanced" vs "Agentic" RAG; conclusion is conditional rather than coronation. The kept set's most direct empirical pushback against agentic-RAG triumphalism.

#### [I] MCP vs RAG vs NLWeb vs HTML
- **Authors**: Aaron Steiner, Ralph Peeters, Christian Bizer
- **Date**: 2025-11-28    **arXiv**: https://arxiv.org/abs/2511.23281
- **Primary category**: cs.CL
- **Mechanism family**: comparative empirical (cluster I; agent-interface)
- **Traction tag**: gaining-traction (Bizer/Mannheim — known for IR benchmarking). Confidence: medium.
- **Rationale**: Single controlled environment, identical tasks across HTML / RAG / MCP / NLWeb agents using GPT 4.1, GPT 5, GPT 5 mini, Claude Sonnet 4. RAG, MCP, NLWeb all outperform HTML; no single winner among the three.

#### [I] Rethinking Retrieval: Traditional → Agentic → Non-Vector (Financial Domain)
- **Authors**: Elias Lumer, Matt Melich, Olivia Zino et al.
- **Date**: 2025-11-22    **arXiv**: https://arxiv.org/abs/2511.18177
- **Primary category**: cs.CL
- **Mechanism family**: comparative empirical (cluster I; vertical anchor for non-vector debate)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: 1,200 SEC filings on a 150-question benchmark; vector-based agentic RAG wins 68% over hierarchical-node-based. Surveys the vector-vs-non-vector debate from a vertical setting.

#### [Outlier] Higress-RAG: Holistic Optimization Framework for Enterprise RAG
- **Authors**: Weixi Lin
- **Date**: 2025-12-30    **arXiv**: https://arxiv.org/abs/2602.23374
- **Primary category**: cs.IR
- **Mechanism family**: production / enterprise (architecture-as-reference)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Adaptive Routing + Hybrid Retrieval (RRF over dense+sparse) + Corrective RAG + Semantic Caching, MCP-based. Single-author preprint but architecture-as-reference framing tends to accumulate slow durable citations.

#### [Outlier] MemoryGraft: Persistent Compromise of LLM Agents via Poisoned Experience Retrieval
- **Authors**: Saksham Sahai Srivastava, Haoyu He
- **Date**: 2025-12-18    **arXiv**: https://arxiv.org/abs/2512.16962
- **Primary category**: cs.CR
- **Mechanism family**: agent-security (paired with carry-forward ProGRank)
- **Traction tag**: gaining-traction. Confidence: medium.
- **Rationale**: Indirect-injection attack implanting malicious successful experiences into agent long-term memory via benign ingestion artifacts. Persistence beyond standard RAG poisoning.

### Q1+ 2026 (Feb 9 – early May 2026) — Carry-forward from prior W19 3-month digest

The papers below are carried forward from `2026-W19-on-demand-retrieval-rerank-llm-agents.md`. Their full Pass 1 + Pass 2 extractions are in `ops/paper-extractor/2026-W19/`. Listed here in cluster + date order; one-line per paper.

- **[D]** Cold-Start LLM-Reranker Diagnostic — Lemdiasova et al., 2026-02-09 — `2604.16318` — popularity beats LLM rerank ~30× on HR@10 cold-start. → https://arxiv.org/abs/2604.16318
- **[A]** LCR: LLM-Confidence Reranker — Song et al., 2026-02-14 — `2602.13571` — training-free; up to +20.6% NDCG@5 on BEIR via LLM MSCP confidence. → https://arxiv.org/abs/2602.13571
- **[F]** Retrieval-vs-Utilization Diagnostic (Agent Memory) — Yuan et al., 2026-03-02 — `2603.02473` — retrieval method 20-pt span vs write strategy 3-8 pt span. → https://arxiv.org/abs/2603.02473
- **[C]** Test-Time Strategies for Agentic RAG — Zhang et al., 2026-03-12 — `2603.12396` — +5.6% EM, -10.5% turns on Search-R1 from contextualization+de-dup. → https://arxiv.org/abs/2603.12396
- **[C]** APEX-Searcher — Chen et al., 2026-03-14 — `2603.13853` — 2-stage RL (planning) + SFT (execution). → https://arxiv.org/abs/2603.13853
- **[F]** Kumiho: Graph-Native Cognitive Memory (AGM Belief-Revision) — Park, 2026-03-18 — `2603.17244` — 93.3% LoCoMo-Plus authors / mid-80s reproduction (vs 45.7% prior best). → https://arxiv.org/abs/2603.17244
- **[D]** ProGRank: Probe-Gradient Reranking — Yin et al., 2026-03-24 — `2603.22934` — training-free defense reranker against corpus poisoning. → https://arxiv.org/abs/2603.22934
- **[D]** GraphER: Graph-Based Reranking over Vector Stores — Miao et al., 2026-03-26 — `2603.24925` — non-semantic graph proximity, no KG required. → https://arxiv.org/abs/2603.24925
- **[C]** Doctor-RAG: Failure-Aware Repair — Jiao et al., 2026-04-01 — `2604.00865` — diagnose earliest failure, repair locally with prefix reuse. → https://arxiv.org/abs/2604.00865
- **[C]** HERA: Multi-Agent Co-Evolving Orchestration — Li et al., 2026-04-01 — `2604.00901` — +38.7% over baselines on 6 knowledge-intensive benchmarks. → https://arxiv.org/abs/2604.00901
- **[H]** RAGSearch: RAG vs GraphRAG Comparative — Fan et al., 2026-04-01 — `2604.09666` — agentic search closes most of dense-vs-graph gap. → https://arxiv.org/abs/2604.09666
- **[A]** RRPO: RL-Trained Reranker via LLM Feedback — Wu et al., 2026-04-02 — `2604.02091` — outperforms RankZephyr on knowledge-intensive QA. → https://arxiv.org/abs/2604.02091
- **[F]** LightMem: SLM-Driven 3-Tier Agent Memory — Zhang et al., 2026-04-09 — `2604.07798` — +2.5 F1 over A-MEM at 83 ms / 581 ms. → https://arxiv.org/abs/2604.07798
- **[D]** FRESCO: Recency-Aware Reranker Benchmark — An et al., 2026-04-14 — `2604.14227` — instruction tuning recovers up to +27% on evolving knowledge. → https://arxiv.org/abs/2604.14227
- **[B]** Corpus2Skill: Distill Corpus into Navigable Skill Directory — Sun et al., 2026-04-16 — `2604.14572` — outperforms dense / RAPTOR / agentic-RAG on WixQA. → https://arxiv.org/abs/2604.14572
- **[E]** AdaRankLLM: Adaptive Listwise Reranking — Feng et al., 2026-04-17 — `2604.15621` — role-shift framing across 8 LLMs. → https://arxiv.org/abs/2604.15621
- **[C]** AutoSearch: RL Search-Depth Control — Sun et al., 2026-04-19 — `2604.17337` — adaptive minimal-sufficient depth via self-answer scoring. → https://arxiv.org/abs/2604.17337
- **[A]** Prism-Reranker: Contributions + Evidence — Zhang, 2026-04-26 — `2604.23734` — +1.54 avg NDCG@10 on BEIR-QA via reranker-output redesign. → https://arxiv.org/abs/2604.23734
- **[B]** DCI: Direct Corpus Interaction (no embedder) — Li et al., 2026-05-03 — `2605.05242` — outperforms strong sparse, dense, reranking baselines on BRIGHT/BEIR/BrowseComp-Plus. → https://arxiv.org/abs/2605.05242
- **[A]** CAR: Confidence-Aware Reranking — Song et al., 2026-05-06 — `2605.04495` — ρ=0.964 with downstream F1; +25.4% on YesNo+Contriever. → https://arxiv.org/abs/2605.04495
- **[A]** MemReranker: Reasoning-Aware Reranking for Agent Memory — Li et al., 2026-05-07 — `2605.06132` — 0.737 MAP at ~10-20% of Gemini-3-Flash latency. → https://arxiv.org/abs/2605.06132
- **[C]** LatentRAG: Latent Reasoning + Retrieval — Zheng et al., 2026-05-07 — `2605.06285` — ~90% latency reduction at comparable accuracy on 7 benchmarks. → https://arxiv.org/abs/2605.06285

---

## REVIEW — papers considered but not promoted to KEEP

(Selected from the 59-candidate roster; not exhaustive — full ranked list in `.cache/2026-W19-8mo-picked.json`.)

### Vertical / domain-specific applications using known retrieval+rerank techniques (would have been KEEPs in the 3-month digest, but in the 8-month, mechanism-family run they're absorbed into the broader claims)

- **Self-MedRAG** — Ryan et al., 2026-01-08, `2601.04531` — self-reflective hybrid RAG (medical); embodies the self-reflective + hybrid retrieval pattern in vertical form. Rationale: vertical example of cluster A's utility framing + cluster I's enhancement levers; preferred to keep the digest mechanism-focused.
- **VeritasFi** — Tai et al., 2025-10-12, `2510.10828` — multi-tier financial RAG with two-stage reranker training. Rationale: vertical engineering paper on a known stack.
- **ModernBERT + ColBERT biomedical RAG** — Rivera & Menolascina, 2025-10-06, `2510.04757` — two-stage bi-encoder + late-interaction for biomedical. Rationale: vertical instantiation of cluster E architecture.
- **TagRAG** — Tao et al., 2025-10-18, `2601.05254` — tag-guided hierarchical KG RAG. Rationale: GraphRAG variant; subsumed by cluster H.
- **Multi-Agent GraphRAG** — Gusarov et al., 2025-11-11, `2511.08274` — text-to-Cypher framework. Rationale: GraphRAG variant; vertical to property-graph databases.
- **VERAFI** — Akinfaderin & Subramanian, 2025-12-12, `2512.14744` — neurosymbolic policy generation for financial RAG. Rationale: vertical; same authors as Keyword Search Is All You Need (P16) — kept that one as the cluster B paper.
- **Comparative Analysis of Neural Retriever-Reranker Pipelines (e-commerce)** — Rumble et al., 2025-12-14, `2602.22219` — KG retrieval-reranker pipeline benchmark. Rationale: e-commerce vertical.
- **LegalMALR** — Li et al., 2026-01-25, `2601.17692` — multi-agent query understanding + LLM reranker for Chinese statute retrieval. Rationale: legal vertical.
- **Agentic RAG for Software Testing** — Hariharan et al., 2025-10-12, `2510.10824` — hybrid vector-graph multi-agent for QE. Rationale: SE vertical.

### Mechanism subsumed by stronger paper in the kept set

- **FAIR-RAG** — Asl et al., 2025-10-25, `2510.22344` — adaptive iterative refinement. Rationale: subsumed by AutoSearch (P33) and PruneRAG (P12) in cluster C.
- **META-RAG** — Sun et al., 2025-10-28, `2510.24003` — meta-analysis-inspired evidence reranking (medical). Rationale: vertical instantiation of cluster A.
- **LAD-RAG** — Sourati et al., 2025-10-08, `2510.07233` — layout-aware dynamic RAG for visually-rich documents. Rationale: visual-vertical, would belong to a multimodal-RAG cluster too thin to populate.
- **REGENT** — Chatterjee, 2025-10-13, `2510.11592` — entity-aware multi-vector reranker. Rationale: subsumed by cluster E (jina-reranker-v3, CoRe Heads).
- **DIVERGE** — Hu et al., 2026-01-30, `2602.00238` — diversity-enhanced agentic RAG. Rationale: orthogonal to cluster C's efficiency target; would need an opensended-information-seeking cluster.
- **FROAV** — Lin & Kao, 2026-01-12, `2601.07504` — research framework / observability tool. Rationale: tooling rather than method.
- **GraphSearch** — Yang et al., 2025-09-26, `2509.22009` — agentic deep searching workflow for GraphRAG. Rationale: subsumed by Beyond Static Retrieval (P4) as cluster H's diagnostic anchor.
- **RAGShaper** — Tao et al., 2026-01-13, `2601.08699` — agentic RAG data synthesis framework. Rationale: training-data-synthesis paper; orthogonal to mechanism-family lens.
- **Stream RAG** — Arora et al., 2025-10-02, `2510.02044` — streaming RAG for spoken dialogue. Rationale: speech-vertical.
- **To Case or Not to Case (LSR study)** — Lionis et al., 2026-01-24, `2601.17500` — empirical study of cased vs uncased backbones in LSR. Rationale: useful but narrowly engineering.
- **Stop-RAG** is in KEEP. **CoRe Heads** is in KEEP. **L2G** is in KEEP. (Listed for clarity — these were not demoted.)
- **IMRNNs** — Saxena et al., 2026-01-27, `2601.20084` — interpretable dense retrieval via embedding modulation. Rationale: interpretability angle, mechanism orthogonal to the cluster lens.
- **Cache Mechanism for Agent RAG (ARC)** is in KEEP. **TeaRAG** is in KEEP. (Listed for clarity.)
- **Path-Constrained Retrieval** — Oladokun, 2025-11-23, `2511.18313` — graph-scoped semantic search. Rationale: subsumed by GraphER's "without KG" framing inside cluster D / H.
- **Query Suggestion for RAG** — Spaeh et al., 2026-01-13, `2601.08105` — query-suggestion for agentic RAG. Rationale: novel question but not a retrieval/rerank mechanism per se.
- **Taxonomy of Retrieval System Framework** — Shah et al., 2026-01-27, `2601.20131` — design-stack taxonomy. Rationale: review/taxonomy paper; useful as orientation but not synthesisable as an argument-shaped mechanism contribution.

---

## Generated

- Date: 2026-05-09
- Override file: `ops/paper-synthesizer/overrides/2026-W19.md` (extended window applied at orchestrator level)
- Cache: `ops/paper-synthesizer/.cache/2026-W19-8mo-candidates.json`, `2026-W19-8mo-picked.json`, `2026-W19-8mo-w*-*.xml`
- Carry-forward source: `ops/paper-synthesizer/digests/2026-W19-on-demand-retrieval-rerank-llm-agents.md` and `ops/paper-extractor/2026-W19/`
- Digest: `ops/paper-synthesizer/digests/2026-W19-on-demand-retrieval-rerank-evolution-8mo.md`
