## A no-go: no coordinate-independent universal $C$ for Euclidean chart norms ^sec-no-go

Track 1 delivers a constant under three regularity hypotheses — but the constant carries the domain-specific parameters $L_{\text{post}}$ and $\rho_{\text{LSI}}$. We now ask the natural follow-up: is there a stronger statement, a *coordinate-independent universal* constant — independent of the geometry of $\mathcal{M}$, of the parameterization, and of the coupled-update structure — that works in some natural ambient norm?

The natural ambient norm to try is Euclidean-on-parameters: identify the parameter manifold $\mathcal{M}$ with a subset of $\mathbb{R}^d$ via a chart and measure $\Vert\Delta M_{\text{bias}}\Vert$ as the Euclidean distance in that chart. The answer is *no* in the following sharp sense: any candidate universal constant must depend on the chart, because rescaling the chart (a change of parameterization that the underlying geometry treats as identity) inflates the Euclidean displacement without changing any information-theoretic or geometric quantity in the bound.

### Chart-rescaling lemma + no-go theorem ^sec-no-go-lemma-thm

The cleanest form of the no-go is structural — a chart-rescaling lemma plus a one-line consequence. The scale family of [[#^sec-no-go-illustration]] is then an illustrative instantiation, not the load-bearing proof.

> [!lemma] Chart-rescaling sensitivity of Euclidean displacement ^lem-chart-rescaling
> Let $\mathcal{M}$ be a statistical manifold and $\phi: U \to \mathbb{R}^d$ a chart on an open set $U \subseteq \mathcal{M}$. For any $a > 0$, write $\phi_a := a\phi$ for the rescaled chart. Then for every pair of probability laws $\mu, \nu$ on $U$ (in particular, the goal-conditional and goal-marginal post-update laws of [[#^eq-bias-quantity]]):
> *(a)* The chart-Euclidean Wasserstein distance scales linearly: $W_2^{\phi_a}(\mu, \nu) = a\cdot W_2^\phi(\mu, \nu)$.
> *(b)* Conditional KL, conditional mutual information, Fisher-Rao geodesic distance, and Hellinger distance are all chart-invariant: they take the same value under $\phi$ and $\phi_a$.

> [!proof]
> (a) The pushforward under the linear map $x \mapsto ax$ rescales Euclidean distances by $a$, hence rescales any optimal coupling's transport cost. (b) KL depends only on the underlying densities and dominating measure (Radon-Nikodym derivatives are reparameterization-invariant); the Fisher metric tensor transforms covariantly under chart change, so the integrated geodesic distance is invariant; Hellinger as an $f$-divergence is reparameterization-invariant. $\square$

> [!theorem] No coordinate-independent universal Euclidean-chart constant ^thm-no-go
> Suppose there were a constant $C_0 < \infty$ — independent of any chart on any statistical manifold $\mathcal{M}$ — such that for every chart $\phi$ on $\mathcal{M}$ and every goal-coupled architecture satisfying (H1) + (H2$'$) with some non-zero post-update displacement, [[#^eq-no-go-hyp]] holds. Then no such $C_0$ exists.

$$\Vert\Delta M_{\text{bias}}\Vert_{\mathrm{Eucl},\,\phi} \;\leq\; C_0 \cdot \sqrt{\,I(G;\,M_{\tau^+} \mid e_\tau,\, M_{\tau^-})\,}.$$ ^eq-no-go-hyp

> [!proof]
> For any architecture realizing $W_2^\phi(P_{M_{\tau^+}\mid G,e,M_{\tau^-}}, P_{M_{\tau^+}\mid e,M_{\tau^-}}) > 0$ and finite positive transferred information, applying [[#^eq-no-go-hyp]] under the rescaled chart $\phi_a$ gives, by [[#^lem-chart-rescaling]], that [[#^eq-no-go-contradiction]] holds with the right-hand side unchanged across charts. Taking $a \to \infty$ contradicts the fixed $C_0 \sqrt I$ on the right. The same conclusion holds for the architectural-corollary form $C\cdot\sqrt{\kappa_{\text{processing}}\cdot I(G;\Omega\mid e, M)}$ under (H$_\kappa$): both sides of the corollary inherit [[#^lem-chart-rescaling]]'s chart-(non)invariance, and the contradiction goes through verbatim. $\square$

$$a \cdot \Vert\Delta M_{\text{bias}}\Vert_{\mathrm{Eucl},\,\phi} \;=\; \Vert\Delta M_{\text{bias}}\Vert_{\mathrm{Eucl},\,\phi_a} \;\leq\; C_0\sqrt{I}.$$ ^eq-no-go-contradiction

The lemma is the clean statement; [[#^thm-no-go]] is the one-line consequence. The proof avoids type-shifts between Dirac points and pushforward laws, never invokes (H2$'$)-violating two-point constructions, and does not assert any specific value of $I$ — it only uses that some architecture realizes finite positive $W_2^\phi$ and finite positive $I$, which is automatic on any non-trivial goal-coupled architecture (for instance, the conjugate-Gaussian example of [[#^sec-track1-conjugate-gauss]] with any $\sigma, \tau > 0$ and a non-degenerate continuous goal distribution).

### Scale-family illustration ^sec-no-go-illustration

The lemma's content is illustrated cleanly on the Gaussian scale family $\mathcal{M}_\sigma = \{\mathcal{N}(0, \sigma^2): \sigma > 0\}$. Two charts on the same manifold:

- **Chart A**: parameter $\sigma$ itself, Euclidean coordinate $\sigma \in (0, \infty)$.
- **Chart B**: parameter $\theta := \log\sigma$, Euclidean coordinate $\theta \in \mathbb{R}$.

The two charts describe the same underlying distributions, so all chart-invariant quantities (KL, Fisher-Rao, MI, Hellinger) agree. Equip $\mathcal{M}_\sigma$ with a goal-coupled architecture: take a continuous goal $G \in \mathbb{R}$ with operating distribution $G \sim \mathcal{N}(0, \delta^2)$ for some small $\delta > 0$, and let the goal-conditional architecture place its post-update concentrated near $\sigma_0 e^G$ for some fixed reference $\sigma_0 > 0$ (e.g., a Gaussian post-update law on Chart B with mean $\theta_0 + G$ and small fixed variance). At small $\delta$, the post-update law concentrates on a tight neighborhood of $\theta_0$ in Chart B (so (H2$'$) holds via LSI on Chart B's Gaussian post-update), and direct computation gives finite positive $W_2^A$ and $W_2^B$ and finite positive transferred MI.

[[#^lem-chart-rescaling]] then gives $W_2^A = e^{\theta_0}\cdot W_2^B$ at the operating point — the scale factor $a = e^{\theta_0}$ comes from the chart change $\sigma = e^\theta$, which is locally linear at $\theta_0$ with slope $e^{\theta_0}$. As $\sigma_0 = e^{\theta_0} \to \infty$, the Chart-A Euclidean displacement grows linearly while the Chart-B Euclidean displacement stays bounded — and [[#^thm-no-go]]'s chart-rescaling argument bites.

### The implication ^sec-no-go-implication

The no-go is *constructive*: it tells us the kind of commitment the bound's universal form requires. To get a universal $C$, the bound must be stated in a coordinate-invariant norm — one that respects the underlying geometry of the statistical manifold rather than an arbitrary chart on it. This is exactly the role of the Fisher-Rao metric, which Čencov's 1982 uniqueness theorem shows is the unique (up to global scale) Riemannian metric on a statistical manifold that is invariant under sufficient statistics.

The counterexample is thus *adjacent in shape but opposite in direction* to Owhadi, Scovel, and Sullivan's Bayesian brittleness results \cite{owhadi-scovel-sullivan-2015-ejs-finite-info,owhadi-scovel-sullivan-2015-siamrev-brittleness}. Their theorem says: under finite information, two practitioners using arbitrarily close models can reach opposite posterior conclusions — Bayesian inference is brittle in the total-variation metric on perturbations to the prior or the data-generating distribution. Theirs is a *no-go for arbitrary stability under finite information* in a fixed metric. Ours is a *no-go for a universal constant absent a coordinate-invariance commitment*, in a setting where (H2$'$)'s post-update concentration assumption explicitly excludes their brittleness regime. The two no-gos constrain different things; neither implies the other; both are honest about what their stability machinery cannot deliver. We discuss the apparent tension explicitly in [[#^sec-related-work]].

### Why we record this no-go rather than waving it away ^sec-no-go-record

Three reasons. First, an honest theory paper should record the structure of *what fails*, not just the structure of what succeeds. Second, the no-go disciplines what we can and cannot claim about [[#^thm-track1-uncond]]: [[#^thm-track1-uncond]]'s constant $C_{T_2}$ is *not* coordinate-independent across the no-go's regime — it depends on the post-update concentration, which is family-specific — and we do not claim otherwise. Third, the no-go *forces* the structural commitment of [[#^sec-track2]]: a chart-independent universal *dimension-free* constant requires more than just any intrinsic-metric choice. The [[#^sec-track2]] commitment to (PI) at full Markov-morphism strength is the load-bearing axiom; combined with Riemannian structure (R) — implicit in the metric framing — and KL as the cascade's information coordinate (K) — built into Step 1's chain rule — Čencov's uniqueness theorem ([[#^thm-fr-uniqueness]]) then forces Fisher-Rao with constant $\sqrt{2}$ uniquely, with no further freedom. Alternative chart-independent commitments (TV-Pinsker, Hellinger-as-divergence) yield weaker bounds: TV-Pinsker is non-tight (universal but loose except at coincident measures); Hellinger-as-divergence violates (R); switching divergences on the RHS violates (K) and breaks the cascade upstream. The no-go thus does not merely tell us "commit to something intrinsic"; under the cascade structure (K) and metric framing (R), it tells us *exactly* what to commit to — (PI) — and the universal $\sqrt{2}$ falls out.
