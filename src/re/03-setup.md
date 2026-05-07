## Setup ^sec-setup

We work with goal-conditioned probabilistic models in a Bayesian-update setting. The state at time $\tau^-$ before update consists of an epistemic component $M_{\tau^-}$ (the model state, an element of a parameter manifold $\mathcal{M}$) and a goal component $G$. An event $e_\tau$ arrives — a token, an observation, a query response — and the model updates to $M_{\tau^+}$. The latent world-state $\Omega_\tau$ is what the event is evidence about. The architecture's update mechanism produces a post-update model state $M_{\tau^+}$ whose law depends — possibly stochastically — on the goal $G$. The goal-conditional post-update law is $P_{M_{\tau^+}|e_\tau, M_{\tau^-}, G}$; the goal-marginal post-update law $P_{M_{\tau^+}|e_\tau, M_{\tau^-}}$ is the natural baseline against which goal-coupling is measured (the operating-distribution average over goals).

### The bias quantity ^sec-bias-quantity

The *goal-conditional bias* measures the displacement of the goal-conditional law from the goal-marginal:

$$\|\Delta M_{\text{bias}}(G)\| \;:=\; d_{\mathcal{M}}\!\left(P_{M_{\tau^+}|e_\tau, M_{\tau^-}, G},\; P_{M_{\tau^+}|e_\tau, M_{\tau^-}}\right),$$ ^eq-bias-quantity

a random variable in $G$. Throughout, $d_{\mathcal{M}}(\cdot, \cdot)$ denotes either the Wasserstein distance $W_2$ on the induced model-distribution (Track 1) or the Fisher-Rao geodesic distance $d_{FR}$ on the statistical-manifold sub-case (Track 2). Euclidean-on-parameters is the choice [[#^sec-no-go]] rules out.

### Goal/Update Coupling Class ^sec-architectural-classification

Architectures partition by whether $G$ has a causal path into the belief-update computation. The partition is monotonic in coupling strength.

> [!table] Goal/Update Coupling Class — partition by conditional-independence structure. ^tab-class-partition cols="l X X"
>
> | Class                   | Goal/update coupling                                                         | Examples                                                                                            |
> |:------------------------|:-----------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------|
> | **Class 1 (Separated)** | Holds by construction — estimator has no causal path from $G$                | Kalman filter + LQR; modular RL with separate world model                                            |
> | **Class 2 (Partial)**   | Holds for some pathways, fails for others                                    | Biological cortex; hybrid systems with separate preprocessing                                        |
> | **Class 3 (Coupled)**   | Fails by construction — $G$ is causally upstream of every downstream output computation | Autoregressive sequence models with causally-aggregated cross-position mixer (transformers, linear attention, Mamba/SSMs, RWKV, RetNet, long-convolutions — [[#^lem-attention-coupled]] + [[#^cor-arch-instantiations]]) |

Class 1 (Separated) is the architectural-separation case studied throughout Bayesian inverse-problems theory. Class 3 (Coupled) is the case the existing hallucination-theory lineage doesn't engage geometrically. Class 2 (Partial) is genuinely intermediate — hybrid LLM systems with retrieval, tools, scratchpads, or external memory — and lives at the system level rather than the architecture level. The Pearl-blanket reading \cite{bruineberg-dolega-dewhurst-baltieri-2022-bbs} of the Markov-blanket apparatus grounds the partition; we do not adopt the Friston-blanket metaphysical reading.

The bound's architectural-corollary form ([[#^eq-arch-corollary-informal]]) factors transferred goal-information through an *attenuation ratio* — the proportion of in-principle-resolvable goal-information that the architecture's update mechanism actually transfers into the post-update model state:

$$\kappa_{\text{processing}} \;:=\; \frac{I(G;\,M_{\tau^+} \mid e_\tau,\, M_{\tau^-})}{I(G;\,\Omega_\tau \mid e_\tau,\, M_{\tau^-})}.$$ ^eq-kappa-processing

Conditioning on $M_{\tau^-}$ matters: prior correlation between goals and prior model state — present even in Class 1 — would inflate the measure otherwise. For Class 1, the data-processing inequality on the chain $G \to \Omega_\tau \to M_{\tau^+}$ (Markov conditional on $(e_\tau, M_{\tau^-})$) gives $\kappa_{\text{processing}} \le 1$ automatically. For Class 2 and Class 3, $\kappa_{\text{processing}} \le 1$ is a named structural commitment; the parrot architecture $M_{\tau^+} := G$ with $G \perp\!\!\!\perp \Omega_\tau$ given $(e_\tau, M_{\tau^-})$ produces $\kappa_{\text{processing}} = \infty$, explicitly outside scope. *Convention.* When both numerator and denominator vanish (no transferred goal-information *and* no residual ambiguity, e.g., a Class 1 architecture on goal-orthogonal evidence), set $\kappa_{\text{processing}} := 0$; the bound's right-hand side is then trivially zero.

### Axioms ^sec-axioms

The universal-constant route ([[#^sec-track2-mechanism]], Track 2) commits to three axioms on the bound's metric $d_{\mathcal{M}}$:

> [!hypothesis] (PI) Sufficient-statistic invariance ^pi-axiom
> The bias bound's metric on $\mathcal{M}$ is invariant under sufficient statistics — equivalently, under Markov morphisms / congruent embeddings of statistical manifolds in the sense of \citet{cencov-1982-stat-decision}.

(PI) at full Markov-morphism strength is what \citeauthor{cencov-1982-stat-decision}'s uniqueness theorem actually requires. Smooth-coordinate invariance alone admits an infinite family of metrics; the strictly-stronger Markov-morphism class singles out Fisher-Rao up to global scalar.

> [!hypothesis] (R) Riemannian structure ^r-axiom
> The bound's metric $d_{\mathcal{M}}$ derives from a smooth Riemannian metric on $\mathcal{M}$.

(R) filters out divergence forms (TV, $\chi^2$, Hellinger-as-divergence) that satisfy (PI) as $f$-divergences but are not metric distances on $\mathcal{M}$ in the Riemannian sense.

> [!hypothesis] (K) KL second-order matching ^k-axiom
> $\mathrm{KL}(P_\theta \,\|\, P_{\theta+\delta}) = \tfrac{1}{2}d_{\mathcal{M}}^2(P_\theta, P_{\theta+\delta}) + O(d_{\mathcal{M}}^3)$.

(K) fixes the global scalar Čencov leaves free, pinning the bound's constant $C$ at $\sqrt{2}$. (R) and (K) are both implicit in any "$\mathbb{E}\,d \le C\sqrt{I}$" theorem-shape with second-order matching; we name them explicitly so the uniqueness statement of [[#^thm-fr-uniqueness]] has its hypotheses fully stated.

The transport-inequality route ([[#^sec-track1-mechanism]], Track 1) and the dimension-restricted slice-wise refinements ([[#^thm-umbrella]]'s Track 2 locally-tight instantiation) introduce additional regularity hypotheses inline with the theorems that invoke them. Throughout the paper we restrict to the *statistical-manifold sub-case*:

> [!hypothesis] (H1) Statistical-manifold sub-case ^h1-axiom
> The model state $M_t \in \mathcal{M}$ corresponds to a probability distribution $P_{M_t}$ over latent world-states, and $\mathcal{M}$ is locally a statistical manifold in the sense of \citet{amari-nagaoka-2000-info-geom}; $\mathcal{M}$, the goal-space, and the event-space are *standard Borel*, so regular conditional probabilities exist as Markov kernels \cite[Theorem 6.3]{kallenberg-2002-foundations}.

(H1) is satisfied by parametric Bayesian posterior families, exponential families, conjugate priors, and the parametric-belief-state subclass of LLMs that admits a natural distributional reading. The standard-Borel regularity is what makes the post-update chain rule (used in both Tracks) hold in the abstract-spaces form \cite[Theorem 3.4]{polyanskiy-wu-2024-info-theory}; \cite[Theorem 5.4]{gray-2011-entropy}.

### Coupled-class autoregressive connectivity ^sec-attention-coupled

The architectural classification's load-bearing application — that *plain decoder-only transformer attention, and more broadly modern autoregressive sequence models, are structurally Class 3 (Coupled)* — is a property of causally-aggregated cross-position mixing, not of any token-distribution-as-belief-state idealization.

> [!lemma] Coupled-class autoregressive connectivity ^lem-attention-coupled
> Let $\mathcal{G}_\theta$ be the directed computational graph of an autoregressive sequence model with parameters $\theta$. Suppose at every layer $\ell \ge 1$ each per-position update factors as $h_\ell^{(j)} = h_{\ell-1}^{(j)} + F_\ell^{(j)}\bigl(\{h_{\ell-1}^{(i)}\}_{i \le j};\,\theta\bigr) + G_\ell\bigl(h_{\ell-1}^{(j)};\,\theta\bigr)$, with $F_\ell^{(j)}$ a causally-aggregated cross-position mixer and $G_\ell$ position-wise. If goal positions $i_G$ and evidence positions $i_E$ satisfy $i_G \cap i_E = \emptyset$, then for every layer $\ell \ge 1$ and position $j \ge \max(i_G \cup i_E)$, $h_\ell^{(j)}$ has a directed-graph path back to every $i_G \le j$ whenever the *per-source non-degeneracy condition* (★) holds: for each $i \le j$, $\partial F_\ell^{(j)}/\partial h_{\ell-1}^{(i)}$ is generically non-zero on the operating set.

> [!corollary] Named-architecture instantiations ^cor-arch-instantiations
> Per-source non-degeneracy is satisfied generically by:
> *(a)* plain decoder-only transformer attention (non-degenerate softmax attention weights, non-singular value projection);
> *(b)* linear-attention transformers with non-vanishing feature map (e.g., $\phi = \mathrm{elu}+1$, $\phi = \exp$);
> *(c)* selective state-space models / Mamba (non-singular discretized $\bar A = \exp(\Delta A)$ with $A < 0$ diagonal, non-zero $\bar B$ and $C$);
> *(d)* RWKV time-mixing (positive time-decay);
> *(e)* RetNet (decay $\gamma \in (0, 1)$);
> *(f)* long-convolution architectures (full-support causal kernel).
>
> Each is structurally Class 3 (Coupled) under standard parameterization.

The proof is a one-induction over layer depth, structurally identical across the architectures of [[#^cor-arch-instantiations]] — the per-source non-degeneracy condition is the architecture-specific input, the directed-graph-path conclusion is the architecture-agnostic output. Robust to RMSNorm / GroupNorm / FlashAttention (position-wise / mathematically-equivalent), causal masking (preserves $\partial F_\ell^{(j)}/\partial h_{\ell-1}^{(i_G)} \ne 0$ for $i_G \le j$), and sliding-window or sparse attention (preserves connectivity by composition across layers when the window pattern admits a multi-hop path). Architectures with explicit goal-to-output blocking — token-dropping at intermediate layers, hard-routing MoE-attention with goal-conditional partitioning, or strictly goal-blind retrieval components — fall outside the lemma's scope and are appropriately Class 2 (Partial). Full proof and per-architecture verifications of (★) in [[#^sec-attention-coupled-proof]].

[[#^lem-attention-coupled]] establishes a *downstream-output graph-reachability* claim: at every layer and every position causally downstream of the goal and evidence, the activation has a directed-graph path back to every goal position. The bias-bound *interpretation* additionally invokes the in-context-learning correspondence \cite{garg-tsipras-liang-valiant-2022-icl,akyurek-schuurmans-andreas-ma-zhou-2023-icl,vonoswald-2023-transformers-gd,xie-raghunathan-liang-ma-2022-icl-implicit-bayes} between the next-token distribution and an implicit posterior; the structural Coupled-class claim is robust without it.
