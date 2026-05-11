# 2026-W19 6-Month Trajectory Run -- Full Paper List

**Operator theme:** Latest retrieval and re-ranking techniques for LLM agents -- 6-month trajectory for a practitioner audience.
**Window:** 2025-11-10 to 2026-05-10 (6 months).
**Source:** arXiv (cs.CL, cs.IR, cs.LG, cs.AI). PubMed / bioRxiv / medRxiv: empty as expected (CS-heavy theme).
**Run override:** `ops/paper-synthesizer/overrides/2026-W19-6mo-trajectory.md`
**Style override:** `ops/paper-synthesizer/overrides/2026-W19-6mo-trajectory-style.md`
**Companion digest:** `ops/paper-synthesizer/digests/2026-W19-on-demand-retrieval-rerank-llm-agents-6mo-trajectory.md`
**Generated:** 2026-05-10

---

## Pipeline summary

- **Candidate pool**: 87 papers (50 from prior W19 extractions covering 2026-02-09 to 2026-05-07; 37 from prior W19 8-month curated cache covering 2025-11-10 to 2026-02-08; all matched at least one of the 8 operator-approved expanded queries).
- **Lanes (literature-scan-coach instances)**: 8 (one per approved query). Lanes ran conceptually in parallel; cross-lane dedup (DOI / normalized title) consolidated to the 87-paper pool.
- **Relevance filter**: orchestrator-direct, three-axis scoring (match strength x criteria fit x novelty) plus the operator's impact axis (citation-weighted lenient on recency, cutoff at early April 2026). Vertical-application penalty applied for papers not teaching a generalizable retrieval/reranker technique.
- **KEEP**: 36 papers (chosen for trajectory coverage and practitioner relevance -- slightly above the standard 25-paper soft cap because the operator's brief asks for ~5 distinct phases each carrying its own argument, and a reasonable phase needs 3-10 papers to hold).
- **DROP / REVIEW**: 42 papers (mostly demoted-for-cap; reasons logged).
- **Pass 1 / Pass 2 status**: 16/36 kept papers have full Pass 1 + Pass 2 extractions on disk (from prior W19 run); the remaining 20/36 ran in **degraded mode** (abstract-only synthesis from the cached 8-month curated set). Per-paper Mode A summaries reflect the abstract-only confidence.
- **Mode A**: 36 per-paper reader-facing summaries written to `ops/paper-synthesizer/2026-W19-6mo/per-paper/`.
- **Mode B**: one trajectory-shaped digest at `ops/paper-synthesizer/digests/2026-W19-on-demand-retrieval-rerank-llm-agents-6mo-trajectory.md`.

## Cross-source dedupe note

Single-source run (arXiv only, by design -- operator's theme is CS-heavy and PubMed / bioRxiv / medRxiv are expected near-zero for this topic). Cross-lane dedup (within arXiv across the 8 expanded queries) was applied via the prior W19 pool, which had already deduped the underlying arXiv records.

## Traction signal -- how it was assessed

The brief asked for citation-weighted assessment lenient on recency, with cutoff at ~April 2026. Direct citation counts within a 6-month preprint window are not reliably observable; the per-paper traction signal is therefore a calibrated heuristic that combines:

- **Pre-cutoff (2025-11-10 to 2026-03-31)**: prior-curation status (pre-selected by the 8-month run signals that the synthesizer judged it worth surfacing); benchmark coverage with concrete numbers; named-lab signal in author list (jina, NVIDIA, AWS, ByteDance, Tsinghua, Italian IR group, etc.); presence of the paper as a baseline cited by later papers in the kept set.
- **Post-cutoff (2026-04-01 to 2026-05-10)**: clear technique contribution; named system; concrete benchmark numbers; model/code release; evaluation against multiple recognized benchmarks (BEIR, MTEB, BRIGHT, BrowseComp-Plus); known-lab affiliation pattern.

Per-paper confidence is reported as `low`, `medium`, `medium-high`, or `high` in the per-paper Mode A summaries -- visible in the digest's per-paper bullets.

---

## KEEP -- 36 papers in the digest

### Phase 1: Mid-Nov 2025 (2025-11-10 to 2025-11-30)

- **Rethinking Retrieval: From Traditional Retrieval Augmented Generation to Agentic and Non-Vector Reasoning Systems in the Financial Domain for Large Language Models** -- Elias Lumer et al., arXiv, 2025-11-22.
  Score: 114.7. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2511.18177](https://arxiv.org/abs/2511.18177)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2511-18177.md`

- **Path-Constrained Retrieval: A Structural Approach to Reliable LLM Agent Reasoning Through Graph-Scoped Semantic Search** -- Joseph Oladokun, arXiv, 2025-11-23.
  Score: 89.5. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2511.18313](https://arxiv.org/abs/2511.18313)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2511-18313.md`

- **MCP vs RAG vs NLWeb vs HTML: A Comparison of the Effectiveness and Efficiency of Different Agent Interfaces to the Web (Technical Report)** -- Aaron Steiner, Ralph Peeters, Christian Bizer, arXiv, 2025-11-28.
  Score: 105.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2511.23281](https://arxiv.org/abs/2511.23281)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2511-23281.md`

### Phase 2: Dec 2025 to Jan 2026 (2025-12-01 to 2026-01-31)

- **Comparative Analysis of Neural Retriever-Reranker Pipelines for Retrieval-Augmented Generation over Knowledge Graphs in E-commerce Applications** -- Teri Rumble et al., arXiv, 2025-12-14.
  Score: 110.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2602.22219](https://arxiv.org/abs/2602.22219)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2602-22219.md`

- **Keyword search is all you need: Achieving RAG-Level Performance without vector databases using agentic tool use** -- Shreyas Subramanian et al., arXiv, 2025-12-19.
  Score: 98.5. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2602.23368](https://arxiv.org/abs/2602.23368)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2602-23368.md`

- **Higress-RAG: A Holistic Optimization Framework for Enterprise Retrieval-Augmented Generation via Dual Hybrid Retrieval, Adaptive Routing, and CRAG** -- Weixi Lin, arXiv, 2025-12-30.
  Score: 78.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2602.23374](https://arxiv.org/abs/2602.23374)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2602-23374.md`

- **LACONIC: Dense-Level Effectiveness for Scalable Sparse Retrieval via a Two-Phase Training Curriculum** -- Zhichao Xu et al., arXiv, 2026-01-04.
  Score: 108.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.01684](https://arxiv.org/abs/2601.01684)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-01684.md`

- **Self-MedRAG: a Self-Reflective Hybrid Retrieval-Augmented Generation Framework for Reliable Medical Question Answering** -- Jessica Ryan et al., arXiv, 2026-01-08.
  Score: 84.7. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.04531](https://arxiv.org/abs/2601.04531)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-04531.md`

- **Multivector Reranking in the Era of Strong First-Stage Retrievers** -- Silvio Martinico et al., arXiv, 2026-01-08.
  Score: 118.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.05200](https://arxiv.org/abs/2601.05200)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-05200.md`

- **TreePS-RAG: Tree-based Process Supervision for Reinforcement Learning in Agentic RAG** -- Tianhua Zhang et al., arXiv, 2026-01-11.
  Score: 105.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.06922](https://arxiv.org/abs/2601.06922)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-06922.md`

- **Is Agentic RAG worth it? An experimental comparison of RAG approaches** -- Pietro Ferrazzi et al., arXiv, 2026-01-12.
  Score: 98.5. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.07711](https://arxiv.org/abs/2601.07711)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-07711.md`

- **PruneRAG: Confidence-Guided Query Decomposition Trees for Efficient Retrieval-Augmented Generation** -- Shuguang Jiao et al., arXiv, 2026-01-16.
  Score: 105.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.11024](https://arxiv.org/abs/2601.11024)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-11024.md`

- **Rerank Before You Reason: Analyzing Reranking Tradeoffs through Effective Token Cost in Deep Search Agents** -- Sahel Sharifymoghaddam, Jimmy Lin, arXiv, 2026-01-20.
  Score: 94.5. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.14224](https://arxiv.org/abs/2601.14224)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-14224.md`

- **XProvence: Zero-Cost Multilingual Context Pruning for Retrieval-Augmented Generation** -- Youssef Mohamed et al., arXiv, 2026-01-26.
  Score: 105.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.18886](https://arxiv.org/abs/2601.18886)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-18886.md`

- **IMRNNs: An Efficient Method for Interpretable Dense Retrieval via Embedding Modulation** -- Yash Saxena et al., arXiv, 2026-01-27.
  Score: 112.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.20084](https://arxiv.org/abs/2601.20084)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-20084.md`

- **Taxonomy of the Retrieval System Framework: Pitfalls and Paradigms** -- Deep Shah, Sanket Badhe, Nehal Kathrotia, arXiv, 2026-01-27.
  Score: 118.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2601.20131](https://arxiv.org/abs/2601.20131)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2601-20131.md`

### Phase 3: Feb 2026 (2026-02-01 to 2026-02-28)

- **Col-Bandit: Zero-Shot Query-Time Pruning for Late-Interaction Retrieval** -- Roi Pony et al., arXiv, 2026-02-02.
  Score: 67.5. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2602.02827](https://arxiv.org/abs/2602.02827)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2602-02827.md`

- **A-RAG: Scaling Agentic Retrieval-Augmented Generation via Hierarchical Retrieval Interfaces** -- Mingxuan Du et al., arXiv, 2026-02-03.
  Score: 105.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2602.03442](https://arxiv.org/abs/2602.03442)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2602-03442.md`

- **Forward Index Compression for Learned Sparse Retrieval** -- Sebastian Bruch et al., arXiv, 2026-02-05.
  Score: 118.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2602.05445](https://arxiv.org/abs/2602.05445)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2602-05445.md`

- **Generative Reasoning Re-ranker** -- Mingfu Liang et al., arXiv, 2026-02-08.
  Score: 118.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2602.07774](https://arxiv.org/abs/2602.07774)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2602-07774.md`

- **Diagnosing LLM-based Rerankers in Cold-Start Recommender Systems: Coverage, Exposure and Practical Mitigations** -- Ekaterina Lemdiasova et al., arXiv, 2026-02-09.
  Score: 54.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2604.16318](https://arxiv.org/abs/2604.16318)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2604-16318.md`

- **LLM-Confidence Reranker: A Training-Free Approach for Enhancing Retrieval-Augmented Generation Systems** -- Zhipeng Song et al., arXiv, 2026-02-14.
  Score: 108.7. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2602.13571](https://arxiv.org/abs/2602.13571)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2602-13571.md`

### Phase 4: March to mid-April 2026 (2026-03-01 to 2026-04-19)

- **Quantifying the Accuracy and Cost Impact of Design Decisions in Budget-Constrained Agentic LLM Search** -- Kyle McCleary et al., arXiv, 2026-03-09.
  Score: 101.5. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2603.08877](https://arxiv.org/abs/2603.08877)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2603-08877.md`

- **Test-Time Strategies for More Efficient and Accurate Agentic RAG** -- Brian Zhang et al., arXiv, 2026-03-12.
  Score: 99.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2603.12396](https://arxiv.org/abs/2603.12396)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2603-12396.md`

- **Doctor-RAG: Failure-Aware Repair for Agentic Retrieval-Augmented Generation** -- Shuguang Jiao et al., arXiv, 2026-04-01.
  Score: 72.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2604.00865](https://arxiv.org/abs/2604.00865)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2604-00865.md`

- **Do We Still Need GraphRAG? Benchmarking RAG and GraphRAG for Agentic Search Systems** -- Dongzhe Fan et al., arXiv, 2026-04-01.
  Score: 109.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2604.09666](https://arxiv.org/abs/2604.09666)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2604-09666.md`

- **Optimizing RAG Rerankers with LLM Feedback via Reinforcement Learning** -- Yuhang Wu et al., arXiv, 2026-04-02.
  Score: 101.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2604.02091](https://arxiv.org/abs/2604.02091)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2604-02091.md`

- **FRESCO: Benchmarking and Optimizing Re-rankers for Evolving Semantic Conflict in Retrieval-Augmented Generation** -- Sohyun An et al., arXiv, 2026-04-14.
  Score: 97.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2604.14227](https://arxiv.org/abs/2604.14227)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2604-14227.md`

- **Don't Retrieve, Navigate: Distilling Enterprise Knowledge into Navigable Agent Skills for QA and RAG** -- Yiqun Sun et al., arXiv, 2026-04-16.
  Score: 105.7. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2604.14572](https://arxiv.org/abs/2604.14572)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2604-14572.md`

- **Rethinking the Necessity of Adaptive Retrieval-Augmented Generation through the Lens of Adaptive Listwise Ranking** -- Jun Feng et al., arXiv, 2026-04-17.
  Score: 95.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2604.15621](https://arxiv.org/abs/2604.15621)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2604-15621.md`

- **AutoSearch: Adaptive Search Depth for Efficient Agentic RAG via Reinforcement Learning** -- Jingbo Sun et al., arXiv, 2026-04-19.
  Score: 97.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2604.17337](https://arxiv.org/abs/2604.17337)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2604-17337.md`

### Phase 5: Mid-April to May 2026 (2026-04-20 to 2026-05-10)

- **Prism-Reranker: Beyond Relevance Scoring -- Jointly Producing Contributions and Evidence for Agentic Retrieval** -- Dun Zhang, arXiv, 2026-04-26.
  Score: 88.2. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2604.23734](https://arxiv.org/abs/2604.23734)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2604-23734.md`

- **Beyond Semantic Similarity: Rethinking Retrieval for Agentic Search via Direct Corpus Interaction** -- Zhuofeng Li et al., arXiv, 2026-05-03.
  Score: 104.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2605.05242](https://arxiv.org/abs/2605.05242)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2605-05242.md`

- **CAR: Query-Guided Confidence-Aware Reranking for Retrieval-Augmented Generation** -- Zhipeng Song et al., arXiv, 2026-05-06.
  Score: 100.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2605.04495](https://arxiv.org/abs/2605.04495)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2605-04495.md`

- **MemReranker: Reasoning-Aware Reranking for Agent Memory Retrieval** -- Chunyu Li et al., arXiv, 2026-05-07.
  Score: 59.5. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2605.06132](https://arxiv.org/abs/2605.06132)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2605-06132.md`

- **LatentRAG: Latent Reasoning and Retrieval for Efficient Agentic RAG** -- Yijia Zheng et al., arXiv, 2026-05-07.
  Score: 109.0. Cluster hint: ``.
  Link: [https://arxiv.org/abs/2605.06285](https://arxiv.org/abs/2605.06285)
  Per-paper Mode A: `ops/paper-synthesizer/2026-W19-6mo/per-paper/arxiv-2605-06285.md`

---

## DROP / REVIEW -- 42 papers (with rationale)

These papers are in the candidate pool and matched at least one of the operator's 8 expanded queries, but were not selected for the digest. Each row lists the rationale.

### demoted-for-cap (20 papers)

- **Explainable Innovation Engine: Dual-Tree Agent-RAG with Methods-as-Nodes and Verifiable Write-Back** -- Renwei Meng, 2026-03-10, score=99.2.
  Link: [https://arxiv.org/abs/2603.09192](https://arxiv.org/abs/2603.09192)

- **LURE-RAG: Lightweight Utility-driven Reranking for Efficient RAG** -- Manish Chandra, Debasis Ganguly, Iadh Ounis, 2026-01-27, score=98.5.
  Link: [https://arxiv.org/abs/2601.19535](https://arxiv.org/abs/2601.19535)

- **ProGRank: Probe-Gradient Reranking to Defend Dense-Retriever RAG from Corpus Poisoning** -- Xiangyu Yin et al., 2026-03-24, score=92.5.
  Link: [https://arxiv.org/abs/2603.22934](https://arxiv.org/abs/2603.22934)

- **AgentGL: Towards Agentic Graph Learning with LLMs via Reinforcement Learning** -- Yuanfu Sun et al., 2026-04-07, score=89.5.
  Link: [https://arxiv.org/abs/2604.05846](https://arxiv.org/abs/2604.05846)

- **MemoryGraft: Persistent Compromise of LLM Agents via Poisoned Experience Retrieval** -- Saksham Sahai Srivastava, Haoyu He, 2025-12-18, score=89.5.
  Link: [https://arxiv.org/abs/2512.16962](https://arxiv.org/abs/2512.16962)

- **APEX-Searcher: Augmenting LLMs' Search Capabilities through Agentic Planning and Execution** -- Kun Chen et al., 2026-03-14, score=83.5.
  Link: [https://arxiv.org/abs/2603.13853](https://arxiv.org/abs/2603.13853)

- **LegalMALR:Multi-Agent Query Understanding and LLM-Based Reranking for Chinese Statute Retrieval** -- Yunhan Li et al., 2026-01-25, score=82.5.
  Link: [https://arxiv.org/abs/2601.17692](https://arxiv.org/abs/2601.17692)

- **VERAFI: Verified Agentic Financial Intelligence through Neurosymbolic Policy Generation** -- Adewale Akinfaderin, Shreyas Subramanian, 2025-12-12, score=82.5.
  Link: [https://arxiv.org/abs/2512.14744](https://arxiv.org/abs/2512.14744)

- **Query Suggestion for Retrieval-Augmented Generation via Dynamic In-Context Learning** -- Fabian Spaeh et al., 2026-01-13, score=80.2.
  Link: [https://arxiv.org/abs/2601.08105](https://arxiv.org/abs/2601.08105)

- **FROAV: A Framework for RAG Observation and Agent Verification -- Lowering the Barrier to LLM Agent Research** -- Tzu-Hsuan Lin, Chih-Hsuan Kao, 2026-01-12, score=80.2.
  Link: [https://arxiv.org/abs/2601.07504](https://arxiv.org/abs/2601.07504)

- **GraphRAG for Engineering Diagrams: ChatP&ID Enables LLM Interaction with P&IDs** -- Achmad Anggawirya Alimin et al., 2026-03-23, score=78.7.
  Link: [https://arxiv.org/abs/2603.22528](https://arxiv.org/abs/2603.22528)

- **A Reference Architecture for Agentic Hybrid Retrieval in Dataset Search** -- Riccardo Terrenzi et al., 2026-03-28, score=78.7.
  Link: [https://arxiv.org/abs/2604.16394](https://arxiv.org/abs/2604.16394)

- **Beyond RAG for Agent Memory: Retrieval by Decoupling and Aggregation** -- Zhanghao Hu et al., 2026-02-02, score=78.2.
  Link: [https://arxiv.org/abs/2602.02007](https://arxiv.org/abs/2602.02007)

- **Agentic Retrieval-Augmented Generation for Financial Document Question Answering** -- Yang Shu et al., 2026-05-06, score=76.2.
  Link: [https://arxiv.org/abs/2605.05409](https://arxiv.org/abs/2605.05409)

- **SYNAPSE: Empowering LLM Agents with Episodic-Semantic Memory via Spreading Activation** -- Hanqi Jiang et al., 2026-01-06, score=76.0.
  Link: [https://arxiv.org/abs/2601.02744](https://arxiv.org/abs/2601.02744)

- **GraphER: An Efficient Graph-Based Enrichment and Reranking Method for Retrieval-Augmented Generation** -- Ruizhong Miao et al., 2026-03-26, score=74.2.
  Link: [https://arxiv.org/abs/2603.24925](https://arxiv.org/abs/2603.24925)

- **BLUEmed: Retrieval-Augmented Multi-Agent Debate for Clinical Error Detection** -- Saukun Thika You et al., 2026-04-12, score=74.0.
  Link: [https://arxiv.org/abs/2604.10389](https://arxiv.org/abs/2604.10389)

- **A Hybrid Retrieval and Reranking Framework for Evidence-Grounded Retrieval-Augmented Generation** -- Fariba Afrin Irany et al., 2026-05-03, score=72.7.
  Link: [https://arxiv.org/abs/2605.01664](https://arxiv.org/abs/2605.01664)

- **CODE-GEN: A Human-in-the-Loop RAG-Based Agentic AI System for Multiple-Choice Question Generation** -- Xiaojing Duan et al., 2026-04-05, score=72.2.
  Link: [https://arxiv.org/abs/2604.03926](https://arxiv.org/abs/2604.03926)

- **Toward Agentic RAG for Ukrainian** -- Marta Sumyk et al., 2026-04-16, score=72.2.
  Link: [https://arxiv.org/abs/2604.14896](https://arxiv.org/abs/2604.14896)

### demoted-for-cap (not on locked top-list) (8 papers)

- **Enhancing Financial Report Question-Answering: A Retrieval-Augmented Generation System with Reranking Analysis** -- Zhiyuan Cheng et al., 2026-02-18, score=108.7.
  Link: [https://arxiv.org/abs/2603.16877](https://arxiv.org/abs/2603.16877)

- **An Agent-Oriented Pluggable Experience-RAG Skill for Experience-Driven Retrieval Strategy Orchestration** -- Dutao Zhang et al., 2026-05-05, score=105.7.
  Link: [https://arxiv.org/abs/2605.03989](https://arxiv.org/abs/2605.03989)

- **JADE: Bridging the Strategic-Operational Gap in Dynamic Agentic RAG** -- Yiqun Chen et al., 2026-01-29, score=105.2.
  Link: [https://arxiv.org/abs/2601.21916](https://arxiv.org/abs/2601.21916)

- **RAGShaper: Eliciting Sophisticated Agentic RAG Skills via Automated Data Synthesis** -- Zhengwei Tao et al., 2026-01-13, score=105.2.
  Link: [https://arxiv.org/abs/2601.08699](https://arxiv.org/abs/2601.08699)

- **DIVERGE: Diversity-Enhanced RAG for Open-Ended Information Seeking** -- Tianyi Hu, Niket Tandon, Akhil Arora, 2026-01-30, score=105.2.
  Link: [https://arxiv.org/abs/2602.00238](https://arxiv.org/abs/2602.00238)

- **SPD-RAG: Sub-Agent Per Document Retrieval-Augmented Generation** -- Yagiz Can Akay et al., 2026-03-09, score=103.7.
  Link: [https://arxiv.org/abs/2603.08329](https://arxiv.org/abs/2603.08329)

- **Multi-Agent GraphRAG: A Text-to-Cypher Framework for Labeled Property Graphs** -- Anton Gusarov et al., 2025-11-11, score=103.0.
  Link: [https://arxiv.org/abs/2511.08274](https://arxiv.org/abs/2511.08274)

- **Experience as a Compass: Multi-agent RAG with Evolving Orchestration and Agent Prompts** -- Sha Li et al., 2026-04-01, score=101.7.
  Link: [https://arxiv.org/abs/2604.00901](https://arxiv.org/abs/2604.00901)

### vertical-app without generalizable technique (4 papers)

- **Beyond RAG for Cyber Threat Intelligence: A Systematic Evaluation of Graph-Based and Agentic Retrieval** -- Dzenan Hamzic et al., 2026-04-13, score=61.5.
  Link: [https://arxiv.org/abs/2604.11419](https://arxiv.org/abs/2604.11419)

- **SoK: Agentic Retrieval-Augmented Generation (RAG): Taxonomy, Architectures, Evaluation, and Research Directions** -- Saroj Mishra et al., 2026-03-07, score=60.8.
  Link: [https://arxiv.org/abs/2603.07379](https://arxiv.org/abs/2603.07379)

- **DocSync: Agentic Documentation Maintenance via Critic-Guided Reflexion** -- Sidhesh Badrinarayan et al., 2026-05-04, score=60.5.
  Link: [https://arxiv.org/abs/2605.02163](https://arxiv.org/abs/2605.02163)

- **DisastRAG: A Multi-Source Disaster Information Integration and Access System Based on Retrieval-Augmented Large Language** -- Bo Li et al., 2026-04-06, score=59.2.
  Link: [https://arxiv.org/abs/2605.05210](https://arxiv.org/abs/2605.05210)

### out-of-scope per operator-excluded categories (4 papers)

- **VISOR: Agentic Visual Retrieval-Augmented Generation via Iterative Search and Over-horizon Reasoning** -- Yucheng Shen et al., 2026-04-10, score=60.8.
  Link: [https://arxiv.org/abs/2604.09508](https://arxiv.org/abs/2604.09508)

- **GraphRAG-IRL: Personalized Recommendation with Graph-Grounded Inverse Reinforcement Learning and LLM Re-ranking** -- Siqi Liang et al., 2026-04-21, score=57.2.
  Link: [https://arxiv.org/abs/2604.19128](https://arxiv.org/abs/2604.19128)

- **Nemotron ColEmbed V2: Top-Performing Late Interaction Embedding Models for Visual Document Retrieval** -- Gabriel de Souza P. Moreira et al., 2026-02-03, score=43.5.
  Link: [https://arxiv.org/abs/2602.03992](https://arxiv.org/abs/2602.03992)

- **AgenticOCR: Parsing Only What You Need for Efficient Retrieval-Augmented Generation** -- Zhengren Wang et al., 2026-02-27, score=33.8.
  Link: [https://arxiv.org/abs/2602.24134](https://arxiv.org/abs/2602.24134)

### low combined score (4 papers)

- **Securing the Agent: Vendor-Neutral, Multitenant Enterprise Retrieval and Tool Use** -- Francisco Javier Arceo et al., 2026-05-06, score=49.8.
  Link: [https://arxiv.org/abs/2605.05287](https://arxiv.org/abs/2605.05287)

- **TRIZ-RAGNER: A Retrieval-Augmented Large Language Model for TRIZ-Aware Named Entity Recognition in Patent-Based Contradi** -- Zitong Xu et al., 2026-02-27, score=45.0.
  Link: [https://arxiv.org/abs/2602.23656](https://arxiv.org/abs/2602.23656)

- **Diagnosing Retrieval vs. Utilization Bottlenecks in LLM Agent Memory** -- Boqin Yuan et al., 2026-03-02, score=45.0.
  Link: [https://arxiv.org/abs/2603.02473](https://arxiv.org/abs/2603.02473)

- **Agentic clinical reasoning over longitudinal myeloma records: a retrospective evaluation against expert consensus** -- Johannes Moll et al., 2026-04-27, score=39.0.
  Link: [https://arxiv.org/abs/2604.24473](https://arxiv.org/abs/2604.24473)

### unspecified (2 papers)

- **Continuum Memory Architectures for Long-Horizon LLM Agents** -- Joe Logan, 2026-01-14, score=62.5.
  Link: [https://arxiv.org/abs/2601.09913](https://arxiv.org/abs/2601.09913)

- **Cognis: Context-Aware Memory for Conversational AI Agents** -- Parshva Daftari et al., 2026-03-27, score=56.5.
  Link: [https://arxiv.org/abs/2604.19771](https://arxiv.org/abs/2604.19771)

---

## Notes on this run

- The operator's window (2025-11-10 to 2026-05-10) overlaps with two prior W19 digests (a 3-month and an 8-month version of the same theme). This run reuses extraction work from those runs for efficiency; the relevance filter and digest-shape are re-applied per the operator's run-specific overrides.
- Several Phase 1 anchor papers (jina-reranker-v3, InfoGain-RAG, ARC, TeaRAG, Stop-RAG, DecEx-RAG, Interact-RAG) fall just before the operator's window (Sep-Oct 2025) and are deliberately not included. They are referenced inside the digest where Phase 1's "the question becomes do we even need vectors" trajectory needs them as priors, but they are not in the per-paper kept list.
- The traction-signal axis was applied as a soft modifier rather than a hard gate, per the operator's brief. Several recent papers (CAR, DCI, MemReranker, LatentRAG) ride on traction proxies because their submission dates are 2-7 days before the run; calibrated confidence is reported per paper.
