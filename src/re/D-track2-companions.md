## Track 2 companions and parametric Euclidean translations ^sec-track2-companions

The locally-tight Fisher-Rao bound ([[#^thm-umbrella]]'s Track 2 instantiation) is one of three Fisher-Rao-spine bounds; the other two — a globally-valid Fisher-Rao backstop and a Hellinger backstop — recover under strictly weaker hypotheses, with universal constants of their own. Together with the conjugate-Gaussian Euclidean translation (review-defusing the no-go's apparent scale-family pathology) and the exponential-family Euclidean generalization, they form the Track 2 family.

### Track 2 globally-valid backstop ^sec-track2-global

Outside the uniform-locality regime — when a few rare goals carry disproportionately large transferred information, or when the operating distribution sits at moderate-to-large $I_M$ — the slice-wise expansion's $(1+o(1))$ remainder is no longer uniformly sharp. A global Fisher-Rao bound is available under strictly weaker hypotheses, at the cost of a slightly larger constant.

> [!theorem] Track 2 global backstop ^thm-track2-global
> Under (H1) and (PI) — for all values of transferred information,
>
> $\mathbb{E}\,d_{FR}\bigl(P_{M_{\tau^+}\mid e, M_{\tau^-}, G},\, P_{M_{\tau^+}\mid e, M_{\tau^-}}\bigr) \;\leq\; 2\,\sqrt{I(G;\,M_{\tau^+}\mid e_\tau, M_{\tau^-})}$.
>
> The constant $2$ is universal, dimension-free, global — no small-information condition required, no (R), no (K). Tightest form: $\mathbb{E}\,d_{FR} \le 2\arccos\!\bigl(\exp(-I_M/2)\bigr) \le \min\bigl(2\sqrt{I_M},\,\pi\bigr)$, by Jensen on the concave map $\psi(K) := 2\arccos(\exp(-K/2))$ — $\psi$ is concave on $[0, \infty)$ (verifiable by $\psi'(K) = \exp(-K/2)/\sqrt{1 - \exp(-K)}$ decreasing). The constant $2$ is sharp — approached arbitrarily closely as $N \to \infty$ on a symmetric $N$-point family ([[#^sec-track2-global-sharpness]] below).

> [!proof]
> By Rényi-divergence monotonicity \cite{vanerven-harremoes-2014-renyi}, $D_{1/2}(P\|Q) \le D_1(P\|Q) = \mathrm{KL}(P\|Q)$, equivalently $\mathrm{BC}(P,Q) := \int\sqrt{pq} \ge \exp(-\mathrm{KL}/2)$. Combined with the chord-arc *identity* (not inequality) $d_{FR} = 2\arccos(\mathrm{BC})$ from the unit-$L^2$-sphere geometry: $d_{FR} \le 2\arccos(\exp(-\mathrm{KL}/2))$. Define $\phi(K) := 4\arccos^2(\exp(-K/2))$; series expansion at $K = 0$ gives $\phi(K)/K \to 4$, decreasing thereafter, so $\phi(K) \le 4K$ globally. Hence $d_{FR}^2 \le 4\,\mathrm{KL}$ slice-wise. Take $\mathbb{E}_G$, substitute the chain rule [[#^lem-chain-rule]]: $\mathbb{E}\,d_{FR}^2 \le 4 I_M$. Jensen on $\sqrt x$: $\mathbb{E}\,d_{FR} \le 2\sqrt{I_M}$. The tightest form uses concavity of $\phi$ before Jensen on $\sqrt x$. $\square$

The $\sqrt 2$ overhead vs. the locally-tight $\sqrt 2$ — i.e., $2 / \sqrt 2 = \sqrt 2$ in raw constant ratio — is *exactly* the chord-arc factor at the unit $L^2$-sphere's antipode in squared-distance form. Under (PI) alone, the Bhattacharyya-coefficient pseudometric $d_{FR} = 2\arccos(\mathrm{BC})$ is automatically (PI)-invariant ($\mathrm{BC}$ is an $f$-divergence), and the bound $d_{FR} \le 2\sqrt{\mathrm{KL}}$ is the cleanest possible (PI)-invariant Fisher-Rao-to-KL bound; (R) + (K) add the local refinement to $\sqrt 2$. This composition (exact chord-arc identity + Rényi-1/2 monotonicity) is strictly tighter than the (chord-arc inequality + Tsybakov 2.4) composition by factor $\pi/(2\sqrt 2) \approx 1.11$ — Tsybakov 2.4 is loose by factor 2 at small $\mathrm{KL}$ ($\mathrm{Hel}^2 \approx \mathrm{KL}/4$ locally vs Tsybakov's $\mathrm{Hel}^2 \le \mathrm{KL}/2$), and Rényi-1/2 monotonicity recovers the lost factor.

#### Sharpness witness ^sec-track2-global-sharpness

The constant $2$ is sharp via a symmetric $N$-point construction. Take $G$ uniform on $\{1, \ldots, N\}$ with $P_{M_{\tau^+}\mid G=g}$ uniform on the $N-1$ atoms other than $g$. By symmetry $P_{M_{\tau^+}}$ is uniform on all $N$ atoms, so $\mathrm{KL}(P_{M_{\tau^+}\mid G=g}\|P_{M_{\tau^+}}) = \log\tfrac{N}{N-1}$ (constant in $g$, so $I_M = \log\tfrac{N}{N-1}$) and $\mathrm{BC} = \sqrt{(N-1)/N}$, giving $d_{FR} = 2\arcsin(1/\sqrt N)$ (also constant in $g$, so $\mathrm{Var}_G(d_{FR}) = 0$ and Jensen is tight). The ratio $\mathbb{E}\,d_{FR}/\sqrt{I_M} = 2\arcsin(1/\sqrt N)/\sqrt{\log\tfrac{N}{N-1}} \to 2$ at rate $1 - 1/(12 N) + O(N^{-2})$ as $N \to \infty$. Numerical confirmation: $N = 100$ achieves $99.92\%$ saturation, $N = 1000$ achieves $99.992\%$. The discrete-alphabet structure — large vocabulary $|V|$ admitting near-disjoint goal-conditional supports — is exactly the structural shape adversarial / jailbreak prompts exploit; the witness is the natural worst-case for goal-coupled architectures.

### Hellinger backstop ^sec-hellinger

The chord companion to [[#^thm-track2-global]]'s arc bound, with the cleanest universal constant.

> [!theorem] Hellinger backstop ^thm-hellinger
> Under (H1) and (PI) — for all values of transferred information,
>
> $\mathbb{E}\,\mathrm{Hel}\bigl(P_{M_{\tau^+}\mid e, M_{\tau^-}, G},\, P_{M_{\tau^+}\mid e, M_{\tau^-}}\bigr) \;\leq\; (1/\sqrt{2}) \cdot \sqrt{I(G;\,M_{\tau^+}\mid e_\tau, M_{\tau^-})}$.
>
> Under (H$_\kappa$), the architectural factorization recovers: $\mathbb{E}\,\mathrm{Hel} \le (1/\sqrt{2})\sqrt{\kappa_{\text{processing}}\cdot I(G;\,\Omega\mid e, M)}$.

> [!proof]
> By \citealt[Lemma 2.4]{tsybakov-2009-nonparametric}, $2\mathrm{Hel}^2(P, Q) \le \mathrm{KL}(P \| Q)$ globally for all probability measures. Apply slice-wise at each $G = g$, take expectation over $G$, and substitute the chain rule [[#^lem-chain-rule]]. $\square$

Hellinger satisfies (PI) — it is an $f$-divergence with $f(t) = (\sqrt{t}-1)^2/2$ preserved under Markov morphisms (Csiszár 1967; Liese-Vajda 1987) — and is locally proportional to Fisher-Rao on the unit-sphere representation. Throughout we adopt the *standard statistician's* Hellinger convention $\mathrm{Hel}^2(P,Q) := \tfrac{1}{2}\|\sqrt p - \sqrt q\|_{L^2}^2 = 1 - \int\sqrt{pq}$, so $\mathrm{Hel} \in [0, 1]$, and the *Amari-Nagaoka* Fisher-Rao convention $d_{FR}(P,Q) = 2\arccos\int\sqrt{pq}$ (twice the great-circle arc on the unit sphere of $\sqrt p$ in $L^2$, $d_{FR} \in [0, \pi]$). Different conventions in the literature differ by factors of 2; the forms above are the ones consistent with $\mathrm{Hel} \in [0, 1]$, $d_{FR} \in [0, \pi]$, and the $2\mathrm{Hel}^2 \le \mathrm{KL}$ inequality used in the proof.

The three Fisher-Rao-spine bounds — locally-tight $\sqrt{2}$ (under (H1)+(H4$'$)+(PI)+(R)+(K)), globally-valid $2$ ([[#^thm-track2-global]], under (H1)+(PI) only), and Hellinger chord $1/\sqrt{2}$ ([[#^thm-hellinger]], under (H1)+(PI) only) — all operate on the unit $L^2$-sphere of $\sqrt p$ via the Amari-Nagaoka spherical-arc convention adopted in [[#^sec-bias-quantity]]. The local theorem under (PI)+(R)+(K)+(H4$'$) coincides with intrinsic Fisher-Rao on parametric submanifolds at second order; the global theorems under (PI) alone bound the *ambient* spherical-arc pseudometric and apply to any pair of probability distributions regardless of submanifold structure. The hypothesis sets are strictly nested and the bounds use the same chord-arc geometry of the $L^2$-sphere; the global constants (2 for the arc, $1/\sqrt 2$ for the chord) are companion bounds at the antipode.

### Hellinger-Fisher-Rao chord-arc geometry ^sec-chord-arc

> [!lemma] Global chord-arc bound on the unit $L^2$-sphere ^lem-chord-arc
> For any probability measures $P, Q$, $d_{FR}(P, Q) \le \pi \cdot \mathrm{Hel}(P, Q)$, with equality at the antipode $\mathrm{Hel}(P, Q) = 1$ (correspondingly $d_{FR}(P, Q) = \pi$).

> [!proof]
> From $d_{FR} = 4\arcsin(\mathrm{Hel}/\sqrt{2})$, define $\phi: (0, 1] \to (0, \pi]$ by $\phi(h) := 4\arcsin(h/\sqrt{2})/h$, so $d_{FR}/\mathrm{Hel} = \phi(\mathrm{Hel})$. Set $g(h) := 4\arcsin(h/\sqrt{2})$. Differentiating: $g'(h) = 4/\sqrt{2 - h^2}$ for $h \in [0, \sqrt{2})$, $g''(h) = 4h/(2 - h^2)^{3/2} > 0$ on $(0, \sqrt{2})$ — so $g$ is *strictly convex* on this interval, with $g(0) = 0$. By the secant-slope monotonicity for convex functions vanishing at zero, $\phi(h) = g(h)/h$ is monotonically increasing on $(0, \sqrt{2})$, with limits $\lim_{h \to 0^+}\phi(h) = g'(0) = 4/\sqrt{2} = 2\sqrt{2}$ and $\phi(1) = g(1) = 4\arcsin(1/\sqrt{2}) = \pi$. Hence $\phi(h) \le \pi$ for all $h \in (0, 1]$, with equality at $h = 1$. $\square$

**Local proportionality.** As $d_{FR} \to 0$, $\mathrm{Hel} \approx d_{FR}/(2\sqrt{2})$, so [[#^thm-umbrella]]'s Track 2 locally-tight bound $\mathbb{E}\,d_{FR} \le \sqrt{2 I_M}$ jointly with [[#^lem-chord-arc]] gives $\mathbb{E}\,\mathrm{Hel} \lesssim (1/2)\sqrt{I_M}$ in the small-information limit — *tighter* than [[#^thm-hellinger]]'s global $(1/\sqrt{2})\sqrt{I_M}$ by a factor of $\sqrt{2}$. So in the (H4$'$) regime, [[#^thm-umbrella]] + [[#^lem-chord-arc]] jointly give the tightest Hellinger bound; [[#^thm-hellinger]] (under (PI) only, no (H4$'$)) is the global statement.

### Conjugate-Gaussian Euclidean translation ^sec-conjugate-gauss-euclidean

When (H1) is realized by a parametric family with known Fisher information, the locally-tight Fisher-Rao bound translates to an explicit Euclidean bound on parameter displacement. The conjugate-Gaussian case is paradigmatic and review-defusing: *Euclidean displacement does not blow up* in the prior-dominant limit, contrary to a naive reading of the no-go.

> [!theorem] Conjugate-Gaussian Euclidean bound ^thm-conjugate-gauss-euclidean
> Under the conjugate-Gaussian setup ($\theta \sim \mathcal{N}(0,\tau^2)$, $\Omega \mid \theta \sim \mathcal{N}(\theta, \sigma^2)$, goal-conditional likelihood-mean shift $\Omega \mid G \sim \mathcal{N}(\beta(G), \sigma^2)$), the post-update parameter law is the Gaussian $\mu_+ \mid G \sim \mathcal{N}(L_{\text{post}}\beta(G),\, L_{\text{post}}^2\sigma^2)$ with $L_{\text{post}} = \tau^2/(\sigma^2+\tau^2)$. The locally-tight Fisher-Rao bound translates to the Euclidean bound on random-parameter displacement
>
> $\mathbb{E}\,|\Delta \mu_+|_{\text{Eucl}} \;\leq\; L_{\text{post}}\,\sigma \cdot \sqrt{2 I_M} \cdot (1 + o(1))$,
>
> with prefactor $L_{\text{post}}\,\sigma = \tau^2\sigma/(\sigma^2+\tau^2) \le \tau/2$ uniformly. Under (H$_\kappa$), $\mathbb{E}\,|\Delta\mu_+|_{\text{Eucl}} \le L_{\text{post}}\sigma\sqrt{2\kappa_{\text{processing}}\,I(G;\Omega \mid e, M)}(1+o(1))$.

> [!proof]
> The post-update parameter law $\mu_+\mid G$ is Gaussian with mean $L_{\text{post}}\beta(G)$ and variance $L_{\text{post}}^2\sigma^2$ (variance preserved across goals because $\sigma_{\text{post}}^2$ is fixed by the conjugate-update structure). The Fisher metric on the manifold $\{\mathcal{N}(\mu, L_{\text{post}}^2\sigma^2) : \mu \in \mathbb{R}\}$ in the $\mu$-coordinate is $\mathbf{I}(\mu) = 1/(L_{\text{post}}^2\sigma^2)$, so the Fisher-Rao geodesic distance between two such laws is $d_{FR}(\mu_1, \mu_2) = |\mu_1-\mu_2|/(L_{\text{post}}\sigma)$ — a flat metric pulled back from $\mathbb{R}$. Hence $|\Delta\mu_+|_{\text{Eucl}} = L_{\text{post}}\sigma \cdot d_{FR}$. Take expectations and substitute the locally-tight Fisher-Rao bound. $\square$

The prefactor $L_{\text{post}}\sigma = \tau^2\sigma/(\sigma^2+\tau^2)$ is bounded above by $\tau/2$ uniformly (AM-GM at the maximizer $\sigma = \tau$) and *vanishes in both extreme limits*: $L_{\text{post}}\sigma \to 0$ as $\sigma \to \infty$ (very noisy observations: the architecture learns essentially nothing from $\Omega$ regardless of goal) and $L_{\text{post}}\sigma \to 0$ as $\sigma \to 0$ (very sharp observations: $L_{\text{post}}\to 1$ but $\sigma\to 0$, so even though the posterior tracks data tightly the data variance vanishes). Maximum at balanced $\sigma=\tau$. The naive "$\sigma\sqrt{2I}$" reading is wrong (correct prefactor is $L_{\text{post}}\sigma$); the "$\sigma_{\text{post}}\sqrt{2I}$" reading is *also* wrong (it conflates inside-posterior covariance $\sigma_{\text{post}}^2 = L_{\text{post}}\sigma^2$ with parameter-law variance $L_{\text{post}}^2\sigma^2$). The [[#^sec-no-go]] no-go still applies as stated to *charts*: $L_{\text{post}}\sigma$ is family-specific.

### Exponential-family Euclidean generalization ^sec-exp-family-euclidean

For an exponential family $P_\theta(x) = h(x)\exp(\theta^\top T(x) - A(\theta))$ with natural parameter $\theta \in \Theta \subseteq \mathbb{R}^d$ and log-partition $A$, the Fisher information metric is $\mathbf{I}(\theta) = \nabla^2 A(\theta)$. The infinitesimal Fisher-Rao expansion gives $d_{FR}^2(P_{\theta_1}, P_{\theta_2}) = (\theta_1 - \theta_2)^\top \mathbf{I}(\theta^*)(\theta_1 - \theta_2) + O(\|\theta_1-\theta_2\|^3)$ for $\theta^*$ on the geodesic between $\theta_1, \theta_2$. So Euclidean displacement on the natural parameter satisfies $\|\theta_1 - \theta_2\|^2 \le \mathbf{I}_{\min}^{-1} \cdot d_{FR}^2$ where $\mathbf{I}_{\min}$ is the minimum eigenvalue of $\mathbf{I}$ along the geodesic.

> [!theorem] Exponential-family Euclidean bound ^thm-exp-family
> For an exponential family in natural-parameter coordinates with Fisher-information minimum-eigenvalue $\mathbf{I}_{\min}$ along the goal-induced geodesic, the locally-tight Fisher-Rao bound translates to
>
> $\mathbb{E}\,\|\Delta\theta_{\text{bias}}\|_{\text{Eucl}} \;\leq\; \mathbf{I}_{\min}^{-1/2} \cdot \sqrt{2 I_M} \cdot (1 + o(1))$,
>
> and under (H$_\kappa$): $\mathbb{E}\,\|\Delta\theta_{\text{bias}}\|_{\text{Eucl}} \le \mathbf{I}_{\min}^{-1/2}\sqrt{2\kappa_{\text{processing}}\,I(G;\Omega \mid e, M)}(1+o(1))$.

> [!proof]
> By [[#^thm-umbrella]]'s Track 2 instantiation, $\mathbb{E}\,d_{FR}^2 \le 2 I_M (1+o(1))$. By the infinitesimal Fisher-Rao expansion, $\|\theta_1 - \theta_2\|^2 \le \mathbf{I}_{\min}^{-1} d_{FR}^2$. Take expectations and Jensen. $\square$

**Worked examples.** *Bernoulli on logit chart, restricted to $p \in [\delta, 1-\delta]$:* $\mathbf{I}(\theta) = p(1-p)$ has no positive lower bound on the full chart $\theta \in \mathbb{R}$; restricting to $p \in [\delta, 1-\delta]$ gives $\mathbf{I}_{\min} \ge \delta(1-\delta)$ and finite, dimension-free Euclidean bound $\mathbb{E}\|\Delta\theta\|_{\text{Eucl}} \le [\delta(1-\delta)]^{-1/2}\sqrt{2 I_M}$ — contingent on boundary avoidance. *Multinomial on log-ratio chart:* Fisher minimum eigenvalue bounded below by $\min_i p_i$ on the simplex interior; for $\delta$-bounded models, $\mathbb{E}\|\Delta\theta\|_{\text{Eucl}} \le \delta^{-1/2}\sqrt{2 I_M}$. *Gaussian-mean chart with fixed variance $v$:* $\mathbf{I}(\mu) = 1/v$ constant on the manifold; $\mathbb{E}\|\Delta\mu\|_{\text{Eucl}} \le \sqrt{v}\sqrt{2 I_M}$. *Gaussian-scale chart $\theta = \sigma$:* $\mathbf{I}(\sigma) = 2/\sigma^2$ — $\mathbf{I}_{\min}^{-1/2} = \sigma/\sqrt{2}$ grows with $\sigma$, recovering the no-go's pathology consistent with [[#^sec-no-go]]; reparameterizing to $\theta = \log\sigma$ gives $\mathbf{I}(\log\sigma) = 2$ constant, restoring a finite Euclidean bound.

The pattern: for natural-parameter charts on simplex / discrete-outcome models with the goal-induced geodesic restricted away from the boundary, the Euclidean Track 2 translation is dimension-free and finite; for scale-family parametrizations off the natural-parameter chart, the prefactor grows in $\sigma$ or $\lambda^{-1}$ — recovering [[#^sec-no-go]]'s pathology consistent with the no-go.
