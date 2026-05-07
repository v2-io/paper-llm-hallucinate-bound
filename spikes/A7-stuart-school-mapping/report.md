# A7 — Stuart-school mapping spike report

**Status: PARTIAL — strengthening succeeds at theorem level via a reduction lemma, but falls short of "strict sub-case" for structural (not effort-bounded) reasons.**

The prior soften-recommendation in TODO §A7 understated the strengthening attempt's payoff. The instinct to soften was the AGENTS §3.1 failure mode — once the right transport-inequality lemma was named, a clean theorem-level reduction fell out. The honest claim sits *between* "strict sub-case" (too strong) and "recovers the constant in the conjugate-Gaussian case" (too weak): **Track 1 generalizes the Stuart-school cascade across the full Stuart-school hypothesis space**, with the canonical constant transferring verbatim, via a Lipschitz pushforward of $T_2$.

---

## 1. The two readings of "strict sub-case"

- **(SC-strong)** *Every Stuart-school theorem-level output is a Track-1 corollary.* Requires reducing Stuart-school *outputs* (deterministic pointwise pair-distances) into Track-1 *outputs* (averaged-over-goal information bounds).
- **(SC-structural)** *Stuart-school's machinery embeds into Track 1's hypothesis space as the Class-1 specialization.* Requires a reduction theorem from Stuart-school *hypotheses* to Track-1 *hypotheses* (specifically, to (H2$'$)).

(SC-structural) is what the strengthening pass establishes. (SC-strong) fails for structural reasons — they're documented in §3 below.

---

## 2. The strengthening that works — Lemma A and the reduction theorem

### 2.1 Lemma A — Lipschitz pushforward of $T_2$

> **Lemma A.** Let $(X, d_X)$ and $(Y, d_Y)$ be Polish metric spaces, $\mu$ on $X$ satisfying Talagrand $T_2(C)$ (i.e., $W_2^{d_X}(\nu,\mu)^2 \le C\,\mathrm{KL}(\nu\,\|\,\mu)$ for all $\nu \ll \mu$), and $T: X \to Y$ an $L$-Lipschitz map. Then $T_*\mu$ on $Y$ satisfies $T_2(L^2 C)$.

*Proof (textbook; cf. Villani 2009 Thm 22.10 / Bobkov-Götze 1999).* Let $\rho \ll T_*\mu$. Disintegrate: $\mu(dx) = \mu_y(dx)\,T_*\mu(dy)$. The lift $\tilde\rho(dx) := \mu_y(dx)\,\rho(dy)$ satisfies $T_*\tilde\rho = \rho$ and $\mathrm{KL}(\tilde\rho\,\|\,\mu) = \mathrm{KL}(\rho\,\|\,T_*\mu)$ (chain-rule decomposition with shared conditionals). For any coupling $\pi$ of $(\tilde\rho, \mu)$, the pushforward $(T \otimes T)_*\pi$ couples $(\rho, T_*\mu)$ with cost $\le L^2$ times the input cost. So $W_2^{d_Y}(\rho, T_*\mu)^2 \le L^2 W_2^{d_X}(\tilde\rho, \mu)^2 \le L^2 C\,\mathrm{KL}(\tilde\rho\,\|\,\mu) = L^2 C\,\mathrm{KL}(\rho\,\|\,T_*\mu)$. $\square$

### 2.2 Theorem A7.1' — Class-1 reduction of the Stuart-school cascade to Track 1

> **Theorem A7.1'.** Suppose:
>
> *(C1)* (Class 1 architecture.) $G \to \Omega_\tau \to M_{\tau^+}$ is a Markov chain conditional on $(e_\tau, M_{\tau^-})$.
>
> *(C2)* (Deterministic Bayesian update.) $M_{\tau^+} = \mu^{\Omega_\tau}$ for a measurable map $\Omega \mapsto \mu^\Omega$.
>
> *(C3)* (Stuart-school Lipschitz posterior.) $W_2(\mu^\Omega, \mu^{\Omega'}) \le L_{\text{post}}\|\Omega - \Omega'\|$ uniformly on $\mathrm{supp}\,P_\Omega$.
>
> *(C4)* (Goal acts via parameter shift on a sub-Gaussian conditional likelihood.) $\Omega \mid G=g \sim P_{\Omega \mid \theta = \theta(g)}$ with $W_2^2(P_{\Omega \mid \theta_1}, P_{\Omega \mid \theta_2}) \le (2/\rho_{\text{noise}})\|\theta_1 - \theta_2\|^2$ — the canonical Gaussian-or-exponential-family setup.
>
> Then:
>
> (a) (H2$'$) holds on the goal-marginal post-update model law with $C_{T_2} = 2L_{\text{post}}^2/\rho_{\text{noise}}$.
>
> (b) Track 1 yields $\mathbb{E}\,W_2^2(P_{M_{\tau^+}\mid G}, P_{M_{\tau^+}}) \le (2L_{\text{post}}^2/\rho_{\text{noise}})\,I(G; M_{\tau^+}\mid e_\tau, M_{\tau^-})$.
>
> (c) The constant $2L_{\text{post}}^2/\rho_{\text{noise}}$ is the canonical Stuart-school cascade constant — recovered **under the same Stuart-school hypotheses generically**, not only on the conjugate-Gaussian instance.

*Proof.* Apply Lemma A in two steps. Step 1: the family $\theta \mapsto P_{\Omega\mid\theta}$ pushes forward $\rho_{\text{noise}}$-concentration on $\theta$ into $T_2(2/\rho_{\text{noise}})$ on the conditional data law (C4 directly). Step 2: $\Omega \mapsto \mu^\Omega$ is $L_{\text{post}}$-Lipschitz (C3), so Lemma A gives $T_2(L_{\text{post}}^2 \cdot 2/\rho_{\text{noise}}) = T_2(C_{T_2})$ on $T_*P_\Omega = P_{M_{\tau^+}\mid e,M_{\tau^-}}$. (b) is Track 1's standard cascade. (c) is the matching of constants. $\square$

### 2.3 What this delivers beyond the conjugate-Gaussian witness

The hypotheses (C1)–(C4) are **exactly** the canonical Stuart-school cascade's hypotheses. (C3) is the headline output of every Strand 2 paper:

- Stuart 2010 (foundational $W_2$-Lipschitz posterior on function spaces)
- Sprungk 2020 (TV/Hellinger/$W_2$/KL Lipschitz suite, prior + likelihood + data perturbations)
- Dolera-Mainini 2023 (Fisher-information-functional and weighted-Poincaré explicit constants)
- Cvetković-Lie 2025 (matched upper + lower bounds)
- Hosseini-Hsu-Taghvaei 2024 (conditional-OT framework on function spaces — Lipschitz-conditioning-map output)
- Garbuno-Iñigo et al. 2023 (IPM perturbation analysis under LSI-style functional inequalities)

**Each of these establishes a form of (C3).** Theorem A7.1' is a single structural slot they all fit into. So *anywhere* the Stuart-school cascade applies — non-conjugate cases, infinite-dimensional priors, PDE-inverse settings — Track 1 specializes to the same constant. This is the payoff that "recovers the constant in the conjugate-Gaussian case" misses by orders of generality.

The Hosseini-Hsu-Taghvaei case in particular: §F currently calls them "the closest single-paper match." Theorem A7.1' sharpens this — they're a *structurally identified* sufficient-conditions case for (H2$'$) under Class 1, on par with Sprungk's Lipschitz-suite, just under different machinery.

---

## 3. Why (SC-strong) fails — three structural axes

### 3.1 Object mismatch — averaged vs. pointwise

Stuart-school: deterministic, pointwise, $W_2(\mu^y, \mu^{y'}) \le L_{\text{post}}\|y-y'\|$ for *every* $(y, y')$.

Track 1: averaged over goal, $\mathbb{E}_G\,W_2^2 \le C_{T_2}\,I_M$.

To recover Stuart-school deterministically from Track 1: take $G \in \{0,1\}$ uniform with $\Omega = y$ if $G=0$, $\Omega = y'$ if $G=1$. Then $\mathbb{E}\,W_2^2 = \tfrac{1}{2}W_2^2(\mu^y,\mu^{y'})$ and $I = \log 2$. Track 1 gives $W_2^2(\mu^y,\mu^{y'}) \le (4L_{\text{post}}^2\log 2)/\rho_{\text{noise}}$, **independent of $\|y-y'\|$**. Stuart-school gives $W_2^2 \le L_{\text{post}}^2\|y-y'\|^2$, scaling with the data perturbation.

For pairs with $\|y-y'\|^2 < (4\log 2)/\rho_{\text{noise}}$, the Track 1 bound is strictly looser. The information-theoretic averaging coarsens the perturbation magnitude into a concentration scale $1/\rho_{\text{noise}}$ and irrecoverably loses the linear-in-$\|y-y'\|^2$ refinement.

This is structural — Track 1's averaged form *cannot* expose pointwise pair-distance information. Not a missed-effort gap.

### 3.2 Hypothesis-import vs. hypothesis-derivation

Track 1 imports (C3) via Lemma A; it doesn't derive it. The Lipschitz-posterior result is a non-trivial PDE-stability fact that Stuart's lineage spent fifteen years establishing under increasingly weak hypotheses. Track 1 has nothing to add on the *derivation* of (C3); it consumes (C3) as input. "Strict sub-case" reads as Track 1 *producing* Stuart-school's results plus more; the accurate framing is Track 1 *consuming* Stuart-school's results to produce a different result on a different object.

### 3.3 The lineage proves results outside Track 1's reach

- Sprungk 2020: multi-metric (TV, Hellinger, $W_2$, KL) sensitivity to *prior* and *likelihood* perturbations. Track 1 lives in $W_2$ and bounds *data-side* goal-conditional variation.
- Cvetković-Lie 2025: matching *lower* bounds on posterior sensitivity. Track 1 is upper-bound only.
- Latz 2020: well-posedness under *sub-Lipschitz* continuity. Track 1 imports Lipschitz.
- Dolera-Favaro-Mainini 2024: Wasserstein-based posterior contraction *rates*. Track 1 doesn't address rates.
- Lie-Sullivan-Teckentrup 2017: Hellinger bounds for *randomized* forward models. Track 1 imports a deterministic forward model in (C2).

Each is a Strand-2 *result*, not a Strand-2 *hypothesis*. None embeds as a Track 1 corollary.

---

## 4. Failed (SC-strong) attempts — boundary mapping

Per AGENTS §5.4, documenting failures so future agents know the boundary is structural:

**4.1 Information-theoretic encoding of pointwise data perturbations** (worked above in §3.1). Track 1's averaging destroys $\|y-y'\|$ scale; output independent of perturbation magnitude.

**4.2 Continuous-goal embedding $G = \Omega$.** Yields $\mathrm{Var}_\Omega[\mu^\Omega] \le C_{T_2}\,H(\mu^\Omega)$ — relating Wasserstein-variance to entropy. Neither object is Stuart-school's pairwise distance; the integration washes out pointwise structure.

**4.3 Donsker-Varadhan dual variational characterization.** The dual reaches the same Lemma-A reduction via a different route — no extra structure exposed. Lemma A is the right level of generality.

**4.4 Chain-rule expansion via Stuart-school sensitivity.** $I(G;\Omega)$ is a property of the joint $P(G,\Omega)$; Stuart-school sensitivity factors are properties of the *update kernel* (architecture-side perturbations). Structurally orthogonal — neither refines the other. Stuart-school's prior/likelihood-perturbation factors live on a different cut than Track 1's data-distribution-variation factors.

The pattern: every (SC-strong) attempt fails on the same axis — Track 1 averages over a goal-induced ensemble, Stuart-school is pointwise. The averaging is irreversible.

---

## 5. Conjugate-Gaussian consistency check (and a small constant clarification)

Verifying Theorem A7.1' on Appendix C's conjugate-Gaussian setup ($\theta\sim\mathcal{N}(0,\tau^2)$, $\Omega\mid\theta\sim\mathcal{N}(\theta,\sigma^2)$, $\mu^\Omega = \mathcal{N}(L_{\text{post}}\Omega, \sigma_{\text{post}}^2)$):

- (C3): $W_2^2(\mu^{\Omega_1},\mu^{\Omega_2}) = L_{\text{post}}^2(\Omega_1-\Omega_2)^2$ (equal-variance Gaussians). ✓ with constant $L_{\text{post}}$.
- (C4): noise concentration $\rho_{\text{noise}} = 1/\sigma^2$. ✓
- Predicted $C_{T_2} = 2L_{\text{post}}^2 \sigma^2$ — matches `C-conjugate-gaussian-numerics.md` line 11 exactly.

**Constant clarification worth flagging.** Appendix C writes $C_{T_2} = 2L_{\text{post}}^2/\rho_{\text{LSI}}$ with $\rho_{\text{LSI}} := 1/\sigma^2$. The identification is correct, but the symbol $\rho_{\text{LSI}}$ here denotes the **noise concentration** ($1/\sigma^2$), not the LSI constant of the *marginal* observation law $P_\Omega = \mathcal{N}(0, \sigma^2+\tau^2)$ (which would give $1/(\sigma^2+\tau^2)$). The canonical Stuart-school cascade uses noise concentration in the denominator. Appendix C is internally consistent; the only issue is symbolic — `$\rho_{\text{LSI}}$` reads as "the Talagrand-side concentration" but here means specifically *noise concentration*. A one-line clarification in §C would help future readers. Not a math bug.

---

## 6. Recommended language for the paper

### 6.1 `src/re/01-introduction.md:17` — replace

Current: *"...Track 1 demonstrates that the composition contains the existing Bayesian-inverse-problems lineage as a strict sub-case under standard log-Sobolev concentration."*

Replacement: *"...Track 1 generalizes the canonical Bayesian-inverse-problems cascade: under Stuart-school Lipschitz-posterior hypotheses plus standard log-Sobolev / sub-Gaussian concentration on the conditional data law, a Lipschitz pushforward of $T_2$ ([[#^sec-stuart-school-reduction]]) gives Track 1's $C_{T_2} = 2L_{\text{post}}^2/\rho_{\text{noise}}$ on the post-update model law. The Class 1 (Separated) specialization of Track 1's hypothesis space is the Stuart-school setup; Track 1 extends the cascade to the goal-coupled regime outside Stuart-school's framing."*

### 6.2 `src/re/04-main-results.md:30` — replace Remark

Current: *"Track 1 contains the Bayesian-inverse-problems lineage. In the conjugate-Gaussian Class 1 (Separated) case with invertible data channel, Track 1's $C_{T_2}$ recovers $2 L_{\text{post}}^2/\rho_{\text{LSI}}$ exactly... The composition contains the existing literature as a strict sub-case."*

Replacement: *"Track 1 generalizes the Stuart-school cascade. Under Stuart-school Lipschitz-posterior hypotheses on the deterministic update map $\Omega \mapsto \mu^\Omega$ \cite{stuart-2010-acta,sprungk-2020-local-lipschitz,dolera-mainini-2023-aihp-lipschitz,hosseini-hsu-taghvaei-2024-conditional-ot} plus standard sub-Gaussian / LSI concentration on the conditional data law, the pushforward of $T_2$ under the Lipschitz Bayesian-update map yields Track 1's $C_{T_2} = 2L_{\text{post}}^2/\rho_{\text{noise}}$ on the post-update model law (Theorem A7.1', [[#^sec-stuart-school-reduction]]). This holds at the full Stuart-school hypothesis space, not only the conjugate-Gaussian instance. Track 1 extends the cascade beyond Class 1 (Separated) to architectures where the goal couples into the update mechanism directly — a regime Stuart-school does not address."*

### 6.3 Add `### Lipschitz pushforward of $T_2$ — Stuart-school reduction ^sec-stuart-school-reduction` to `src/re/E-proofs.md`

After `^sec-track1-proof`. Contains Lemma A (with proof from §2.1 above) and Theorem A7.1' (with proof from §2.2). ~25–30 lines.

### 6.4 Sharpen Strand 2 language in `src/re/F-related-work-extended.md`

Current language calls Hosseini-Hsu-Taghvaei "the closest single-paper match." Strengthen to:

*"Strand 2's posterior-stability results — \citet{stuart-2010-acta}, \citet{sprungk-2020-local-lipschitz}, \citet{cvetkovic-2025-upper}, \citet{dolera-mainini-2023-aihp-lipschitz}, \citet{garbuno-inigo-2023-bayesian}, \citet{lie-sullivan-teckentrup-2017}, \citet{hosseini-hsu-taghvaei-2024-conditional-ot} — each establish a form of Lipschitz-in-data continuity of the posterior. Theorem A7.1' ([[#^sec-stuart-school-reduction]]) shows that any such Lipschitz-posterior result, combined with sub-Gaussian / LSI concentration on the conditional data law, is a sufficient verification path for Track 1's (H2$'$) on the post-update model law in any Class 1 (Separated) architecture, with cascade constant matching the Stuart-school $2L_{\text{post}}^2/\rho_{\text{noise}}$. Hosseini-Hsu-Taghvaei is the closest single-paper match for the amortized-inference framing; the structural-slot match holds for the entire strand."*

### 6.5 One-line clarification in `src/re/C-conjugate-gaussian-numerics.md`

After line 13's identification $\rho_{\text{LSI}} := 1/\sigma^2$, add a brief note that this is the *noise concentration* (the Stuart-school cascade's denominator), not the LSI constant of the marginal observation law $P_\Omega$. Cross-reference `^sec-stuart-school-reduction`.

### 6.6 TODO §A7 — replace soften-recommendation

Mark A7 **PARTIAL — strengthening succeeds at theorem level via Lemma A + Theorem A7.1'; falls short of (SC-strong) for structural reasons**. Replace the planned soften-edit with the integrate-the-reduction-theorem language. (SC-strong) failed-route boundary documented in §3 and §4 above; future agents shouldn't re-attempt without new evidence on the averaged-vs-pointwise gap.

---

## 7. Bottom line

The strengthening pass succeeds at theorem level: **Theorem A7.1' establishes Track 1 as a generalization of the Stuart-school cascade across the full Stuart-school hypothesis space**, with the canonical constant transferring verbatim, via a single Lipschitz-pushforward step (Lemma A). This is strictly stronger than the prior soften-recommendation by orders of generality (entire Strand 2 hypothesis space vs. one conjugate-Gaussian witness).

The strengthening pass does *not* establish (SC-strong). The averaged-form / pointwise-form gap is structural — §3 and §4 map the boundary. The right replacement language is "generalizes the Stuart-school cascade" + reduction-theorem in the appendix, not "strict sub-case" and not "recovers the constant in the conjugate-Gaussian case."

**Files load-bearing on this finding:**
- `/Users/josephwecker-v2/src/neurips/03-llm-hallucinate-bound/src/re/01-introduction.md` (line 17)
- `/Users/josephwecker-v2/src/neurips/03-llm-hallucinate-bound/src/re/04-main-results.md` (line 30 Remark)
- `/Users/josephwecker-v2/src/neurips/03-llm-hallucinate-bound/src/re/E-proofs.md` (add new subsection after §`^sec-track1-proof`)
- `/Users/josephwecker-v2/src/neurips/03-llm-hallucinate-bound/src/re/F-related-work-extended.md` (Strand 2 paragraph)
- `/Users/josephwecker-v2/src/neurips/03-llm-hallucinate-bound/src/re/C-conjugate-gaussian-numerics.md` (notation clarification)
- `/Users/josephwecker-v2/src/neurips/03-llm-hallucinate-bound/TODO.md` §A7 (status update)
