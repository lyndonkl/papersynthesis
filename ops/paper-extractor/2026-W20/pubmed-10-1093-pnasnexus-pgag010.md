---
paper_id: pubmed:10.1093/pnasnexus/pgag010
title: "What is emergence, after all?"
authors: ["Abbas K Rizi"]
date: 2026-01-19
source: pubmed
url: https://academic.oup.com/pnasnexus/article/doi/10.1093/pnasnexus/pgag010/8429832
doi: 10.1093/pnasnexus/pgag010
extracted_on: 2026-05-14
passes_completed: [1, 2]
full_text_available: true
---

## Pass 1 — Inspectional reading

### Metadata observed at inspectional level
- Journal: PNAS Nexus, Volume 5, Issue 2
- Accepted: December 27, 2025; Published: January 19, 2026
- Section headings visible from the article page:
  - Levels of description
  - Many-to-one maps and coarse-graining
  - Reductionism and "theory of everything"
  - A new ontology
  - Effective theories
  - Onset of emergence, symmetry breaking, and criticality
  - Renormalization and universality
  - Duality and emergence
  - Emergence in networks and social systems
  - Emergence of herd immunity in a population
  - Weak versus strong emergence
  - Conclusion and discussion

### The Five Cs

**1. Category** — Position / perspective piece (secondary: theoretical synthesis / pedagogical primer). The headings ("A new ontology," "Weak versus strong emergence," "Conclusion and discussion") and the framing language ("clarifies emergence as a measurable and physically grounded phenomenon") indicate a conceptual essay arguing a stance, not an empirical study or a new model. It functions as a primer that surveys the formal machinery (coarse-graining, effective theories, renormalization, universality, duality) in service of a single thesis about what emergence *is*.

**2. Context** — Sits in the long-running debate over emergence in complex systems, anchored historically by Aristotle ("the whole is something besides the parts"), Mill's mechanical-vs-chemical distinction, and P.W. Anderson's "more is different," with contemporary touchpoints in supervenience and causal autonomy. The networks / social-systems and herd-immunity sections place it adjacent to the statistical-physics-of-collective-behavior literature.

**3. Correctness (first-glance)** — No first-glance concerns. The piece invokes well-established formalism (renormalization group, symmetry breaking, criticality, universality) and uses canonical examples (temperature, magnetism, herd immunity) that fit the standard physicist's account of emergence. The risk profile of a perspective piece is over-claiming a settled ontology — the section "Weak versus strong emergence" suggests the author engages with that fault line rather than papering over it, which is the right move.

**4. Contributions** — Claims to demystify emergence by framing it as "a measurable and physically grounded phenomenon" rather than a metaphysical surplus, showing how collective behavior arises from local interactions under global constraints. The structure suggests four packaged moves: (a) recasting emergence through coarse-graining and many-to-one maps, (b) tying emergence to symmetry breaking and criticality, (c) extending the apparatus to networks / social systems / epidemics, and (d) adjudicating the weak-vs-strong-emergence debate. Framing is assertive — "is" rather than "may be" — so this is a position paper defending a particular ontology, not a hedged survey.

**5. Clarity** — `clear`. Title and abstract align; section structure is transparent and tracks a single argumentative arc from formal definition through canonical examples to the philosophical payoff. No acronym soup; example domains (magnetism, herd immunity) are universally accessible.

### One-line summary
A perspective piece arguing that emergence is a measurable, physically grounded phenomenon produced by coarse-graining of locally interacting systems under global constraints, illustrated through magnetism, criticality, networks, and herd immunity, and used to adjudicate weak-vs-strong emergence.

## Pass 2 — Content grasp

### Acquisition note
PDF download from `academic.oup.com` was blocked by a Cloudflare browser-integrity challenge (HTTP 403 to curl with browser user-agent). Full text was acquired via Source 2 of the recipe — WebFetch on the article landing page returned the full body across all twelve named sections (>10K chars including methods-equivalent formalism, examples, equations, and conclusion). `full_text_available=true`.

### Main argument and supporting evidence (3–5 sentences)
Rizi argues that emergence is *not* a metaphysical surplus or a mystery, but a precise, operational, measurable feature of physical systems: it is what arises when a *many-to-one coarse-graining map* from a micro-description to a macro-description retains predictive power, and when the resulting macro-variables — order parameters, effective theories, universality classes — have explanatory autonomy from the substrate. The supporting evidence is a chain of canonical physics examples worked at definition-level depth: temperature as a coarse-grained variable that becomes sharp in the thermodynamic limit (fluctuation term `1/N → 0`), magnetization as a symmetry-broken order parameter `m(T)` that turns on below a critical temperature `Tc`, the renormalization-group fixed point that explains universality (the liquid–gas transition sharing a class with ferromagnetism), and duality (sine–Gordon ↔ Thirring; AdS/CFT) showing that "different ontologies can describe the same physics." The argument is then extended beyond physics by transferring the same machinery to networks (Erdős–Rényi percolation transition at `pc`) and epidemics (herd-immunity threshold `πR* = 1 − 1/R₀`, with the firewall/giant-component picture as a network-level order parameter). The paper closes by adjudicating the philosophical fault line: *weak emergence* (the in-principle-derivable but practically autonomous kind) is real and scientifically respectable; *strong emergence* (irreducible higher-level causal powers that allegedly violate substrate dynamics) is dismissed as "stepping outside the scope of scientific method." Hedging is preserved exactly in the extraction below — e.g., the brain "near-criticality" claim and the consciousness claims remain tentative.

### The Big Question
What is the field-of-complex-systems trying to settle here? Whether "emergence" picks out a real, scientifically tractable property of nature — and if so, what *operational test* distinguishes genuinely emergent behavior from sloppy talk about complexity. The broader problem the paper addresses: complex-systems discourse uses "emergence" as a near-mystical placeholder ("vague or mystical references to emergence may sound compelling"), and the field needs a definition that is (a) measurable, (b) grounded in physical mechanism, and (c) sharp enough to exclude the metaphysical reading without ruling out the real phenomenon.

### Specific hypotheses / design claims defended
This is a position paper, so the testable units are *defended claims*, not experimental hypotheses:

1. **Operational definition claim.** Emergence occurs *iff* there exists a many-to-one map `F: (x₁,...,xₙ) ↦ (X₁,...,Xₙ′)` with `N′ < N` such that the macro-description remains predictive — i.e., emergence = predictive coarse-graining.
2. **Effective-theory autonomy claim.** Effective theories (thermodynamics, hydrodynamics, mean-field) are *not* approximations to micro-theories — they are "self-contained, predictive, and often universal descriptions" with their own ontology.
3. **Criticality-as-locator claim.** Continuous phase transitions provide a *locator* for emergence: at `Tc` the order parameter turns on, correlation length and relaxation time diverge (or peak in finite systems), and mutual information / transfer entropy rise — these are the measurable signatures.
4. **Universality claim.** Microscopically distinct systems can share macroscopic behavior (liquid–gas ≡ ferromagnet class), demonstrating "substrate independence" — which is offered as evidence that emergent properties are *real* (not artifacts of micro-detail) because they survive under coarse-graining flow toward an RG fixed point.
5. **Network extensibility claim.** The same apparatus — order parameter, critical threshold, percolation — applies to networks (giant component at `pc`) and to epidemiology (herd immunity at `πR* = 1 − 1/R₀`), demonstrating the framework's scope.
6. **Strong-emergence-is-out-of-scope claim.** Strong emergence (irreducible higher-level laws) "amounts to introducing new causal principles not anchored in substrate dynamics, and thus steps outside the scope of scientific method." Weak emergence is what science is allowed to talk about.
7. **Downward-causation-without-violation claim.** Higher-level structures "can constrain or guide" components "without violating the underlying laws" — top-down causation is admitted, but bounded by substrate dynamics.

### The paper's stated taxonomy of emergence (focus area)
The taxonomy the paper offers is dual-axis rather than a tree:

- **Philosophical axis: weak vs strong emergence.** Weak emergence = collective behavior with "explanatory autonomy" that is "in principle, possible but practically difficult to derive from purely microscopic descriptions." Strong emergence = phenomena that are "fundamentally irreducible," possibly violating physical laws. The paper accepts weak, rejects strong as unscientific.
- **Mechanism axis: routes to emergence.** Three named routes are described, with the explicit caveat that "criticality is neither the only route to emergence nor trivial to establish empirically":
  1. **Equilibrium critical points** (symmetry-breaking continuous phase transitions; RG fixed points → universality classes).
  2. **Nonequilibrium absorbing-state transitions** (irreversible dynamics; "often fall into the directed percolation universality class").
  3. **Network/connectivity transitions** (giant-component formation at percolation threshold `pc`; herd immunity).
- **Substrate-relation axis: duality as same-emergence-from-different-ontologies.** Sine–Gordon ↔ Thirring (boson↔fermion); AdS/CFT (CFT in d dimensions ↔ gravity in d+1) — same emergent physics from "ontologically distinct variables."
- **Epistemological axis: levels of description.** Knowledge is layered ("raw experience → language → higher-order concepts"); what we call emergent depends on the level we are operating at.

### The paper's operational definition (focus area)
The single sharpest operational definition in the paper:

> "Emergence occurs when there exists a many-to-one map from a micro-level theory to a macro-level theory, such that the macro description remains predictive."

Formally: `F: (x₁(tᵢ),...,xₙ(tₖ)) ↦ (X₁(tⱼ′),...,Xₙ′(tₗ′))` with `N′ < N`, "lossy data compression in which only the information needed for prediction survives."

The *measurable tests* the paper offers for distinguishing emergent from non-emergent behavior:
1. **Order parameter turns on at a critical point** (e.g., `m(T) > 0` for `T < Tc`).
2. **Correlation length and relaxation time diverge** (or peak in finite systems) at the transition.
3. **Information-theoretic diagnostics:** "mutual information rises near criticality, transfer entropy reveals increasingly predictive interactions."
4. **Effective information increases under coarse-graining** (causal-test signature).
5. **Universality:** macroscopic behavior is "largely independent of microscopic details" — i.e., the coarse-grained description is stable under RG flow to a fixed point.

Caveats the paper explicitly attaches (hedging preserved):
- "Current evidence favors near-criticality over exact self-tuned criticality" in biological systems.
- "Power laws and avalanches are insufficient on their own" to establish criticality empirically.
- "Distance-to-criticality" framing is preferred to "the brain sits precisely at criticality."

### Practical implications for measuring emergence in multi-agent systems (focus area)
The paper does not address multi-agent AI systems directly, but its apparatus transfers cleanly. The implications visible in the text:

1. **A predictive coarse-graining must exist.** To call an MAS behavior "emergent" rigorously, one must exhibit a many-to-one map `F` from agent-level state to a population-level macro-variable that *retains predictive power*. Without that, the label is the kind of "vague argument" the paper's Persian-tale conclusion warns against.
2. **Look for an order parameter and a critical threshold.** The herd-immunity / percolation transfer to social networks is the most directly applicable template: identify a macroscopic quantity (giant-component size, consensus fraction, infection prevalence, coordination index) that turns on past a control-parameter threshold.
3. **Use information-theoretic measures.** Mutual information, transfer entropy, and effective-information-under-coarse-graining are explicitly cited as "diagnostics that pinpoint the onset of emergence" — these are computable on MAS trajectories.
4. **Substrate independence as evidence of genuine emergence.** If different MAS architectures with distinct agent-level "ontologies" (different model families, different prompting frames, different communication protocols) exhibit the *same* macro-behavior under the same global constraints, that is the universality signal the paper treats as the strongest evidence the macro-property is real, not an artifact.
5. **Heterogeneous network structure matters.** The herd-immunity section explicitly contrasts mean-field (`πR* = 1 − 1/R₀`) with "real populations [that] form heterogeneous, spatially embedded networks," and notes degree-based interventions: "immunizing a highly connected node can disrupt many transmission routes." For MAS, this translates to: high-degree agents (broadcast/relay agents) carry disproportionate weight in collective emergence; coarse-graining cannot ignore degree heterogeneity.
6. **Mesoscale matters.** "A mesoscale theory can clarify what aspects a good coarse-graining should focus on... at this intermediate level — specifically, how communities interact — it can capture most of the predictive signals." For MAS, the community/team level is likely the right coarse-graining target, not the whole population and not individual agents.
7. **Beware strong-emergence framing.** Claims that an MAS exhibits behavior *irreducible* to its components are, per this paper, outside the scope of scientific method. The legitimate move is to admit weak emergence: "in principle derivable but practically autonomous."

### Unfamiliar terms requiring gloss for a non-specialist reader
- **Coarse-graining** — Mapping a fine-grained micro-state onto a smaller set of macro-variables (`N → N′ < N`), discarding micro-detail while preserving enough information for macro-prediction. "Lossy data compression in which only the information needed for prediction survives."
- **Many-to-one map** — A function where many distinct inputs share an output; the formal core of the paper's definition of emergence.
- **Order parameter** — A coarse-grained scalar (or vector) that is zero in the symmetric phase and non-zero in the broken-symmetry phase (e.g., magnetization `m(T)`). "Compresses the full 10²³-spin microstate into a single coarse-grained vector."
- **Critical point / `Tc`** — The control-parameter value at which a continuous phase transition occurs; correlation length and relaxation time diverge there (or peak in finite systems).
- **Symmetry breaking** — At criticality, "the spin-flip symmetry of the Hamiltonian remains intact, but the actual state chooses a specific direction" — the equations stay symmetric, the realized state doesn't.
- **Renormalization group (RG)** — A flow on theory-space generated by iterated coarse-graining; fixed points of the flow are scale-invariant and "attractive along irrelevant directions," producing universality.
- **Universality class** — Set of microscopically distinct systems sharing identical critical exponents (e.g., liquid–gas and ferromagnet in the same class).
- **Effective theory** — A self-contained predictive description in terms of macro-variables (thermodynamics, hydrodynamics, mean-field) that is "not merely an approximation" to the micro-theory.
- **Mean-field theory** — "The zeroth-order effective description" — replaces fluctuating local interactions with their average.
- **Absorbing-state transition** — A nonequilibrium phase transition where the system can fall into configurations it cannot escape; "often fall into the directed percolation universality class."
- **Duality** — A one-to-one dictionary between two ontologically distinct theories that describe the same physics; examples: sine–Gordon ↔ Thirring, AdS/CFT.
- **AdS/CFT correspondence** — Holographic equivalence between a d-dimensional conformal field theory (no gravity) and a (d+1)-dimensional bulk theory with gravity.
- **Giant component** — In a random graph, the connected subgraph that contains a finite fraction of all nodes; appears past the percolation threshold `pc`.
- **Percolation threshold `pc`** — Critical edge probability above which a giant component exists.
- **Basic reproduction number `R₀`** — Expected number of secondary infections per primary in a fully susceptible population (measles: `R₀ ~ 15`).
- **Herd-immunity threshold `πR* = 1 − 1/R₀`** — Vaccinated fraction above which random infection chains die out in a mean-field population.
- **Effective reproduction number `Re = (1 − πR) R₀`** — Adjusted reproduction number after vaccination of fraction `πR`.
- **Mutual information / transfer entropy** — Information-theoretic measures the paper cites as emergence diagnostics; transfer entropy quantifies directional predictive influence.
- **Effective information** — A causal-test quantity that "can increase under coarse-graining" — used as a signature of emergent causal structure.
- **Supervenience** — (Background; implicit) the philosophical claim that higher-level properties depend on lower-level ones without being reducible — the philosophical scaffolding the paper engages without naming heavily.
- **Downward / top-down causation** — Higher-level structures "constraining or guiding" component behavior "without violating the underlying laws."

### Figure-by-figure analysis
The WebFetch rendering of the landing-page article did not include rendered figures or numbered figure captions in the body — equations and section content were preserved but figure objects (which on `academic.oup.com` are loaded as separate image assets) were not. From section content I can identify the *content* the figures presumably illustrate:

- **Coarse-graining schematic** (Many-to-one maps section) — Illustrates the function `F: (x₁,...,xₙ) ↦ (X₁,...,Xₙ′)`. *Takeaway*: many micro-states map to one macro-state; the macro-state retains predictive power.
- **Magnetization vs temperature `m(T)`** (Onset of emergence section) — Order parameter rising from zero below `Tc`. *Takeaway*: visual realization of symmetry breaking and the order-parameter signature of emergence.
- **RG flow** (Renormalization section) — Flow toward a scale-invariant fixed point, with irrelevant directions attracted. *Takeaway*: explains universality.
- **Erdős–Rényi giant-component transition** (Networks section) — Order parameter (giant component size) vs edge probability `p`, with discontinuity at `pc`. *Takeaway*: network analog of a phase transition.
- **Herd-immunity firewall** (Herd immunity section) — Vaccinated nodes forming overlapping clusters that "coalesce" into a global barrier. *Takeaway*: nonlinear collapse of transmission paths past `πR*`.

Figure-by-figure analysis at the granularity of axes / error bars / sample sizes is not possible from the abstract-page rendering. (PDF source unavailable due to Cloudflare; HTML fallback succeeded for text but not embedded figures.)

### References worth follow-up
The WebFetch rendering surfaced authors and concepts but did not render the numbered reference list inline. Load-bearing intellectual debts named in the body:

- **Aristotle / Mill / P. W. Anderson** — Historical anchors for the "more is different" tradition; load-bearing for the paper's framing of the weak/strong distinction.
- **Renormalization group literature** (Wilson lineage, implied) — Load-bearing for the universality-class argument and the RG-fixed-point picture.
- **Directed percolation universality class literature** — Load-bearing for the nonequilibrium absorbing-state route to emergence.
- **AdS/CFT correspondence literature** — Load-bearing for the duality argument; the most ambitious physics claim in the paper.
- **Brain-criticality / near-criticality literature** — Load-bearing for the calibration the paper offers ("current evidence favors near-criticality over exact self-tuned criticality"; "distance-to-criticality perspective").
- **Effective-information / integrated information theory literature** (implied, Tononi-adjacent) — Load-bearing for the claim that "effective information can increase under coarse-graining."
- **Edgar Allan Poe — "The Philosophy of Composition"** — Background citation used to illustrate the aesthetic-from-constraints point; not load-bearing for the physics arguments.

Follow-up priority for an MAS-emergence research agenda would order: effective-information literature first (operationalizes the coarse-graining test), then near-criticality methodology (calibrates how to *not* over-claim criticality from power laws alone), then mesoscale community detection (gives concrete coarse-graining targets).

### Confusions / unresolved points
1. **"Predictive" is doing a lot of work in the operational definition.** The definition requires the macro-description to "remain predictive," but the paper does not specify a quantitative predictivity threshold or a comparison protocol (predictive relative to what baseline? at what error tolerance?). This is the gap between "elegant definition" and "test you can run on a dataset."
2. **The information-theoretic diagnostics list is asserted, not derived.** Mutual information, transfer entropy, and effective information are named as emergence diagnostics, but the paper does not adjudicate when they agree, when they disagree, or which is primary. Practitioners want a decision rule.
3. **Weak vs strong is a clean binary in the paper; reality may be a spectrum.** The dismissal of strong emergence as "outside the scope of scientific method" is rhetorically strong, but the paper concedes that consciousness and life "do not neatly correspond to a phase transition." It is not clear whether these are weak-emergence-not-yet-derived or something else; the paper leaves this open.
4. **Top-down causation without law violation — mechanism left implicit.** The claim that higher-level structures "constrain or guide" components "without violating the underlying laws" is asserted, with the dominance-hierarchies example, but the mechanism by which constraint-without-violation is implemented (boundary conditions? selection pressure? statistical filtering?) is not spelled out.
5. **The Persian-tale conclusion is rhetorical rather than load-bearing.** The opening of the Conclusion uses a folk tale about horse-drawing to dramatize the dangers of vague usage. This is stylistic and does not advance the operational definition; readers expecting a closing technical synthesis may find the conclusion section softer than the body.
6. **Substrate independence is offered as evidence both *for* the reality of macro-properties and *against* strong emergence.** This is a careful move but the paper does not fully separate the two uses — substrate-independent macro-behavior is consistent with weak emergence by definition, but the paper sometimes phrases it as if substrate independence were *itself* the proof. The argument needs the additional premise that substrate-independent regularities admit micro-derivations, which is asserted rather than argued.
7. **Hedging on consciousness is correct but unstable.** The paper preserves hedging on consciousness ("could, in principle, arise from entirely different physical substrates") while elsewhere using consciousness as the canonical example where strong-emergence claims are "outside the scope of scientific method." The two stances are compatible but the paper does not reconcile them in one place.

