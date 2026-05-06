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
> *(Track 2, Fisher-Rao):* Under additional (H4$'$) — uniform-locality on the goal-conditional slice-wise KL — $C = \sqrt{2}$ with metric $d_{FR}$. The constant is universal, dimension-free, and carries no domain-specific parameters.

> [!hypothesis] (H2$'$) Talagrand $T_2$ on the post-update law ^h2-prime
> The post-update law $P_{M_{\tau^+}\mid e, M_{\tau^-}}$ satisfies $W_2^2(P,\, P_{M_{\tau^+}\mid e, M_{\tau^-}}) \le C_{T_2} \cdot \mathrm{KL}(P \,\|\, P_{M_{\tau^+}\mid e, M_{\tau^-}})$ for all probability measures $P$. Sufficient conditions in [[#^sec-h2-prime-suff]]: log-Sobolev on the post-update density (Otto-Villani $C_{T_2} = 2/\rho_{\text{LSI}}$); dimension-free sub-Gaussian Lipschitz concentration \cite{gozlan-2009-t2-characterization}.

> [!hypothesis] (H4$'$) Uniform local regime ^h4-prime
> $\mathrm{ess\,sup}_g\,\mathrm{KL}(P_{M_{\tau^+}\mid e, M_{\tau^-}, G=g}\,\|\,P_{M_{\tau^+}\mid e, M_{\tau^-}}) \le \delta_\star$ for some $\delta_\star \in (0, 1)$. Every goal-conditional slice — not merely the average — is uniformly close to the goal-marginal on the statistical manifold. (H4$'$) is strictly stronger than $\mathbb{E}_G[\mathrm{KL}_g] = I \ll 1$; small mean does not imply small ess-sup.

**Remarks on [[#^thm-umbrella]].**

*The two tracks bound different metrics with the same square-root-in-information shape.* Track 1 lives on $W_2$, Track 2 on $d_{FR}$. Both deliver bounds of form $\mathbb{E}\,d \le C\sqrt{I_M}$ where $I_M = I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})$ is transferred goal-information. The two are not "different scalings"; they are bounds on different metrics with the same information dependence.

*The bound is unconditional in the architectural classification.* Both Tracks bound transferred goal-information directly. (H1)–(H2$'$) and (H1)–(H4$'$)–(PI)–(R)–(K) are regularity hypotheses on the post-update law and the metric. Neither makes a structural commitment about how the goal $G$ enters the architecture's update mechanism. The architectural reading enters at corollary level via (H$_\kappa$) below.

*Track 2's constant is universal and dimension-free.* Track 1's $C_{T_2}$ is family-specific (depends on the post-update concentration). Track 2's $\sqrt{2}$ is the same constant on every statistical manifold under the (PI)+(R)+(K) triple, by Čencov uniqueness ([[#^thm-fr-uniqueness]] below).

*Track 1 contains the Bayesian-inverse-problems lineage.* In the conjugate-Gaussian Class 1 (Separated) case with invertible data channel, Track 1's $C_{T_2}$ recovers $2 L_{\text{post}}^2/\rho_{\text{LSI}}$ exactly — the canonical cascade constant from \citet{stuart-2010-acta} and the lineage that follows. The composition contains the existing literature as a strict sub-case.

*Track 1 outside (H2$'$).* Heavy-tailed post-updates without log-Sobolev or dimension-free sub-Gaussian concentration fall outside Track 1's $T_2$ scope. A weaker $T_1$ form via bounded support gives the distance bound at $W_1$ rather than $W_2$ — adequate for the distance reading, weaker on the squared-distance side. Track 2 under (PI)+(R)+(K) does not require (H2$'$) and remains available.

### A no-go that forces (PI) ^sec-no-go

The universal-constant route (Track 2's $\sqrt{2}$) is not coincidental. A scale-family construction shows that no coordinate-independent universal constant exists for Euclidean chart norms — making the (PI) commitment load-bearing.

> [!theorem] No-go on Euclidean chart norms ^thm-no-go
> Suppose there were a constant $C_0 < \infty$ — independent of any chart on any statistical manifold — such that for every chart $\phi$ on $\mathcal{M}$ and every goal-coupled architecture satisfying (H1)+(H2$'$) with non-zero post-update displacement, $\mathbb{E}\,\|\Delta M_{\text{bias}}\|_{\mathrm{Eucl},\phi} \le C_0 \sqrt{I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})}$. Then no such $C_0$ exists.

The proof is short: a chart rescaling $\phi \mapsto a\phi$ scales the chart-Euclidean Wasserstein distance linearly while leaving the right-hand side (chart-invariant information) unchanged; taking $a \to \infty$ contradicts the fixed $C_0\sqrt{I}$. Full statement and proof in [[#^sec-no-go-proof]]. The Gaussian scale family with chart $\sigma$ versus $\log\sigma$ is the cleanest illustration.

**Remark.** [[#^thm-no-go]] is *adjacent in shape but opposite in direction* to Owhadi-Scovel-Sullivan's Bayesian-brittleness results \cite{owhadi-scovel-sullivan-2015-ejs-finite-info,owhadi-scovel-sullivan-2015-siamrev-brittleness}. Their no-go is for *arbitrary stability under finite information* in fixed metrics; ours is for *a universal constant absent a coordinate-invariance commitment*, in a setting where (H2$'$)'s post-update concentration explicitly excludes their brittleness regime. The two no-gos constrain different things; neither implies the other.

### Čencov uniqueness and sharpness ^sec-fr-uniqueness

Track 2's constant $\sqrt{2}$ is not just universal under (PI)+(R)+(K) — it is the *unique sharp* such constant.

> [!theorem] Uniqueness and sharpness of the Fisher-Rao $+\sqrt{2}$ bound ^thm-fr-uniqueness
> Let $\mathcal{M}$ be a statistical-manifold sub-case (H1), and let the bound take the umbrella form $\mathbb{E}\,d_{\mathcal{M}}(\Delta M_{\text{bias}}) \le C\sqrt{I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})}$ under the constraints (PI)+(R)+(K). Then:
>
> *(a)* $d_{\mathcal{M}}$ is uniquely the Fisher-Rao geodesic distance.
>
> *(b)* No constant $C < \sqrt{2}$ uniformly bounds $\mathbb{E}\,d_{FR}/\sqrt{I_M}$ across the (H4$'$) regime: there exist conjugate-Gaussian Class 1 instances on which $\mathbb{E}\,d_{FR}^2/I_M \to 2$ as the goal variation shrinks at fixed $I_M$. Hence $C = \sqrt{2}$ is the unique sharp upper-bound constant under (PI)+(R)+(K)+(H4$'$).

Proof in [[#^sec-fr-uniqueness-proof]]. Part (a) is Čencov's 1982 uniqueness theorem applied to $\mathcal{M}$: the Fisher information metric is the unique (up to global positive scalar) Riemannian metric invariant under Markov morphisms. Part (b) is direct verification on the conjugate-Gaussian saturation.

**Remark.** Alternative chart-independent commitments (TV with Pinsker, Hellinger-as-divergence, $\chi^2$, Rényi) are all defeated: TV-Pinsker is non-tight (the constant is universal but the inequality is loose except at coincident measures); Hellinger-as-divergence and $\chi^2$-as-divergence violate (R); switching divergences on the right-hand side violates (K). Under the cascade structure (K) and the metric framing (R), the no-go ([[#^thm-no-go]]) tells us *exactly* what to commit to — (PI) — and the universal $\sqrt{2}$ falls out.

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

*The factorization is the contribution-headline.* Coupling strength $\kappa_{\text{processing}}$ × residual ambiguity $I(G;\Omega\mid e, M)$ — architecture × information. The unconditional theorem [[#^thm-umbrella]] is the structural backbone whose math holds without (H$_\kappa$); the corollary is the operational reading.

*Class 1 (Separated) gives (H$_\kappa$) automatically.* The Markov chain $G \to \Omega_\tau \to M_{\tau^+}$ (conditional on $(e_\tau, M_{\tau^-})$) plus data-processing inequality yields $\kappa_{\text{processing}} \le 1$ by construction. (H$_\kappa$) is a derived consequence, not a commitment, for Class 1.

*Class 2 (Partial) and Class 3 (Coupled) require (H$_\kappa$) as a named structural commitment.* Two clean sufficient conditions and a parrot-architecture worst-case witness ($\kappa_{\text{processing}} = \infty$ when $M_{\tau^+} := G$ on goals orthogonal to the latent world-state) are documented in [[#^sec-h-kappa-suff]]. The unconditional theorem still bounds parrot-architecture displacement directly by transferred information; the κ × 𝒜 factorization just doesn't apply.

*The realized $\kappa_{\text{processing}}$ is empirically accessible.* A behavioral two-goal probe — run the architecture on a fixed event set under two goal states, measure divergence of the epistemic content of the response — gives a lower bound on $\kappa_{\text{processing}}$ at the operating point. For architectures with explicit attention or routing, activation-level mediation analyses give a tighter handle. Both are out of scope for the present theory paper.
