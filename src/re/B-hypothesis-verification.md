## Hypothesis verification details ^sec-h2-prime-suff

This appendix collects the regularity-condition verifications referenced in [[#^sec-track1-mechanism]] and [[#^sec-track2-mechanism]].

### (H2$'$) Talagrand $T_2$ inequality on the post-update law — sufficient conditions ^sec-h2-prime-routes

(H2$'$) requires $W_2^2(P, P_{M_{\tau^+} | e, M_{\tau^-}}) \leq C_{T_2} \mathrm{KL}(P \,\|\, P_{M_{\tau^+} | e, M_{\tau^-}})$ for all probability measures $P$. Three clean sufficient conditions:

**Route (a): LSI on the post-update law.** If $P_{M_{\tau^+} | e, M_{\tau^-}}$ satisfies a logarithmic Sobolev inequality with constant $\rho_{\text{post}} > 0$,

$$\mathrm{Ent}_{P_{M_{\tau^+} | e, M_{\tau^-}}}(f^2) \;\leq\; \tfrac{2}{\rho_{\text{post}}}\,\mathbb{E}_{P_{M_{\tau^+} | e, M_{\tau^-}}}[\|\nabla f\|^2] \quad \text{for all sufficiently smooth } f,$$

then by \cite[Theorem 1]{otto-villani-2000-jfa}, (H2$'$) holds with $C_{T_2} = 2/\rho_{\text{post}}$. A sufficient condition for LSI, by Bakry-Émery's curvature-dimension criterion \cite{bakry-1985-diffusions}, is $K$-strong log-concavity of the post-update density: $-\nabla^2 \log p_{M_{\tau^+}| e, M_{\tau^-}} \succeq K \cdot I$ for some $K > 0$, giving $\rho_{\text{post}} \geq K$.

**Hypothesis (S) — own proof of strong log-concavity for Bayesian post-updates.** When the post-update law is itself a Bayesian posterior with negative log-likelihood $\Phi(\theta;\omega)$ and prior density $\pi(\theta)$, the posterior negative log-density is $U(\theta;\omega) = \Phi(\theta;\omega) - \log\pi(\theta)$. Strong log-concavity of the posterior is a *direct* statement about the Hessian-in-$\theta$ of $U$: $\nabla^2_\theta U(\theta;\omega) \succeq K_{\text{eff}}\cdot I$ uniformly in $\omega \in \Omega$, for some $K_{\text{eff}} > 0$. Two clean sufficient conditions:

- *(S-i) Convex likelihood + strongly log-concave prior.* If $\nabla^2_\theta\Phi(\theta;\omega) \succeq 0$ uniformly in $(\theta,\omega)$ (likelihood log-concave in $\theta$) and $\pi$ is $K$-strongly log-concave (so $-\nabla^2_\theta\log\pi \succeq K\cdot I$), then $\nabla^2_\theta U \succeq K\cdot I$, giving $K_{\text{eff}} \ge K$.
- *(S-ii) Bounded negative likelihood curvature dominated by prior curvature.* If $\nabla^2_\theta\Phi(\theta;\omega) \succeq -K_0\cdot I$ uniformly with $K_0 < K$ (likelihood may be locally non-convex but its negative-curvature is bounded), and $\pi$ is $K$-strongly log-concave, then $\nabla^2_\theta U \succeq (K - K_0)\cdot I$, giving $K_{\text{eff}} \ge K - K_0 > 0$.

Either condition gives Bakry-Émery $\rho_{\text{post}} \ge K_{\text{eff}}$ and Otto-Villani $C_{T_2} \le 2/K_{\text{eff}}$. \citet{sprungk-2020-local-lipschitz} derives sharper local-Lipschitz constants for the posterior across TV / Hellinger / $W_2$ / KL; \citet{cvetkovic-2025-upper} establish matched lower bounds; \citet{dolera-mainini-2023-aihp-lipschitz} give global $W_2$-Lipschitz constants in terms of Fisher-information functionals — which can sharpen $C_{T_2}$ beyond the bare $2/K_{\text{eff}}$. Mixed-Hessian smoothness $\|\partial^2_{\theta\omega}\Phi\| \le H$ is *not* a substitute: it controls how the posterior mode shifts with $\omega$, but the LSI / strong-convexity claim is about the curvature in $\theta$ and must be made directly.

**Route (b)** *(corrected — bounded support gives $T_1$, not $T_2$).* Bare bounded support of diameter $D$ on $\mathcal{M}$ is **not** a $T_2$-sufficient condition. *Counterexample.* On $\{0, 1\} \subset \mathbb{R}$ (diameter $D = 1$), let $\nu = \tfrac{1}{2}\delta_0 + \tfrac{1}{2}\delta_1$ and $\mu_\epsilon = (\tfrac{1}{2}-\epsilon)\delta_0 + (\tfrac{1}{2}+\epsilon)\delta_1$ for $\epsilon \in (0, 1/2)$. Then $W_2^2(\mu_\epsilon, \nu) = \epsilon$ (the optimal coupling moves mass $\epsilon$ from $0$ to $1$), while $\mathrm{KL}(\mu_\epsilon\,\|\,\nu) = 2\epsilon^2 + O(\epsilon^4)$, so $W_2^2/\mathrm{KL} = 1/(2\epsilon) + O(1) \to \infty$ as $\epsilon \to 0^+$ — no constant $C$ uniformizes the ratio. The structural reason: \citet{gozlan-2009-t2-characterization} established that $T_2$ is *equivalent* to dimension-free Gaussian concentration of $\mu^{\otimes n}$, strictly stronger than diameter (Talagrand-type product concentration requires LSI / curvature input, not just bounded support).

What does follow from diameter is the *weaker* $T_1$ inequality: by $W_1 \le D \cdot \mathrm{TV}$ and Pinsker $\mathrm{TV} \le \sqrt{\mathrm{KL}/2}$,

$$W_1^2(P, P_{M_{\tau^+}| e, M_{\tau^-}}) \;\le\; C_{T_1}\,\mathrm{KL}(P\,\|\, P_{M_{\tau^+}| e, M_{\tau^-}}), \qquad C_{T_1} = D^2/2$$

(squared convention matching (H2$'$); equivalently $W_1 \le (D/\sqrt 2)\sqrt{\mathrm{KL}}$, sharp on the two-point Bernoulli at $p = 1/2$ — \citealt{bobkov-gotze-1999-t2-subgaussian} with Hoeffding sub-Gaussian variance proxy $\sigma^2 = D^2/4$ for distributions on a diameter-$D$ set, applied to the $T_1$-equivalent Lipschitz-sub-Gaussian characterization). Substituting $W_1$ for $W_2$ in Step 2 of the [[#^sec-track1-mechanism]] cascade preserves the *distance-form* bound $\mathbb{E}\|\Delta M_{\text{bias}}\| \le (D/\sqrt 2)\sqrt{I(G; M_{\tau^+}| e, M_{\tau^-})}$ at the $T_1$ level — at the cost of giving up [[#^thm-umbrella]]'s tighter squared-distance / linear-in-$I$ refinement [[#^eq-umbrella]]. Token-distribution belief states for LLMs on the simplex are more naturally treated under Track 2 (Fisher-Rao, [[#^sec-track2-mechanism]]), where the simplex's constant positive sectional curvature (on the round-sphere image $x \mapsto (\sqrt{x_1}, \dots, \sqrt{x_n})$) provides Bakry-Émery CD$(K, n-1)$ with $K > 0$, an LSI w.r.t. Fisher-Rao volume, and the universal $\sqrt{2}\sqrt{I}$ form holds without Track 1's diameter-only weakening.

**Route (c): dimension-free sub-Gaussian Lipschitz concentration.** Per \citet{gozlan-2009-t2-characterization}, $\mu$ satisfies $T_2(C)$ iff $\mu^{\otimes n}$ enjoys dimension-free Gaussian concentration of Lipschitz functionals: there exist constants $C', \lambda > 0$ such that $\mathbb{E}_{\mu^{\otimes n}}[\exp(\lambda(f - \mathbb{E}f)^2)] \leq 2$ uniformly in $n$ for every 1-Lipschitz $f: \mathbb{R}^n \to \mathbb{R}$. \citet{bobkov-gotze-1999-t2-subgaussian} characterizes the strictly weaker *single-Lipschitz-function* version (giving $T_1$); the Gozlan strengthening to $T_2$ is what makes single-distribution sub-Gaussian moments insufficient on their own. When dimension-free product concentration holds, $C_{T_2}$ admits an explicit form in the variance proxy.

**When both routes fail.** Heavy-tailed post-updates without LSI and without dimension-free sub-Gaussian concentration are outside Track 1's $T_2$ scope. The $T_1$ fallback under bounded support (Route (b) as corrected above) recovers the distance form at weaker constants — adequate for $\mathbb{E}\|\Delta M_{\text{bias}}\| \le C\sqrt{I}$. Track 2 under (PI) + (R) + (K) does not require (H2$'$) and remains available; [[#^thm-hellinger]]'s Hellinger backstop is a global universal-constant fallback under (PI) only.

### KL-to-Fisher second-order expansion ^sec-h2-prime-kl-fisher

For nearby distributions $P_\theta, P_{\theta + \delta}$ on a parametric family with Fisher information $\mathbf{I}(\theta)$:

$$\mathrm{KL}(P_{\theta + \delta} \,\|\, P_\theta) = \tfrac{1}{2} \delta^\top \mathbf{I}(\theta) \delta + O(\|\delta\|^3) = \tfrac{1}{2} d_{FR}^2(P_\theta, P_{\theta + \delta}) + O(d_{FR}^3).$$

Standard derivation: \citealt{cover-thomas-2006-info-theory} §12.5; \citealt{amari-nagaoka-2000-info-geom} §3.7 Theorem 3.1. The $O(d_{FR}^3)$ remainder is sharp in the sense that the second-order term is exact and the third-order term is generically non-zero (off-exponential-family).

### (H$_\kappa$) sufficient conditions ^sec-h-kappa-suff

The architectural-corollary commitment (H$_\kappa$) is that $\kappa_{\text{processing}} = I(G; M_{\tau^+}| e, M_{\tau^-})/I(G; \Omega_\tau| e, M_{\tau^-})$ is bounded by some named architectural constant $\kappa^* < \infty$ (typically $1$). For Class 1 (Separated) architectures, the data-processing inequality applied to the Markov chain $G \to \Omega_\tau \to M_{\tau^+}$ (conditional on $(e_\tau, M_{\tau^-})$ by architectural separation) gives $\kappa_{\text{processing}} \le 1$ automatically. For Class 2 (Partial) and Class 3 (Coupled), two structural conditions each give $\kappa_{\text{processing}} \le 1$ (or $\le 1+\alpha$ in the second condition):

1. *Goal-blind effective kernel.* Suppose the post-update map factors as $M_{\tau^+} = K(M_{\tau^-}, e_\tau, \widetilde{\Omega}_\tau)$ with $K$ deterministic, where $\widetilde{\Omega}_\tau$ is a goal-conditional reweighting of $\Omega_\tau$ that is *non-amplifying*: $I(G; \widetilde{\Omega}_\tau | e_\tau, M_{\tau^-}) \le I(G; \Omega_\tau | e_\tau, M_{\tau^-})$. Then conditional on $(e_\tau, M_{\tau^-})$, $G \to \widetilde{\Omega}_\tau \to M_{\tau^+}$ is a Markov chain (since $K$ depends on $G$ only through $\widetilde{\Omega}_\tau$), and DPI applied along this chain gives

$$I(G; M_{\tau^+}| e_\tau, M_{\tau^-}) \;\le\; I(G; \widetilde{\Omega}_\tau | e_\tau, M_{\tau^-}) \;\le\; I(G; \Omega_\tau | e_\tau, M_{\tau^-}),$$

i.e., $\kappa_{\text{processing}} \le 1$.

2. *Bounded direct architectural channel.* Suppose the architecture's *direct* goal-coupling pathway (independent of $\Omega_\tau$) has bounded conditional MI relative to the resolvable channel: $I(G; M_{\tau^+} | e_\tau, M_{\tau^-}, \Omega_\tau) \le \alpha\,I(G; \Omega_\tau | e_\tau, M_{\tau^-})$ for some $\alpha \ge 0$. The chain rule of mutual information conditioned on $(e_\tau, M_{\tau^-})$ gives $I(G; M_{\tau^+}, \Omega_\tau | e_\tau, M_{\tau^-}) = I(G; \Omega_\tau | e_\tau, M_{\tau^-}) + I(G; M_{\tau^+} | e_\tau, M_{\tau^-}, \Omega_\tau)$, and using $I(G; M_{\tau^+}| e_\tau, M_{\tau^-}) \le I(G; M_{\tau^+}, \Omega_\tau | e_\tau, M_{\tau^-})$ (additional side information cannot decrease MI), we get $\kappa_{\text{processing}} \le 1+\alpha$. The case $\alpha = 0$ — architectural channel adds nothing beyond what $\Omega_\tau$ provides given $(e_\tau, M_{\tau^-})$ — gives $\kappa_{\text{processing}} \le 1$.

**Worst-case witness — parrot architecture.** Consider a degenerate Coupled-class architecture whose update rule is $M_{\tau^+} := G$ (the post-update model state is identically the goal). Two computations:

*Numerator.* Since $M_{\tau^+} = G$ deterministically conditional on $(e_\tau, M_{\tau^-})$, $I(G; M_{\tau^+} | e_\tau, M_{\tau^-}) = H(G | e_\tau, M_{\tau^-})$ exactly.

*Denominator.* Suppose $G \perp\!\!\!\perp \Omega_\tau$ given $(e_\tau, M_{\tau^-})$ — the goal carries no information about the latent world-state beyond what the evidence and prior have already pinned down. (Operationally this is the "make me feel good" goal of [[#^sec-architectural-classification]]: the user's affective goal is independent of the empirical question the evidence resolves.) Then $I(G; \Omega_\tau | e_\tau, M_{\tau^-}) = 0$.

Hence $\kappa_{\text{processing}} = H(G | e_\tau, M_{\tau^-}) / 0 = +\infty$. (H$_\kappa$) explicitly fails. This shows the architectural commitment is *real* for non-Separated architectures, not a free move. The unconditional theorems ([[#^thm-umbrella]], [[#^thm-track2-global]], [[#^thm-hellinger]]) still bound the parrot architecture's displacement by transferred information directly — the prefactor is $\sqrt{H(G | e_\tau, M_{\tau^-})}$ rather than $\sqrt{\kappa\,I(G;\Omega)}$ — but the $\kappa \times \mathcal{A}$ factorization (and hence the architectural-corollary form) does not apply.
