## Track 1: a transport-inequality cascade ^sec-track1

We derive the constant $C$ on the post-update law directly, in two steps. The cascade is composed from textbook information-theoretic and transport-inequality machinery; the contribution is the application to the goal-conditional bias quantity [[#^eq-bias-quantity]] on the post-update law and the architectural reading via [[#^cor-track1-arch]].

### Hypotheses ^sec-track1-hyp

**(H1) Statistical-manifold sub-case.** The model state $M_t \in \mathcal{M}$ corresponds to a probability distribution $P_{M_t}$ over latent world-states, and $\mathcal{M}$ is locally a statistical manifold in the sense of Amari and Nagaoka \cite{amari-nagaoka-2000-info-geom}. This is satisfied by parametric Bayesian posterior families, exponential families, conjugate priors, and the parametric-belief-state subclass of LLMs that admits a natural distributional reading. We assume throughout that $\mathcal{M}$, the goal-space, and the event-space are *standard Borel* (e.g., Polish with Borel σ-algebra), so regular conditional probabilities exist as Markov kernels \cite[Theorem 6.3]{kallenberg-2002-foundations}; under this regularity the conditional KL chain-rule identity [[#^eq-chain-rule]] of [[#^sec-track1-cascade]] Step 1 holds in the abstract-spaces form \cite[Theorem 3.4]{polyanskiy-wu-2024-info-theory}\cite[Theorem 5.4]{gray-2011-entropy}.

**(H2$'$) Talagrand $T_2$ inequality on the goal-marginal post-update distribution.** The post-update law $P_{M_{\tau^+} \mid e, M_{\tau^-}}$ satisfies a quadratic Talagrand transport inequality with constant $C_{T_2} > 0$:

$$W_2^2(P,\, P_{M_{\tau^+} \mid e, M_{\tau^-}}) \;\leq\; C_{T_2} \cdot \mathrm{KL}(P \,\Vert\, P_{M_{\tau^+} \mid e, M_{\tau^-}}) \quad \text{for all probability measures } P.$$ ^eq-h2-prime

Two clean sufficient conditions for ($T_2$) (proofs in [[#^sec-h2-prime-suff]]):

- *(a) LSI on the post-update distribution.* If $P_{M_{\tau^+} \mid e, M_{\tau^-}}$ satisfies a logarithmic Sobolev inequality with constant $\rho > 0$, the Otto-Villani inequality \cite[Theorem 1]{otto-villani-2000-jfa} gives $C_{T_2} = 2/\rho$. Bakry-Émery \cite{bakry-1985-diffusions} supplies $\rho \geq K$ when the post-update density is $K$-strongly log-concave.
- *(b) Dimension-free sub-Gaussian Lipschitz concentration.* In the sense of \citet{gozlan-2009-t2-characterization}, $C_{T_2}$ admits an explicit form in the variance proxy \cite{bobkov-gotze-1999-t2-subgaussian,gozlan-2009-t2-characterization}. (\citet{bobkov-gotze-1999-t2-subgaussian} characterizes $T_1$ from single-Lipschitz-function sub-Gaussian moments; Gozlan's strengthening to $T_2$ requires *dimension-free* product-measure concentration, strictly stronger.)

*Bounded-support remark.* Bare bounded support of diameter $D$ on $\mathcal{M}$ is *not* a $T_2$-sufficient condition (\citealt{gozlan-2009-t2-characterization} — $T_2$ is equivalent to dimension-free Gaussian concentration of $\mu^{\otimes n}$, strictly stronger than diameter, with a clean two-point Bernoulli counterexample showing $W_2^2/\mathrm{KL}$ can be unbounded; see [[#^sec-h2-prime-suff]]). What does follow from diameter is the weaker $T_1$ inequality $W_1(P, P_{M_{\tau^+}\mid e, M_{\tau^-}}) \le (D/\sqrt{2})\sqrt{\mathrm{KL}}$ with $C_{T_1} = D^2/4$, sharp on Bernoulli$(1/2)$. The $T_1$ form supports the *distance* reading of [[#^eq-bias-quantity]] at $W_1$ rather than $W_2$ — adequate for our distance-form bound, at the cost of giving up [[#^thm-track1-uncond]]'s tighter squared-distance / linear-in-$I$ refinement [[#^eq-track1-sq]]. Token-distribution belief states for LLMs on the simplex are more naturally treated under Track 2 ([[#^sec-track2]]), where the simplex's constant positive sectional curvature on the round-sphere image gives Bakry-Émery CD$(K, n-1)$ with $K > 0$ and the universal $\sqrt{2}\sqrt{I}$ form holds.

The post-update law $P_{M_{\tau^+}\mid e, M_{\tau^-}}$ is the actually-realized goal-marginal output of the architecture's update mechanism — there is no separate hypothesis on the latent observation distribution and no separate posterior-pushforward step, because we never leave the model space.

### Cascade — two steps ^sec-track1-cascade

**Step 1 — Chain rule of relative entropy on the post-update law.** By \citet[Theorem 2.5.3]{cover-thomas-2006-info-theory} applied to the conditional law of $M_{\tau^+}$ given $(e, M_{\tau^-})$ marginalized over $G$:

$$\mathbb{E}_G\bigl[\,\mathrm{KL}(P_{M_{\tau^+} \mid e, M_{\tau^-}, G} \,\Vert\, P_{M_{\tau^+} \mid e, M_{\tau^-}})\,\bigr] \;=\; I(G;\,M_{\tau^+} \mid e_\tau,\, M_{\tau^-}).$$ ^eq-chain-rule

This is exact. The right-hand side is the *transferred* goal-information into the post-update model state — the actually-realized coupling between $G$ and $M_{\tau^+}$ given the prior model state and the event.

**Step 2 — Talagrand $T_2$ slice-wise + expectation.** Apply (H2$'$) slice-wise at each $G = g$:

$$W_2^2(P_{M_{\tau^+} \mid e, M_{\tau^-}, G=g},\, P_{M_{\tau^+} \mid e, M_{\tau^-}}) \;\leq\; C_{T_2} \cdot \mathrm{KL}(P_{M_{\tau^+} \mid e, M_{\tau^-}, G=g} \,\Vert\, P_{M_{\tau^+} \mid e, M_{\tau^-}}).$$

Take expectation over $G$ and substitute [[#^eq-chain-rule]]:

> [!theorem] Track 1, unconditional ^thm-track1-uncond
> Under (H1) and (H2$'$), the squared-distance bound [[#^eq-track1-sq]] holds and equivalently, by Jensen, the distance bound [[#^eq-track1-dist]] holds.

$$\mathbb{E}\bigl[W_2^2\bigl(P_{M_{\tau^+}\mid e, M_{\tau^-}, G},\, P_{M_{\tau^+}\mid e, M_{\tau^-}}\bigr)\bigr] \;\leq\; C_{T_2} \cdot I(G;\,M_{\tau^+} \mid e_\tau,\, M_{\tau^-}),$$ ^eq-track1-sq

$$\mathbb{E}\,W_2\bigl(P_{M_{\tau^+}\mid e, M_{\tau^-}, G},\, P_{M_{\tau^+}\mid e, M_{\tau^-}}\bigr) \;\leq\; \sqrt{C_{T_2}} \cdot \sqrt{\,I(G;\,M_{\tau^+} \mid e_\tau,\, M_{\tau^-})\,}.$$ ^eq-track1-dist

[[#^thm-track1-uncond]] is unconditional in the architectural classification: the LHS bounds the variance-around-marginal of the post-update law under goal variation, and the RHS is the transferred goal-information that the architecture's processing graph realizes. (H1) and (H2$'$) are regularity hypotheses on the post-update law; neither makes a structural commitment about how $G$ enters the architecture.

### Architectural corollary ^sec-track1-arch

The architectural reading of [[#^thm-track1-uncond]] follows from the [[#^sec-attenuation-ratio]] definition of $\kappa_{\text{processing}}$ as the architectural attenuation ratio. The substitution $I(G; M_{\tau^+} \mid e, M_{\tau^-}) = \kappa_{\text{processing}} \cdot I(G; \Omega_\tau \mid e_\tau, M_{\tau^-})$ is *definitional* (per [[#^eq-kappa-processing]]); the substantive content of the architectural commitment is the *boundedness* of this ratio, named (H$_\kappa$):

> [!hypothesis] (H$_\kappa$) Bounded architectural attenuation ^hyp-h-kappa
> $\kappa_{\text{processing}} \leq \kappa^* < \infty$, with $\kappa^*$ a named architectural constant (typically $1$).

For Class 1 (Separated), $G \to \Omega \to M_{\tau^+}$ is a Markov chain conditional on $(e, M_{\tau^-})$ and the data-processing inequality gives $\kappa_{\text{processing}} \leq 1$ automatically — (H$_\kappa$) is not a commitment but a consequence. For Class 2 (Partial) and Class 3 (Coupled) it is a *named structural commitment*; [[#^sec-h-kappa-status]] documents two sufficient conditions and a worst-case witness (parrot architecture: $\kappa_{\text{processing}} = \infty$, outside scope).

> [!corollary] Track 1, architectural factorization ^cor-track1-arch
> Under (H1), (H2$'$), and (H$_\kappa$) at level $\kappa^*$, the architectural-factorization bound [[#^eq-track1-arch]] holds.

$$\mathbb{E}\,W_2\bigl(P_{M_{\tau^+}\mid e, M_{\tau^-}, G},\, P_{M_{\tau^+}\mid e, M_{\tau^-}}\bigr) \;\leq\; \sqrt{C_{T_2} \cdot \kappa^* \cdot I(G;\,\Omega_\tau \mid e_\tau,\, M_{\tau^-})}.$$ ^eq-track1-arch

In Class 1 (Separated), the architecture's update mechanism is goal-blind, so $G$ enters $M_{\tau^+}$ only through the data channel $\Omega$. The chain $G \to \Omega \to M_{\tau^+}$ is Markov conditional on $(e, M_{\tau^-})$, and DPI gives $\kappa_{\text{processing}} \le 1$ — the architecture cannot amplify resolvable goal-information beyond what the data channel transfers, but it can saturate this bound (the conjugate-Gaussian Class 1 example of [[#^sec-track1-conjugate-gauss]] saturates it because the data channel $\Omega \to L_{\text{post}}\Omega$ is invertible). Class 1 thus does *not* collapse the bias to zero in general — it bounds the bias by the data-channel attenuation, with zero only in the degenerate sub-case where $G \perp\!\!\!\perp \Omega$ given $(e, M_{\tau^-})$. In Class 2 (Partial), $\kappa_{\text{processing}}$ scales the effective information transfer through the shared pathways. In Class 3 (Coupled), $\kappa_{\text{processing}}$ can approach one (or, pathologically, exceed it — see [[#^sec-h-kappa-status]] parrot witness). The corollary is what gives the bound its operational architecture-engaged reading; the unconditional theorem is the structural backbone whose math holds without (H$_\kappa$)'s boundedness commitment.

### Geometric interpretation ^sec-track1-geom

When (H2$'$) is verified via LSI on the post-update parameter law (route (a) above), $C_{T_2} = 2/\rho_{\text{post}}$, where $\rho_{\text{post}}$ is the LSI constant of $P_{M_{\tau^+}\mid e, M_{\tau^-}}$ as a law on the parameter manifold $\mathcal{M}$ — *not* the LSI constant of the inside-posterior covariance. In the conjugate-Gaussian case the post-update parameter law has variance $L_{\text{post}}^2\sigma^2$ (the spread of the random parameter $\mu_+ = L_{\text{post}}\Omega$ under the data noise), giving $\rho_{\text{post}} = 1/(L_{\text{post}}^2\sigma^2)$ and $C_{T_2} = 2 L_{\text{post}}^2\sigma^2 = 2 L_{\text{post}}^2/\rho_{\text{LSI}}$ where $\rho_{\text{LSI}} = 1/\sigma^2$ is the *observation-side* LSI constant (computation in [[#^sec-conjugate-gauss-numerics]]). The unconditional reformulation thus *recovers* the canonical $2 L_{\text{post}}^2/\rho_{\text{LSI}}$ of the Stuart-school cascade as a special case under route (a), with the additional benefit that any of routes (a)/(b)/(c) suffices to verify (H2$'$). The inside-posterior covariance $\sigma_{\text{post}}^2 = L_{\text{post}}\sigma^2$ — the spread of the posterior measure on $\theta$ at a fixed observation — is a *different* object and would give the wrong $C_{T_2}$ if substituted; the conflation is a known submission-blocker pitfall and is corrected explicitly in [[#^sec-conjugate-gauss-numerics]].

The constant $C_{T_2}$ has a clean reading as *post-update geometric stiffness*: how resistant the architecture's update mechanism is to goal-driven perturbation, measured at the post-update law itself rather than reconstructed from observation-side concentration plus posterior-pushforward Lipschitz behavior. Smaller $C_{T_2}$ corresponds to a more concentrated post-update distribution (sharper posterior), which leaves the goal less room to displace it within the concentration support.

The squared-distance bound [[#^eq-track1-sq]] is *linear* in transferred information: doubling the transferred goal-information at most doubles the squared $W_2$-displacement. The distance bound [[#^eq-track1-dist]] is $\sqrt{I}$-form by Jensen and matches the umbrella shape [[#^eq-umbrella]].

### Worked example: conjugate Gaussian ^sec-track1-conjugate-gauss

Take a one-dimensional latent $\theta$ with prior $\theta \sim \mathcal{N}(0, \tau^2)$ encoded by $M_{\tau^-}$, observation channel $\Omega \mid \theta \sim \mathcal{N}(\theta, \sigma^2)$, and goal-conditional reweighting $\Omega \mid G \sim \mathcal{N}(\beta(G), \sigma^2)$ — the goal shifts the world-state, the architecture's update mechanism is goal-blind (Class 1, Separated). Bayesian updating gives the posterior on $\theta$ given $\Omega = \omega$ as $\mathcal{N}(L_{\text{post}}\,\omega,\, \sigma_{\text{post}}^2)$ with $L_{\text{post}} = \tau^2/(\sigma^2+\tau^2)$ and $\sigma_{\text{post}}^2 = \sigma^2\tau^2/(\sigma^2+\tau^2) = L_{\text{post}}\sigma^2$. Identifying $M_{\tau^+}$ with the posterior-mean parameter $\mu_+ := L_{\text{post}}\,\Omega$ (variance $\sigma_{\text{post}}^2$ fixed), the goal-conditional law on $\mathcal{M}$ is $\mu_+ \mid G \sim \mathcal{N}(L_{\text{post}}\beta(G),\, L_{\text{post}}^2\sigma^2)$.

*Two distinct variances are at play and must not be conflated:* $\sigma_{\text{post}}^2 = L_{\text{post}}\sigma^2$ is the *inside-posterior* covariance (the spread of the posterior measure on $\theta$ for a single fixed observation), while $L_{\text{post}}^2\sigma^2 = L_{\text{post}}\,\sigma_{\text{post}}^2$ is the variance of the *law of $\mu_+$ given $G$* (the spread of the random model state under the data noise). Track 1's $C_{T_2}$ comes from LSI on the *post-update parameter law*, hence the latter variance: $C_{T_2} = 2/\rho_{\text{post}} = 2\,L_{\text{post}}^2\sigma^2$. At small $\mathrm{Var}_G(\beta)$, the cascade is sharp:

$$\mathbb{E}[W_2^2] \;\approx\; L_{\text{post}}^2\,\mathrm{Var}_G(\beta) \;=\; 2 L_{\text{post}}^2\sigma^2 \cdot \frac{\mathrm{Var}_G(\beta)}{2\sigma^2} \;=\; C_{T_2}\cdot I(G;\,M_{\tau^+}\mid e, M_{\tau^-}),$$

matching [[#^thm-track1-uncond]] with equality.

The realized attenuation ratio is $\kappa_{\text{processing}}^{\text{realized}} = 1$: the goal-blind kernel $\Omega \mapsto L_{\text{post}}\Omega$ is invertible (deterministic linear), so the data-processing inequality $G \to \Omega \to M_{\tau^+}$ saturates and $I(G; M_{\tau^+} \mid e, M_{\tau^-}) = I(G; \Omega \mid e, M_{\tau^-})$ exactly. In this conjugate-Gaussian Class 1 (Separated) setup the architecture realizes *no* information-theoretic attenuation; $\kappa = 1$ is a witness that the example sits at the worst-case Class 1 corner where DPI is tight. Substituting into the cascade:

$$\mathbb{E}[W_2^2] \;\leq\; C_{T_2}\cdot I(G;\,M_{\tau^+}\mid e, M_{\tau^-}) \;=\; 2 L_{\text{post}}^2\sigma^2 \cdot I(G;\Omega\mid e, M_{\tau^-}) \;=\; \frac{2 L_{\text{post}}^2}{\rho_{\text{LSI}}}\cdot I(G;\Omega\mid e, M_{\tau^-}),$$

with $\rho_{\text{LSI}} = 1/\sigma^2$. *This is exactly the canonical Stuart-school cascade constant* — recovered as $C_{T_2}$ alone, with $\kappa = 1$ from DPI saturation. The framework's contribution here is not architectural attenuation (the Class 1 conjugate-Gaussian example doesn't exhibit any) but the unconditional theorem's recovery of the Stuart cascade as a special case of the post-update LSI route. Architectural attenuation $\kappa < 1$ requires either a non-invertible data channel (information lost between $\Omega$ and $M_{\tau^+}$) or a Class 2 / Class 3 architecture; [[#^sec-conjugate-gauss-numerics]] compares regimes.

In the prior-dominant limit ($\tau^2 \ll \sigma^2$): $C_{T_2} \approx 2\tau^4/\sigma^2 \to 0$ — vanishing prior pins the parameter law to zero regardless of goal. In the likelihood-dominant limit ($\sigma^2 \ll \tau^2$): $C_{T_2} \approx 2\sigma^2 \to 0$ — sharp observations lock the posterior mean to the evidence and goal-induced bias scales with the data noise. The constant is largest at $\tau \sim \sigma$ (balanced prior-likelihood tension); goal-coupling bias is largest where the posterior is most reactive to evidence — neither prior-dominated nor evidence-dominated.

### Cite-and-distinguish ^sec-track1-cite

The closest single-paper match for the cascade machinery is Hosseini, Hsu, and Taghvaei's *Conditional Optimal Transport on Function Spaces* \cite{hosseini-hsu-taghvaei-2024-conditional-ot}, which develops conditional triangular transport for amortized Bayesian inference and obtains regularity estimates on the conditioning maps from prior to posterior. Their target is *amortized inference*: building a network that maps observations to posteriors. Our target is *bias under goal-coupling*: bounding the displacement induced when the architecture's update mechanism receives the goal as part of its input. Related machinery; different application. The $\kappa_{\text{processing}}$ corollary and the architectural classification of [[#^sec-setup]] are not in their setting.

The Stuart school of Bayesian inverse problems supplies *sufficient-condition machinery* for verifying (H2$'$) in canonical cases: \citet[Theorem 4.6]{stuart-2010-acta} establishes Hellinger-distance well-posedness of the posterior measure under bounded-log-likelihood and Lipschitz-in-data assumptions; \citet{sprungk-2020-local-lipschitz} gives local Lipschitz stability across TV / Hellinger / $W_2$ / KL; \citet{cvetkovic-2025-upper} match Sprungk's upper bounds with lower bounds; \citet{dolera-mainini-2023-aihp-lipschitz} obtain global $W_2$-Lipschitz continuity of probability kernels with explicit constants in terms of Fisher-information functionals. In the unconditional reformulation these results enter as *background* — they help verify (H2$'$) when the post-update is itself a Bayesian posterior — rather than as load-bearing main-theorem hypotheses; the cascade no longer requires a separate posterior-pushforward step. \citet{garbuno-inigo-2023-bayesian} develop integral-probability-metric perturbation analysis under log-Sobolev-style functional inequalities; relevant to (H2$'$) verification under route (a).
