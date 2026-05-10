# 2026-W19 On-Demand Run — Full Paper List

**Operator theme:** Latest retrieval and re-ranking techniques for LLM agents.
**Window:** 2026-02-09 → 2026-05-09.
**Source:** arXiv (cs.IR / cs.CL / cs.LG / cs.AI).

## Pipeline summary

- Fetched: 889 keyword-matched arXiv records (after dedupe across queries; 1869 raw arXiv records before keyword filter).
- Pre-filtered to top 50 candidates by title+abstract theme score (cs.IR primary + retrieval-and-rerank-keyword cs.CL/cs.LG/cs.AI).
- Pass 1 extractions written for all 50.
- Relevance filter: 25 KEEP, 25 REVIEW (cap-demoted from KEEP), 0 DROP.
- Pass 2: degraded-mode (abstract-only) on the 25 KEEPs.
- Pass A: per-paper layered summary on all 25 KEEPs.
- Pass B: 5 argument-shaped clusters + 3 outliers.

## Cross-source dedupe note

Single-source run (arXiv only). No cross-source dedupe needed.

---

## KEEP — 25 papers in the digest

### [C2] Diagnosing LLM-based Rerankers in Cold-Start Recommender Systems: Coverage, Exposure and Practical Mitigations
- **Authors**: Ekaterina Lemdiasova et al.
- **Date**: 2026-02-09    **arXiv**: https://arxiv.org/abs/2604.16318    **PDF**: https://arxiv.org/pdf/2604.16318v1
- **Primary category**: cs.IR    **All categories**: cs.IR, cs.CL
- **Matched keywords**: hybrid retrieval, reranker, reranking, cross-encoder
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 10.3
- **Rationale**: Negative-result diagnostic: LLM rerankers fail in cold-start; popularity beats them by ~30x. High-information.
- **One-line**: Cross-encoder rerankers fail in cold-start movie recommendation: HR@10 of 0.268 (popularity) vs 0.008 (LLM rerank); blames retrieval coverage, not reranker capacity.

### [C1] LLM-Confidence Reranker: A Training-Free Approach for Enhancing Retrieval-Augmented Generation Systems
- **Authors**: Zhipeng Song et al.
- **Date**: 2026-02-14    **arXiv**: https://arxiv.org/abs/2602.13571    **PDF**: https://arxiv.org/pdf/2602.13571v1
- **Primary category**: cs.CL    **All categories**: cs.CL, cs.AI
- **Matched keywords**: retrieval-augmented generation, rag, reranker, reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 12.63
- **Rationale**: Training-free reranker using LLM-confidence (MSCP) — novel, clean, training-free, plug-and-play. Core theme.
- **One-line**: Training-free reranker that scores by LLM Maximum-Semantic-Cluster-Proportion confidence; up to +20.6% NDCG@5 on BEIR over fine-tuned rerankers using 7-9B LLMs.

### [C4] Diagnosing Retrieval vs. Utilization Bottlenecks in LLM Agent Memory
- **Authors**: Boqin Yuan et al.
- **Date**: 2026-03-02    **arXiv**: https://arxiv.org/abs/2603.02473    **PDF**: https://arxiv.org/pdf/2603.02473v2
- **Primary category**: cs.AI    **All categories**: cs.AI
- **Matched keywords**: memory-augmented, agent memory, reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.42
- **Rationale**: 3x3 diagnostic: retrieval method dominates over write strategy in agent memory. High-information empirical finding.
- **One-line**: 3x3 diagnostic on agent memory: retrieval method dominates (20-pt accuracy span) vs write strategy (3-8 pts); raw chunks match expensive summarization at zero LLM-call cost.

### [C3] Test-Time Strategies for More Efficient and Accurate Agentic RAG
- **Authors**: Brian Zhang et al.
- **Date**: 2026-03-12    **arXiv**: https://arxiv.org/abs/2603.12396    **PDF**: https://arxiv.org/pdf/2603.12396v1
- **Primary category**: cs.IR    **All categories**: cs.IR, cs.AI
- **Matched keywords**: agentic rag, retrieval-augmented generation, rag
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 8.97
- **Rationale**: Test-Time Strategies for agentic RAG: minimal contextualization + de-dup on Search-R1; clean engineering result.
- **One-line**: Test-time tweaks (contextualization + de-dup of retrieved docs) on Search-R1; +5.6% EM and -10.5% turns on HotpotQA + Natural Questions.

### [C3] APEX-Searcher: Augmenting LLMs' Search Capabilities through Agentic Planning and Execution
- **Authors**: Kun Chen et al.
- **Date**: 2026-03-14    **arXiv**: https://arxiv.org/abs/2603.13853    **PDF**: https://arxiv.org/pdf/2603.13853v2
- **Primary category**: cs.CL    **All categories**: cs.CL, cs.AI
- **Matched keywords**: retrieval-augmented generation, iterative retrieval, rag
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 8.98
- **Rationale**: APEX-Searcher: 2-stage RL+SFT decoupling planning vs execution to escape sparse-reward issues. Strong technique.
- **One-line**: Two-stage agentic-search training: stage-1 RL with decomposition-specific rewards (planning); stage-2 SFT on multi-hop trajectories (execution).

### [C5] Graph-Native Cognitive Memory for AI Agents: Formal Belief Revision Semantics for Versioned Memory Architectures
- **Authors**: Young Bin Park
- **Date**: 2026-03-18    **arXiv**: https://arxiv.org/abs/2603.17244    **PDF**: https://arxiv.org/pdf/2603.17244v1
- **Primary category**: cs.AI    **All categories**: cs.AI, cs.IR, cs.LO
- **Matched keywords**: agent memory, reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.01
- **Rationale**: Kumiho: graph-native agent memory grounded in AGM belief-revision postulates. Unusual formal grounding.
- **One-line**: Graph-native agent memory grounded in AGM belief-revision postulates with hybrid retrieval + client-side LLM rerank; 93.3% LoCoMo-Plus authors / mid-80s reproduction (vs 45.7% prior best).

### [C2] ProGRank: Probe-Gradient Reranking to Defend Dense-Retriever RAG from Corpus Poisoning
- **Authors**: Xiangyu Yin et al.
- **Date**: 2026-03-24    **arXiv**: https://arxiv.org/abs/2603.22934    **PDF**: https://arxiv.org/pdf/2603.22934v2
- **Primary category**: cs.AI    **All categories**: cs.AI
- **Matched keywords**: retrieval-augmented generation, rag, reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.84
- **Rationale**: ProGRank: probe-gradient reranker as security defense; novel mechanism. Core theme.
- **One-line**: Training-free defense reranker that probes the retriever's gradient response under perturbation; competitive even under adaptive attacks, with a surrogate variant for unavailable retrievers.

### [C2] GraphER: An Efficient Graph-Based Enrichment and Reranking Method for Retrieval-Augmented Generation
- **Authors**: Ruizhong Miao et al.
- **Date**: 2026-03-26    **arXiv**: https://arxiv.org/abs/2603.24925    **PDF**: https://arxiv.org/pdf/2603.24925v1
- **Primary category**: cs.LG    **All categories**: cs.LG, cs.CL, cs.IR
- **Matched keywords**: retrieval-augmented generation, rag, reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 10.85
- **Rationale**: Graph-based reranking over vector stores (no KG required) — practical technique. Core theme.
- **One-line**: Graph-based reranker that runs over standard vector stores (no KG required), retriever-agnostic with claimed negligible latency overhead.

### [C4] Do We Still Need GraphRAG? Benchmarking RAG and GraphRAG for Agentic Search Systems
- **Authors**: Dongzhe Fan et al.
- **Date**: 2026-04-01    **arXiv**: https://arxiv.org/abs/2604.09666    **PDF**: https://arxiv.org/pdf/2604.09666v1
- **Primary category**: cs.IR    **All categories**: cs.IR, cs.AI
- **Matched keywords**: agentic rag, retrieval-augmented generation, graphrag, rag
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.28
- **Rationale**: RAGSearch: unified benchmark dense-RAG vs GraphRAG under agentic search; standardized protocol; full test sets.
- **One-line**: Unified benchmark of dense-RAG vs GraphRAG under agentic search; agentic search closes most of the dense-vs-graph gap (especially RL-based); GraphRAG holds advantage on complex multi-hop when its offline cost amortizes.

### [C3] Experience as a Compass: Multi-agent RAG with Evolving Orchestration and Agent Prompts
- **Authors**: Sha Li et al.
- **Date**: 2026-04-01    **arXiv**: https://arxiv.org/abs/2604.00901    **PDF**: https://arxiv.org/pdf/2604.00901v2
- **Primary category**: cs.AI    **All categories**: cs.AI
- **Matched keywords**: agent retrieval, retrieval-augmented generation, rag
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.08
- **Rationale**: HERA: jointly evolves multi-agent topology and per-role prompts; +38.7% over recent baselines.
- **One-line**: Multi-agent RAG that co-evolves agent topology (reward-guided sampling) and per-role prompts (dual-axis credit assignment); +38.7% average across six knowledge-intensive benchmarks.

### [C3] Doctor-RAG: Failure-Aware Repair for Agentic Retrieval-Augmented Generation
- **Authors**: Shuguang Jiao et al.
- **Date**: 2026-04-01    **arXiv**: https://arxiv.org/abs/2604.00865    **PDF**: https://arxiv.org/pdf/2604.00865v1
- **Primary category**: cs.IR    **All categories**: cs.IR
- **Matched keywords**: agentic rag, retrieval-augmented generation, rag
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.08
- **Rationale**: Doctor-RAG: trajectory-level failure diagnosis + tool-conditioned local repair with prefix reuse. Novel mechanism.
- **One-line**: Failure-aware repair for agentic RAG: diagnoses earliest failure point in a trajectory, repairs locally with prefix reuse; beats full-pipeline rerun on accuracy and token cost.

### [C1] Optimizing RAG Rerankers with LLM Feedback via Reinforcement Learning
- **Authors**: Yuhang Wu et al.
- **Date**: 2026-04-02    **arXiv**: https://arxiv.org/abs/2604.02091    **PDF**: https://arxiv.org/pdf/2604.02091v1
- **Primary category**: cs.CL    **All categories**: cs.CL, cs.AI, cs.IR
- **Matched keywords**: retrieval-augmented generation, rag, reranker, reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 12.29
- **Rationale**: RL alignment of reranker to LLM utility (RRPO); a structural shift from relevance-as-target to utility-as-target. Core theme.
- **One-line**: RL-trains rerankers using LLM-generation feedback as the reward (no human labels), with a reference-anchored deterministic baseline; outperforms RankZephyr on knowledge-intensive QA.

### [C5] Lightweight LLM Agent Memory with Small Language Models
- **Authors**: Jiaquan Zhang et al.
- **Date**: 2026-04-09    **arXiv**: https://arxiv.org/abs/2604.07798    **PDF**: https://arxiv.org/pdf/2604.07798v3
- **Primary category**: cs.AI    **All categories**: cs.AI
- **Matched keywords**: agent memory, re-ranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.43
- **Rationale**: LightMem: SLM-driven 3-tier agent memory + 2-stage retrieval; production-grade efficiency.
- **One-line**: SLM-driven 3-tier (STM/MTM/LTM) agent memory + 2-stage vector-coarse + semantic-consistency-rerank retrieval; +2.5 F1 over A-MEM on LoCoMo at 83 ms retrieval / 581 ms end-to-end.

### [C2] FRESCO: Benchmarking and Optimizing Re-rankers for Evolving Semantic Conflict in Retrieval-Augmented Generation
- **Authors**: Sohyun An et al.
- **Date**: 2026-04-14    **arXiv**: https://arxiv.org/abs/2604.14227    **PDF**: https://arxiv.org/pdf/2604.14227v1
- **Primary category**: cs.IR    **All categories**: cs.IR, cs.AI
- **Matched keywords**: retrieval-augmented generation, rag, re-ranker
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 10.06
- **Rationale**: FRESCO recency-aware reranker benchmark + instruction tuning; reveals systematic reranker bias. Core theme + benchmark.
- **One-line**: Recency-aware reranker benchmark using paired recency-seeking queries + Wikipedia revision history; reveals a consistent reranker bias toward older docs; instruction tuning recovers up to +27% on evolving knowledge.

### [C4] Don't Retrieve, Navigate: Distilling Enterprise Knowledge into Navigable Agent Skills for QA and RAG
- **Authors**: Yiqun Sun et al.
- **Date**: 2026-04-16    **arXiv**: https://arxiv.org/abs/2604.14572    **PDF**: https://arxiv.org/pdf/2604.14572v2
- **Primary category**: cs.IR    **All categories**: cs.IR, cs.AI, cs.CL, cs.MA
- **Matched keywords**: agentic rag, retrieval-augmented generation, dense retrieval, rag
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.37
- **Rationale**: Corpus2Skill: distills corpus into a navigable skill directory; reframes retrieval as navigation. Sharp technique.
- **One-line**: Distills corpus into a navigable skill directory (LLM summaries at each level + doc-ID retrieval); outperforms dense / RAPTOR / agentic-RAG on WixQA, with single-domain corpora as the right regime.

### [C2] Rethinking the Necessity of Adaptive Retrieval-Augmented Generation through the Lens of Adaptive Listwise Ranking
- **Authors**: Jun Feng et al.
- **Date**: 2026-04-17    **arXiv**: https://arxiv.org/abs/2604.15621    **PDF**: https://arxiv.org/pdf/2604.15621v1
- **Primary category**: cs.IR    **All categories**: cs.IR, cs.AI, cs.CL
- **Matched keywords**: retrieval-augmented generation, reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.57
- **Rationale**: AdaRankLLM: adaptive listwise reranking + distillation; identifies role-shift of adaptive retrieval w.r.t. model strength. Core theme.
- **One-line**: Adaptive listwise reranker with passage dropout + progressive distillation for small LLMs; identifies a role-shift of adaptive retrieval (filter for weak models, efficiency lever for strong ones).

### [C3] AutoSearch: Adaptive Search Depth for Efficient Agentic RAG via Reinforcement Learning
- **Authors**: Jingbo Sun et al.
- **Date**: 2026-04-19    **arXiv**: https://arxiv.org/abs/2604.17337    **PDF**: https://arxiv.org/pdf/2604.17337v1
- **Primary category**: cs.AI    **All categories**: cs.AI
- **Matched keywords**: agentic rag, retrieval-augmented generation, rag
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.18
- **Rationale**: AutoSearch: RL framework for adaptive search depth via self-answering. Sharp technique.
- **One-line**: RL framework for agentic-RAG search-depth control: scores each step's intermediate self-answer to find minimal-sufficient depth and penalize over-searching.

### [C1] Prism-Reranker: Beyond Relevance Scoring -- Jointly Producing Contributions and Evidence for Agentic Retrieval
- **Authors**: Dun Zhang
- **Date**: 2026-04-26    **arXiv**: https://arxiv.org/abs/2604.23734    **PDF**: https://arxiv.org/pdf/2604.23734v1
- **Primary category**: cs.IR    **All categories**: cs.IR
- **Matched keywords**: retrieval-augmented generation, rag, reranker
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 13.12
- **Rationale**: Reranker-output redesign (contribution + evidence-passage) for agentic retrieval; explicit attempt to redefine reranker interface. Core theme.
- **One-line**: Reranker family (0.8B-9B) that outputs a contribution statement and an evidence-passage rewrite alongside the relevance verdict; +1.54 average NDCG@10 on BEIR-QA when applied to Qwen3-Reranker-4B.

### [C4] Beyond Semantic Similarity: Rethinking Retrieval for Agentic Search via Direct Corpus Interaction
- **Authors**: Zhuofeng Li et al.
- **Date**: 2026-05-03    **arXiv**: https://arxiv.org/abs/2605.05242    **PDF**: https://arxiv.org/pdf/2605.05242v1
- **Primary category**: cs.IR    **All categories**: cs.IR, cs.AI
- **Matched keywords**: reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.36
- **Rationale**: Direct Corpus Interaction: bold position — agent uses grep/scripts directly, no embeddings/index. Outperforms strong baselines.
- **One-line**: Lets the agent grep / read / script the raw corpus directly (no embedder, no index, no retrieval API); reportedly outperforms strong sparse, dense, and reranking baselines on BRIGHT, BEIR, BrowseComp-Plus.

### [C1] CAR: Query-Guided Confidence-Aware Reranking for Retrieval-Augmented Generation
- **Authors**: Zhipeng Song et al.
- **Date**: 2026-05-06    **arXiv**: https://arxiv.org/abs/2605.04495    **PDF**: https://arxiv.org/pdf/2605.04495v1
- **Primary category**: cs.CL    **All categories**: cs.CL, cs.AI
- **Matched keywords**: retrieval-augmented generation, rag, reranker, reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 11.08
- **Rationale**: Training-free reranking by generator confidence change (CAR); ρ=0.964 with downstream F1. Core theme.
- **One-line**: Training-free reranker that uses semantic-consistency-of-sampled-answers as a usefulness signal; +25.4% on YesNo + Contriever and ρ=0.964 with downstream generation F1.

### [C1] MemReranker: Reasoning-Aware Reranking for Agent Memory Retrieval
- **Authors**: Chunyu Li et al.
- **Date**: 2026-05-07    **arXiv**: https://arxiv.org/abs/2605.06132    **PDF**: https://arxiv.org/pdf/2605.06132v1
- **Primary category**: cs.CL    **All categories**: cs.CL
- **Matched keywords**: agent memory, reranker, reranking
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 13.58
- **Rationale**: Reranker family for agent memory; multi-teacher LLM distillation; benchmarked at scale. Core theme; sharp technique.
- **One-line**: Reranker family (0.6B / 4B) for agent memory; multi-teacher LLM distillation; 0.737 MAP at ~10-20% the latency of Gemini-3-Flash.

### [C3] LatentRAG: Latent Reasoning and Retrieval for Efficient Agentic RAG
- **Authors**: Yijia Zheng et al.
- **Date**: 2026-05-07    **arXiv**: https://arxiv.org/abs/2605.06285    **PDF**: https://arxiv.org/pdf/2605.06285v1
- **Primary category**: cs.CL    **All categories**: cs.CL, cs.LG
- **Matched keywords**: agentic rag, retrieval-augmented generation, dense retrieval, rag
- **Score**: relevance 100.0 (match 1.0 / criteria 1.0 / novelty 1.0); prefilter 9.48
- **Rationale**: LatentRAG: shifts the agentic loop into latent space; ~90% latency cut. Strong methodological reframing.
- **One-line**: Runs agentic-RAG reasoning + retrieval in latent space (one forward pass), with a parallel decoder for transparency; ~90% latency reduction at comparable accuracy on seven benchmarks.

### [OUT] AgenticOCR: Parsing Only What You Need for Efficient Retrieval-Augmented Generation
- **Authors**: Zhengren Wang et al.
- **Date**: 2026-02-27    **arXiv**: https://arxiv.org/abs/2602.24134    **PDF**: https://arxiv.org/pdf/2602.24134v1
- **Primary category**: cs.CV    **All categories**: cs.CV, cs.CL
- **Matched keywords**: retrieval-augmented generation, rag, reranking
- **Score**: relevance 95.5 (match 1.0 / criteria 0.9 / novelty 1.0); prefilter 9.7
- **Rationale**: AgenticOCR: positioned as a third RAG primitive (alongside embed + rerank) for visual docs; multi-modal retrieval contribution.
- **One-line**: Query-driven OCR module for visual-RAG that recognizes only regions of interest, sitting alongside embedding + reranking; claims expert-level performance on long visual documents.

### [OUT] Quantifying the Accuracy and Cost Impact of Design Decisions in Budget-Constrained Agentic LLM Search
- **Authors**: Kyle McCleary et al.
- **Date**: 2026-03-09    **arXiv**: https://arxiv.org/abs/2603.08877    **PDF**: https://arxiv.org/pdf/2603.08877v1
- **Primary category**: cs.AI    **All categories**: cs.AI
- **Matched keywords**: retrieval-augmented generation, dense retrieval, rag, re-ranking
- **Score**: relevance 95.5 (match 1.0 / criteria 0.9 / novelty 1.0); prefilter 9.96
- **Rationale**: BCAS: measurement harness for budget-constrained agentic search; mostly measurement contributions, useful guidance.
- **One-line**: Measurement harness for budget-constrained agentic search across 6 LLMs and 3 QA benchmarks; hybrid lexical+dense + lightweight rerank dominates the cost-accuracy frontier; deeper search caps quickly.

### [OUT] A Reference Architecture for Agentic Hybrid Retrieval in Dataset Search
- **Authors**: Riccardo Terrenzi et al.
- **Date**: 2026-03-28    **arXiv**: https://arxiv.org/abs/2604.16394    **PDF**: https://arxiv.org/pdf/2604.16394v1
- **Primary category**: cs.IR    **All categories**: cs.IR, cs.AI
- **Matched keywords**: hybrid retrieval, dense retrieval
- **Score**: relevance 95.5 (match 1.0 / criteria 0.9 / novelty 1.0); prefilter 9.26
- **Rationale**: Reference architecture for agentic hybrid retrieval; software-architecture framing but well-grounded with 7-variant evaluation.
- **One-line**: Reference architecture for agentic hybrid retrieval in dataset search (BM25 + dense + RRF + LLM-agent rerank + offline pseudo-query metadata expansion); ReAct vs multi-agent horizontal architectures compared with explicit governance tactics.

---

## REVIEW — 25 papers (cap-demoted from KEEP, all with rationale)

These papers passed criteria scoring at 50+ but did not fit in the 25-paper KEEP cap.
Several would have been clear KEEPs in a more permissive run; none are dropped silently.

### Task-Adaptive Retrieval over Agentic Multi-Modal Web Histories via Learned Graph Memory
- **Authors**: Saman Forouzandeh et al.    **Date**: 2026-04-09    **arXiv**: https://arxiv.org/abs/2604.07863
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: demoted-for-cap
- **Rationale**: ACGM: learned graph-memory retriever for web agents with modality decay constants; strong but web-agent-specific.

### Cognis: Context-Aware Memory for Conversational AI Agents
- **Authors**: Parshva Daftari et al.    **Date**: 2026-03-27    **arXiv**: https://arxiv.org/abs/2604.19771
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: explicit-llm-agent, demoted-for-cap
- **Rationale**: Cognis: production memory stack with hybrid + cross-encoder rerank; well-engineered integration but limited novelty.

### SoK: Agentic Retrieval-Augmented Generation (RAG): Taxonomy, Architectures, Evaluation, and Research Directions
- **Authors**: Saroj Mishra et al.    **Date**: 2026-03-07    **arXiv**: https://arxiv.org/abs/2603.07379
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: review, review, demoted-for-cap
- **Rationale**: [review/SoK] for agentic RAG; valuable taxonomy + risk analysis but no new method.

### Securing the Agent: Vendor-Neutral, Multitenant Enterprise Retrieval and Tool Use
- **Authors**: Francisco Javier Arceo et al.    **Date**: 2026-05-06    **arXiv**: https://arxiv.org/abs/2605.05287
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: explicit-llm-agent, demoted-for-cap
- **Rationale**: OGX/Securing-the-Agent: formalizes relevance-vs-authorization gap with ABAC-gated retrieval; architectural rather than algorithmic technique.

### An Agent-Oriented Pluggable Experience-RAG Skill for Experience-Driven Retrieval Strategy Orchestration
- **Authors**: Dutao Zhang et al.    **Date**: 2026-05-05    **arXiv**: https://arxiv.org/abs/2605.03989
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: demoted-for-cap
- **Rationale**: Experience-RAG Skill: pluggable retrieval-strategy selection layer; clear competing position to Adaptive-RAG.

### LongVidSearch: An Agentic Benchmark for Multi-hop Evidence Retrieval Planning in Long Videos
- **Authors**: Rongyi Yu et al.    **Date**: 2026-03-15    **arXiv**: https://arxiv.org/abs/2603.14468
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: explicit-llm-agent, demoted-for-cap
- **Rationale**: LongVidSearch: long-video multi-hop retrieval-planning benchmark; surfaces retrieval as the bottleneck. Useful infrastructure.

### Explainable Innovation Engine: Dual-Tree Agent-RAG with Methods-as-Nodes and Verifiable Write-Back
- **Authors**: Renwei Meng    **Date**: 2026-03-10    **arXiv**: https://arxiv.org/abs/2603.09192
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: demoted-for-cap
- **Rationale**: Explainable Innovation Engine: methods-as-nodes + verifiable write-back; knowledge-unit redesign for derivation-heavy domains.

### SPD-RAG: Sub-Agent Per Document Retrieval-Augmented Generation
- **Authors**: Yagiz Can Akay et al.    **Date**: 2026-03-09    **arXiv**: https://arxiv.org/abs/2603.08329
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: demoted-for-cap
- **Rationale**: SPD-RAG: hierarchical sub-agent-per-doc; clear technique with strong LOONG numbers, but limited to multi-document QA setting.

### Beyond RAG for Cyber Threat Intelligence: A Systematic Evaluation of Graph-Based and Agentic Retrieval
- **Authors**: Dzenan Hamzic et al.    **Date**: 2026-04-13    **arXiv**: https://arxiv.org/abs/2604.11419
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: demoted-for-cap
- **Rationale**: CTI benchmark of 4 RAG architectures over 3.3K QAs; clear comparative finding (hybrid graph+text wins multi-hop).

### VISOR: Agentic Visual Retrieval-Augmented Generation via Iterative Search and Over-horizon Reasoning
- **Authors**: Yucheng Shen et al.    **Date**: 2026-04-10    **arXiv**: https://arxiv.org/abs/2604.09508
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: demoted-for-cap
- **Rationale**: VISOR: structured Evidence Space + sliding-window for visual agentic RAG; multimodal-specific.

### AgentGL: Towards Agentic Graph Learning with LLMs via Reinforcement Learning
- **Authors**: Yuanfu Sun et al.    **Date**: 2026-04-07    **arXiv**: https://arxiv.org/abs/2604.05846
- **Score**: 95.5 (match 1.0 / criteria 0.9)
- **Tags**: explicit-llm-agent, demoted-for-cap
- **Rationale**: AgentGL: RL-driven agentic graph learning; significant on TAG benchmarks but graph-learning is adjacent to general agent retrieval.

### Toward Agentic RAG for Ukrainian
- **Authors**: Marta Sumyk et al.    **Date**: 2026-04-16    **arXiv**: https://arxiv.org/abs/2604.14896
- **Score**: 86.5 (match 1.0 / criteria 0.7)
- **Tags**: vertical-application, demoted-for-cap
- **Rationale**: Agentic RAG for Ukrainian: low-resource case study; useful 'retrieval is the bottleneck' finding but vertical.

### Agentic Retrieval-Augmented Generation for Financial Document Question Answering
- **Authors**: Yang Shu et al.    **Date**: 2026-05-06    **arXiv**: https://arxiv.org/abs/2605.05409
- **Score**: 86.5 (match 1.0 / criteria 0.7)
- **Tags**: vertical-application, demoted-for-cap
- **Rationale**: FinAgent-RAG: contrastive retriever (hard-negative mining for numerical-distinct passages) + PoT + cost router; technique additions but vertical.

### BLUEmed: Retrieval-Augmented Multi-Agent Debate for Clinical Error Detection
- **Authors**: Saukun Thika You et al.    **Date**: 2026-04-12    **arXiv**: https://arxiv.org/abs/2604.10389
- **Score**: 77.5 (match 1.0 / criteria 0.5)
- **Tags**: vertical-application, demoted-for-cap
- **Rationale**: BLUEmed: multi-agent debate + hybrid RAG for clinical errors; debate framework interesting but vertical.

### From Intent to Execution: Composing Agentic Workflows with Agent Recommendation
- **Authors**: Kishan Athrey et al.    **Date**: 2026-05-05    **arXiv**: https://arxiv.org/abs/2605.03986
- **Score**: 77.5 (match 0.8 / criteria 0.7)
- **Tags**: demoted-for-cap
- **Rationale**: Multi-agent system composition with two-stage IR + critique; technique exists but the contribution is MAS-composition.

### DocSync: Agentic Documentation Maintenance via Critic-Guided Reflexion
- **Authors**: Sidhesh Badrinarayan et al.    **Date**: 2026-05-04    **arXiv**: https://arxiv.org/abs/2605.02163
- **Score**: 77.5 (match 1.0 / criteria 0.5)
- **Tags**: vertical-application, demoted-for-cap
- **Rationale**: DocSync: AST-RAG + Reflexion for doc maintenance; AST-aware RAG framing is mildly novel but software-engineering vertical.

### Agentic clinical reasoning over longitudinal myeloma records: a retrospective evaluation against expert consensus
- **Authors**: Johannes Moll et al.    **Date**: 2026-04-27    **arXiv**: https://arxiv.org/abs/2604.24473
- **Score**: 77.5 (match 1.0 / criteria 0.5)
- **Tags**: vertical-application, demoted-for-cap
- **Rationale**: Agentic clinical reasoning on myeloma; rigorous empirical comparison but vertical.

### GraphRAG for Engineering Diagrams: ChatP&ID Enables LLM Interaction with P&IDs
- **Authors**: Achmad Anggawirya Alimin et al.    **Date**: 2026-03-23    **arXiv**: https://arxiv.org/abs/2603.22528
- **Score**: 77.5 (match 1.0 / criteria 0.5)
- **Tags**: vertical-application, explicit-llm-agent, demoted-for-cap
- **Rationale**: ChatP&ID: GraphRAG for P&IDs; standard GraphRAG, engineering-vertical.

### GraphRAG-IRL: Personalized Recommendation with Graph-Grounded Inverse Reinforcement Learning and LLM Re-ranking
- **Authors**: Siqi Liang et al.    **Date**: 2026-04-21    **arXiv**: https://arxiv.org/abs/2604.19128
- **Score**: 73.0 (match 1.0 / criteria 0.4)
- **Tags**: demoted-for-cap
- **Rationale**: GraphRAG-IRL: recommender-systems application; uses retrieval+rerank but the subject is recommendation.

### MemRerank: Preference Memory for Personalized Product Reranking
- **Authors**: Zhiyuan Peng et al.    **Date**: 2026-03-31    **arXiv**: https://arxiv.org/abs/2603.29247
- **Score**: 73.0 (match 1.0 / criteria 0.4)
- **Tags**: demoted-for-cap
- **Rationale**: MemRerank: e-commerce product reranking; preference memory technique exists but the subject is product reranking.

### A Hybrid Retrieval and Reranking Framework for Evidence-Grounded Retrieval-Augmented Generation
- **Authors**: Fariba Afrin Irany et al.    **Date**: 2026-05-03    **arXiv**: https://arxiv.org/abs/2605.01664
- **Score**: 73.0 (match 1.0 / criteria 0.4)
- **Tags**: demoted-for-cap
- **Rationale**: Bedrock + Cohere biomedical RAG pilot; standard tooling, no novel technique.

### Enhancing Financial Report Question-Answering: A Retrieval-Augmented Generation System with Reranking Analysis
- **Authors**: Zhiyuan Cheng et al.    **Date**: 2026-02-18    **arXiv**: https://arxiv.org/abs/2603.16877
- **Score**: 73.0 (match 1.0 / criteria 0.4)
- **Tags**: vertical-application, demoted-for-cap
- **Rationale**: Financial 10-K QA reranker ablation; standard hybrid+cross-encoder, vertical.

### DisastRAG: A Multi-Source Disaster Information Integration and Access System Based on Retrieval-Augmented Large Language Models
- **Authors**: Bo Li et al.    **Date**: 2026-04-06    **arXiv**: https://arxiv.org/abs/2605.05210
- **Score**: 73.0 (match 1.0 / criteria 0.4)
- **Tags**: vertical-application, demoted-for-cap
- **Rationale**: DisastRAG: multi-path disaster info system; vertical.

### TRIZ-RAGNER: A Retrieval-Augmented Large Language Model for TRIZ-Aware Named Entity Recognition in Patent-Based Contradiction Mining
- **Authors**: Zitong Xu et al.    **Date**: 2026-02-27    **arXiv**: https://arxiv.org/abs/2602.23656
- **Score**: 73.0 (match 1.0 / criteria 0.4)
- **Tags**: vertical-application, demoted-for-cap
- **Rationale**: TRIZ-RAGNER: patent-NER vertical; standard RAG.

### CODE-GEN: A Human-in-the-Loop RAG-Based Agentic AI System for Multiple-Choice Question Generation
- **Authors**: Xiaojing Duan et al.    **Date**: 2026-04-05    **arXiv**: https://arxiv.org/abs/2604.03926
- **Score**: 73.0 (match 1.0 / criteria 0.4)
- **Tags**: vertical-application, demoted-for-cap
- **Rationale**: CODE-GEN: educational MCQ generation; vertical.

---

## Generated

- Date: 2026-05-09
- Override file: `ops/paper-synthesizer/overrides/2026-W19.md`
- Cache: `ops/paper-synthesizer/.cache/2026-W19-search-results.json`, `2026-W19-prefilter.json`, `2026-W19-pass1-candidates.json`, `2026-W19-relevance.json`
- Per-paper Pass 1+2 extractions: `ops/paper-extractor/2026-W19/`
- Per-paper Pass A summaries: `ops/paper-synthesizer/2026-W19/per-paper/`
- Digest: `ops/paper-synthesizer/digests/2026-W19-on-demand-retrieval-rerank-llm-agents.md`
