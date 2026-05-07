## Main Results ^sec-main-results

The umbrella theorem bounds the goal-conditional displacement of the post-update model state by transferred goal-information. Two named tracks supply the constant — a transport-inequality cascade (Track 1) and a Fisher-Rao geometry route (Track 2) — both flowing from a common chain-rule move on the post-update law (mechanism in [[#^sec-mechanism]]).

> [!theorem] Umbrella bound on goal-conditional displacement ^thm-umbrella
> Under (H1) and the regularity hypotheses below, for fixed event-prior pair $(e_\tau, M_{\tau^-})$ with $\mathbb{E}$ taken over $G \sim P(G \mid e_\tau, M_{\tau^-})$:
>
> $\mathbb{E}\,\|\Delta M_{\text{bias}}\| \;\leq\; C \cdot \sqrt{I(G;\,M_{\tau^+}\mid e_\tau,\, M_{\tau^-})},$  ^eq-umbrella
>
> with $C$ supplied by either of two routes:
>
> *(Track 1, transport-inequality):* Under additional (H2$'$) — a Talagrand $T_2$ inequality on the post-update law — $C = \sqrt{C_{T_2}}$ with metric $W_2$. The constant $C_{T_2}$ recovers the canonical Stuart-school cascade value $2 L_{\text{post}}^2/\rho_{\text{LSI}}$ as a special case under standard log-Sobolev concentration.
>
> *(Track 2, Fisher-Rao spherical-arc):* The bound holds with metric $d_{FR}$ in the *ambient Amari-Nagaoka spherical-arc convention* of [[#^sec-bias-quantity]] ($d_{FR}(P, Q) = 2\arccos\!\int\!\sqrt{pq}$, the great-circle arc on the unit $L^2$-sphere of $\sqrt p$). Two universal forms — both dimension-free, neither carrying domain-specific parameters:
>
> &nbsp;&nbsp;&nbsp;&nbsp;*locally tight* — under (PI)+(R)+(K) on the natural categorical metric assignment plus (H4$'$) at parameter $\delta_\star$, $C = \sqrt{2(1+R(\delta_\star))}$ with explicit $R(\delta_\star) \to 0$ as $\delta_\star \to 0$ (locally tight at $\sqrt 2$ in the limit; Čencov uniqueness pins the metric and constant via [[#^thm-fr-uniqueness]]);
>
> &nbsp;&nbsp;&nbsp;&nbsp;*globally valid* — under (PI) alone (no (R), no (K), no (H4$'$)), the *ambient spherical-arc bound* $C = 2$ holds throughout — sharp via a symmetric $N$-point witness as $N \to \infty$ ([[#^thm-track2-global]] in [[#^sec-track2-companions]]; the $\sqrt 2$ overhead is exactly the chord-arc factor at the unit $L^2$-sphere's antipode in squared-distance form). On parametric submanifolds the ambient spherical arc is the chart-invariant pseudometric; submanifold-intrinsic geodesics may be longer (the local-tight regime is exactly where ambient and intrinsic agree at second order).

> [!hypothesis] (H2$'$) Talagrand $T_2$ on the post-update law ^h2-prime
> $W_2^2(P,\, P_{M_{\tau^+}\mid e, M_{\tau^-}}) \le C_{T_2}\,\mathrm{KL}(P \,\|\, P_{M_{\tau^+}\mid e, M_{\tau^-}})$ for all $P$. Sufficient conditions in [[#^sec-h2-prime-suff]] (LSI, Otto-Villani; dimension-free sub-Gaussian Lipschitz concentration \cite{gozlan-2009-t2-characterization}).

> [!hypothesis] (H4$'$) Uniform local regime ^h4-prime
> $\mathrm{ess\,sup}_g\,\mathrm{KL}(P_{M_{\tau^+}\mid G=g}\,\|\,P_{M_{\tau^+}}) \le \delta_\star$ for some $\delta_\star \in (0, 1)$ — every goal-conditional slice uniformly close to the goal-marginal, not merely the average (strictly stronger than small-$I_M$). Adversarial / rare-high-KL prompts (jailbreaks, persona injection) exit (H4$'$); the global $C = 2$ bound (Theorem D.1) is the operating tool there.

**Remarks on [[#^thm-umbrella]].**

*The two tracks bound different metrics with the same square-root-in-information shape.* Track 1 lives on $W_2$, Track 2 on $d_{FR}$. Both deliver bounds of form $\mathbb{E}\,d \le C\sqrt{I_M}$ where $I_M = I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})$ is transferred goal-information. The two are not "different scalings"; they are bounds on different metrics with the same information dependence.

*The bound is unconditional in the architectural classification.* Both Tracks bound transferred goal-information directly. (H1)–(H2$'$) and (H1)–(H4$'$)–(PI)–(R)–(K) are regularity hypotheses on the post-update law and the metric. Neither makes a structural commitment about how the goal $G$ enters the architecture's update mechanism. The architectural reading enters at corollary level via (H$_\kappa$) below.

*Track 2's constant is universal and dimension-free.* Track 1's $C_{T_2}$ is family-specific (depends on the post-update concentration). Track 2's $\sqrt{2}$ is the same constant across the entire categorical metric assignment under the (PI)+(R)+(K) triple, by Čencov uniqueness ([[#^thm-fr-uniqueness]] below); on the parametric submanifold of any specific application, the induced metric is Fisher-Rao with the same constant.

*Track 1 generalizes the Stuart-school cascade.* Under Stuart-school Lipschitz-posterior hypotheses on the deterministic update map $\Omega \mapsto \mu^\Omega$ \cite{stuart-2010-acta,sprungk-2020-local-lipschitz,dolera-mainini-2023-aihp-lipschitz,hosseini-hsu-taghvaei-2024-conditional-ot} plus $T_2$ concentration on the goal-induced parameter measure and slice-wise sub-Gaussianity of the conditional data law, [[#^thm-stuart-school-reduction]] yields a $C_{T_2}$ of the canonical Stuart-school cascade form $\propto L_{\text{post}}^2/\rho_{\text{noise}}$ on the post-update model law — tight at $2L_{\text{post}}^2/\rho_{\text{noise}}$ on conjugate-Gaussian and exponential-family-conjugate instances (recovered via direct sub-Gaussian read-off on the post-update parameter law, [[#^sec-conjugate-gauss-numerics]]); the structural Lipschitz-composition route delivers the same canonical form with an absolute multiplicative overhead in general. The cascade form transfers across the full Strand 2 hypothesis space; Track 1 extends the cascade beyond Class 1 (Separated) to architectures where the goal couples into the update mechanism directly — a regime Stuart-school does not address.

*Track 1 outside (H2$'$).* Heavy-tailed post-updates without log-Sobolev or dimension-free sub-Gaussian concentration fall outside Track 1's $T_2$ scope. A weaker $T_1$ form via bounded support gives the distance bound at $W_1$ rather than $W_2$ — adequate for the distance reading, weaker on the squared-distance side. Track 2 under (PI)+(R)+(K) does not require (H2$'$) and remains available.

### A no-go that forces (PI) ^sec-no-go

The universal-constant route (Track 2's $\sqrt{2}$) is not coincidental. A scale-family construction shows that no coordinate-independent universal constant exists for Euclidean chart norms — making the (PI) commitment load-bearing.

> [!theorem] No-go on Euclidean chart norms ^thm-no-go
> Suppose there were a constant $C_0 < \infty$ — independent of any chart on any statistical manifold — such that for every chart $\phi$ on $\mathcal{M}$ and every goal-coupled architecture satisfying (H1)+(H2$'$) with non-zero post-update displacement, $\mathbb{E}\,\|\Delta M_{\text{bias}}\|_{\mathrm{Eucl},\phi} \le C_0 \sqrt{I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})}$. Then no such $C_0$ exists.

The proof is short: a chart rescaling $\phi \mapsto a\phi$ scales the chart-Euclidean Wasserstein distance linearly while leaving the right-hand side (chart-invariant information) unchanged; taking $a \to \infty$ contradicts the fixed $C_0\sqrt{I}$. Full statement and proof in [[#^sec-no-go-proof]]. The Gaussian scale family with chart $\sigma$ versus $\log\sigma$ is the cleanest illustration.

**Remark.** [[#^thm-no-go]] is *adjacent in shape but opposite in direction* to Owhadi-Scovel-Sullivan's Bayesian-brittleness results \cite{owhadi-scovel-sullivan-2015-ejs-finite-info,owhadi-scovel-sullivan-2015-siamrev-brittleness}. Their no-go is for *arbitrary stability under finite information* in fixed metrics; ours is for *a universal constant absent a coordinate-invariance commitment*, in a setting where (H2$'$)'s post-update concentration explicitly excludes their brittleness regime. The two no-gos constrain different things; neither implies the other.

### Čencov uniqueness and sharpness ^sec-fr-uniqueness

The no-go requires a coordinate-invariance commitment if a universal constant is wanted at all; (PI)+(R)+(K) is the natural commitment for an information-coordinate cascade; and Čencov uniqueness within that commitment leaves little further freedom.

> [!theorem] Uniqueness and sharpness of the Fisher-Rao $+\sqrt{2}$ bound (local) ^thm-fr-uniqueness
> Under (H1)+(PI)+(R)+(K)+(H4$'$), in the umbrella form $\mathbb{E}\,d_{\mathcal{M}}(\Delta M_{\text{bias}}) \le C\sqrt{I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})}$: *(a)* $d_{\mathcal{M}}$ is uniquely the ambient Amari-Nagaoka Fisher-Rao spherical-arc distance, agreeing with submanifold-intrinsic Fisher-Rao geodesics at second order in the (H4$'$) regime; *(b)* $C = \sqrt 2$ is the unique sharp upper-bound constant — no $C < \sqrt 2$ holds uniformly across the (H4$'$) regime.

Part (a) follows from Čencov's 1982 uniqueness theorem applied to the natural categorical metric assignment of (PI). Part (b) is verified by a symmetric two-point witness on the conjugate-Gaussian Class 1 family: $G \in \{-a, +a\}$ uniform delivers $\mathbb{E}\,d_{FR}/\sqrt{I_M} \to \sqrt 2$ as $a/\sigma \to 0$ (the symmetry forces $d_{FR}$ exactly constant across slices, so Jensen is tight). Full proof + witness construction in [[#^sec-fr-uniqueness-proof]]. Alternative chart-independent commitments (TV, Hellinger-as-divergence, $\chi^2$, Rényi) are all defeated by (R)/(K) or non-tightness; the no-go narrows the candidate space, and (PI)+(R)+(K) selects Fisher-Rao + $\sqrt 2$.

### The architectural corollary ^sec-architectural-corollary

The umbrella theorem bounds displacement by *transferred* goal-information. The architectural reading factors this transferred information into a structural-architectural quantity (where can the goal flow?) and an information-theoretic quantity (how much could the goal in principle resolve?).

> [!hypothesis] (H$_\kappa$) Bounded architectural attenuation ^h-kappa
> $\kappa_{\text{processing}} \le \kappa^* < \infty$, with $\kappa^*$ a named architectural constant (typically $1$ for non-amplifying architectures).

> [!corollary] Architectural factorization ^cor-architectural-factorization
> Under (H1) + the Track-specific hypotheses + (H$_\kappa$) at level $\kappa^*$, the bound factors as
>
> $\mathbb{E}\,\|\Delta M_{\text{bias}}\| \;\leq\; C\sqrt{\kappa^* \cdot I(G;\,\Omega_\tau\mid e_\tau,\, M_{\tau^-})},$  ^eq-arch-corollary
>
> with $C$ supplied by Track 1 or Track 2 as in [[#^thm-umbrella]].

**Remarks on [[#^cor-architectural-factorization]].**

*The factorization is the contribution-headline.* Coupling strength $\kappa_{\text{processing}}$ × residual ambiguity $I(G;\Omega\mid e, M)$ — architecture × information. [[#^thm-umbrella]]'s unconditional form is the structural backbone whose math holds without (H$_\kappa$); the corollary is the operational reading.

*Class 1 (Separated) gives (H$_\kappa$) automatically.* The Markov chain $G \to \Omega_\tau \to M_{\tau^+}$ (conditional on $(e_\tau, M_{\tau^-})$) plus data-processing inequality yields $\kappa_{\text{processing}} \le 1$ by construction. (H$_\kappa$) is a derived consequence, not a commitment, for Class 1.

*Class 2 (Partial) and Class 3 (Coupled) require (H$_\kappa$) as a named structural commitment.* Two clean sufficient conditions and a parrot-architecture worst-case witness ($\kappa_{\text{processing}} = \infty$ when $M_{\tau^+} := G$ on goals orthogonal to the latent world-state) are documented in [[#^sec-h-kappa-suff]]. The unconditional theorem still bounds parrot-architecture displacement directly by transferred information; the $\kappa \times \mathcal{A}$ factorization just doesn't apply.

*Transferred information has a closed-form empirical estimator under binary-uniform goal probing.* For $G \in \{g_1, g_2\}$ uniform — the natural two-goal probe protocol — the transferred goal-information equals the Jensen-Shannon divergence of the goal-conditional response distributions: $I(G;\,M_{\tau^+}\mid e_\tau, M_{\tau^-}) = \mathrm{JSD}(P_{M_{\tau^+}\mid g_1},\,P_{M_{\tau^+}\mid g_2})$. JSD is directly Monte-Carlo estimable from response samples under each goal state. In the local Track 2 regime (under (PI)+(R)+(K)+(H4$'$)) this gives the operational bound $\mathbb{E}\,\|\Delta M_{\text{bias}}\| \le \sqrt{2\,\widehat{\mathrm{JSD}}}$; outside (H4$'$) — the regime adversarial / rare-high-KL probes occupy — the global Track 2 spherical-arc backstop gives $\mathbb{E}\,d_{FR} \le 2\sqrt{\widehat{\mathrm{JSD}}}$ (or the sharper $2\arccos(\exp(-\widehat{\mathrm{JSD}}/2))$). Either form needs no $\kappa$-factorization. The factorized form requires additionally lower-bounding $I(G;\Omega \mid e, M_{\tau^-})$, which depends on architecture-side modeling (representation-engineering, steering-vector, or mechanistic-interpretability methods on attention-pattern analysis); we revisit this in [[#^sec-conclusion]] as a primary future direction.
