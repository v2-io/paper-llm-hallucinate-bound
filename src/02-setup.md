## Setup: belief-goal-coupled architectures and the bias quantity ^sec-setup

We work with goal-conditioned probabilistic models in a Bayesian-update setting. The state at time $\tau^-$ before update consists of an epistemic component $M_{\tau^-}$ (the model state, an element of a parameter manifold $\mathcal{M}$) and a goal component $G$ (a context vector encoding what the model is trying to do — the prompt, the task, the active subgoal). An event $e_\tau$ arrives — a token, an observation, a query response — and the model updates. The latent world-state $\Omega_\tau$ is what the event is evidence about.

### Goal-conditional and goal-marginal post-update laws ^sec-conditional-marginal

Given prior model state and event $(M_{\tau^-}, e_\tau)$, the architecture's update mechanism produces a post-update model state $M_{\tau^+}$ that depends — possibly stochastically — on the goal $G$. We characterize this dependence at the law level. The *goal-conditional* post-update law is

$$P_{M_{\tau^+} \mid e_\tau, M_{\tau^-}, G} \;=\; \text{conditional law of } M_{\tau^+} \text{ given } (M_{\tau^-}, e_\tau, G).$$

For deterministic update mechanisms, this is the Dirac mass $\delta_{f_X^M(M_{\tau^-},\, e_\tau,\, G)}$ for some function $f_X^M$. The *goal-marginal* post-update law marginalizes $G$ out:

$$P_{M_{\tau^+} \mid e_\tau, M_{\tau^-}}(\cdot) \;:=\; \int P_{M_{\tau^+} \mid e_\tau, M_{\tau^-}, G=g}(\cdot)\, dP_G(g \mid e_\tau, M_{\tau^-}).$$

The goal-marginal is the natural baseline against which goal-coupling is measured: it is the post-update distribution one obtains when the goal is averaged over the operating distribution. The bound thus controls *deviation from the goal-marginal operating baseline*, not deviation from an evidence-only or truth-supported posterior — those would require a separate axiom relating goal-marginal to evidence-only baseline (see [[#^sec-bias-baseline]]). For Class 2 (Partial) and Class 3 (Coupled) architectures, the goal-marginal is the only operationally well-defined "decoupled" baseline (a coupled architecture cannot be run goal-blind); for deterministic update mechanisms, the goal-marginal is the *pushforward law* $\mathrm{Law}(f_X^M(M_-, e_\tau, G) \mid e_\tau, M_{\tau^-})$, whose *barycenter* is the deterministic-update mean $f_M(M_-, e_\tau) := \mathbb{E}_G[f_X^M(M_-, e_\tau, G) \mid e_\tau, M_{\tau^-}]$. The marginal is not a Dirac at the mean — it is a mixture/pushforward distribution whose centroid is the mean.

The *goal-conditional bias* measures the displacement of the goal-conditional law from the goal-marginal:

$$\|\Delta M_{\text{bias}}(G)\| \;:=\; \|P_{M_{\tau^+} \mid e_\tau, M_{\tau^-}, G},\; P_{M_{\tau^+} \mid e_\tau, M_{\tau^-}}\|_{\mathcal{M}},$$ ^eq-bias-quantity

a random variable in $G$. Throughout, when we write $\|\cdot\|_{\mathcal{M}}$ (or just $\|\cdot\|$) without a subscript, we mean either the $W_2$ Wasserstein distance on the induced model-distribution (Track 1, [[#^sec-track1]]) or the Fisher-Rao geodesic distance on the statistical-manifold sub-case (Track 2, [[#^sec-track2]]). Euclidean-on-parameters is the choice the no-go ([[#^sec-no-go]]) rules out.

For deterministic update mechanisms the distributional definition [[#^eq-bias-quantity]] reduces algebraically: $W_2(\delta_{f_X^M(G)}, P_{M_{\tau^+}\mid e, M})^2 = \mathbb{E}_{G'}\Vert f_X^M(M_-, e, G) - f_X^M(M_-, e, G')\Vert^2$, so $\mathbb{E}_G\Vert\Delta M_{\text{bias}}(G)\Vert_{W_2}^2 = 2\,\mathrm{Var}_G(f_X^M)$. The bound's distance form $\mathbb{E}\Vert\Delta M_{\text{bias}}\Vert \leq C\sqrt{I}$ thus controls the goal-induced $\sqrt{2}$-scaled L²-deviation of the deterministic update from its goal-marginal mean — what an information-theoretic "how far from baseline does goal-coupling pull the update" target naturally measures.

### Architectural classification: Goal/Update Coupling Class ^sec-architectural-classification

Whether $f_X^M$ has a non-trivial $G$ dependence at all is a structural property of the architecture. Following the Pearl-blanket reading of the Markov-blanket apparatus articulated by Bruineberg et al. \cite{bruineberg-dolega-dewhurst-baltieri-2022-bbs}, we partition architectures by the conditional-independence structure of their internal processing graph — specifically, whether $G$ has a causal path into the belief-update computation. The partition is monotonic in coupling strength and we call it the architecture's *Goal/Update Coupling Class* (or simply *Class*).

{::nomarkdown}\begin{table}[h]
  \centering
  \caption{Goal/Update Coupling Class --- partition of architectures by conditional-independence structure.}
  \label{tab-class-partition}
  \small
  \begin{tabularx}{\textwidth}{@{}l X X X@{}}
    \toprule
    Class & Goal/update coupling & Topology & Examples \\
    \midrule
    \textbf{Class 1 (Separated)} & Holds by construction --- the estimator has no causal path from $G$ & Separate estimator and planner connected through a state-estimate interface & Kalman filter + LQR; modular RL with separate world model \\
    \textbf{Class 2 (Partial)} & Holds for some pathways, fails for others & Some shared infrastructure, some separate pathways & Biological cortex; hybrid systems with separate preprocessing \\
    \textbf{Class 3 (Coupled)} & Fails by construction --- $G$ is causally upstream of every computation & Single mechanism handles both belief-update and goal-conditioned processing & Transformer LLM (attention processes goals and observations together --- \Cref{thm-attention-coupled}) \\
    \bottomrule
  \end{tabularx}
\end{table}{:/nomarkdown}

The partition is structural, not parametric. In Class 1 (Separated), no goal information reaches the belief update under any task distribution. In Class 3 (Coupled), the goal is part of the input to the same mechanism that processes the evidence — every internal computation has a directed-graph path from the goal. Class 2 (Partial) is genuinely intermediate: the same hybrid architecture may be more or less goal-coupled under different distributions of tasks. The numbering is monotonic in coupling strength: more goal-coupling means higher Class.

This classification is the *Pearl-blanket form* of the architectural-separation distinction. It is structurally consistent with — but does not adopt — the Friston-blanket reading \cite{friston-2013-life,friston-2019-particular-physics} in which Markov blankets are taken to demarcate self-from-other in a metaphysically substantive way. Bruineberg et al. argue that the Friston-blanket reading overruns what the conditional-independence formalism delivers; we agree, and the explicit Coupled-class scope-exit (plain decoder-only transformer inference does not satisfy architectural separation under the token-distribution-as-belief-state idealization) is the scope honesty their critique calls for.

### The architectural attenuation ratio ^sec-attenuation-ratio

The bound's architectural-corollary form factors transferred goal-information into the architecture's processing graph through an *attenuation ratio* — the proportion of in-principle-resolvable goal-information about the latent world-state that the architecture's update mechanism actually transfers into the post-update model state. We name this ratio $\kappa_{\text{processing}}$ and use it as the bound's coupling-strength coefficient:

$$\kappa_{\text{processing}} \;:=\; \frac{I(G \,;\, M_{\tau^+} \mid e_\tau,\, M_{\tau^-})}{I(G \,;\, \Omega_\tau \mid e_\tau,\, M_{\tau^-})},$$ ^eq-kappa-processing

where $I$ is conditional mutual information. The conditioning on $M_{\tau^-}$ matters: without it, prior correlation between goals and prior model state — which exists even in Separated-class architectures — inflates the measure. The numerator is the *transferred* goal-information that actually enters the post-update model; the denominator is the *resolvable* goal-information about the latent world-state available to the architecture in principle. The ratio captures *how much of what's available the architecture's coupling channel transfers*.

For Class 1 (Separated) architectures, $G \to \Omega_\tau \to M_{\tau^+}$ is a Markov chain conditional on $(e_\tau, M_{\tau^-})$ by architectural separation, and the data-processing inequality gives $\kappa_{\text{processing}} \leq 1$ automatically — the architecture's separated structure can only *attenuate* the available information. For Class 2 (Partial) and Class 3 (Coupled) architectures, $G$ enters the post-update map directly via the architectural channel (e.g., attention reading $G$ as part of its query) on a path that bypasses $\Omega_\tau$. Most natural Class 2/3 architectures still satisfy $\kappa_{\text{processing}} \leq 1$ (the goal flows through similar pathways to the evidence), but the ratio is *not* automatically bounded — pathological architectures can amplify. The extreme case is the *parrot architecture*, $M_{\tau^+} := G$ directly, where the post-update state IS the goal: numerator is $H(G \mid e, M)$, denominator can be zero or near-zero, and $\kappa_{\text{processing}} = \infty$. The architectural corollary's commitment (H$_\kappa$, [[#^sec-h-kappa-status]]) is precisely “$\kappa_{\text{processing}}$ is bounded” — automatic for Class 1, a named structural commitment for Class 2/3.

The ratio is well-defined when $I(G; \Omega_\tau \mid e_\tau, M_{\tau^-}) > 0$; the degenerate case where the latent world-state carries no resolvable goal-information (so the denominator vanishes) collapses to the unconditional theorem on transferred information directly, with no architectural-corollary form available. Operationally this captures architectures whose $G$ is genuinely orthogonal to the evidence channel — e.g., a "make me feel good" goal where the relevant ambiguity isn't in the evidence at all; the bound's transferred-information form still applies, just without the κ × $\mathcal{A}$ factorization.

Two empirical handles on $\kappa_{\text{processing}}$ are immediate. First, a behavioral two-goal probe: run the architecture on a representative event set $\mathcal{E}$ under two distinct goal states $G_1, G_2$ and measure the divergence of the epistemic content of the response, normalized by the maximum observed divergence. Second, in architectures with explicit attention or routing, the conditional mutual information can be lower-bounded by activation-level mediation analyses. Both are out of scope for the present theory paper but flagged as natural future operationalizations.

### The bound — two layers ^sec-bound-two-layers

We state the bound in two layers: an *unconditional* theorem in transferred information, and an *architectural corollary* under (H$_\kappa$).

**The umbrella theorem (unconditional in the architectural classification).** For both tracks, [[#^sec-track1]] and [[#^sec-track2]] derive — *for fixed event-prior pair $(e_\tau, M_{\tau^-})$, with $\mathbb{E}$ taken over $G \sim P(G \mid e_\tau, M_{\tau^-})$* —

$$\mathbb{E}\,\|\Delta M_{\text{bias}}\| \;\leq\; C \cdot \sqrt{\,I(G;\,M_{\tau^+} \mid e_\tau,\, M_{\tau^-})\,},$$ ^eq-umbrella

with $C$ supplied by either the transport-inequality cascade ($C = \sqrt{C_{T_2}}$ on $W_2$, by Jensen on the squared bound; sufficient conditions for the $T_2$ inequality on the post-update law include LSI on the post-update distribution or dimension-free sub-Gaussian Lipschitz concentration) or the Fisher-Rao route — locally tight $C = \sqrt{2}$ on $d_{FR}$ under (PI) + (R) + (K) + (H4$'$), or globally valid $C = \pi/\sqrt 2$ on $d_{FR}$ under (PI) only ([[#^thm-track2-glob]]), with strictly nested hypotheses. A direct Hellinger statement ([[#^thm-hellinger]]) gives universal constant $C = 1/\sqrt 2$ on the chord under (PI) only — companion to [[#^thm-track2-glob]]'s arc form on the same unit $L^2$-sphere. The right-hand side is the *transferred* goal-information into the post-update model state — the actually-realized coupling, observable at the bound's left-hand-side scale. Track 1 additionally delivers the tighter *squared-distance* form

$$\mathbb{E}\,\|\Delta M_{\text{bias}}\|^2 \;\leq\; C_{T_2} \cdot I(G;\,M_{\tau^+} \mid e_\tau,\, M_{\tau^-}),$$ ^eq-umbrella-sq

linear in transferred information, when the Wasserstein metric and (H2$'$) hold.

**The architectural corollary (under (H$_\kappa$)).** A coupling-attenuation hypothesis (H$_\kappa$) names the architectural-bandwidth inequality

$$I(G;\,M_{\tau^+} \mid e_\tau,\, M_{\tau^-}) \;\leq\; \kappa_{\text{processing}} \cdot I(G;\,\Omega_\tau \mid e_\tau,\, M_{\tau^-}).$$ ^eq-h-kappa

(H$_\kappa$) is *automatic* for Class 1 (Separated) architectures: $G \to \Omega \to M_{\tau^+}$ is a Markov chain conditional on $(e, M_{\tau^-})$ by architectural separation, and the data-processing inequality gives (H$_\kappa$) with $\kappa_{\text{processing}} \leq 1$. For Class 2 (Partial) and Class 3 (Coupled) it is a *named structural commitment* on the architecture — [[#^sec-h-kappa-status]] documents two clean sufficient conditions (goal-blind effective kernel; architectural-channel bandwidth bound) and a worst-case witness (parrot architecture with $\kappa_{\text{processing}} = \infty$, explicitly outside scope). Under (H$_\kappa$), substituting into [[#^eq-umbrella]] recovers the architectural factorization

$$\mathbb{E}\,\|\Delta M_{\text{bias}}\| \;\leq\; C \cdot \sqrt{\,\kappa_{\text{processing}} \cdot I(G;\,\Omega_\tau \mid e_\tau,\, M_{\tau^-})\,}.$$ ^eq-arch-corollary

The unconditional theorem is the structural backbone — its math is verifiable without committing to (H$_\kappa$). The architectural corollary is the *interpretation* this paper foregrounds: goal-driven displacement of the model state from its goal-marginal operating baseline (and, under (H$_{\text{neutral}}$) of [[#^sec-bias-baseline]], from an evidence-only goal-blind baseline) factors into a structural-architectural quantity (where can the goal flow?) and an information-theoretic quantity (how much could the goal in principle resolve?). The bound says nothing about *frequency* of hallucination — that is the lineage of \cite{kalai-2023-calibrated}, \cite{kalai-2025-why}, and the calibration-constraint corpus more broadly. It bounds the *size* of the displacement when goal-coupling is the cause.
