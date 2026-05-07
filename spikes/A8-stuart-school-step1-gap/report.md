# A8 — Stuart-school reduction Step 1 gap

**Status: PARTIAL — strengthening succeeds at theorem level via a clean unbundling of (C4) into separable hypotheses, but the structural route does not recover the canonical $2L_{\text{post}}^2/\rho_{\text{noise}}$ constant verbatim. The constant transfers up to an absolute multiplicative overhead (factor $\geq 2$ at minimum, regime-dependent in general). The §C conjugate-Gaussian instance recovers the *tight* canonical constant via a different derivation (direct sub-Gaussian read-off on the post-update parameter law), not via the structural reduction. Theorem E.2's claim (c) — "the canonical Stuart-school cascade constant — recovered under the same Stuart-school hypotheses generically" — needs to narrow to "a constant of the canonical Stuart-school form $\propto L_{\text{post}}^2/\rho_{\text{noise}}$; the tight constant $2L_{\text{post}}^2/\rho_{\text{noise}}$ is recovered on conjugate-Gaussian and exponential-family-conjugate instances via direct sub-Gaussian read-off."**

The gap identified by Codex finding 5 + Opus 2.1 is real and structurally deep: the two-step Lipschitz-pushforward composition inherently loses the contraction benefit that the §C calculation exploits. The honest framing is that the reduction theorem provides a *qualitative* sufficient-condition path from Stuart-school hypotheses to (H2′), with the *quantitative* canonical constant landing tightly only when the post-update parameter law admits a direct sub-Gaussian read-off.

This finding modifies the A7 spike's conclusions: Theorem A7.1′ overclaims the constant in claim (c). The unbundled hypothesis set with multiplicative overhead is the corrected form.

---

## 1. The gap, sharpened

### 1.1 What (C4) literally says vs. what Step 1 needs

The current (C4) reads $W_2^2(P_{\Omega \mid \theta_1}, P_{\Omega \mid \theta_2}) \le (2/\rho_{\text{noise}})\|\theta_1 - \theta_2\|^2$. This is *Lipschitz-in-parameter for the kernel* — a sensitivity statement about the family. It says nothing about whether any single member satisfies a $T_2$ inequality, and nothing about whether the marginal $P_\Omega = \int P_{\Omega\mid\theta}\,dP_\theta(\theta)$ does.

Step 1 of the proof claims this "pushes forward $\rho_{\text{noise}}$-concentration on $\theta$ into $T_2(2/\rho_{\text{noise}})$ on the conditional data law (C4 directly)." The phrase "$\rho_{\text{noise}}$-concentration on $\theta$" has no referent: there is no measure on $\theta$-space declared to satisfy any concentration property in (C1)–(C4). Step 1 does not produce a $T_2$ measure to feed Lemma E.1.

**Three things have been silently bundled into (C4):** (i) conditional likelihoods $P_{\Omega\mid\theta}$ are individually $T_2$ with constant $\approx 2/\rho_{\text{noise}}$; (ii) the kernel $\theta \mapsto P_{\Omega\mid\theta}$ is Lipschitz-in-$\theta$ in $W_2$ with some constant $L_{\text{lik}}$ (in Gaussian-shift, $L_{\text{lik}} = 1$); (iii) some concentration on the goal-induced parameter law $P_\theta$ is presumed.

### 1.2 Why the gap matters quantitatively

Read literally, $W_2^2(P_{\Omega\mid\theta_1}, P_{\Omega\mid\theta_2}) \le (2/\rho_{\text{noise}})\|\theta_1-\theta_2\|^2$ is *not even verified* on the canonical Gaussian-shift case unless $\rho_{\text{noise}} \le 2$: for $P_{\Omega\mid\theta} = \mathcal{N}(\theta, \sigma^2 I)$ we have $W_2^2 = \|\theta_1-\theta_2\|^2$, which is bounded by $(2\sigma^2)\|\theta_1-\theta_2\|^2$ only when $\sigma^2 \ge 1/2$. So (C4)'s formula is doing double duty as both a Lipschitz-of-kernel bound *and* a sub-Gaussian envelope on slice variance.

---

## 2. Strengthening attempt 1 — direct $T_2$ on the marginal $P_\Omega$ (FAILS)

The cleanest attempted move: replace (C4) with $P_\Omega \in T_2(2/\rho_{\text{noise}})$ directly. Then Lemma E.1 applies in one step with the $L_{\text{post}}$-Lipschitz map $\Omega \mapsto \mu^\Omega$ to give $T_2(2L_{\text{post}}^2/\rho_{\text{noise}})$ — the canonical form.

**Fails on the canonical instance.** For conjugate-Gaussian, $P_\Omega = \mathcal{N}(0, \sigma^2+\tau^2)$ has $T_2$-constant $2(\sigma^2+\tau^2)$, not $2\sigma^2 = 2/\rho_{\text{noise}}$. The hypothesis is too strong unless $\tau = 0$.

---

## 3. Strengthening attempt 2 — unbundle (C4) and add (C0) (PARTIAL SUCCESS)

The unbundled hypothesis set:

- **(C0)** [new] *Goal-induced parameter measure has $T_2$.* $P_\theta := \theta_*P_G$ on parameter space satisfies $T_2(C_\theta)$.
- **(C1)** [unchanged] Class 1 architecture: $G \to \Omega_\tau \to M_{\tau^+}$ Markov chain.
- **(C2)** [unchanged] Deterministic Bayesian update.
- **(C3)** [unchanged] Stuart-school Lipschitz posterior: $W_2(\mu^\Omega, \mu^{\Omega'}) \le L_{\text{post}}\|\Omega - \Omega'\|$.
- **(C4a)** [unbundled from C4] *Slice $T_2$.* For $P_\theta$-a.e. $\theta$, $P_{\Omega\mid\theta} \in T_2(2/\rho_{\text{noise}})$.
- **(C4b)** [unbundled from C4] *Lipschitz-in-$\theta$ kernel.* $W_2(P_{\Omega\mid\theta_1}, P_{\Omega\mid\theta_2}) \le L_{\text{lik}}\|\theta_1-\theta_2\|$.

(Canonical Gaussian-shift: $L_{\text{lik}} = 1$, slice $T_2$ constant $= 2\sigma^2 = 2/\rho_{\text{noise}}$.)

### 3.1 Lemma A8.1 — Tensorization of $T_2$ with Lipschitz-conditional kernel

**Statement.** Let $P_\theta$ on $\Theta$ satisfy $T_2(C_\theta)$, and let kernel $K(\theta, \cdot) := P_{\Omega\mid\theta}$ satisfy (i) $K(\theta, \cdot) \in T_2(C_{\text{slice}})$ uniformly and (ii) $W_2(K(\theta_1, \cdot), K(\theta_2, \cdot)) \le L_{\text{lik}}\|\theta_1-\theta_2\|$. Then the joint $P_\theta \otimes K$ on $\Theta \times \Omega$ with the $L^2$-product metric satisfies $T_2(C_J)$ with $C_J \le \max\bigl((1 + 2L_{\text{lik}}^2)\,C_\theta,\;\; 2\,C_{\text{slice}}\bigr)$.

**Proof sketch.** Disintegration + chain rule on KL:
$$\mathrm{KL}(\rho \,\|\, P_\theta \otimes K) = \mathrm{KL}(\rho_\Theta \,\|\, P_\theta) + \int \mathrm{KL}(\rho_\theta \,\|\, K(\theta, \cdot))\,d\rho_\Theta.$$

Construct coupling: $\pi^\Theta$ optimal $W_2$-coupling of $(\rho_\Theta, P_\theta)$; for each pair $(\theta, \theta')$, $\pi^\Omega$ optimal $W_2$-coupling of $(\rho_\theta, K(\theta', \cdot))$. Triangle + Cauchy-Schwarz on the second piece using (ii) gives $W_2^2(\rho_\theta, K(\theta', \cdot)) \le 2 W_2^2(\rho_\theta, K(\theta, \cdot)) + 2L_{\text{lik}}^2\|\theta-\theta'\|^2$. Apply (i) to the first piece, $T_2(C_\theta)$ to the marginal, and combine. $\square$

### 3.2 Project to $\Omega$, apply Lemma E.1 once more

Projection $(\theta, \Omega) \mapsto \Omega$ is 1-Lipschitz, so $P_\Omega = (\pi_\Omega)_*(P_\theta \otimes K) \in T_2(C_J)$ by Lemma E.1. Then $\Omega \mapsto \mu^\Omega$ is $L_{\text{post}}$-Lipschitz by (C3), so:

$$\boxed{C_{T_2}^{\text{(structural)}} \;\le\; L_{\text{post}}^2 \cdot \max\bigl((1+2L_{\text{lik}}^2)\,C_\theta,\;\;4/\rho_{\text{noise}}\bigr).}$$

### 3.3 Verification on conjugate-Gaussian — the structural route is loose

For $\theta \sim \mathcal{N}(0, \tau^2)$, $\Omega\mid\theta \sim \mathcal{N}(\theta, \sigma^2)$: $C_\theta = 2\tau^2$, $L_{\text{lik}} = 1$, $4/\rho_{\text{noise}} = 4\sigma^2$, so $\max = \max(6\tau^2, 4\sigma^2)$.

- Structural: $C_{T_2}^{\text{(struct)}} \le L_{\text{post}}^2 \cdot \max(6\tau^2, 4\sigma^2)$.
- §C direct: $C_{T_2}^{\text{(direct)}} = 2L_{\text{post}}^2 \sigma^2$.

**Ratio $\ge \max(3\tau^2/\sigma^2, 2)$.** Looser by factor $\ge 2$ in noise-dominant regime, by $3\tau^2/\sigma^2$ in prior-dominant.

### 3.4 Why the structural route is structurally lossy

The §C calculation succeeds because the post-update parameter law is itself Gaussian: $\mu_+ \mid G = \mathcal{N}(L_{\text{post}}\beta(G),\,L_{\text{post}}^2\sigma^2)$, with $T_2$ read off directly from variance $L_{\text{post}}^2\sigma^2$. The Bayesian update *contracts*, and §C exploits this directly.

The structural route composes Lipschitz pushforwards. It never "sees" that the post-update law is *more concentrated* than the Lipschitz-pushforward bound admits. Two laws with the same Lipschitz pushforward map can produce post-update laws with different concentration; Lipschitz-composition bounds the worse one.

**This is the fundamental obstruction.** Composing Lipschitz constants is tight on Lipschitz-distance between distributions of pushforwards, but $T_2$ is about concentration of a single distribution, which can be tighter than Lipschitz-composition admits.

---

## 4. Strengthening attempt 3 — Bakry-Émery on posterior density (FAILS for the right object)

Hypothesis (S-i) in §B gives strong log-concavity of the *inside-posterior* on $\theta$ given $\omega$, with $K_{\text{eff}} = K_{\text{prior}} + K_{\text{lik}} = 1/\tau^2 + 1/\sigma^2$, hence $T_2(2L_{\text{post}}\sigma^2)$ on the inside-posterior (variance $\sigma_{\text{post}}^2 = L_{\text{post}}\sigma^2$).

But Track 1 needs $T_2$ on the *parameter law* — the law of $\mu_+ = L_{\text{post}}\Omega$ under $\omega$-randomness, with variance $L_{\text{post}}^2\sigma^2$. These differ by a factor of $L_{\text{post}}$. Bakry-Émery on the posterior density addresses the wrong object.

---

## 5. The honest landing — narrowed Theorem E.2

### 5.1 Recommended option — unbundled hypotheses + narrowed claim (c)

> **Theorem E.2 (revised).** *Suppose:*
>
> *(C0)* (Goal-induced parameter concentration.) $P_\theta := \theta_*P_G$ satisfies Talagrand $T_2(C_\theta)$ on parameter space.
>
> *(C1)* Class 1 architecture: $G \to \Omega_\tau \to M_{\tau^+}$ Markov chain conditional on $(e_\tau, M_{\tau^-})$.
>
> *(C2)* Deterministic Bayesian update: $M_{\tau^+} = \mu^{\Omega_\tau}$.
>
> *(C3)* Stuart-school Lipschitz posterior: $W_2(\mu^\Omega, \mu^{\Omega'}) \le L_{\text{post}}\|\Omega-\Omega'\|$ on supp $P_\Omega$.
>
> *(C4a)* Slice $T_2$: $P_{\Omega\mid\theta} \in T_2(2/\rho_{\text{noise}})$ for $P_\theta$-a.e. $\theta$.
>
> *(C4b)* Lipschitz-in-$\theta$ kernel: $W_2(P_{\Omega\mid\theta_1}, P_{\Omega\mid\theta_2}) \le L_{\text{lik}}\|\theta_1-\theta_2\|$.
>
> *Then:*
>
> *(a)* (H2′) holds with $C_{T_2} \le L_{\text{post}}^2\,\max\bigl((1+2L_{\text{lik}}^2)C_\theta,\;\;4/\rho_{\text{noise}}\bigr)$.
>
> *(b)* Track 1 yields $\mathbb{E}\,W_2^2(P_{M_{\tau^+}\mid G}, P_{M_{\tau^+}}) \le C_{T_2}\,I_M$.
>
> *(c)* The constant has the canonical Stuart-school form $\propto L_{\text{post}}^2/\rho_{\text{noise}}$ — recovering the cascade's order-of-magnitude scaling under Stuart-school hypotheses, with an absolute multiplicative overhead from the kernel-tensorization step. The tight canonical constant $2L_{\text{post}}^2/\rho_{\text{noise}}$ is recovered only on instances where the post-update parameter law is itself sub-Gaussian with variance $L_{\text{post}}^2/\rho_{\text{noise}}$ (e.g., conjugate-Gaussian and exponential-family-conjugate cases).

---

## 6. Failed routes — boundary mapping

**6.1 Direct $T_2$ on marginal $P_\Omega$:** Fails on canonical instance unless $\tau = 0$.

**6.2 Bakry-Émery on inside-posterior:** Wrong object (variance $L_{\text{post}}\sigma^2$, not parameter-law $L_{\text{post}}^2\sigma^2$).

**6.3 Single-step Lipschitz pushforward via deterministic $\theta \mapsto \Omega$:** Conditional kernel is random; Lemma A8.1 is the lift, paying the $1+2L_{\text{lik}}^2$ overhead.

**6.4 Direct LSI on $P_\Omega$ via convolution:** Gaussian + Gaussian gives $C_{T_2}(P_\Omega) = 2(\sigma^2+\tau^2)$, post-update $\le 2L_{\text{post}}^2(\sigma^2+\tau^2)$ — looser by factor $1+\tau^2/\sigma^2$.

**6.5 Conditional-density transport-tensorization (Djellout-Guillin-Wu, Bolley-Villani):** Equivalent shape with same overhead.

**6.6 Donsker-Varadhan dual:** Equivalent statement; no extra structure.

**Pattern:** every attempt to derive the canonical $2L_{\text{post}}^2/\rho_{\text{noise}}$ via *structural* composition fails at the same point — structural Lipschitz-composition is blind to the contraction benefit.

---

## 7. Bottom line

The Step-1 gap is real and structural. The strengthening pass succeeds at recovering the *cascade form* under cleanly-stated separable hypotheses (C0)+(C4a)+(C4b) via Lemma A8.1. The pass does *not* recover the *tight constant* — that's a conjugate-specific number from a direct sub-Gaussian read-off on the post-update parameter law.

Theorem E.2's claim (c) needs to narrow from "the canonical Stuart-school cascade constant — recovered ... generically" to "a constant of the canonical Stuart-school form $\propto L_{\text{post}}^2/\rho_{\text{noise}}$, recovered generically; the tight $2L_{\text{post}}^2/\rho_{\text{noise}}$ is recovered on conjugate-Gaussian and exponential-family-conjugate instances via direct sub-Gaussian read-off." Same shape, more honest.

**This is a partial strengthening, not a walk-back.** The structural-reduction theorem stands (with unbundled hypotheses and explicit overhead constant). The cascade form transfers across the full Strand-2 hypothesis space. What narrows is the *constant tightness* claim.

This finding sharpens the A7 spike's conclusions — Theorem A7.1' overclaims the constant in claim (c); the unbundled hypothesis set with multiplicative overhead is the corrected form.
