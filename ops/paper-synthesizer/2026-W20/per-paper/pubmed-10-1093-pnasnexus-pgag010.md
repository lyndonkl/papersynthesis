---
paper_id: pubmed:10.1093/pnasnexus/pgag010
title: "What is emergence, after all?"
authors: ["Abbas K Rizi"]
date: 2026-01-19
source: pubmed
url: https://academic.oup.com/pnasnexus/article/doi/10.1093/pnasnexus/pgag010/8429832
extraction_path: ops/paper-extractor/2026-W20/pubmed-10-1093-pnasnexus-pgag010.md
synthesized_on: 2026-05-14
mode: a
full_text_available: true
---

## Headline
Emergence is not metaphysical surplus but a measurable, operational property: it is what you have when a many-to-one coarse-graining from micro-state to macro-state stays predictive, and its measurable signatures are an order parameter turning on at a critical threshold, diverging correlation length and relaxation time, and rising mutual information / transfer entropy / effective-information-under-coarse-graining.

## Summary
Rizi argues that emergence should be defined as a predictive coarse-graining: a many-to-one map `F: (x₁,...,xₙ) ↦ (X₁,...,Xₙ′)` with `N′ < N` whose macro-variables retain predictive power and have "explanatory autonomy" from the substrate. The supporting argument is a chain of canonical examples worked at definition depth — temperature sharpening as `1/N → 0`, magnetization as a symmetry-broken order parameter `m(T)` below `Tc`, renormalization-group fixed points producing universality classes that bind microscopically distinct systems (liquid–gas ≡ ferromagnet), and duality (sine–Gordon ↔ Thirring, AdS/CFT) showing the same emergent physics arising from ontologically distinct variables — extended to networks (Erdős–Rényi percolation at `pc`) and epidemics (herd immunity at `πR* = 1 − 1/R₀`). The paper closes by adjudicating the philosophical fault line: weak emergence (in-principle-derivable but practically autonomous) is admitted as scientifically respectable; strong emergence (irreducible higher-level causal powers) is dismissed as "stepping outside the scope of scientific method," while top-down causation is permitted as constraint without law-violation.

## Specifics

**The operational definition (verbatim).** "Emergence occurs when there exists a many-to-one map from a micro-level theory to a macro-level theory, such that the macro description remains predictive." Framed as "lossy data compression in which only the information needed for prediction survives." The paper does *not* specify a quantitative predictivity threshold or comparison baseline — that gap is left to practitioners.

**What to observe (the measurable signatures of emergence).** Five diagnostics, asserted as a bundle rather than ranked:
- An **order parameter** that is zero in the symmetric phase and non-zero past the threshold (e.g., `m(T) > 0` for `T < Tc`).
- **Correlation length and relaxation time diverge** at the transition (peak in finite systems).
- **Mutual information rises near criticality**; **transfer entropy** reveals "increasingly predictive interactions."
- **Effective information increases under coarse-graining** — the causal-test signature.
- **Universality**: macroscopic behavior is "largely independent of microscopic details," i.e., the coarse-grained description is stable under RG flow toward a fixed point.

**Three named mechanism-routes to emergence** (with the paper's own caveat that "criticality is neither the only route to emergence nor trivial to establish empirically"):
1. Equilibrium critical points (continuous phase transitions, symmetry breaking, RG fixed points → universality classes).
2. Nonequilibrium absorbing-state transitions ("often fall into the directed percolation universality class").
3. Network / connectivity transitions (giant-component formation at percolation threshold `pc`; herd immunity).

**The network/epidemic transfer (most directly applicable to systems-of-interacting-agents thinking).** The same apparatus carries over: in Erdős–Rényi graphs a giant component appears past `pc`; in mean-field epidemics herd immunity locks in past `πR* = 1 − 1/R₀` (measles: `R₀ ~ 15`). The paper explicitly contrasts mean-field with "real populations [that] form heterogeneous, spatially embedded networks" and flags degree-based interventions: "immunizing a highly connected node can disrupt many transmission routes." Mesoscale (community-level) coarse-grainings are recommended over either whole-population or per-agent: "at this intermediate level — specifically, how communities interact — it can capture most of the predictive signals."

**Substrate independence as evidence of genuine emergence.** Microscopically distinct systems sharing macro-behavior (the liquid–gas / ferromagnet universality class is the canonical case; duality is the more ambitious case) is offered as the strongest evidence that the macro-property is real rather than an artifact of micro-detail.

**Weak vs strong emergence — the verdict.** Weak emergence ("in principle, possible but practically difficult to derive from purely microscopic descriptions") is admitted. Strong emergence (irreducible higher-level laws that allegedly violate substrate dynamics) "amounts to introducing new causal principles not anchored in substrate dynamics, and thus steps outside the scope of scientific method." Top-down causation is admitted as higher-level structures "constraining or guiding" components "without violating the underlying laws" — but the mechanism for constraint-without-violation is asserted rather than spelled out.

**Hedging preserved verbatim** (load-bearing for the systems-thinking reader):
- "Current evidence favors near-criticality over exact self-tuned criticality" in biological systems.
- "Power laws and avalanches are insufficient on their own" to establish criticality empirically.
- "Distance-to-criticality" framing is preferred to "the brain sits precisely at criticality."
- Consciousness "could, in principle, arise from entirely different physical substrates" — hedged, and the paper concedes consciousness and life "do not neatly correspond to a phase transition."

**Gaps the paper leaves open (relevant when porting the framework to hierarchical multi-agent orchestrators).**
- "Predictive" is undefined quantitatively — no threshold, no baseline-comparison protocol.
- The information-theoretic diagnostics (mutual information, transfer entropy, effective information) are bundled, not adjudicated — when they agree, when they disagree, which is primary, is left open.
- The weak/strong binary may oversimplify a spectrum (the paper concedes some phenomena "do not neatly correspond to a phase transition").
- The mechanism of constraint-without-violation in top-down causation is left implicit.

**Type and posture.** Position / perspective piece (secondary: theoretical synthesis / pedagogical primer). Framing is assertive — "is" rather than "may be" — so this is a defended ontology, not a hedged survey. Anchored historically in Aristotle, Mill, P.W. Anderson's "more is different"; methodologically in the Wilson-lineage renormalization group, directed-percolation universality, and AdS/CFT.

## Why this matters in this run's context

Reference frame for Cluster 1 (Emergence becomes a measurable property when you fix the right interaction-graph topology and look at competing feedbacks at the right scale): supplies the five diagnostic signatures of emergence and the operational coarse-graining definition that lets the orchestrator instrument "emergent behavior" as a measurement rather than a hand-wave.
