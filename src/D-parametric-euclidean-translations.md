## Generalized parametric Euclidean translations ^sec-parametric-euclidean-translations

This appendix generalizes the conjugate-Gaussian Euclidean bound of [[#^sec-track2-euclidean]] ([[#^thm-conjugate-gauss-euclidean]]) to general exponential families and records the Hellinger-Fisher-Rao geometric relationship that underwrites [[#^thm-hellinger]] as a chord-vs-arc complement to [[#^thm-track2-uncond]].

### Theorem D.1: Exponential-family Euclidean bound ^sec-exp-family-euclidean

For an exponential family $P_\theta(x) = h(x)\exp(\theta^\top T(x) - A(\theta))$ with natural parameter $\theta \in \Theta \subseteq \mathbb{R}^d$ and log-partition $A$, the Fisher information metric is $\mathbf{I}(\theta) = \nabla^2 A(\theta)$. The Fisher-Rao geodesic distance has no general closed form, but the infinitesimal metric is

$$d_{FR}^2(P_{\theta_1}, P_{\theta_2}) = (\theta_1 - \theta_2)^\top \mathbf{I}(\theta^*)(\theta_1 - \theta_2) + O(\Vert\theta_1-\theta_2\Vert^3),$$

where $\theta^*$ is on the geodesic between $\theta_1, \theta_2$. So Euclidean displacement on the natural parameter satisfies $\Vert\theta_1 - \theta_2\Vert^2 \leq \mathbf{I}_{\min}^{-1} \cdot d_{FR}^2$ where $\mathbf{I}_{\min}$ is the minimum eigenvalue of $\mathbf{I}$ along the geodesic.

> [!theorem] Exponential-family Euclidean bound ^thm-exp-family
> For an exponential family in natural-parameter coordinates with Fisher-information minimum-eigenvalue $\mathbf{I}_{\min}$ along the goal-induced geodesic, [[#^thm-track2-uncond]] translates to the Euclidean bound [[#^eq-exp-family-euclidean]]; under (H$_\kappa$) the architectural form is $\mathbb{E}\,\Vert\Delta\theta_{\text{bias}}\Vert_{\text{Eucl}} \leq \mathbf{I}_{\min}^{-1/2}\sqrt{2\kappa_{\text{processing}} I(G;\Omega \mid e, M)}(1+o(1))$.

$$\mathbb{E}\,\Vert\Delta\theta_{\text{bias}}\Vert_{\text{Eucl}} \;\leq\; \mathbf{I}_{\min}^{-1/2} \cdot \sqrt{2 \cdot I(G; M_{\tau^+} \mid e_\tau, M_{\tau^-})} \cdot (1 + o(1)).$$ ^eq-exp-family-euclidean

> [!proof]
> By [[#^thm-track2-uncond]], $\mathbb{E}\,d_{FR}^2 \leq 2 I_M (1+o(1))$. By the infinitesimal Fisher-Rao expansion, $\Vert\theta_1 - \theta_2\Vert^2 \leq \mathbf{I}_{\min}^{-1} d_{FR}^2$. Take expectations and Jensen. $\square$

**Worked examples.**

- *Bernoulli on logit chart, restricted to $p \in [\delta, 1-\delta]$.* $P_\theta = \mathrm{Bernoulli}(p)$ with $\theta = \log(p/(1-p))$. Fisher information $\mathbf{I}(\theta) = p(1-p)$ has *no* positive lower bound on the full chart $\theta \in \mathbb{R}$ ($p(1-p) \to 0$ as $p \to 0$ or $1$). Restricting the goal-induced geodesic to remain in the interior $p \in [\delta, 1-\delta]$ for some $\delta > 0$ gives $\mathbf{I}_{\min} \ge \delta(1-\delta)$, so $\mathbf{I}_{\min}^{-1/2} \le [\delta(1-\delta)]^{-1/2}$ and the Euclidean logit-displacement bound $\mathbb{E}\Vert\Delta\theta\Vert_{\text{Eucl}} \le [\delta(1-\delta)]^{-1/2}\sqrt{2 I_M}$ — *finite, dimension-free*, but contingent on the boundary-avoidance restriction. The full-chart claim "globally bounded by $2\sqrt{2 I_M}$" is *not* available because the prefactor diverges at the deterministic-coin boundaries.

- *Multinomial on log-ratio chart.* $P_\theta$ on $K$ outcomes with $\theta_i = \log(p_i/p_K)$. Fisher information has minimum eigenvalue bounded below by $\min_i p_i$ on the simplex interior, so $\mathbf{I}_{\min}^{-1/2}$ is bounded uniformly *away* from the simplex boundary. For models that stay $\delta$-bounded from the boundary, Euclidean log-ratio displacement is bounded by $\delta^{-1/2}\sqrt{2 I_M}$.

- *Gaussian-mean chart (with fixed variance $v$).* $\mathbf{I}(\mu) = 1/v$, so $\mathbf{I}_{\min}^{-1/2} = \sqrt v$ (constant on the manifold). Euclidean mean-displacement: $\sqrt v\,\sqrt{2 I_M}$. For the conjugate-Gaussian post-update parameter law $\mathcal{N}(\mu, L_{\text{post}}^2\sigma^2)$ (variance $v = L_{\text{post}}^2\sigma^2$, *not* the inside-posterior variance $\sigma_{\text{post}}^2 = L_{\text{post}}\sigma^2$), this becomes $L_{\text{post}}\sigma\sqrt{2 I_M}$ — recovering [[#^thm-conjugate-gauss-euclidean]].

- *Gaussian-scale chart $\theta = \sigma$.* $\mathbf{I}(\sigma) = 2/\sigma^2$, so $\mathbf{I}_{\min}^{-1/2} = \sigma/\sqrt{2}$ — *grows* with $\sigma$. The [[#^sec-no-go]] no-go's scale-family pathology recovers here: Euclidean displacement on $\sigma$ has unbounded prefactor as $\sigma \to \infty$. Reparameterizing to $\theta = \log\sigma$ gives $\mathbf{I}(\log\sigma) = 2$ constant, and the Euclidean displacement is bounded by $1/\sqrt{2} \cdot \sqrt{2 I_M} = \sqrt{I_M}$ — finite, consistent with the fact that $\log\sigma$ is the *natural-parameter chart* of the Gaussian-scale family on which the Fisher-Rao-to-Euclidean conversion is bounded.

The pattern: for natural-parameter charts on simplex / discrete-outcome models *with the goal-induced geodesic restricted away from the boundary* (Bernoulli logit on $p \in [\delta, 1-\delta]$; multinomial log-ratio with $\min_i p_i \ge \delta$), the Euclidean Track 2 translation is dimension-free and finite, prefactor $\sim \delta^{-1/2}$. For scale-family parametrizations off the natural-parameter chart (Gaussian-$\sigma$, exponential-$\lambda$), the prefactor grows in $\sigma$ or $\lambda^{-1}$ — recovering the no-go's pathology consistent with [[#^sec-no-go]]. The Gaussian-mean and conjugate-Gaussian-mean cases are the cleanest: $\mathbf{I}(\mu) = 1/\sigma^2$ and $\mathbf{I}_{\min}^{-1/2}$ is a fixed constant on the manifold.

### Hellinger-Fisher-Rao relationship ^sec-hellinger-fr-relationship

[[#^thm-hellinger]]'s Hellinger backstop and [[#^thm-track2-uncond]]'s Fisher-Rao bound are connected through the unit-sphere representation of statistical manifolds. We adopt the standard statistician's Hellinger and Amari-Nagaoka Fisher-Rao conventions throughout:

- $\mathrm{Hel}^2(P,Q) := \tfrac{1}{2}\Vert\sqrt p - \sqrt q\Vert_{L^2}^2 = 1 - \int\sqrt{pq}\,d\mu$, so $\mathrm{Hel} \in [0, 1]$, with the global inequality $2\mathrm{Hel}^2 \le \mathrm{KL}$ (\citealt[Lemma 2.4]{tsybakov-2009}).
- $d_{FR}(P,Q) := 2\arccos\int\sqrt{pq}\,d\mu = 2\theta$ where $\theta$ is the angle between $\sqrt p$ and $\sqrt q$ on the unit sphere of $L^2$, so $d_{FR} \in [0, \pi]$.

Under these conventions, Hellinger and Fisher-Rao satisfy

$$\mathrm{Hel}^2(P,Q) \;=\; 1 - \cos(d_{FR}/2) \;=\; 2\sin^2(d_{FR}/4), \qquad \mathrm{Hel}(P,Q) \;=\; \sqrt{2}\,\sin\!\bigl(d_{FR}/4\bigr).$$

(Under the convention $\mathrm{Hel}^2 = \tfrac{1}{2}\Vert\sqrt p - \sqrt q\Vert_{L^2}^2$, Hellinger equals the $L^2$ chord between $\sqrt p$ and $\sqrt q$ rescaled by $1/\sqrt 2$; Fisher-Rao is twice the great-circle angle on the unit sphere of $\sqrt p$. Different conventions in the literature differ by factors of 2; the forms above are the ones consistent with $\mathrm{Hel} \in [0, 1]$ and $d_{FR} \in [0, \pi]$ and the $2\mathrm{Hel}^2 \le \mathrm{KL}$ inequality used in [[#^thm-hellinger]].)

> [!lemma] Global chord-arc bound on the unit $L^2$-sphere ^lem-chord-arc
> For any probability measures $P, Q$, the global chord-arc bound [[#^eq-chord-arc]] holds, with equality at the antipode $\mathrm{Hel}(P, Q) = 1$ (correspondingly $d_{FR}(P, Q) = \pi$).

$$d_{FR}(P, Q) \;\leq\; \pi \cdot \mathrm{Hel}(P, Q).$$ ^eq-chord-arc

> [!proof]
> From $d_{FR} = 4\arcsin(\mathrm{Hel}/\sqrt{2})$, define $\phi: (0, 1] \to (0, \pi]$ by $\phi(h) := 4\arcsin(h/\sqrt{2})/h$, so $d_{FR}/\mathrm{Hel} = \phi(\mathrm{Hel})$. Set $g(h) := 4\arcsin(h/\sqrt{2})$. Differentiating: $g'(h) = 4/\sqrt{2 - h^2}$ for $h \in [0, \sqrt{2})$, and $g''(h) = 4h/(2 - h^2)^{3/2} > 0$ on $(0, \sqrt{2})$ — so $g$ is *strictly convex* on this interval, with $g(0) = 0$. By the standard secant-slope monotonicity for convex functions vanishing at zero, $\phi(h) = g(h)/h$ is monotonically increasing on $(0, \sqrt{2})$, with limits $\lim_{h \to 0^+}\phi(h) = g'(0) = 4/\sqrt{2} = 2\sqrt{2}$ and $\phi(1) = g(1) = 4\arcsin(1/\sqrt{2}) = 4\cdot(\pi/4) = \pi$. Hence $\phi(h) \le \pi$ for all $h \in (0, 1]$, with equality at $h = 1$. $\square$

This global chord-arc bound is what underwrites [[#^thm-track2-glob]]'s universal $\pi/\sqrt{2}$ Fisher-Rao constant: $d_{FR} \le \pi\,\mathrm{Hel}$ slice-wise, then Tsybakov's $2\,\mathrm{Hel}^2 \le \mathrm{KL}$ gives $d_{FR}^2 \le \pi^2\mathrm{Hel}^2 \le (\pi^2/2)\,\mathrm{KL}$ slice-wise, and the chain rule + Jensen on $\sqrt{\,\cdot\,}$ deliver $\mathbb{E}\,d_{FR} \le (\pi/\sqrt{2})\sqrt{I_M}$ globally. The constant $\pi/\sqrt 2 \approx 2.22$ is dimension-free and requires no small-information condition; the $\pi/2 \approx 1.57$ overhead vs. [[#^thm-track2-uncond]]'s locally-tight $\sqrt 2$ is the worst-case arc-chord ratio at the sphere's antipode.

**Local proportionality.** As $d_{FR} \to 0$, $\mathrm{Hel} \approx d_{FR}/(2\sqrt{2})$, so $\mathbb{E}\,\mathrm{Hel} \approx \mathbb{E}\,d_{FR}/(2\sqrt{2})$. [[#^thm-track2-uncond]]'s bound $\mathbb{E}\,d_{FR} \le \sqrt{2 I_M}$ then gives $\mathbb{E}\,\mathrm{Hel} \lesssim \sqrt{2 I_M}/(2\sqrt{2}) = (1/2)\sqrt{I_M}$ in the small-information limit — *tighter* than [[#^thm-hellinger]]'s global $(1/\sqrt{2})\sqrt{I_M}$ at small $I_M$. So in the (H4$'$) regime, [[#^thm-track2-uncond]] + [[#^lem-chord-arc]] jointly give the tightest Hellinger bound: $(1/2)\sqrt{I_M}$, beating [[#^thm-hellinger]] by a factor of $\sqrt 2$. [[#^thm-hellinger]] (under (PI) only, no (H4$'$)) is the global statement.
