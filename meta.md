---
title: "How Much Can LLMs Hallucinate? An Upper Bound via Coupling and Ambiguity"
authors:
  - name: Joseph A. Wecker
    affiliation: Independent
    email: joseph.wecker@gmail.com
---

Hallucination theory bounds *frequency* from below — calibrated LLMs must hallucinate at some rate. We bound *size* from above: the goal-coupling-induced displacement of the post-update belief state under coupled belief-goal inference. Applying the chain rule of relative entropy directly to the post-update law, marginalized over the goal, equals the *transferred* goal-information that actually enters the model state, delivering

$$\mathbb{E}\,\|\Delta M_{\mathrm{bias}}\| \le C\sqrt{I(G;\,M_{\tau^+} \mid e_\tau, M_{\tau^-})}.$$

Two universal Fisher-Rao constants are forced by Čencov's 1982 uniqueness theorem under a parameterization-invariance commitment: $C = \sqrt{2}$ locally tight (with Riemannian structure, KL-coordinate matching, and uniform-locality on goal-conditional slices; first-moment sharp via a symmetric two-point witness), and $C = 2$ globally without uniform-locality (Rényi-1/2 monotonicity composed with the chord-arc identity, sharp via a symmetric $N$-point witness; the $\sqrt 2$ gap is exactly the chord-arc factor at the unit $L^2$-sphere's antipode). A no-go theorem rules out any coordinate-independent universal constant for Euclidean chart norms via a scale-family construction — making the parameterization-invariance commitment load-bearing rather than coincidental.

A parallel transport-inequality track generalizes the canonical Stuart-school posterior-stability cascade beyond Class 1 (Separated) to goal-coupled architectures, via a Lipschitz pushforward of $T_2$ under the Bayesian-update map. Operationally the bound factors as coupling strength $\kappa_{\mathrm{processing}}$ × residual ambiguity, with architectures partitioning into a monotonic Separated / Partial / Coupled ladder grounded in conditional-independence structure. Plain decoder-only transformer attention is structurally Coupled by construction, by graph-reachability induction on layer depth. For binary-uniform two-goal probing, the transferred goal-information has a closed-form Jensen-Shannon-divergence estimator on the goal-conditional response distributions, giving an immediately-computable operational bound from the unconditional theorem.
