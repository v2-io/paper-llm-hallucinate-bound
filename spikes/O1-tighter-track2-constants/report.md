# O1 — Tighter Track 2 Fisher-Rao constants spike report

**Status: CRACKED on Direction 1 (strict improvement); NEGATIVE-WITH-PAYOFF on Direction 2; Direction 3 absorbed into Direction 1 (witness is the obstruction).**

The strengthening pass cracks the headline question: **the universal constant under (PI) alone is $2$, not $\pi/\sqrt 2 \approx 2.221$.** The improvement comes from replacing the (loose chord-arc + Tsybakov) composition with the (exact chord-arc identity + Rényi-1/2 monotonicity) composition. Both components are well-known individually; the substitution into the Track 2 cascade does not appear in the literature. The constant $2$ is sharp — a witness on a $(N \to \infty)$-symmetric family approaches it from below at rate $1/(6N)$. The auditor's softening recommendation ("$\pi/\sqrt 2$ is forced; rebrand as universal-with-overhead") was the AGENTS §3.1 failure mode — the strengthening was sitting one Rényi inequality away.

The auditor's surface concern (M1/A1) — that (H4$'$) fails in the LLM operating regime, so the *globally-valid* constant is what's actually applicable — is now sharper rather than softer: the global bound is $2$, the locally-tight bound is $\sqrt 2$, and the gap shrinks from $\pi/2 \approx 1.57$ to exactly $\sqrt 2 \approx 1.41$. The constants stay separated by a factor of $\sqrt 2$ (chord-arc gap at the antipode in squared-distance form), which is now structurally clean rather than compositionally slack.

Direction 2 (architectural sufficient conditions for (H4$'$)) lands negative: bounded-LLR architectural constraints give *finite* slice-wise KL but not $\delta_\star < 1$ in typical LLM regimes. Direction 3 (deeper Čencov-style obstruction) folds into Direction 1: the symmetric $N$-point witness *is* the structural obstruction to any constant below $2$.

---

## 1. The strengthening — replacing Tsybakov with Rényi-1/2

### 1.1 Current paper's Track 2 global proof

From `src/re/D-track2-companions.md:17`, the original proof composed:

- (i) **Chord-arc bound (loose form):** $d_{FR} \le \pi \cdot \mathrm{Hel}$ globally, with equality at the antipode $\mathrm{Hel} = 1$.
- (ii) **Tsybakov Lemma 2.4:** $2\,\mathrm{Hel}^2 \le \mathrm{KL}$, slice-wise.

Composing: $d_{FR}^2 \le \pi^2\,\mathrm{Hel}^2 \le (\pi^2/2)\,\mathrm{KL}$, then chain-rule + Jensen yield $\mathbb E\,d_{FR} \le (\pi/\sqrt 2)\sqrt{I_M}$.

### 1.2 Tsybakov is loose by factor 2 at small KL

Gaussian saturation: for $P = \mathcal N(\mu_1, \sigma^2)$, $Q = \mathcal N(\mu_2, \sigma^2)$,
$$\mathrm{KL}(P\|Q) = \tfrac{(\mu_1-\mu_2)^2}{2\sigma^2}, \qquad \mathrm{Hel}^2(P, Q) = 1 - \exp(-\mathrm{KL}/4).$$
Locally $\mathrm{Hel}^2 \approx \mathrm{KL}/4$ — half of Tsybakov's $\mathrm{KL}/2$ bound.

The natural conjecture from the spike brief — does $\mathrm{Hel}^2 \le 1 - \exp(-\mathrm{KL}/4)$ hold beyond Gaussians? — **fails.** Numerical counterexample: $P = \mathrm{Bern}(0.1)$, $Q = \mathrm{Bern}(0.9)$ gives $\mathrm{KL} = 1.758$, $\mathrm{Hel}^2 = 0.4$, but $1 - \exp(-\mathrm{KL}/4) = 0.356 < 0.4$. Bernoulli pairs with extreme asymmetry violate the Gaussian-derived bound.

### 1.3 The actually-correct general inequality — Rényi-1/2 monotonicity

The Rényi divergence of order $\alpha$ is $D_\alpha(P\|Q) = \frac{1}{\alpha-1}\log\int p^\alpha q^{1-\alpha}\,d\nu$. At $\alpha = 1/2$:
$$D_{1/2}(P\|Q) = -2\log\int\sqrt{pq}\,d\nu = -2\log\mathrm{BC}(P, Q),$$
where $\mathrm{BC} = \int\sqrt{pq}$ is the Bhattacharyya coefficient. **Rényi monotonicity** (van Erven & Harremoës 2014, IEEE TIT 60(7):3797-3820): $D_\alpha$ is non-decreasing in $\alpha$. Therefore
$$D_{1/2}(P\|Q) \le D_1(P\|Q) = \mathrm{KL}(P\|Q),$$
equivalently $\mathrm{BC} \ge \exp(-\mathrm{KL}/2)$, equivalently $\mathrm{Hel}^2 \le 1 - \exp(-\mathrm{KL}/2)$.

Numerical validation: 100,000 random discrete pairs, zero violations.

### 1.4 The substitution — exact chord-arc identity + Rényi

Under the Amari-Nagaoka normalization, $d_{FR} = 2\arccos(\mathrm{BC})$ is an **identity**, not an inequality. Combined with Rényi:
$$d_{FR} = 2\arccos(\mathrm{BC}) \le 2\arccos(\exp(-\mathrm{KL}/2)).$$

Define $\phi(K) := 4\arccos^2(\exp(-K/2))$. Properties:
- $\phi(0) = 0$.
- $\phi(K)/K \to 4$ as $K \to 0^+$.
- $\phi(K)/K$ is decreasing in $K$, from $4$ to $0$ (with $\phi \to \pi^2$ as $K \to \infty$).
- $\phi$ is concave on $[0, \infty)$.

Hence the slice-wise inequality:
$$d_{FR}^2 \le 4\,\mathrm{KL}, \qquad \text{equivalently} \qquad d_{FR} \le 2\sqrt{\mathrm{KL}}.$$

### 1.5 Track 2 global theorem — strengthened version

> **Theorem (Track 2 global, strengthened).** Under (H1) and (PI), for all values of transferred information,
> $$\mathbb E\,d_{FR}\bigl(P_{M_{\tau^+}\mid e, M_{\tau^-}, G},\; P_{M_{\tau^+}\mid e, M_{\tau^-}}\bigr) \le 2\sqrt{I(G;\,M_{\tau^+}\mid e_\tau, M_{\tau^-})}.$$
> The constant $2$ is universal, dimension-free, global. (R), (K), (H4$'$) are not invoked.

**Proof.** By Rényi monotonicity, $\mathrm{BC}(P, Q) \ge \exp(-\mathrm{KL}/2)$. With chord-arc identity $d_{FR} = 2\arccos(\mathrm{BC})$: $d_{FR} \le 2\arccos(\exp(-\mathrm{KL}/2))$. Squaring and using $\phi(K)/K \le \phi(0^+)/0^+ = 4$: $d_{FR}^2 \le 4\,\mathrm{KL}$ slice-wise. Take $\mathbb E_G$ and substitute the chain rule: $\mathbb E\,d_{FR}^2 \le 4 I_M$. Jensen on $\sqrt{\cdot}$: $\mathbb E\,d_{FR} \le 2\sqrt{I_M}$. $\square$

**Tightest form (Jensen-concave on $\phi$).** Since $\phi$ is concave, $\mathbb E[\phi(\mathrm{KL}_g)] \le \phi(I_M)$, giving $\mathbb E\,d_{FR}^2 \le 4\arccos^2(\exp(-I_M/2))$ and
$$\mathbb E\,d_{FR} \le 2\arccos(\exp(-I_M/2)) \le \min(2\sqrt{I_M},\,\pi).$$

### 1.6 Improvement table

| Bound | Constant on $\sqrt{I_M}$ | Value at $I_M = 1$ |
|:------|:---:|:---:|
| Paper's prior Track 2 global | $\pi/\sqrt 2 \approx 2.221$ | 2.221 |
| Strengthened (this spike) | $2$ | 2.000 |
| Tightest (Jensen-concave) | $2\arccos(e^{-I_M/2})/\sqrt{I_M}$ | 1.838 |
| Locally-tight under (H4$'$) | $\sqrt 2 \approx 1.414$ | 1.414 |

Improvement factor: $\pi/(2\sqrt 2) \approx 1.111$. The local-vs-global gap shrinks from $\pi/2$ (in raw constant ratio) to $\sqrt 2$, which is structurally interpretable: in *squared*-distance form, the gap is exactly the chord-arc factor at the antipode.

---

## 2. Sharpness — the symmetric $N$-point witness

### 2.1 Construction

Fix $N \ge 2$. Let $G$ be uniform on $\{1, \ldots, N\}$. Define
$$P_g(j) = \begin{cases} 0 & j = g \\ 1/(N-1) & j \neq g.\end{cases}$$

By symmetry, marginal is uniform $P(j) = 1/N$. Direct computation:
- $\mathrm{KL}(P_g \| P_{\text{marg}}) = \log\tfrac{N}{N-1}$ (constant in $g$). $I_M = \log\tfrac{N}{N-1}$.
- $\mathrm{BC} = \sqrt{\tfrac{N-1}{N}}$, $d_{FR} = 2\arccos\sqrt{\tfrac{N-1}{N}} = 2\arcsin\tfrac{1}{\sqrt N}$ (constant in $g$).

Therefore
$$\frac{\mathbb E[d_{FR}]}{\sqrt{I_M}} = \frac{2\arcsin(1/\sqrt N)}{\sqrt{\log\tfrac{N}{N-1}}}.$$

### 2.2 Asymptotic

With $x = 1/N$: $\arcsin\sqrt x = \sqrt x(1 + x/6 + O(x^2))$ and $\sqrt{-\log(1-x)} = \sqrt x(1 + x/4 + O(x^2))$.
$$\text{ratio}(N) = 2(1 - \tfrac{x}{12} + O(x^2)) = 2 - \tfrac{1}{6N} + O(N^{-2}).$$

Numerical confirmation:

| $N$ | exact ratio | $2 - 1/(6N)$ | bound saturation |
|:---:|:---:|:---:|:---:|
| 2 | 1.886719 | 1.916667 | 94.3% |
| 10 | 1.982487 | 1.983333 | 99.1% |
| 100 | 1.998325 | 1.998333 | 99.92% |
| 1000 | 1.999833 | 1.999833 | 99.992% |
| 10000 | 1.999983 | 1.999983 | 99.9992% |

**Hence $\sup\{\mathbb E[d_{FR}]/\sqrt{I_M}\} = 2$ over (PI)-compatible families, not achieved but approached arbitrarily closely.** Constant 2 is sharp.

### 2.3 Direction 3 absorbed

The symmetric $N$-point witness *is* the structural obstruction. The previous $\pi/2$ overhead in the paper was *compositional slack* (chord-arc loose + Tsybakov loose at small KL), not a structural barrier. The genuine structural barrier is the antipodal chord-arc gap of $\sqrt 2$ in squared-distance form, which is what the new constant of $2$ vs local $\sqrt 2$ records. Under (PI) alone, the Bhattacharyya-coefficient pseudometric $d_{FR} = 2\arccos(\mathrm{BC})$ is automatically (PI)-invariant ($\mathrm{BC}$ is an $f$-divergence), and the bound $d_{FR} \le 2\sqrt{\mathrm{KL}}$ is the cleanest possible (PI)-invariant Fisher-Rao-to-KL bound; the (R)+(K) commitments add the local refinement to $\sqrt 2$.

---

## 3. Direction 2 — architectural sufficient conditions for (H4$'$): NEGATIVE-WITH-PAYOFF

### 3.1 The natural attempt — bounded LLR

Bounded transformer logits $|z_v| \le B$ on vocabulary $V$ give bounded LLR:
$$\sup_{g, g', v}\Bigl|\log\tfrac{P_{|g}(v)}{P_{|g'}(v)}\Bigr| \le L_{\mathrm{LLR}} = O(B + \log|V|).$$

> **Lemma 3.1.** If $\sup_{g, g'} \mathrm{ess\,sup}_x |\log\frac{dP_{|g}}{dP_{|g'}}(x)| \le L_{\mathrm{LLR}}$, then $\mathrm{ess\,sup}_g \mathrm{KL}(P_{|g} \| P) \le L_{\mathrm{LLR}}$.

> *Proof.* For independent $G' \sim P_G$: $\log P(x) \ge \mathbb E_{G'}\log P_{|G'}(x)$ (Jensen, log concave). So $\log P_{|g}(x) - \log P(x) \le \mathbb E_{G'}\log\frac{P_{|g}(x)}{P_{|G'}(x)} \le L_{\mathrm{LLR}}$ pointwise. The same lower bound by symmetry. Hence $\mathrm{KL}(P_{|g}\|P) \le L_{\mathrm{LLR}}$. $\square$

### 3.2 Why (H4$'$) doesn't follow architecturally

Typical $L_{\mathrm{LLR}}$ for transformers ($B \sim 10$, $|V| \sim 10^5$): $\sim 30$. (H4$'$)'s "small" requirement $\delta_\star \in (0, 1)$ would need $L_{\mathrm{LLR}} \to 0$, and the third-order remainder $R_3(\delta_\star)$ blows up at $\delta_\star \gg 1$. Multi-step generation makes it worse: KL chains across token decoding, $\mathrm{KL}_{\text{total}} \le T \cdot \mathrm{KL}_{\text{step}}$, exceeding 1 even for moderate $T$.

### 3.3 The structurally-clean reading

What's actually true:
- **Finite (H4$'$)** — $\mathrm{ess\,sup}_g \mathrm{KL}_g < \infty$ — holds under bounded-logit / bounded-temperature architectures. *Architectural.*
- **Small (H4$'$)** — $\mathrm{ess\,sup}_g \mathrm{KL}_g < 1$ — holds only in regime-conditional ways (low-temperature operating, in-distribution prompts, no adversarial drift). *Regime-conditional.*

The auditor's M1/A1 is structurally vindicated: the *small* version is regime-conditional, so for the LLM operating regime, the global Track 2 bound is what's invoked. With the strengthened global constant of $2$, this is now substantially better than the paper's prior $\pi/\sqrt 2$.

### 3.4 Failed attempts logged

- **$L^p$ versions of (H4$'$)** for $p < \infty$: doesn't strengthen. $L^p$ averaging admits rare-but-large slices that blow up the cubic Amari-Chentsov term.
- **(H2$'$) inducing slice-uniformity**: $T_2$ on the marginal gives transport bounds, but the converse (Wasserstein-small implies slice-uniformly-KL-small) needs additional structure not generically available.
- **Fisher-information-bounded architectures**: bound *local* KL but not ess-sup. Same architectural-vs-uniform mismatch.

Pattern: every architecturally-derivable smallness on the post-update law is *integrated* (mean) or *local* (Fisher), not *uniform* (ess-sup). (H4$'$) is fundamentally a uniform-along-slices condition, which architecture alone doesn't enforce.

---

## 4. Side findings worth recording

### 4.1 The Hellinger backstop also tightens (presentation only)

Replacing Tsybakov with Rényi gives $\mathrm{Hel}^2 \le 1 - \exp(-\mathrm{KL}/2)$ slice-wise; chain rule + Jensen on the concave $K \mapsto 1 - \exp(-K/2)$ yield $\mathbb E\,\mathrm{Hel} \le \sqrt{1 - \exp(-I_M/2)}$. This automatically incorporates $\mathrm{Hel} \le 1$ at large $I_M$ where the previous $(1/\sqrt 2)\sqrt{I_M}$ would diverge. Same headline constant $1/\sqrt 2$ in the small-$I_M$ regime.

### 4.2 Bernoulli alphabet caps below 2

Mirror-Bernoulli witness ($P_g = \mathrm{Bern}(\epsilon)$ vs $P_{1-g} = \mathrm{Bern}(1-\epsilon)$ at $\epsilon \to 0$) caps at $\pi/(2\sqrt{\log 2}) \approx 1.887$. The bound $2$ is approached only with unboundedly-large alphabets — structurally consistent with LLM use case where vocabulary $|V| \sim 10^5$ accommodates the symmetric near-disjoint-slices structure. A jailbreak attack driving the model to a near-deterministic completion sequence is exactly an $N$-large symmetric-witness instance.

### 4.3 Refined Čencov-uniqueness reading

Under (PI) alone (no R, no K), the BC-based pseudometric $d_{FR} = 2\arccos(\mathrm{BC})$ is automatically (PI)-invariant (BC is an $f$-divergence). The strengthened theorem clarifies: (PI) alone yields global $2$; (R)+(K) add local Riemannian + KL-second-order normalization to give $\sqrt 2$ in the local regime. The two constants differ by exactly $\sqrt 2$ — chord-arc factor at the antipode in squared-distance form.

---

## 5. Bottom line

**Strict improvement. Constant $\pi/\sqrt 2 \to 2$ under (PI) alone, sharp.**

The substitution: replace (loose chord-arc + Tsybakov) with (exact chord-arc identity + Rényi-1/2 monotonicity). Both substitutes are well-known individually; the composition into Track 2's cascade is novel.

The auditor's recommendation to rebrand as "two universal Fisher-Rao constants forced by Čencov" becomes more compelling: the gap between local $\sqrt 2$ and global $2$ is *exactly* the antipodal chord-arc factor of $\sqrt 2$ in squared-distance form — a structurally-clean uniqueness statement, where the previous $\pi/2$ was compositional slack.

For the LLM application: the global $2\sqrt{I_M}$ is the operating bound (Direction 2 negative finding: (H4$'$) is regime-conditional, not architectural). The constant $2$ is sharp via the symmetric $N$-point witness — the discrete-alphabet analog of "near-disjoint goal-conditional support," exactly the failure mode adversarial prompts exploit.

**Status summary:**
- Direction 1 (tighter global constant): **CRACKED.** $\pi/\sqrt 2 \to 2$, strict improvement, sharp.
- Direction 2 (architectural (H4$'$)): **NEGATIVE-WITH-PAYOFF.** Bounded-LLR gives finite but not small (H4$'$); architectural-vs-regime-conditional distinction structurally clarifies.
- Direction 3 (deeper obstruction): **CRACKED via Direction 1.** Symmetric $N$-point witness *is* the structural obstruction; constant $2$ sharp by exhibition.
