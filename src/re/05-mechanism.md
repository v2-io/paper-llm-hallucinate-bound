## Mechanism ^sec-mechanism

Both tracks bridge to the bound through the same move: a chain rule of relative entropy applied directly to the post-update law, marginalized over the goal. This *is* the structural composition of the two literatures — the Bayesian-inverse-problems posterior-stability machinery and the architectural classification meet at this identity.

> [!lemma] Chain rule on the post-update law ^lem-chain-rule
> Under (H1), $\mathbb{E}_G\bigl[\mathrm{KL}(P_{M_{\tau^+}\mid e, M_{\tau^-}, G} \,\|\, P_{M_{\tau^+}\mid e, M_{\tau^-}})\bigr] \;=\; I(G;\,M_{\tau^+}\mid e_\tau, M_{\tau^-})$.

The identity is exact. The right-hand side is *transferred* goal-information — the actually-realized coupling between $G$ and the post-update model state. The left-hand side averages KL between goal-conditional and goal-marginal post-update laws. (H1)'s standard-Borel regularity is what makes this identity hold in the abstract-spaces form (\citealt[Theorem 3.4]{polyanskiy-wu-2024-info-theory}; \citealt[Theorem 5.4]{gray-2011-entropy}). Combined with either a transport inequality on the post-update law or a Fisher-Rao second-order expansion of KL, the bound follows by taking expectation over $G$ and applying Jensen.

### Track 1 — transport-inequality cascade ^sec-track1-mechanism

Two steps.

**Step 1.** Apply [[#^lem-chain-rule]]: $\mathbb{E}_G[\mathrm{KL}_g] = I_M$ where $\mathrm{KL}_g$ is the goal-conditional-vs-marginal KL at $G = g$ and $I_M = I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})$.

**Step 2.** Apply (H2$'$) slice-wise: $W_2^2(P_{M_{\tau^+}\mid G=g}, P_{M_{\tau^+}}) \le C_{T_2} \cdot \mathrm{KL}_g$. Take expectation over $G$ and substitute Step 1:

$$\mathbb{E}\bigl[W_2^2(P_{M_{\tau^+}\mid G},\, P_{M_{\tau^+}})\bigr] \;\leq\; C_{T_2} \cdot I_M.$$

Jensen on $\sqrt{\,\cdot\,}$ delivers the distance form $\mathbb{E}\,W_2 \le \sqrt{C_{T_2}\,I_M}$.

The cascade is composed from textbook information-theoretic and transport-inequality machinery — Otto-Villani for the LSI-implies-$T_2$ direction, Bakry-Émery for the $K$-strong-log-concavity-implies-LSI direction, Gozlan's characterization of $T_2$ via dimension-free sub-Gaussian Lipschitz concentration, Bobkov-Götze for the strictly weaker single-Lipschitz-function $T_1$ version. The contribution is the application of these machinery elements to the goal-conditional bias quantity on the post-update law: there is no separate posterior-pushforward step, because the chain rule lives on the post-update law directly. Full proof and (H2$'$) sufficient-condition verifications in [[#^sec-h2-prime-suff]].

### Track 2 — Fisher-Rao expansion ^sec-track2-mechanism

One step.

> [!lemma] KL-to-Fisher-Rao second-order expansion ^lem-kl-fr-expansion
> On the *ambient L²-sphere of $\sqrt p$* equipped with the Fisher metric $\mathbf{I}$ (the maximal statistical manifold, of which every probability distribution is a point), for nearby $P, Q$: $\mathrm{KL}(P \,\|\, Q) = \tfrac{1}{2}d_{FR}^2(P, Q) + O(d_{FR}^3)$ in the Amari-Nagaoka spherical-arc convention.

This is the infinitesimal form of the Bregman divergence on the exponential-family Fenchel geometry — exact at second order, tight in the small-information regime (\citealt{cover-thomas-2006-info-theory} §12.5; \citealt{amari-nagaoka-2000-info-geom} §3.7 Theorem 3.1). The ambient framing absorbs the goal-marginal-baseline-as-mixture concern: $P_{M_{\tau^+}\mid G=g}$ and $P_{M_{\tau^+}}$ (which is a goal-mixture, generally outside any parametric submanifold) are both points on the ambient L²-sphere by construction; the spherical-arc expansion applies regardless of submanifold structure. Apply [[#^lem-kl-fr-expansion]] slice-wise at each $G = g$ under (H4$'$) (every goal-conditional slice uniformly close to the goal-marginal in the ambient arc, so the expansion is sharp slice-wise with controlled remainder). Take expectation over $G$ and substitute [[#^lem-chain-rule]]:

$$\mathbb{E}\bigl[d_{FR}^2(P_{M_{\tau^+}\mid G},\, P_{M_{\tau^+}})\bigr] \;\leq\; 2 \cdot I_M \cdot (1 + o(1)).$$

Jensen on $\sqrt{\,\cdot\,}$: $\mathbb{E}\,d_{FR} \le \sqrt{2}\sqrt{I_M}\,(1 + o(1))$.

The $(1+o(1))$ is the third-order remainder, controlled uniformly under (H4$'$) by the Amari-Chentsov tensor and the minimum Fisher eigenvalue along the goal-induced geodesic. The constant $\sqrt{2}$ is what (PI)+(R)+(K) buys: Čencov uniqueness ([[#^thm-fr-uniqueness]]) forces Fisher-Rao with that exact constant.

**Outside (H4$'$).** When rare goals carry disproportionately large transferred information, or when the operating distribution sits at moderate-to-large $I_M$, the slice-wise expansion is no longer uniformly sharp. Track 2 has globally-valid companion bounds — Fisher-Rao at the universal constant $2$ via Rényi-1/2 monotonicity composed with the exact chord-arc identity, and a direct Hellinger statement at $1/\sqrt{2}$ — under (H1)+(PI) only, no (R), (K), or (H4$'$). The full taxonomy, proofs, and sharpness witness are in [[#^sec-track2-companions]]. The $\sqrt 2$ overhead vs. the locally-tight $\sqrt 2$ is exactly the chord-arc factor at the unit $L^2$-sphere's antipode in squared-distance form — a geometric maximum, not a slack — and is the cleanest possible (PI)-invariant Fisher-Rao-to-KL bound under (PI) alone.

### No-go — chart rescaling ^sec-no-go-mechanism

The proof of [[#^thm-no-go]] is short. Under any chart $\phi$ on $\mathcal{M}$ and rescaling $\phi_a := a\phi$ (a smooth coordinate change the underlying geometry treats as identity):

- *Chart-Euclidean $W_2$ scales linearly:* $W_2^{\phi_a}(\mu, \nu) = a\cdot W_2^{\phi}(\mu, \nu)$ — the pushforward under $x \mapsto ax$ rescales transport cost by $a$.
- *KL, conditional MI, Fisher-Rao geodesic, Hellinger — all chart-invariant:* relative entropies depend only on densities and dominating measures (reparameterization-invariant); Fisher metric tensor transforms covariantly so integrated geodesic distance is invariant; Hellinger as $f$-divergence is reparameterization-invariant.

For any architecture realizing finite positive $W_2^\phi > 0$ and finite positive transferred information $I$, the candidate universal-constant inequality would have to satisfy $a \cdot \|\Delta M_{\text{bias}}\|_{\mathrm{Eucl}, \phi} \le C_0\sqrt{I}$ for all $a > 0$ at fixed $C_0\sqrt{I}$. Taking $a \to \infty$ contradicts the fixed right-hand side. Both required quantities ($W_2^\phi > 0$ and $I > 0$) are automatic on any non-trivial goal-coupled architecture — for instance, the conjugate-Gaussian Class 1 setup with any $\sigma, \tau > 0$ and a non-degenerate continuous goal distribution. The Gaussian scale family with two charts (Chart A: $\sigma$; Chart B: $\log\sigma$) is the canonical illustration: the same intrinsic geometry, Chart-A Euclidean displacement grows linearly with the operating scale while Chart-B stays bounded.

The implication is constructive. To get a universal constant the bound must be stated in a coordinate-invariant norm — one that respects the underlying geometry of the statistical manifold rather than an arbitrary chart on it. This is exactly the role Fisher-Rao plays under (PI)+(R)+(K). Alternative chart-independent commitments (TV with Pinsker, Hellinger-as-divergence, $\chi^2$, Rényi) yield strictly weaker bounds — the no-go does not just say "commit to something intrinsic"; it says *exactly* what to commit to.
