## Mechanism ^sec-mechanism

Both tracks bridge to the bound through the same move: a chain rule of relative entropy applied directly to the post-update law, marginalized over the goal. This is the structural composition of the two literatures — the Bayesian-inverse-problems posterior-stability machinery and the architectural classification meet at this identity.

> [!lemma] Chain rule on the post-update law ^lem-chain-rule
> Under (H1), $\mathbb{E}_G\bigl[\mathrm{KL}(P_{M_{\tau^+}\mid e, M_{\tau^-}, G} \,\|\, P_{M_{\tau^+}\mid e, M_{\tau^-}})\bigr] \;=\; I(G;\,M_{\tau^+}\mid e_\tau, M_{\tau^-})$.

The identity is exact (\citealt[Theorem 3.4]{polyanskiy-wu-2024-info-theory}; \citealt[Theorem 5.4]{gray-2011-entropy} for the abstract-spaces form). The right-hand side is *transferred* goal-information — the actually-realized coupling between $G$ and the post-update model state. Combined with either a transport inequality on the post-update law or a Fisher-Rao second-order expansion of KL, the bound follows by taking expectation over $G$ and applying Jensen.

### Track 1 — transport-inequality cascade ^sec-track1-mechanism

Apply (H2$'$) slice-wise: $W_2^2(P_{M_{\tau^+}\mid G=g}, P_{M_{\tau^+}}) \le C_{T_2} \cdot \mathrm{KL}_g$. Take expectation over $G$, substitute [[#^lem-chain-rule]] for the slice-wise mean, and apply Jensen on $\sqrt{\,\cdot\,}$: $\mathbb{E}\,W_2 \le \sqrt{C_{T_2} I_M}$. The cascade composes textbook information-theoretic and transport-inequality machinery — Otto-Villani for the LSI-implies-$T_2$ direction, Bakry-Émery for $K$-strong-log-concavity-implies-LSI, Gozlan's dimension-free sub-Gaussian Lipschitz-concentration characterization. The contribution is the application to the goal-conditional bias quantity on the post-update law: there is no separate posterior-pushforward step, because the chain rule lives on the post-update law directly. Full proof + (H2$'$) sufficient-condition verifications in [[#^sec-h2-prime-suff]].

### Track 2 — Fisher-Rao expansion ^sec-track2-mechanism

The KL-to-Fisher-Rao second-order expansion on the ambient $L^2$-sphere of $\sqrt p$ — $\mathrm{KL}(P\,\|\,Q) = \tfrac{1}{2}d_{FR}^2(P, Q) + O(d_{FR}^3)$ in the Amari-Nagaoka spherical-arc convention (\citealt{amari-nagaoka-2000-info-geom} §3.7) — applies to nearby points on the ambient sphere. The ambient framing absorbs the goal-marginal-baseline-as-mixture concern: both the slice law $P_{M_{\tau^+}\mid G=g}$ and the goal-marginal mixture $P_{M_{\tau^+}}$ are points on the ambient sphere by construction. Apply slice-wise under (H4$'$), take $\mathbb{E}_G$, substitute [[#^lem-chain-rule]], and apply Jensen on $\sqrt{\,\cdot\,}$: $\mathbb{E}\,d_{FR} \le \sqrt 2\,\sqrt{I_M}\,(1 + o(1))$. The $(1+o(1))$ remainder is controlled uniformly under (H4$'$) by the Amari-Chentsov tensor and minimum Fisher eigenvalue (full bound in [[#^sec-track2-proof]]). The constant $\sqrt 2$ is what (PI)+(R)+(K) buys: Čencov uniqueness pins it ([[#^thm-fr-uniqueness]]).

*Outside (H4$'$).* Track 2 has globally-valid companion bounds (ambient FR spherical-arc at $C = 2$, Hellinger chord at $1/\sqrt 2$) under (H1)+(PI) only — full taxonomy and chord-arc-at-antipode geometric reading in [[#^sec-track2-companions]].

### No-go — chart rescaling ^sec-no-go-mechanism

The no-go's proof is a chart-rescaling argument: $\phi \mapsto a\phi$ scales the chart-Euclidean $W_2$ linearly while leaving KL, MI, Fisher-Rao spherical-arc, and Hellinger chart-invariant; taking $a \to \infty$ contradicts any candidate fixed $C_0\sqrt I$. Gaussian scale charts $\sigma$ vs. $\log\sigma$ illustrate. Constructively: universal constants require coordinate-invariant norms — under (PI)+(R)+(K), Čencov uniqueness selects Fisher-Rao + $\sqrt 2$ ([[#^sec-no-go-proof]]).
