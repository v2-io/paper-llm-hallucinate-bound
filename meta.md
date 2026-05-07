---
title: "How Much Can LLMs Hallucinate? An Upper Bound on Goal-Coupling Displacement"
authors:
  - name: Joseph A. Wecker
    affiliation: Independent
    email: joseph.wecker@gmail.com
---

Hallucination theory bounds *frequency* from below — calibrated LLMs must hallucinate at some rate. We bound from above a complementary quantity: the goal-coupling-induced displacement of the post-update belief state — the operational shape of *sycophancy* \citep{sharma-2023-sycophancy}, where LLM responses match user beliefs over truthful ones. The chain rule of relative entropy on the post-update law equals the *transferred* goal-information that enters the model state, delivering

$$\mathbb{E}\,\|\Delta M_{\mathrm{bias}}\| \le C\sqrt{I(G;\,M_{\tau^+} \mid e_\tau, M_{\tau^-})}.$$

Čencov's 1982 uniqueness theorem under categorical parameterization-invariance forces two universal Fisher-Rao constants: $C = \sqrt 2$ locally tight (under Riemannian structure + KL-coordinate matching + uniform-locality on goal-conditional slices; first-moment sharp via a symmetric two-point witness), and $C = 2$ globally on the ambient spherical-arc pseudometric (sharp via a symmetric $N$-point witness). A no-go theorem makes the parameterization-invariance commitment load-bearing. A parallel transport-inequality track recovers the canonical Stuart-school cascade form $\propto L_{\mathrm{post}}^2/\rho_{\mathrm{noise}}$ across the Strand 2 hypothesis space (tight on conjugate-Gaussian instances). Operationally the bound factors as coupling strength × residual ambiguity, with architectures partitioning into a Separated / Partial / Coupled ladder; transformer attention and modern autoregressive sequence models (linear attention, Mamba, RWKV, RetNet, long-convolutions) are structurally Coupled. Binary-uniform two-goal probing gives a closed-form Jensen-Shannon-divergence estimator of the transferred information. The result is a conditional theory of goal-induced displacement on belief-state representations under named regularity hypotheses, not a semantic metric on false outputs.
