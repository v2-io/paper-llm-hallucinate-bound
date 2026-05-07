---
title: "How Much Can LLMs Hallucinate? An Upper Bound via Coupling and Ambiguity"
authors:
  - name: Joseph A. Wecker
    affiliation: Independent
    email: joseph.wecker@gmail.com
---

The dominant lineage in hallucination theory bounds *frequency* from below — calibrated LLMs *must* hallucinate at some rate. We bound *size* from above: the goal-conditional displacement of the post-update model state from the goal-marginal, under coupled belief-goal inference. The two axes are orthogonal — how often versus how much an LLM hallucinates. The size axis was open: posterior-stability machinery from Bayesian inverse problems had not been brought to coupled inference.

The main theorem bounds the displacement by transferred information,

$$\mathbb{E}\,\|\Delta M_{\mathrm{bias}}\| \le C \sqrt{I(G; M_{\tau^+} \mid e, M_{\tau^-})},$$

under standard regularity conditions and *independent of any architectural-class commitment*. Under a named coupling-attenuation hypothesis, this factors as $C\sqrt{\kappa_{\mathrm{processing}} \cdot I(G; \Omega_\tau \mid e_\tau, M_{\tau^-})}$ — coupling strength times residual ambiguity.

Two routes deliver $C$. A transport-inequality track uses a Talagrand $T_2$ inequality on the post-update law, verifiable via log-Sobolev concentration or dimension-free sub-Gaussian moments. A Fisher-Rao geometry track yields *two* universal dimension-free constants on $d_{FR}$: $C = \sqrt{2}$ locally tight under parameterization-invariance + Riemannian structure + KL-coordinate matching + uniform-locality, and $C = \pi/\sqrt 2$ globally valid under parameterization-invariance alone (with the $\pi/2$ overhead being exactly the worst-case arc-chord ratio at the unit-sphere antipode). The (PI) commitment is load-bearing: no chart-independent universal constant exists under Euclidean coordinates (a two-chart scale-family construction), and the four-condition triple uniquely pins Fisher-Rao + $\sqrt{2}$ as the locally-tight constant. A direct Hellinger statement gives a third universal constant $1/\sqrt 2$ on the chord — companion to the global Fisher-Rao bound on the same unit $L^2$-sphere.

Architectures partition by goal-update coupling into a monotonic ladder — Separated, Partial, Coupled. A structural lemma derives Coupled status for transformer attention from connectivity alone (under non-degenerate attention). For conjugate-Gaussian inverse problems, the bound's Euclidean translation carries prefactor $L_{\mathrm{post}}\sigma$, bounded by $\tau/2$ uniformly and vanishing in extreme observation-noise limits.
