---
title: "How Much Can LLMs Hallucinate? An Upper Bound via Coupling and Ambiguity"
authors:
  - name: Joseph A. Wecker
    affiliation: Independent
    email: joseph.wecker@gmail.com
---

Hallucination theory bounds *frequency* from below — calibrated LLMs must hallucinate at some rate. We bound *size* from above: the goal-coupling-induced displacement of the post-update belief state. Applying the chain rule of relative entropy directly to the post-update law, marginalized over the goal, equals the *transferred* goal-information that actually enters the model. A Fisher-Rao second-order expansion delivers

$$\mathbb{E}\,\|\Delta M_{\mathrm{bias}}\| \le C\sqrt{I(G;\,M_{\tau^+} \mid e_\tau, M_{\tau^-})},$$

with $C = \sqrt 2$ universal, dimension-free, locally tight under parameterization-invariance + Riemannian structure + KL-coordinate matching — forced by Čencov's 1982 uniqueness theorem, made load-bearing by a no-go ruling out coordinate-naive Euclidean alternatives — and $C = \pi/\sqrt 2$ globally without uniform-locality. A parallel transport-inequality track generalizes the canonical Stuart-school posterior-stability cascade to goal-coupled architectures. Operationally the bound reads as $\kappa_{\mathrm{processing}} \times$ residual ambiguity (coupling strength × informational uncertainty), and architectures partition into a monotonic Separated / Partial / Coupled ladder — with plain decoder-only transformer attention structurally Coupled by construction.
