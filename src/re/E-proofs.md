## Proofs of main results ^sec-proofs

This appendix collects full proofs deferred from §4–§5 of the main text. Proof structure: each section restates the formal claim from main text, then provides the full derivation. Auxiliary lemmas used in proofs are stated where they first arise.

### Track 1 cascade — full derivation ^sec-track1-proof

The umbrella theorem's Track 1 instantiation ([[#^thm-umbrella]] under (H1) + (H2$'$)) follows from a two-step composition: chain rule on the post-update law, then slice-wise Talagrand $T_2$.

> [!proof]
> *Step 1 — Chain rule of relative entropy on the post-update law.* By \citet[Theorem 2.5.3]{cover-thomas-2006-info-theory} applied to the conditional law of $M_{\tau^+}$ given $(e_\tau, M_{\tau^-})$ marginalized over $G$:
>
> $\mathbb{E}_G\bigl[\mathrm{KL}(P_{M_{\tau^+}\mid e, M_{\tau^-}, G}\,\|\,P_{M_{\tau^+}\mid e, M_{\tau^-}})\bigr] \;=\; I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})$.
>
> The (H1) standard-Borel regularity makes this hold in the abstract-spaces form (\citealt[Theorem 3.4]{polyanskiy-wu-2024-info-theory}; \citealt[Theorem 5.4]{gray-2011-entropy}). The right-hand side is *transferred* goal-information into the post-update model state.
>
> *Step 2 — Slice-wise Talagrand $T_2$.* Apply [[#^h2-prime]] slice-wise at each $G = g$:
>
> $W_2^2(P_{M_{\tau^+}\mid e, M, G=g},\, P_{M_{\tau^+}\mid e, M}) \;\leq\; C_{T_2} \cdot \mathrm{KL}(P_{M_{\tau^+}\mid e, M, G=g}\,\|\,P_{M_{\tau^+}\mid e, M})$.
>
> Take expectation over $G$ and substitute Step 1:
>
> $\mathbb{E}\bigl[W_2^2(P_{M_{\tau^+}\mid G},\, P_{M_{\tau^+}})\bigr] \;\leq\; C_{T_2} \cdot I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})$.
>
> Jensen's inequality on $\sqrt{x}$ delivers the distance form
>
> $\mathbb{E}\,W_2(P_{M_{\tau^+}\mid G},\, P_{M_{\tau^+}}) \;\leq\; \sqrt{C_{T_2}} \cdot \sqrt{I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})}$. $\square$

The architectural-corollary form ([[#^cor-architectural-factorization]] under (H$_\kappa$)) follows by substituting $I(G; M_{\tau^+}\mid e, M_{\tau^-}) \le \kappa_{\text{processing}} \cdot I(G; \Omega_\tau\mid e, M_{\tau^-})$ on the right-hand side; the substitution is *definitional* per [[#^eq-kappa-processing]], with the boundedness of $\kappa_{\text{processing}}$ being the substantive content of (H$_\kappa$).

### Lipschitz pushforward of $T_2$ — Stuart-school reduction ^sec-stuart-school-reduction

Track 1's (H2$'$) is most naturally verified through a two-step Lipschitz-pushforward of $T_2$ that matches the canonical Stuart-school cascade across the full Strand 2 hypothesis space — not only conjugate-Gaussian. The reduction is one textbook lemma + one elementary composition.

> [!lemma] Lipschitz pushforward of $T_2$ ^lem-pushforward-t2
> Let $(X, d_X)$ and $(Y, d_Y)$ be Polish metric spaces, $\mu$ on $X$ satisfying Talagrand $T_2(C)$ — that is, $W_2^{d_X}(\nu, \mu)^2 \le C\,\mathrm{KL}(\nu \,\|\, \mu)$ for all $\nu \ll \mu$ — and let $T: X \to Y$ be $L$-Lipschitz. Then $T_*\mu$ on $Y$ satisfies $T_2(L^2 C)$.

> [!proof]
> Let $\rho \ll T_*\mu$. Disintegrate $\mu(dx) = \mu_y(dx)\,T_*\mu(dy)$ along $T$. The lift $\tilde\rho(dx) := \mu_y(dx)\,\rho(dy)$ satisfies $T_*\tilde\rho = \rho$ and $\mathrm{KL}(\tilde\rho \,\|\, \mu) = \mathrm{KL}(\rho \,\|\, T_*\mu)$ (chain-rule decomposition with shared conditionals). For any coupling $\pi$ of $(\tilde\rho, \mu)$, the pushforward $(T \otimes T)_*\pi$ couples $(\rho, T_*\mu)$ with cost $\le L^2$ times the input cost. Hence $W_2^{d_Y}(\rho, T_*\mu)^2 \le L^2\,W_2^{d_X}(\tilde\rho, \mu)^2 \le L^2 C\,\mathrm{KL}(\tilde\rho \,\|\, \mu) = L^2 C\,\mathrm{KL}(\rho \,\|\, T_*\mu)$. (Standard $T_2$-tensorization-style argument; cf. \citealt{bobkov-gotze-1999-t2-subgaussian}.) $\square$

> [!theorem] Stuart-school reduction — generalized cascade-constant transfer ^thm-stuart-school-reduction
> Suppose:
>
> *(C1)* (Class 1 architecture.) $G \to \Omega_\tau \to M_{\tau^+}$ is a Markov chain conditional on $(e_\tau, M_{\tau^-})$.
>
> *(C2)* (Deterministic Bayesian update.) $M_{\tau^+} = \mu^{\Omega_\tau}$ for a measurable map $\Omega \mapsto \mu^\Omega$ on $\mathrm{supp}\,P_\Omega$.
>
> *(C3)* (Stuart-school Lipschitz posterior.) $W_2(\mu^\Omega, \mu^{\Omega'}) \le L_{\text{post}}\,\|\Omega - \Omega'\|$ uniformly on $\mathrm{supp}\,P_\Omega$.
>
> *(C4)* (Goal acts via parameter shift on a sub-Gaussian conditional likelihood.) $\Omega \mid G = g \sim P_{\Omega \mid \theta = \theta(g)}$ with $W_2^2(P_{\Omega \mid \theta_1}, P_{\Omega \mid \theta_2}) \le (2/\rho_{\text{noise}})\|\theta_1 - \theta_2\|^2$ — the canonical Gaussian-or-exponential-family setup for the conditional data law.
>
> Then:
>
> *(a)* (H2$'$) holds on the goal-marginal post-update model law with $C_{T_2} = 2L_{\text{post}}^2/\rho_{\text{noise}}$.
>
> *(b)* Track 1 yields $\mathbb{E}\,W_2^2(P_{M_{\tau^+}\mid G},\, P_{M_{\tau^+}}) \le (2L_{\text{post}}^2/\rho_{\text{noise}})\,I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})$.
>
> *(c)* The constant $2L_{\text{post}}^2/\rho_{\text{noise}}$ is the canonical Stuart-school cascade constant — recovered under the same Stuart-school hypotheses generically, not only on the conjugate-Gaussian instance.

> [!proof]
> Apply [[#^lem-pushforward-t2]] in two steps.
>
> *Step 1.* The conditional-data-law family $\theta \mapsto P_{\Omega\mid\theta}$ pushes forward $\rho_{\text{noise}}$-concentration on $\theta$ into $T_2(2/\rho_{\text{noise}})$ on the conditional data law (C4 directly).
>
> *Step 2.* The map $\Omega \mapsto \mu^\Omega$ is $L_{\text{post}}$-Lipschitz on $\mathrm{supp}\,P_\Omega$ (C3). [[#^lem-pushforward-t2]] gives $T_2(L_{\text{post}}^2 \cdot 2/\rho_{\text{noise}}) = T_2(C_{T_2})$ on $T_*P_\Omega = P_{M_{\tau^+}\mid e, M_{\tau^-}}$.
>
> (b) follows from Track 1's standard cascade ([[#^sec-track1-proof]]). (c) is the matching of constants. $\square$

Each Strand 2 paper — \citet{stuart-2010-acta}, \citet{sprungk-2020-local-lipschitz}, \citet{cvetkovic-2025-upper}, \citet{dolera-mainini-2023-aihp-lipschitz}, \citet{garbuno-inigo-2023-bayesian}, \citet{lie-sullivan-teckentrup-2017}, \citet{hosseini-hsu-taghvaei-2024-conditional-ot} — establishes a form of (C3) under increasingly weak hypotheses. [[#^thm-stuart-school-reduction]] is a single structural slot they all fit into; anywhere the Stuart-school cascade applies, Track 1 specializes to the same cascade constant under (C1)–(C4). The result is *not* a sub-case statement — Stuart-school proves outputs (matching lower bounds, multi-metric extensions, sub-Lipschitz refinements, contraction rates, randomized forward models) outside Track 1's reach. The averaged-over-goal form of Track 1 also cannot recover Stuart-school's pointwise pair-distance information on its own; the two literatures share machinery and exchange a constant, not theorem closures. Spike report at `spikes/A7-stuart-school-mapping/report.md` documents the boundary in full.

### Track 2 cascade — full derivation ^sec-track2-proof

The umbrella theorem's Track 2 instantiation (under (H1) + (H4$'$) + (PI) + (R) + (K)) follows in one step using the KL-to-Fisher-Rao expansion.

> [!proof]
> Apply [[#^lem-kl-fr-expansion]] under (H1) + (H4$'$) slice-wise at each $G = g$ to get
>
> $d_{FR}^2(P_{M_{\tau^+}\mid e, M, G=g},\, P_{M_{\tau^+}\mid e, M}) \;\leq\; 2\,\mathrm{KL}(P_{M_{\tau^+}\mid G=g}\,\|\,P_{M_{\tau^+}})\,(1 + o(1))$.
>
> Under (H4$'$) the remainder is controlled uniformly: with bounded Amari-Chentsov tensor $|T_{ijk}\delta^i\delta^j\delta^k| \le \mathcal{T}_\star\|\delta\|^3$ on the goal-induced neighborhood and minimum Fisher eigenvalue $\mathbf{I}_{\min} > 0$, the slice-wise inequality $d_{FR}^2(P_{M_{\tau^+}\mid G=g}, P_{M_{\tau^+}}) \le 2\,\mathrm{KL}_g(1 + R_3(\delta_\star))$ holds with $R_3(\delta_\star) = (\mathcal{T}_\star/3)\sqrt{2\delta_\star/\mathbf{I}_{\min}^3} \to 0$ as $\delta_\star \to 0$.
>
> Take expectation over $G$ and substitute the chain-rule identity from [[#^lem-chain-rule]]:
>
> $\mathbb{E}\bigl[d_{FR}^2(P_{M_{\tau^+}\mid G},\, P_{M_{\tau^+}})\bigr] \;\leq\; 2 \cdot I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-}) \cdot (1 + o(1))$.
>
> Jensen on $\sqrt{x}$ delivers the distance form
>
> $\mathbb{E}\,d_{FR}(P_{M_{\tau^+}\mid G},\, P_{M_{\tau^+}}) \;\leq\; \sqrt{2} \cdot \sqrt{I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})} \cdot (1 + o(1))$. $\square$

The constant $\sqrt{2}$ emerges from the second-order coefficient $\tfrac{1}{2}$ in the KL-to-Fisher expansion (\citealt{amari-nagaoka-2000-info-geom} §3.7 Theorem 3.1) — exactly what (K) crystallizes as a normalization. Outside (H4$'$), the locally-tight bound's $(1+o(1))$ remainder is no longer uniformly sharp; companion bounds in [[#^sec-track2-companions]] cover the moderate-to-large $I_M$ regime under strictly weaker hypotheses (Track 2 global, Hellinger backstop).

### No-go on Euclidean chart norms — full proof ^sec-no-go-proof

[[#^thm-no-go]]'s proof uses a chart-rescaling lemma plus a one-line consequence.

> [!lemma] Chart-rescaling sensitivity of Euclidean displacement ^lem-chart-rescaling
> Let $\mathcal{M}$ be a statistical manifold and $\phi: U \to \mathbb{R}^d$ a chart on an open set $U \subseteq \mathcal{M}$. For any $a > 0$, write $\phi_a := a\phi$ for the rescaled chart. For every pair of probability laws $\mu, \nu$ on $U$ (in particular, the goal-conditional and goal-marginal post-update laws of [[#^eq-bias-quantity]]):
> *(a)* The chart-Euclidean Wasserstein distance scales linearly: $W_2^{\phi_a}(\mu, \nu) = a\cdot W_2^\phi(\mu, \nu)$.
> *(b)* Conditional KL, conditional mutual information, Fisher-Rao geodesic distance, and Hellinger distance are all chart-invariant: they take the same value under $\phi$ and $\phi_a$.

> [!proof]
> *(a)* The pushforward under the linear map $x \mapsto ax$ rescales Euclidean distances by $a$, hence rescales any optimal coupling's transport cost.
> *(b)* KL depends only on the underlying densities and dominating measure (Radon-Nikodym derivatives are reparameterization-invariant). The Fisher metric tensor transforms covariantly under chart change, so the integrated geodesic distance is invariant. Hellinger as an $f$-divergence is reparameterization-invariant. $\square$

> [!proof]
> *Proof of [[#^thm-no-go]].* Suppose for contradiction that a coordinate-independent $C_0 < \infty$ exists such that for every chart $\phi$ on $\mathcal{M}$ and every architecture satisfying (H1)+(H2$'$) with non-zero post-update displacement,
>
> $\|\Delta M_{\text{bias}}\|_{\mathrm{Eucl},\,\phi} \le C_0 \sqrt{I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})}$.
>
> For any architecture realizing $W_2^\phi(P_{M_{\tau^+}\mid G,e,M_{\tau^-}}, P_{M_{\tau^+}\mid e,M_{\tau^-}}) > 0$ and finite positive transferred information, applying the supposed bound under the rescaled chart $\phi_a$ gives, by [[#^lem-chart-rescaling]],
>
> $a \cdot \|\Delta M_{\text{bias}}\|_{\mathrm{Eucl},\,\phi} \;=\; \|\Delta M_{\text{bias}}\|_{\mathrm{Eucl},\,\phi_a} \;\leq\; C_0\sqrt{I}$,
>
> with the right-hand side unchanged across charts. Taking $a \to \infty$ contradicts the fixed $C_0\sqrt{I}$. The same conclusion holds for the architectural-corollary form $C\sqrt{\kappa_{\text{processing}}\cdot I(G;\Omega\mid e, M)}$ under (H$_\kappa$): both sides inherit [[#^lem-chart-rescaling]]'s chart-(non)invariance, and the contradiction goes through verbatim. $\square$

The proof avoids type-shifts between Dirac points and pushforward laws, never invokes (H2$'$)-violating two-point constructions, and does not assert any specific value of $I$ — it only uses that some architecture realizes finite positive $W_2^\phi$ and finite positive $I$, automatic on any non-trivial goal-coupled architecture (e.g., the conjugate-Gaussian setup with any $\sigma, \tau > 0$ and a non-degenerate continuous goal distribution). The Gaussian scale family with two charts (Chart A: $\sigma$; Chart B: $\log\sigma$) is the canonical illustration: same intrinsic geometry, Chart-A Euclidean displacement grows linearly while Chart-B stays bounded as the operating scale grows.

### Čencov uniqueness and sharpness — full proof ^sec-fr-uniqueness-proof

[[#^thm-fr-uniqueness]] has two parts.

> [!proof]
> *Proof of (a) — Uniqueness of the metric.* (PI) + (R) invokes Čencov's uniqueness theorem \cite{cencov-1982-stat-decision} (modern treatment \citealt[Theorem 5.1]{ay-2017-information}): on $\mathcal{M}$, the Fisher information metric $\mathbf{I}$ is the unique (up to a global positive scalar $c > 0$) Riemannian metric invariant under Markov morphisms. Write $d_{\mathcal{M}} = \sqrt{c}\,d_{FR}$ where $d_{FR}$ is at the Amari-Nagaoka normalization $\mathbf{I}(\theta) = -\mathbb{E}[\nabla^2 \log p_\theta]$. The KL-to-Fisher second-order expansion (\citealt{amari-nagaoka-2000-info-geom} §3.7 Theorem 3.1) gives $\mathrm{KL}(P_\theta \| P_{\theta+\delta}) = \tfrac{1}{2} d_{FR}^2 + O(d_{FR}^3)$, so $\tfrac{1}{2}d_{\mathcal{M}}^2 = (c/2)d_{FR}^2 + O(d_{FR}^3)$. Constraint (K) requires $\tfrac{1}{2}d_{\mathcal{M}}^2$ agree with $\mathrm{KL}$ at second order, forcing $c = 1$ and $d_{\mathcal{M}} = d_{FR}$.

> [!proof]
> *Proof of (b) — Sharpness of the constant.* Use the symmetric two-point witness on the conjugate-Gaussian Class 1 (Separated) family. Take $G \in \{-a, +a\}$ uniform with $\beta(g) = g$, prior $\theta \sim \mathcal{N}(0, \tau^2)$, observation $\Omega \mid G = g \sim \mathcal{N}(g, \sigma^2)$, and posterior $M_{\tau^+} = L_{\text{post}}\Omega$. Then $P_{M_{\tau^+}\mid G=g} = \mathcal{N}(L_{\text{post}}g,\, L_{\text{post}}^2\sigma^2)$ and the goal-marginal is the equal-weight mixture of these two Gaussians (centered at $\pm L_{\text{post}}a$). For $a \to 0$ at fixed ratio $a/\sigma$ the mixture's variance excess is $L_{\text{post}}^2 a^2 = O(a^2)$ — second-order — while the mean-shift is first order, so the mixture is approximately Gaussian at $\mathcal{N}(0,\, L_{\text{post}}^2\sigma^2)$ to leading order. The Fisher-Rao distance between two equal-variance univariate Gaussians is $|\mu_1 - \mu_2|/\sigma_{\text{shared}}$, giving $d_{FR}(P_{M_{\tau^+}\mid G=\pm a}, P_{M_{\tau^+}}) = a/\sigma$ at leading order, *exactly equal across both goal slices by symmetry*. Hence $\mathrm{Var}_G(d_{FR}) = O(a^4)$ and Jensen is tight in the small-$a$ limit. The transferred information for binary-Gaussian channels at small SNR is $I_M = a^2/(2\sigma^2) + O(a^4)$. Therefore $\mathbb{E}\,d_{FR}/\sqrt{I_M} = (a/\sigma)/\sqrt{a^2/(2\sigma^2)} \cdot (1+o(1)) = \sqrt 2\,(1+o(1))$ as $a \to 0$, and equivalently $\mathbb{E}\,d_{FR}^2/I_M \to 2$. The sharpness holds at the first-moment level — Jensen is asymptotically tight by the symmetry-induced near-constancy of $d_{FR}$ across slices — so any candidate constant $C < \sqrt 2$ fails on this family. Combined with (a), $C = \sqrt 2$ is the unique sharp upper-bound constant. $\square$

The upshot: once we adopt (PI) at full Markov-morphism strength, plus Riemannian structure, plus KL as the cascade's information coordinate, the *only* such-invariant choice of norm on $\mathcal{M}$ is Fisher-Rao, and the *unique sharp* upper-bound constant is $\sqrt{2}$. Alternative chart-independent commitments — TV with Pinsker, Hellinger-as-divergence, $\chi^2$, Rényi — give weaker bounds: TV-Pinsker is non-tight (the constant is universal but the inequality is loose except at coincident measures); Hellinger-as-divergence and $\chi^2$-as-divergence violate (R); switching divergences on the RHS violates (K). The global [[#^thm-track2-global]]'s $\pi/\sqrt{2}$ is also sharp in its own (PI)-only regime — achieved in the limit $\mathrm{Hel} \to 1$ at the unit $L^2$-sphere's antipode.

### Coupled-class attention connectivity — full proof ^sec-attention-coupled-proof

> [!proof]
> *Proof of [[#^lem-attention-coupled]].* By induction on layer depth.
>
> *Layer 0 (embedding).* $h_0^{(i)}$ depends only on $X_i$ — the position-$i$ token embedding. Goal positions $i_G$ produce embeddings $h_0^{(i_G)}$ that are functions only of the goal tokens at those positions; same for evidence positions $i_E$. No cross-position dependence yet.
>
> *Layer $\ell \ge 1$.* A standard transformer block (pre-LN or post-LN) computes
>
> $h_\ell^{(j)} = h_{\ell-1}^{(j)} + \mathrm{Attn}_\ell(\mathrm{LN}(h_{\ell-1}))^{(j)} + \mathrm{MLP}_\ell(\mathrm{LN}(h_{\ell-1}^{(j)}))$,
>
> where LayerNorm and the MLP are *position-wise* (the operation at position $i$ depends only on $h_{\ell-1}^{(i)}$, not on other positions). This induces a directed position-graph with two edge types at each layer: (i) a *same-position* residual edge $h_{\ell-1}^{(j)} \to h_\ell^{(j)}$ always present (via the residual stream); (ii) *cross-position* attention edges $h_{\ell-1}^{(i)} \to h_\ell^{(j)}$ present whenever $\mathrm{Attn}_\ell^{(j,i)}(\theta) \ne 0$. Position-wise LayerNorm and MLP preserve both edge types.
>
> *Inductive claim.* For every $\ell \ge 0$ and every input position $i \le j$, $h_\ell^{(j)}$ has a directed-graph path back to position $i$ in the input.
>
> *Inductive step.* The same-position residual chain gives $i = j$. For $i \ne j$ with $i \le j$, non-degenerate attention at any single layer $\ell' \le \ell$ along the path gives a cross-position edge $h_{\ell'-1}^{(i)} \to h_{\ell'}^{(j)}$, which composes with the residual chain on either side to yield a directed-graph path from input position $i$ to $h_\ell^{(j)}$.
>
> *Coupled-class conclusion.* For any goal position $i_G \le j$, $h_\ell^{(j)}$ has a path back to position $i_G$ in the input whenever attention is non-degenerate on the $(j, i_G)$ edge at some layer $\ell' \le \ell$. So under non-degenerate attention, $G$ (encoded at positions $i_G$) is causally upstream of every quantity contributing to a post-update model state read off from position $j \ge \max(i_G \cup i_E)$. Class 3 (Coupled) by construction.
>
> *Robustness to architectural variants.*
> - RMSNorm, GroupNorm, FlashAttention preserve the position-graph: position-wise normalization in the first two cases; mathematically-equivalent attention implementation in the third.
> - Causal masking preserves $\mathrm{Attn}_\ell^{(j, i_G)} \ne 0$ for $i_G \le j$ — the regime the lemma covers.
> - Sliding-window or sparse attention preserves connectivity by composition across layers when the window/sparsity pattern admits a multi-hop path from $i_G$ to $j$, which is the case for trained LLMs in their operating regime.
> - Architectures with explicit goal-to-output attention masking, or token-dropping at intermediate layers, fall outside the lemma's scope and are appropriately Class 2 (Partial). $\square$

[[#^lem-attention-coupled]] establishes a *downstream-output graph-reachability* claim: at every layer and every position causally downstream of the goal and evidence under standard causal masking, the activation has a directed-graph path back to at least one goal position. *Three caveats:*

- *Graph reachability is not the same as causal-influence magnitude.* A directed-graph path with near-zero attention weights produces a formal edge with negligible quantitative influence on $h_\ell^{(j)}$. The connectivity claim is therefore *structural* — about the existence of a path, not the magnitude of effect — and translates into Class 3 (Coupled) classification under the Markov-blanket conditional-independence reading. Bounding $\kappa_{\text{processing}}$ requires the architectural-bandwidth conditions of [[#^sec-h-kappa-suff]] (information-bottleneck on the goal channel; bounded direct-channel capacity uniformly over operating distributions).
- *Causal masking restricts the lemma's scope to downstream positions.* For $j < \min(i_G)$ — positions strictly upstream of any goal token — there is no causal path from goal to $h_\ell^{(j)}$ under causal attention masks; those positions are Class 1 (Separated) in their own right.
- *Sparse and sliding-window attention require a multi-hop reachability assumption.* The connectivity proof composes single-layer attention edges across layers; for sliding-window or sparse-attention architectures, multi-hop connectivity from $i_G$ to $j$ requires at least one composition of single-layer paths through the window/sparsity pattern. Architectures whose sparsity pattern excludes goal-to-output communication entirely fall outside the lemma's hypothesis and are Class 2 (Partial).

The bias-bound *interpretation* — bounding the displacement of an implicit posterior under goal-conditional re-prompting — additionally invokes the in-context-learning correspondence \cite{garg-tsipras-liang-valiant-2022-icl,akyurek-schuurmans-andreas-ma-zhou-2023-icl,vonoswald-2023-transformers-gd,xie-raghunathan-liang-ma-2022-icl-implicit-bayes} between the next-token distribution and an implicit posterior. The structural Coupled-class claim of [[#^lem-attention-coupled]] is robust without it; the bias-bound *application* is conditional on the in-context-learning correspondence, which has its own scope (in-distribution prompts: tight; OOD/jailbreak: degraded to a bound on output-distribution displacement rather than belief-state displacement).
