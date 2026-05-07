## Introduction ^sec-introduction

Recent hallucination theory bounds the *frequency* with which calibrated language models must produce false outputs as a consequence of training-set structure or calibration constraints — \citet{kalai-2023-calibrated} on singleton-fact rates, \citet{kalai-2025-why} on training-and-evaluation-incentive origins, \citet{karbasi-2025-im} on detection impossibility, \citet{wu-grama-szpankowski-2024} on VC-dimension obstructions, \citet{suzuki-2025-hallucinations} on probabilistic negligibility. Hallucination in this lineage is treated as architecture-agnostic.

Bayesian inverse-problems theory in the lineage of \citet{stuart-2010-acta} has spent fifteen years building Lipschitz-stability bounds on the posterior under perturbations of the prior, the likelihood, and the data — \citet{sprungk-2020-local-lipschitz}, \citet{cvetkovic-2025-upper}, \citet{dolera-mainini-2023-aihp-lipschitz}, \citet{garbuno-inigo-2023-bayesian}, \citet{hosseini-hsu-taghvaei-2024-conditional-ot}. The transport-inequality apparatus driving these bounds — Otto-Villani, Bakry-Émery, Gozlan, Bobkov-Götze — is mature and verified across decades of inverse-problems practice.

Neither lineage engages the implicit belief-goal-coupling structure of attention-based architectures — a structure intrinsic to LLMs by construction ([[#^lem-attention-coupled]]), not an incidental property of training.

Engaging this structure directly reframes the question: how much can an LLM be pulled away from what its evidence supports by the goal it is asked to satisfy? This paper bounds the displacement.

**This paper composes the two.** Apply the chain rule of relative entropy directly to the *post-update* law, marginalized over the goal: $\mathbb{E}_G\bigl[\,\mathrm{KL}(P_{M_{\tau^+}|e, M_{\tau^-}, G} \,\|\, P_{M_{\tau^+}|e, M_{\tau^-}})\bigr] = I(G; M_{\tau^+}|e_\tau, M_{\tau^-})$. The right-hand side is the *transferred* goal-information that actually enters the post-update model state. Combined with a Fisher-Rao second-order expansion on the post-update statistical manifold, this delivers an upper bound on goal-conditional displacement:

$$\mathbb{E}\,\|\Delta M_{\text{bias}}\| \;\leq\; C \cdot \sqrt{\,I(G; M_{\tau^+}\,|\,e_\tau, M_{\tau^-})\,}.$$ ^eq-umbrella-informal

Under a parameterization-invariance commitment at full Markov-morphism strength — plus Riemannian structure and KL-coordinate matching — Čencov's 1982 uniqueness theorem forces Fisher-Rao with constant $C = \sqrt{2}$. *Universal, dimension-free, no domain-specific parameters.* A scale-family no-go theorem rules out any coordinate-independent universal constant for Euclidean chart norms — making the (PI) commitment load-bearing, not coincidental. We call this *Track 2*.

A parallel *Track 1* derivation via a Talagrand transport inequality on the same post-update law recovers the canonical Stuart-school cascade constant $C_{T_2} = 2 L_{\text{post}}^2/\rho_{\text{LSI}}$ as a special case, with $C = \sqrt{C_{T_2}}$ on $W_2$. Track 2's universal constant is what makes the composition novel; Track 1 demonstrates that the composition contains the existing Bayesian-inverse-problems lineage as a strict sub-case under standard log-Sobolev concentration. Both flow from the same chain-rule move on the post-update law.

**The architectural reading.** Under a coupling-attenuation hypothesis (H$_\kappa$), the bound factors:

$$\mathbb{E}\,\|\Delta M_{\text{bias}}\| \;\leq\; C \cdot \sqrt{\,\kappa_{\text{processing}} \cdot I(G;\,\Omega_\tau\,|\,e_\tau, M_{\tau^-})\,},$$ ^eq-arch-corollary-informal

into an *architectural coupling factor* $\kappa_{\text{processing}}$ (how much of the available goal-information the architecture's update mechanism transfers) and a *residual ambiguity factor* $I(G; \Omega \mid e, M)$ (how much the goal could in principle resolve about the latent world-state beyond what the evidence already pins down). Architectures partition by their goal-update topology into a monotonic ladder — Class 1 (Separated), Class 2 (Partial), Class 3 (Coupled). For Class 1, $\kappa_{\text{processing}} \le 1$ holds automatically by data-processing on the Markov chain $G \to \Omega \to M_{\tau^+}$. For Class 2 and Class 3, (H$_\kappa$) is a named structural commitment with documented sufficient conditions and a worst-case witness (parrot architecture, $\kappa_{\text{processing}} = \infty$) excluded by scope.

Plain decoder-only transformer attention is *Class 3 (Coupled) by construction* in a precise structural sense: every internal computation has a directed-graph path from any input position whenever attention weights are non-degenerate ([[#^lem-attention-coupled]], by induction on layer depth, robust to RMSNorm / FlashAttention / causal masking / sliding-window). The structural Coupled-class claim does not depend on the token-distribution-as-belief-state idealization that the bias-bound *application* additionally invokes via the in-context-learning correspondence \cite{garg-tsipras-liang-valiant-2022-icl,akyurek-schuurmans-andreas-ma-zhou-2023-icl,vonoswald-2023-transformers-gd,xie-raghunathan-liang-ma-2022-icl-implicit-bayes}.

**Contributions.**

1. **An architectural classification.** Goal/Update Coupling Class — Class 1 (Separated), Class 2 (Partial), Class 3 (Coupled) — partitions architectures monotonically by goal-update topology, grounded in the Pearl-blanket reading \cite{bruineberg-dolega-dewhurst-baltieri-2022-bbs} of the Markov-blanket apparatus. [[#^lem-attention-coupled]] derives Class 3 status for transformer attention from connectivity alone.

2. **An umbrella upper bound** [[#^eq-umbrella-informal]] on goal-conditional displacement of the post-update model state, derived via chain rule on the post-update law. Two named tracks supply $C$ — a transport-inequality cascade (Track 1) and a Fisher-Rao geometry route (Track 2).

3. **A no-go that forces a coordinate commitment.** No coordinate-independent universal constant exists for Euclidean chart norms (a scale-family construction). Under the (PI) + (R) + (K) triple, Čencov's uniqueness theorem forces Fisher-Rao + $\sqrt{2}$ universally — no further freedom.

4. **An architectural-corollary form** [[#^eq-arch-corollary-informal]] under (H$_\kappa$), recovering the $\kappa \times \mathcal{A}$ factorization that gives the bound its operational reading.

[[#^sec-setup]] sets up the architectures and the (PI), (R), (K) axioms. [[#^sec-main-results]] states the umbrella theorem with both tracks, the no-go, and the architectural corollary. [[#^sec-mechanism]] sketches the mechanism — both proofs flow from the post-update chain rule. Limitations and the bound's relation to the frequency-lower-bound lineage are in [[#^sec-conclusion]].
