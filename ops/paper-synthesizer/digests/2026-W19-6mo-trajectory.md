---
week: 2026-W19
type: on-demand-digest
run_suffix: 6mo-trajectory
mode: b
window_from: 2025-11-10
window_to: 2026-05-10
topic: "Latest retrieval and re-ranking techniques for LLM agents — 6-month trajectory"
audience: "Practitioner building an LLM-agent system right now"
kept_count: 36
cluster_count: 9
prior_digests_referenced: ["2026-W19-on-demand-retrieval-rerank-llm-agents", "2026-W19-on-demand-retrieval-rerank-evolution-8mo"]
sources_used: ["arXiv (cs.CL, cs.IR, cs.LG, cs.AI)"]
generated: 2026-05-10
generated_by: papersynthesis-orchestrator (Mode B direct-write fallback; subagent unavailable)
papers_list_path: ops/paper-synthesizer/2026-W19-6mo-papers.md
per_paper_summary_dir: ops/paper-synthesizer/2026-W19-6mo/per-paper/
---

# Retrieval and Re-ranking for LLM Agents — 6-Month Trajectory (Nov 2025 → May 2026)

## Headline

The 6-month arc has a single dominant question: **what is the right retrieval interface for an LLM agent?** In November 2025 the field was still defending the standard pipeline — embed the corpus, top-k retrieve, optionally rerank, hand the result to the LLM. By May 2026 three independent threads have weakened that default. The first is **rerank-for-utility**: train (or, increasingly, do not train) the reranker to score documents by how much they help the LLM answer, not by IR-style relevance — Generative Reasoning Re-ranker, RRPO, LCR, and CAR converge on this. The second is **rethink the retrieval interface**: expose retrieval as agent tools (A-RAG), distill the corpus into a navigable skill tree (Corpus2Skill), strip embeddings out entirely (Keyword Search Is All You Need; Direct Corpus Interaction). The third is **efficiency as a first-class research target**: Doctor-RAG, AutoSearch, Test-Time Strategies, LatentRAG all attack the per-query cost of agentic RAG. The practitioner-relevant outcome: hybrid retrieval (dense + sparse, RRF-merged) with a good reranker remains the production default and the kept set strongly supports it; agentic-RAG is worth piloting but not strictly better than enhanced workflow RAG; vector indexes are still the safe bet but the no-embedder thread is too strong to ignore. What did **not** settle: GraphRAG's value once an agent is in the loop (one paper says agentic interaction closes most of the gap; another says graphs still help on structural queries), and whether rerankers should output more than a score (Prism-Reranker says yes; the field has not followed yet).

---

## Trajectory by phase

### Phase 1: Mid–late November 2025 — the question becomes "do we need vectors?"

The window opens with three papers that, collectively, frame the next 6 months. Lumer et al.'s SEC-filing benchmark is the first systematic head-to-head between vector-based agentic RAG and a non-vector hierarchical-node alternative; the vector arm with hybrid search + metadata filtering wins 68% of comparisons but the gap is smaller than the discourse implied, and the cost story flips on preprocessing. Steiner, Peeters, and Bizer publish the four-way MCP vs RAG vs NLWeb vs HTML comparison — RAG, MCP, and NLWeb all beat raw HTML browsing across four LLM backbones, but no single structured-interface family wins. Oladokun's Path-Constrained Retrieval is small-scale (180 nodes) but documents a sharp diagnostic: vector retrieval frequently returns structurally disconnected context, with structural-consistency scores at 24–32% vs 100% under graph constraints.

**The inflection here**: in mid-November, "RAG" still meant "vector top-k plus optional rerank." By November 28, the kept set already shows three papers questioning whether that default is right — one on cost, one on interface choice, one on structural correctness. The vector-vs-non-vector debate is now in the literature, not just on Twitter.

**Practitioner read for Phase 1**: nothing in this phase is itself production-ready, but the diagnostic message is — your existing vector RAG probably works, and the alternatives are real. Watch the next two phases for whether the alternatives mature.

### Phase 2: December 2025 – January 2026 — consolidation, production stacks, and methods diversify

Phase 2 is the densest phase in the kept set (15 papers) and the most heterogeneous. Three sub-threads run simultaneously.

**Production stacks land.** Higress-RAG ([Lin, 2025-12-30](https://arxiv.org/abs/2602.23374)) is the first complete enterprise-grade reference architecture in the window — Adaptive Routing + Hybrid Retrieval (RRF) + Semantic Caching (50ms target) + Corrective RAG, all on the Model Context Protocol. It is single-author but the architectural inventory matters: this is what production RAG looked like at the start of 2026. Self-MedRAG ([Ryan et al., 2026-01-08](https://arxiv.org/abs/2601.04531)) codifies a transferable recipe — BM25 + Contriever + RRF + NLI verification with query reformulation — that practitioners outside medical QA can lift directly. Rumble et al.'s comparative grid on STaRK ([2025-12-14](https://arxiv.org/abs/2602.22219)) gives the practitioner-relevant data: cross-encoders reliably lift retrieval precision when added; the family choice matters less than the addition itself.

**Reranker design diversifies.** Sharifymoghaddam and Lin ([2026-01-20](https://arxiv.org/abs/2601.14224)) introduce Effective Token Cost on BrowseComp-Plus and report the actionable finding of the phase: moderate listwise reranking gives larger accuracy gains than the same compute spent on additional reasoning. If your test-time budget is tight, spend the marginal token on rerank, not on more thinking. Multivector Reranking in the Era of Strong First-Stage Retrievers ([Martinico et al.](https://arxiv.org/abs/2601.05200)) replaces the token-level "gather" stage in ColBERT-family pipelines with a learned-sparse retriever, collapsing multivector retrieval into the standard two-stage architecture. PruneRAG ([Jiao et al., 2026-01-16](https://arxiv.org/abs/2601.11024)) attacks two iterative-RAG failure modes (evidence forgetting; uncontrolled query expansion) and contributes a portable metric — Evidence Forgetting Rate — that practitioners can adopt without the rest of the architecture.

**Learned-sparse retrieval rejoins the conversation.** LACONIC ([Xu et al., 2026-01-04](https://arxiv.org/abs/2601.01684)) puts a Llama-3-8B learned-sparse retriever at #15 on the MTEB Retrieval leaderboard with 71% less index memory than dense, runnable on CPU. This is the single most concrete invitation in the phase to revisit LSR; combined with XProvence ([Mohamed et al., 2026-01-26](https://arxiv.org/abs/2601.18886)) — Naver's multilingual zero-cost context pruning fused into the reranker, weights on Hugging Face — the off-the-shelf sparse-and-pruning toolkit looks materially better in January than it did in November.

A fourth sub-thread — **agentic-RAG paradigm comparison** — also lands here. Ferrazzi et al. ([2026-01-12](https://arxiv.org/abs/2601.07711)) directly answers "is agentic RAG worth it?" with an honest "it depends": neither agentic nor enhanced workflow RAG dominates; basic RAG remains viable for simple queries. TreePS-RAG ([Zhang et al., 2026-01-11](https://arxiv.org/abs/2601.06922)) introduces process supervision via Monte-Carlo on rollout trees, the cleanest "process RL without process labels" result in the kept set. Keyword Search Is All You Need ([Subramanian et al. AWS, 2025-12-19](https://arxiv.org/abs/2602.23368)) is the single most-cited paper of Phase 2 in subsequent kept-set papers — agentic keyword tools alone reach 90%+ of vector-RAG performance, and the field starts referencing this as the headline for the no-embedder thread.

**The inflection here**: by end of January, the practitioner has clear defaults — hybrid retrieval + reranker + RRF + iterative refinement — and clear questions to track — does agentic actually pay; do you need vectors at all.

### Phase 3: Late January – February 2026 — rerank-for-utility hardens; diagnostic literature lands

Phase 3 is the methodological turning point on rerankers. Two papers in February together define the shift.

**Train rerankers for LLM utility, not IR relevance.** Generative Reasoning Re-ranker (GR2, [Liang et al., Meta-affiliated, 2026-02-08](https://arxiv.org/abs/2602.07774)) puts the recipe end-to-end: semantic-ID encoding (≥99% unique), mid-train on those IDs, SFT on rejection-sampled reasoning traces from a stronger LLM, then RL-tune for ranking quality. The paper enumerates the three limitations of prior LLM-as-reranker work (overlooks reranking, no RL, non-semantic IDs) and addresses all three. LCR ([Song et al., 2026-02-14](https://arxiv.org/abs/2602.13571)) takes the opposite approach for the same goal: training-free, score documents by Maximum Semantic Cluster Proportion — the LLM's own confidence under sampling — using only a 7-9B model; reports up to +20.6% NDCG@5 over fine-tuned reranker baselines on BEIR + TREC.

**Diagnostic literature lands.** Lemdiasova and Zmanovskii ([2026-02-09](https://arxiv.org/abs/2604.16318)) document a catastrophic failure mode in cold-start movie recommendation — popularity-baseline HR@10 = 0.268 vs LLM-cross-encoder reranker HR@10 = 0.008 — and locate the bottleneck at retrieval coverage (recall@200 = 0.109), not at the reranker. The methodological message generalizes: when retrieval coverage is poor, no reranker rescues you. Col-Bandit ([Pony et al., 2026-02-02](https://arxiv.org/abs/2602.02827)) attacks the production-side ColBERT cost — top-K identification with statistical bounds, zero-shot, drop-in, no index changes. A-RAG ([Du et al., 2026-02-03](https://arxiv.org/abs/2602.03442)) reframes retrieval as three agent-callable primitives (keyword, semantic, chunk-read) — the cleanest expression of "expose tools, let the agent orchestrate" so far. Forward Index Compression for LSR ([Bruch et al., 2026-02-05](https://arxiv.org/abs/2602.05445)) is engineering plumbing — DotVByte for inner-product compression on the LSR forward index — that production teams adopting LACONIC will need.

**The inflection here**: by mid-February, "rerank for LLM utility" is no longer a research thesis; it is the default direction with both trained (GR2) and training-free (LCR) instantiations. The diagnostic literature also re-anchors the field: rerankers are not a free lunch, and retrieval-side coverage is the upstream constraint.

### Phase 4: March – mid-April 2026 — efficiency becomes the first-class research target

Phase 4 is unified by a single research target: cost. Eight papers in this window attack agentic-RAG cost from different angles, and three of them are practitioner-immediately-useful.

**Test-time strategies that need no retraining.** Test-Time Strategies for More Efficient and Accurate Agentic RAG ([Zhang et al., Adobe Research, 2026-03-12](https://arxiv.org/abs/2603.12396)) sits on top of Search-R1 and adds two modules: contextualization and de-duplication. +5.6% EM and -10.5% turns on multi-hop QA, no retraining. The de-dup pattern in particular is generally useful — if your iterative RAG retrieves the same document twice, the second retrieval is wasted compute and wasted context. Doctor-RAG ([Jiao et al., 2026-04-01](https://arxiv.org/abs/2604.00865)) decouples failure diagnosis from repair with prefix reuse; even partial adoption — just the failure-diagnosis stage as a circuit breaker — pays off vs the standard "did it fail; rerun from scratch" pattern. AutoSearch ([Sun et al., 2026-04-19](https://arxiv.org/abs/2604.17337)) lets the agent learn its own search depth via RL with self-answering reward — minimum-sufficient depth, not a fixed hyperparameter.

**Measurement harnesses arrive.** McCleary and Ghawaly's BCAS ([2026-03-09](https://arxiv.org/abs/2603.08877)) is a budget-constrained agentic-search harness across 6 LLMs and 3 QA benchmarks. The findings are practitioner defaults: hybrid lexical+dense retrieval with lightweight reranking gives the largest average accuracy gain; search depth helps to a small cap; completion budget matters most on synthesis-heavy tasks. The reproducibility of the harness is itself the contribution — practitioners can re-run it on their own LLM choices.

**The retrieval-replacement thread strengthens.** Corpus2Skill ([Sun, Wei, Hsieh, 2026-04-16](https://arxiv.org/abs/2604.14572)) replaces top-k retrieval with hierarchical agent navigation over a distilled skill tree; outperforms dense retrieval, RAPTOR, and agentic-RAG baselines on enterprise QA. Combined with Keyword Search Is All You Need from Phase 2, the kept set now has two strong "do not retrieve, do something else" papers from independent groups.

**Reranker design surfaces new dimensions.** RRPO ([Wu et al., 2026-04-02](https://arxiv.org/abs/2604.02091)) is the cleanest expression of the rerank-for-utility direction — RL with LLM-generation quality as reward, no human relevance labels, beats RankZephyr. AdaRankLLM ([Feng et al., 2026-04-17](https://arxiv.org/abs/2604.15621)) reframes adaptive RAG: it is no longer about whether to retrieve at all (LLMs got noise-robust enough that the necessity question matters less), it is about noise filtering. FRESCO ([An et al., 2026-04-14](https://arxiv.org/abs/2604.14227)) documents that rerankers consistently prefer older, semantically richer documents over recent factually-current ones — instruction tuning recovers up to +27% on evolving-knowledge tasks. Prism-Reranker ([Zhang, 2026-04-26](https://arxiv.org/abs/2604.23734)) changes what rerankers output: not just a score but a contribution statement and a rewritten evidence passage, eliminating the token cost of dumping full documents into context.

**The graph-vs-vector question gets a new answer.** Do We Still Need GraphRAG? ([Fan et al., 2026-04-01](https://arxiv.org/abs/2604.09666)) introduces RAGSearch and shows that under agentic search, the dense-RAG vs GraphRAG performance gap shrinks substantially — agentic interaction implicitly compensates for the absence of explicit graph structure.

**The inflection here**: efficiency stops being a side-note and becomes the unifying research target. Where Phase 2 papers asked "does this technique work?", Phase 4 papers ask "does this technique work cheaply?" The practitioner gets a deeper bench of efficiency tools and a clearer picture of which knobs actually move the cost-accuracy frontier.

### Phase 5: Mid-April – May 2026 — the inflection: rerank-for-utility, latent loops, and "no embedder" arrive together

Phase 5 is short (4 papers) but unusually concentrated. Three of the four are direct continuations of Phase 3 / Phase 4 threads, now sharper.

**The training-free reranker takes its strongest form.** CAR ([Song et al., 2026-05-06](https://arxiv.org/abs/2605.04495)) is the LCR group's three-month follow-up. Same generator-confidence mechanism, but with a query-level gate: skip reranking on already-confident queries. The gate makes CAR cheaper than LCR in production by adding latency only when needed. +25.4% YesNo reranker improvement under Contriever; gains correlate with downstream generation quality. As of the window's end, CAR is the lowest-friction reranking pilot in the kept set.

**The "no embedder" position takes its strongest form.** Direct Corpus Interaction ([Li et al., 2026-05-03](https://arxiv.org/abs/2605.05242)) is the strongest version of the retrieval-replacement thread — agent uses general-purpose terminal tools (grep, file reads, shell commands, lightweight scripts) on the raw corpus; no embedder, no vector index, no retrieval API; outperforms strong sparse, dense, AND reranking baselines on BEIR, BRIGHT, and BrowseComp-Plus. The author list is unusually deep for a preprint (Choi, Zou, Han, Lin among them). The empirical claim is unusually strong. The next 2-3 months of replication attempts will determine whether this is a real shift or a setup-specific result.

**Latent loops appear.** LatentRAG ([Zheng and Worring, 2026-05-07](https://arxiv.org/abs/2605.06285)) shifts both reasoning and retrieval into continuous latent space — latent tokens for thoughts and subqueries generated in a single forward pass, eliminating the autoregressive-thought latency that defines current agentic RAG. This is the most structurally aggressive efficiency claim in the kept set. Track it; do not deploy it.

**Specialized rerankers for agent-specific failures.** MemReranker ([Li et al., 2026-05-07](https://arxiv.org/abs/2605.06132)) targets three failure modes specific to agent-memory retrieval — score miscalibration, ranking degradation under temporal/causal queries, no dialogue-context disambiguation — with multi-teacher distillation into a 0.6B/4B Qwen3-Reranker family. The diagnostic generalizes beyond memory: any reranker handling temporal or causal queries hits these failure modes.

**The inflection here**: in early May, three independent answers to "what should retrieval for an agent look like" landed in the same week. They do not converge. Training-free LLM-confidence reranking (CAR) keeps the standard pipeline and improves the rerank stage; Direct Corpus Interaction throws out the pipeline and lets the agent search the corpus directly; LatentRAG keeps the pipeline but moves it into latent space. The practitioner needs to pick one of these to track over the next quarter; my read is that CAR is the lowest-risk pilot, DCI is the one with the largest implications if it replicates, and LatentRAG is the one to watch for follow-up work.

---

## Where things stand now (early May 2026 — the practitioner's view)

### Mature enough to use today

- **Hybrid retrieval (dense + sparse) merged via Reciprocal Rank Fusion**, with a cross-encoder reranker on top. The kept set converges on this from at least four angles: McCleary and Ghawaly's BCAS finds it gives the largest average accuracy gain under budget; Higress-RAG uses it as the production default; Self-MedRAG codifies the BM25 + Contriever + RRF + NLI recipe; Rumble et al. confirm cross-encoders reliably help on production-scale knowledge-graph data. If you are starting an LLM-agent system today, this is the empirically-supported default.
- **Allocate test-time compute to reranking before reasoning.** Sharifymoghaddam and Lin's Effective Token Cost analysis is the most actionable finding of the window for budgeted systems: moderate listwise reranking gives larger accuracy gains than equivalent compute spent on additional reasoning steps.
- **Multilingual context pruning fused into the reranker.** XProvence is open-weights on Hugging Face, supports 100+ languages via cross-lingual transfer from 16, and adds zero-cost pruning (no extra forward pass). If your application has any non-English content, this is off-the-shelf today.
- **Forward-index compression for LSR (DotVByte / StreamVByte).** Pure plumbing, drop-in.

### Worth piloting

- **Training-free LLM-confidence rerankers (LCR / CAR).** Zero retraining, plug-and-play, query-level gating in CAR avoids the unnecessary-latency objection. CAR is the strongest in the kept set as of May 2026; LCR is the simpler reference. Pilot on your real query distribution and measure both NDCG@5 and downstream generation quality.
- **Learned-sparse retrieval (LACONIC).** If your retrieval cost is dominated by GPU dense-retriever inference or vector-index RAM, the 71% memory savings and CPU-deployable serving are practical. The MTEB #15 ranking gives an externally-verifiable quality floor.
- **Agent-callable retrieval primitives (A-RAG pattern).** If you are using a frontier LLM with reliable tool-calling, expose keyword search, semantic search, and chunk-read as separate tools and let the model orchestrate. More flexible than picking one retriever upfront; scales with model capability.
- **Corpus2Skill (distill the corpus into a navigable skill tree).** Heavy offline cost, low serve-time cost. Worth piloting if your corpus is stable and your queries are exploratory; less attractive if your corpus updates frequently.
- **Doctor-RAG-style failure diagnosis as a circuit breaker.** Even just the failure-diagnosis stage — without the full repair mechanism — replaces the wasteful "did it fail; rerun" pattern.
- **PruneRAG's Evidence Forgetting Rate as a metric.** Adopt the metric without the architecture; it tells you when iterative depth is dropping evidence.

### Still research, do not put in production

- **Direct Corpus Interaction (DCI / "agent uses grep").** Strongest preprint in the window, but unreplicated. The operational implications of removing the embedder are too large to commit on a single paper. Re-evaluate at the end of Q3 2026.
- **LatentRAG (latent-space reasoning and retrieval).** Structurally novel; eliminates autoregressive-thought latency. Two-author paper; track for follow-up replications.
- **TreePS-RAG / RRPO (process-supervision RL for agentic RAG).** Methodologically clean but training-time investment that production teams should adopt downstream of someone else doing the heavy lifting. Track for the off-the-shelf checkpoint.
- **Prism-Reranker's "reranker outputs more than a score."** The contribution-statement + evidence-passage output is a real practitioner pain point, but the kept set has not yet shown follow-ups adopting the format. Pilot if the token-savings story is large for you; otherwise wait.
- **GraphRAG.** Fan et al. say agentic interaction closes most of the dense-vs-graph gap; older Phase 1 papers (Oladokun's PCR diagnostic) say structural correctness still favors graphs. The field has not settled.

### What did not change across the 6 months

- **No consensus benchmark for agentic RAG.** BrowseComp-Plus, RAGSearch, FRESCO, BCAS, RAGBench, STaRK, MTEB Retrieval, BEIR, and BRIGHT all appear in the kept set; no two papers use exactly the same evaluation slate. Comparisons across papers remain hard.
- **No accepted answer on whether GraphRAG is worth the operational cost** once an agent is in the loop.
- **No production-ready latent-space reasoning.** LatentRAG is the first kept-set paper proposing it; it is too early to evaluate.
- **Cold-start retrieval coverage** remains a first-order failure mode (Lemdiasova and Zmanovskii). Rerankers do not fix it.

---

## Papers, by theme

### Theme A — Vector-vs-non-vector / retrieval-replacement

The trajectory's defining argument. Five papers, three independent groups, two strong "no embedder" positions by May.

- **Rethinking Retrieval: From Traditional RAG to Agentic and Non-Vector Reasoning Systems in the Financial Domain** — Lumer et al., arXiv, 2025-11-22. First systematic head-to-head on SEC filings; vector-based agentic RAG with hybrid + metadata wins 68% of comparisons; preprocessing cost is the hidden non-vector advantage. Traction: gaining-traction (sets the agenda); confidence medium. → [link](https://arxiv.org/abs/2511.18177)
- **Keyword search is all you need: Achieving RAG-Level Performance without vector databases using agentic tool use** — Subramanian et al. (AWS), arXiv, 2025-12-19. Tool-using agent with only basic keyword search reaches ≥90% of vector-RAG performance; cited downstream as the headline of the no-embedder thread. Traction: high-confidence-prominent; confidence medium-high. → [link](https://arxiv.org/abs/2602.23368)
- **Don't Retrieve, Navigate: Distilling Enterprise Knowledge into Navigable Agent Skills (Corpus2Skill)** — Sun, Wei, Hsieh, arXiv, 2026-04-16. Distill corpus into hierarchical skill directory offline; agent navigates at serve time; outperforms dense retrieval, RAPTOR, and agentic-RAG baselines on enterprise QA. Traction: high-confidence-prominent; confidence high. → [link](https://arxiv.org/abs/2604.14572)
- **Beyond Semantic Similarity: Rethinking Retrieval for Agentic Search via Direct Corpus Interaction (DCI)** — Li et al., arXiv, 2026-05-03. Agent uses grep + file reads + shell commands on raw corpus; no embedder, no vector index; outperforms strong sparse, dense, AND reranking baselines on BEIR, BRIGHT, BrowseComp-Plus. Strongest "no embedder" claim of the window. Traction: high-confidence-prominent; confidence high. → [link](https://arxiv.org/abs/2605.05242)
- **MCP vs RAG vs NLWeb vs HTML** — Steiner, Peeters, Bizer, arXiv, 2025-11-28. Four-way controlled comparison across four LLM backbones; RAG, MCP, and NLWeb all beat raw HTML; no single structured-interface family wins. Traction: gaining-traction; confidence medium-high. → [link](https://arxiv.org/abs/2511.23281)

### Theme B — Rerank-for-LLM-utility (training-free)

The lowest-friction reranker direction in the window. Two papers from the same group; a third (FRESCO) documents the failure mode the direction addresses.

- **LLM-Confidence Reranker (LCR)** — Song et al., arXiv, 2026-02-14. Score documents by LLM confidence (Maximum Semantic Cluster Proportion) over multinomial samples; +20.6% NDCG@5 over fine-tuned reranker baselines using only 7-9B LLMs. Traction: high-confidence-prominent; confidence high. → [link](https://arxiv.org/abs/2602.13571)
- **CAR: Query-Guided Confidence-Aware Reranking** — Song et al., arXiv, 2026-05-06. LCR follow-up; same confidence mechanism plus a query-level gate (skip reranking when query-only confidence is high); +25.4% YesNo reranker under Contriever; ranking gains correlate with downstream generation quality. Lowest-risk reranking pilot in the kept set. Traction: high-confidence-prominent; confidence high. → [link](https://arxiv.org/abs/2605.04495)
- **FRESCO: Benchmarking and Optimizing Re-rankers for Evolving Semantic Conflict** — An et al., arXiv, 2026-04-14. Benchmark for time-varying ground truth; rerankers consistently prefer older, semantically richer documents over recent factually-current ones; instruction tuning recovers up to +27%. Traction: high-confidence-prominent; confidence high. → [link](https://arxiv.org/abs/2604.14227)

### Theme C — Rerank-for-LLM-utility (trained / RL)

The training-time mirror of Theme B. Industry-team contributions; production-relevant recipes.

- **Generative Reasoning Re-ranker (GR2)** — Liang et al. (Meta-affiliated), arXiv, 2026-02-08. Three-stage training: semantic-ID encoding, mid-train, SFT on reasoning traces, then RL-tune. Replicable for ranking tasks beyond recommendations. Traction: high-confidence-prominent; confidence medium-high. → [link](https://arxiv.org/abs/2602.07774)
- **RRPO: Optimizing RAG Rerankers with LLM Feedback via RL** — Wu et al., arXiv, 2026-04-02. RL with LLM-generation quality as reward; no human labels; beats RankZephyr (strong listwise baseline) on knowledge-intensive QA; reference-anchored deterministic baseline for stability. Traction: high; confidence high. → [link](https://arxiv.org/abs/2604.02091)
- **AdaRankLLM: Rethinking the Necessity of Adaptive RAG through the Lens of Adaptive Listwise Ranking** — Feng et al., arXiv, 2026-04-17. Reframes adaptive retrieval as noise filtering rather than necessity gating; two-stage progressive distillation brings capability to smaller open-source LLMs (3 datasets x 8 LLMs). Traction: medium-high; confidence medium-high. → [link](https://arxiv.org/abs/2604.15621)

### Theme D — Hybrid retrieval and production stacks

The empirically-supported practitioner default and its production-architecture instantiations.

- **Higress-RAG: Holistic Optimization Framework for Enterprise RAG** — Lin, arXiv, 2025-12-30. Reference architecture: Adaptive Routing + Hybrid Retrieval (RRF) + Semantic Caching (50ms) + CRAG, on Model Context Protocol. The integration play of Phase 2. Traction: gaining-traction; confidence medium. → [link](https://arxiv.org/abs/2602.23374)
- **Self-MedRAG: Self-Reflective Hybrid RAG** — Ryan et al., arXiv, 2026-01-08. BM25 + Contriever + RRF + NLI verification + query reformulation; recipe is portable beyond medical QA. Traction: medium; confidence medium. → [link](https://arxiv.org/abs/2601.04531)
- **Comparative Analysis of Neural Retriever-Reranker Pipelines for RAG over Knowledge Graphs in E-commerce** — Rumble et al., arXiv, 2025-12-14. Pipeline grid on STaRK production-scale benchmark; cross-encoders reliably lift retrieval precision when added. Traction: medium; confidence medium. → [link](https://arxiv.org/abs/2602.22219)
- **Is Agentic RAG worth it?** — Ferrazzi et al., arXiv, 2026-01-12. Empirical comparison of basic vs enhanced vs agentic RAG; no paradigm dominates strictly; choice depends on query complexity and cost. Traction: medium; confidence medium. → [link](https://arxiv.org/abs/2601.07711)

### Theme E — Agentic-RAG efficiency

Phase 4's unifying research target. Six papers attacking per-query cost from different angles.

- **Test-Time Strategies for More Efficient and Accurate Agentic RAG** — Zhang et al. (Adobe Research), arXiv, 2026-03-12. Two test-time modules on Search-R1 (contextualization + de-duplication); +5.6% EM, -10.5% turns; no retraining. Free improvement for anyone using Search-R1. Traction: high-confidence-prominent; confidence medium-high. → [link](https://arxiv.org/abs/2603.12396)
- **Doctor-RAG: Failure-Aware Repair for Agentic RAG** — Jiao et al., arXiv, 2026-04-01. Decouples failure diagnosis from repair; reuses validated reasoning prefixes; circuit-breaker pattern for production. Traction: medium-high; confidence medium-high. → [link](https://arxiv.org/abs/2604.00865)
- **AutoSearch: Adaptive Search Depth for Efficient Agentic RAG via RL** — Sun et al., arXiv, 2026-04-19. Self-answering reward identifies minimal-sufficient depth; "stop when you know" operationalized. Traction: medium-high; confidence medium-high. → [link](https://arxiv.org/abs/2604.17337)
- **PruneRAG: Confidence-Guided Query Decomposition Trees** — Jiao et al., arXiv, 2026-01-16. Adaptive node expansion + confidence-guided accept/prune; introduces Evidence Forgetting Rate as a portable metric. Traction: medium; confidence medium. → [link](https://arxiv.org/abs/2601.11024)
- **TreePS-RAG: Tree-based Process Supervision for RL in Agentic RAG** — Zhang et al. (MIT/CUHK), arXiv, 2026-01-11. Monte-Carlo over rollout trees for online process supervision; no intermediate labels. Methodologically clean; not yet off-the-shelf. Traction: medium-high; confidence medium-high. → [link](https://arxiv.org/abs/2601.06922)
- **LatentRAG: Latent Reasoning and Retrieval for Efficient Agentic RAG** — Zheng and Worring, arXiv, 2026-05-07. Both reasoning and retrieval in continuous latent space; eliminates autoregressive-thought latency in a single forward pass. Most structurally aggressive efficiency claim of the window. Traction: high-confidence-prominent; confidence medium-high. → [link](https://arxiv.org/abs/2605.06285)

### Theme F — Reranker pipeline design and effectiveness

Test-time compute allocation; multivector pipelines; cost analysis. Anchored by Sharifymoghaddam and Lin.

- **Rerank Before You Reason: Effective Token Cost in Deep Search Agents** — Sharifymoghaddam, Lin, arXiv, 2026-01-20. Introduces Effective Token Cost metric on BrowseComp-Plus; moderate listwise reranking gives larger accuracy gains than equivalent reasoning-budget. Most directly actionable Phase 2 finding. Traction: high-confidence-prominent; confidence high. → [link](https://arxiv.org/abs/2601.14224)
- **Multivector Reranking in the Era of Strong First-Stage Retrievers** — Martinico et al. (Italian IR group), arXiv, 2026-01-08. Replaces ColBERT-family token-level "gather" with single-vector LSR; multivector retrieval becomes standard two-stage. Migration path for production ColBERT. Traction: high; confidence medium-high. → [link](https://arxiv.org/abs/2601.05200)
- **Col-Bandit: Zero-Shot Query-Time Pruning for Late-Interaction Retrieval** — Pony et al., arXiv, 2026-02-02. Casts late-interaction reranking as Top-K identification with statistical bounds; drop-in, no retraining. Traction: medium-high; confidence medium-high. → [link](https://arxiv.org/abs/2602.02827)
- **Quantifying the Accuracy and Cost Impact of Design Decisions in Budget-Constrained Agentic LLM Search (BCAS)** — McCleary, Ghawaly, arXiv, 2026-03-09. Reproducible measurement harness; 6 LLMs x 3 QA benchmarks; produces practitioner defaults. Traction: medium-high; confidence medium-high. → [link](https://arxiv.org/abs/2603.08877)

### Theme G — Reranker output design and specialization

Phase 4-5 sub-thread on what rerankers should emit and on agent-specific failure modes.

- **Prism-Reranker: Beyond Relevance Scoring** — Zhang, arXiv, 2026-04-26. Emits relevance verdict + contribution statement + self-contained evidence passage; eliminates token cost of dumping full documents into context; Qwen3.5 backbone, 0.8B/2B/4B/9B sizes; +1.54 NDCG@10 on BEIR-QA. Traction: high-confidence-prominent; confidence high. → [link](https://arxiv.org/abs/2604.23734)
- **MemReranker: Reasoning-Aware Reranking for Agent Memory Retrieval** — Li et al., arXiv, 2026-05-07. Targets three failure modes (score miscalibration, ranking degradation under temporal/causal queries, no dialogue-context disambiguation) via multi-teacher distillation into 0.6B/4B Qwen3-Reranker family. Diagnostic generalizes beyond memory. Traction: medium-high; confidence medium-high. → [link](https://arxiv.org/abs/2605.06132)
- **XProvence: Zero-Cost Multilingual Context Pruning for RAG** — Mohamed et al. (Naver), arXiv, 2026-01-26. Pruning fused into reranker (no extra forward pass); 16 trained languages, 100+ supported via cross-lingual transfer; weights released. Off-the-shelf today for non-English settings. Traction: high-confidence-prominent; confidence medium-high. → [link](https://arxiv.org/abs/2601.18886)

### Theme H — Learned-sparse retrieval

The Phase 2-3 LSR resurgence. Two complementary papers (model + index plumbing).

- **LACONIC: Dense-Level Effectiveness for Scalable Sparse Retrieval** — Xu et al., arXiv, 2026-01-04. Llama-3-based LSR with two-phase training (weakly-supervised pre-finetune + hard-negative SFT); 8B variant 60.2 nDCG on MTEB Retrieval (#15 leaderboard); 71% less index memory than dense; CPU-deployable. Traction: high-confidence-prominent; confidence high. → [link](https://arxiv.org/abs/2601.01684)
- **Forward Index Compression for Learned Sparse Retrieval** — Bruch et al. (Italian IR group), arXiv, 2026-02-05. StreamVByte best out-of-the-box; new DotVByte tailored to inner-product computation; MsMarco evaluation. Engineering plumbing for LSR adoption. Traction: high; confidence high. → [link](https://arxiv.org/abs/2602.05445)

### Theme I — Diagnostics, taxonomies, and graph-vs-vector

Reference papers for orientation and the graph-vs-vector evidence base.

- **Diagnosing LLM-based Rerankers in Cold-Start Recommender Systems** — Lemdiasova, Zmanovskii, arXiv, 2026-02-09. Cross-encoder reranker HR@10 = 0.008 vs popularity baseline 0.268 in cold-start movie recommendation; bottleneck is retrieval coverage (recall@200 = 0.109), not reranker capacity. The diagnostic generalizes — diagnose retrieval coverage before blaming the reranker. Traction: high; confidence high. → [link](https://arxiv.org/abs/2604.16318)
- **Do We Still Need GraphRAG? Benchmarking RAG and GraphRAG for Agentic Search Systems** — Fan et al., arXiv, 2026-04-01. Introduces RAGSearch benchmark; under agentic search, dense-RAG-vs-GraphRAG gap shrinks substantially; agentic interaction implicitly compensates for absence of explicit graph structure. Traction: high; confidence high. → [link](https://arxiv.org/abs/2604.09666)
- **Path-Constrained Retrieval (PCR)** — Oladokun, arXiv, 2025-11-23. Restricting semantic search to graph-reachable nodes gives 100% structural consistency vs 24-32% for vector and hybrid baselines on small PathRAG-6 benchmark; technique is research-grade, but the diagnostic (vector retrieval frequently returns structurally disconnected context) is the operational point. Traction: signal-uncertain; confidence low. → [link](https://arxiv.org/abs/2511.18313)
- **A-RAG: Scaling Agentic RAG via Hierarchical Retrieval Interfaces** — Du et al., arXiv, 2026-02-03. Three agent-callable retrieval primitives (keyword + semantic + chunk-read); agent chooses dynamically; matches or exceeds existing approaches with comparable or lower retrieved-token count; scales with model size. Traction: high-confidence-prominent; confidence medium-high. → [link](https://arxiv.org/abs/2602.03442)
- **Taxonomy of the Retrieval System Framework** — Shah et al., arXiv, 2026-01-27. Four-layer stack (Representation, Granularity, Orchestration, Robustness) with failure modes named per layer. Design-checklist reference. Traction: medium; confidence medium. → [link](https://arxiv.org/abs/2601.20131)
- **IMRNNs: Interpretable Dense Retrieval via Embedding Modulation** — Saxena et al., arXiv, 2026-01-27. Bidirectional inference-time adapters on dense retrievers; query-conditioned document modulation + corpus-feedback-conditioned query modulation; no reranker forward pass. Traction: medium; confidence medium. → [link](https://arxiv.org/abs/2601.20084)

---

## Outliers

The kept set is unusually coherent for a 6-month, 36-paper digest. The only paper that does not slot cleanly into one theme is **MemReranker**, which sits at the intersection of Theme G (reranker output / specialization) and the agent-memory area excluded by the operator's scope rules; the operator's override permits memory papers that teach a generalizable reranker insight, and MemReranker's three-failure-modes diagnostic does. It appears in Theme G with that framing.

The other near-outlier — **Path-Constrained Retrieval** — is structurally a Theme I paper (graph-vs-vector evidence) but methodologically a single-author small-benchmark preprint that does not reach the empirical bar of the other Theme I papers; its inclusion is justified by the diagnostic finding (vector retrieval frequently returns structurally disconnected context), not by the technique itself.

---

## Notes for the next 6 months

- **Watch DCI replication.** Direct Corpus Interaction is the strongest preprint in the kept set and the one with the largest practitioner implications. If it replicates beyond the original setup over the next 2-3 months, reconsider the vector-store paradigm in earnest.
- **Watch CAR adoption.** CAR is the lowest-risk training-free reranker pilot today; if it appears as a baseline in subsequent papers, the rerank-for-utility direction is settling.
- **Watch the reranker-output dimension.** Prism-Reranker proposes that rerankers should emit contribution statements and rewritten evidence passages; the kept set has not yet shown follow-ups. If a second independent paper adopts this output shape, it becomes a real direction.
- **Watch latent-space agentic RAG.** LatentRAG is the first kept-set paper proposing it. Track for replications and for whether the latent representations are stable enough to interpret.
- **The benchmark fragmentation problem.** The kept set uses BrowseComp-Plus, RAGSearch, FRESCO, BCAS, RAGBench, STaRK, MTEB Retrieval, BEIR, and BRIGHT. Cross-paper comparisons remain hard. A consolidation paper would be the highest-value contribution the field could make in Q3 2026.

---

## Full list

See [`ops/paper-synthesizer/2026-W19-6mo-papers.md`](../2026-W19-6mo-papers.md) for the unsynthesized table of every kept paper plus the full dropped-with-rationale list.
