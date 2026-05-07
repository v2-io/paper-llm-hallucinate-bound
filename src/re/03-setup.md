## Setup ^sec-setup

We work with goal-conditioned probabilistic models in a Bayesian-update setting. The state at time $\tau^-$ before update consists of an epistemic component $M_{\tau^-}$ (the model state, an element of a parameter manifold $\mathcal{M}$) and a goal component $G$. An event $e_\tau$ arrives — a token, an observation, a query response — and the model updates to $M_{\tau^+}$. The latent world-state $\Omega_\tau$ is what the event is evidence about. The architecture's update mechanism produces a post-update model state $M_{\tau^+}$ whose law depends — possibly stochastically — on the goal $G$. The goal-conditional post-update law is $P_{M_{\tau^+}|e_\tau, M_{\tau^-}, G}$; the goal-marginal post-update law $P_{M_{\tau^+}|e_\tau, M_{\tau^-}}$ is the natural baseline against which goal-coupling is measured (the operating-distribution average over goals).

### The bias quantity ^sec-bias-quantity

The *goal-conditional bias* measures the displacement of the goal-conditional law from the goal-marginal:

$$\|\Delta M_{\text{bias}}(G)\| \;:=\; d_{\mathcal{M}}\!\left(P_{M_{\tau^+}|e_\tau, M_{\tau^-}, G},\; P_{M_{\tau^+}|e_\tau, M_{\tau^-}}\right),$$ ^eq-bias-quantity

a random variable in $G$. Throughout, $d_{\mathcal{M}}(\cdot, \cdot)$ denotes one of two distinct objects, used cleanly within their respective tracks. *(Track 1)* the Wasserstein distance $W_2$ on **laws over the parameter manifold $\mathcal{M}$** — the goal-conditional and goal-marginal post-update random elements of $\mathcal{M}$ are compared as probability laws on $\mathcal{M}$ with a ground metric on $\mathcal{M}$. *(Track 2)* the Fisher-Rao spherical-arc distance $d_{FR}$ on the statistical-manifold sub-case (H1), where each model state $M_t \in \mathcal M$ carries an associated probability distribution $P_{M_t}$ over the latent world-state — and the bias quantity is the random spherical arc between $P_{M_{\tau^+}\mid e_\tau, M_{\tau^-}, G}$ and $P_{M_{\tau^+}\mid e_\tau, M_{\tau^-}}$ as points on the unit $L^2$-sphere of $\sqrt p$. We adopt the *Amari-Nagaoka spherical-arc convention* $d_{FR}(P, Q) := 2\arccos\int\sqrt{pq}$ throughout, with $d_{FR} \in [0, \pi]$. (Equal to the intrinsic Fisher-Rao geodesic on the full simplex / nonparametric ambient space; on a parametric submanifold the ambient spherical arc is the chart-invariant pseudometric we bound.) The locally-tight $\sqrt 2$ regime (under (PI)+(R)+(K)+(H4$'$)) operates in the small-displacement limit where the ambient arc agrees with submanifold-intrinsic geodesics at second order; the globally-valid $C = 2$ regime (under (PI) alone) operates on the ambient arc directly. Euclidean-on-parameters is the choice [[#^sec-no-go]] rules out.

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

The bound's architectural-corollary form [[#^eq-arch-corollary-informal]] factors transferred goal-information through an *attenuation ratio* — the proportion of in-principle-resolvable goal-information that the architecture's update mechanism actually transfers into the post-update model state:

$$\kappa_{\text{processing}} \;:=\; \frac{I(G;\,M_{\tau^+} \mid e_\tau,\, M_{\tau^-})}{I(G;\,\Omega_\tau \mid e_\tau,\, M_{\tau^-})}.$$ ^eq-kappa-processing

Conditioning on $M_{\tau^-}$ matters: prior correlation between goals and prior model state — present even in Class 1 — would inflate the measure otherwise. *Class 1 formally:* conditional on $(e_\tau, M_{\tau^-})$, $G \perp\!\!\!\perp M_{\tau^+} \mid \Omega_\tau$ — $G$ affects $M_{\tau^+}$ only through the latent world-state $\Omega_\tau$. This conditional independence is the formal content of "estimator has no causal path from $G$" and gives the Markov chain $G \to \Omega_\tau \to M_{\tau^+}$ (conditional on $(e_\tau, M_{\tau^-})$), to which the data-processing inequality applies, yielding $\kappa_{\text{processing}} \le 1$ automatically. For Class 2 and Class 3, $\kappa_{\text{processing}} \le 1$ is a named structural commitment; the parrot architecture $M_{\tau^+} := G$ with $G \perp\!\!\!\perp \Omega_\tau$ given $(e_\tau, M_{\tau^-})$ produces $\kappa_{\text{processing}} = \infty$, explicitly outside scope. *Convention.* When both numerator and denominator vanish (no transferred goal-information *and* no residual ambiguity, e.g., a Class 1 architecture on goal-orthogonal evidence), set $\kappa_{\text{processing}} := 0$; the bound's right-hand side is then trivially zero.

### Axioms ^sec-axioms

The universal-constant route ([[#^sec-track2-mechanism]], Track 2) commits to three axioms on the bound's metric $d_{\mathcal{M}}$:

> [!hypothesis] (PI) Sufficient-statistic invariance across the natural category ^pi-axiom
> The bias bound's distance / divergence is a *natural assignment* on the category of standard parametric statistical models — for each model, a candidate distance or divergence — commuting with congruent Markov morphisms (sufficient statistics) in the sense of \citet{cencov-1982-stat-decision}. The induced object on $\mathcal{M}$ inherits this categorical assignment.

(PI) at full Markov-morphism strength is the *categorical* invariance Čencov's uniqueness theorem requires: the assignment must respect every sufficient-statistic morphism across the category, not merely smooth coordinate changes on a single fixed $\mathcal M$. (PI) alone admits both Riemannian metrics and $f$-divergences as candidates (the global Fisher-Rao spherical-arc bound and the Hellinger backstop in [[#^sec-track2-companions]] are the two (PI)-only theorems); (R) below adds the Riemannian-metric specifier needed for Čencov's local uniqueness statement.

> [!hypothesis] (R) Riemannian structure ^r-axiom
> The bound's metric $d_{\mathcal{M}}$ derives from a smooth Riemannian metric on $\mathcal{M}$.

(R) restricts the (PI)-invariant candidates to Riemannian metrics specifically, filtering out divergence-form alternatives (TV, $\chi^2$, Hellinger-as-divergence) that are (PI)-invariant as $f$-divergences but are not metric distances in the Riemannian sense.

> [!hypothesis] (K) KL second-order matching ^k-axiom
> $\mathrm{KL}(P_\theta \,\|\, P_{\theta+\delta}) = \tfrac{1}{2}d_{\mathcal{M}}^2(P_\theta, P_{\theta+\delta}) + O(d_{\mathcal{M}}^3)$.

(K) fixes the global scalar Čencov leaves free, pinning the bound's constant $C$ at $\sqrt{2}$. (R) and (K) are both implicit in any "$\mathbb{E}\,d \le C\sqrt{I}$" theorem-shape with second-order matching; we name them explicitly so the uniqueness statement of [[#^thm-fr-uniqueness]] has its hypotheses fully stated.

The transport-inequality route ([[#^sec-track1-mechanism]], Track 1) and the dimension-restricted slice-wise refinements ([[#^thm-umbrella]]'s Track 2 locally-tight instantiation) introduce additional regularity hypotheses inline with the theorems that invoke them. Throughout the paper we restrict to the *statistical-manifold sub-case*:

> [!hypothesis] (H1) Statistical-manifold sub-case ^h1-axiom
> The model state $M_t \in \mathcal{M}$ corresponds to a probability distribution $P_{M_t}$ over latent world-states, and $\mathcal{M}$ is locally a statistical manifold in the sense of \citet{amari-nagaoka-2000-info-geom}; $\mathcal{M}$, the goal-space, and the event-space are *standard Borel*, so regular conditional probabilities exist as Markov kernels \cite[Theorem 6.3]{kallenberg-2002-foundations}.

(H1) is satisfied by parametric Bayesian posterior families, exponential families, conjugate priors, and the parametric-belief-state subclass of LLMs that admits a natural distributional reading. The standard-Borel regularity is what makes the post-update chain rule (used in both Tracks) hold in the abstract-spaces form \cite[Theorem 3.4]{polyanskiy-wu-2024-info-theory}; \cite[Theorem 5.4]{gray-2011-entropy}.

*Coupled-class autoregressive connectivity (deferred).* Lemma E.4 ([[#^lem-attention-coupled]] in [[#^sec-attention-coupled-proof]]) establishes that plain decoder-only transformer attention — and the broader family of autoregressive sequence models with causally-aggregated cross-position mixers under a per-source non-degeneracy condition (linear attention \citep{katharopoulos-2020-linear-attention}, selective state-space models / Mamba \citep{gu-dao-2024-mamba}, RWKV \citep{peng-2023-rwkv}, RetNet \citep{sun-2023-retnet}, long-convolution / Hyena \citep{poli-2023-hyena}) — is structurally Class 3 by directed-graph reachability across layer depth. The result is a *downstream-output graph-reachability* claim, not a quantitative coupling-magnitude claim — quantitative magnitude lives in $\kappa_{\text{processing}}$ — and is robust without invoking the in-context-learning correspondence \cite{garg-tsipras-liang-valiant-2022-icl,akyurek-schuurmans-andreas-ma-zhou-2023-icl,vonoswald-2023-transformers-gd,xie-raghunathan-liang-ma-2022-icl-implicit-bayes} that the bias-bound *application* additionally invokes.
