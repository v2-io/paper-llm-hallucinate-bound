# De novo audit — 2026-05-07 (Opus 4.7, evening)

*First-hand read of all 12 segments + bib + PDF render. No prior-audit consultation. Auditor: Claude Opus 4.7 (1M).*

Rendered length: **10 pages of main body** (title/abstract + §1–§6, refs start p.11). NeurIPS 9-page main-text budget — paper is **~1 page over**. Page distribution:

| § | Page span | Notes |
|---|---|---|
| Title + abstract | p.1 | Abstract is unusually dense — packs 4 distinct results |
| §1 Introduction | p.1–p.2 | Substantial; 4 contribution items duplicate spine |
| §2 Related Work | p.3 | ~1 page; tight |
| §3 Setup | p.4–p.5 | Class-3 lemma is heavy for a Setup section |
| §4 Main Results | p.6–p.8 | Three theorems + remarks; well-structured |
| §5 Mechanism | p.9 | Compact |
| §6 Conclusion | p.10 | Single page; could absorb compression |

---

## Severity 1 — must-fix before submission

### 1.1 Missing bib entry: `lie-sullivan-teckentrup-2017`

**Tested.** Used twice in source (`F-related-work-extended.md:13`, `E-proofs.md:68`) but absent from `llm-hallucinate-neurips-2026.extracted.bib`. Bibtex doesn't warn (since the key is referenced through `\citet`, missing keys produce `?` in the rendered output). Run `grep '?' .build/.../llm-hallucinate-neurips-2026.bbl` to confirm. **Action:** `bin/refs add lie-sullivan-teckentrup-2017` and re-emit.

### 1.2 Free-floating author-year citation in §F.5

**Tested.** Line 33 of `F-related-work-extended.md`: *"Su-Kempe-Ullrich 2024 address jailbreaking from a statistical perspective"* — no `\cite{}` wrapper, no bib entry. Will display as plain prose, not as a numbered citation, breaking the bracketed-superscript style consistency. **Action:** add bibkey `su-kempe-ullrich-2024` and migrate to `\citet{...}`, or remove the reference.

### 1.3 Doubled parentheses in §3 rendered output

**Tested.** Page 4 of PDF renders *"The bound's architectural-corollary form ((2)) factors..."*. Source `03-setup.md:27` has `([[#^eq-arch-corollary-informal]])`; the build pipeline maps `[[#^eq-...]]` → `\eqref{...}` which auto-adds parens, so source-side parens compound. **Action:** drop the parens in source (`[[#^eq-arch-corollary-informal]] factors...`), or convert to `\Cref{eq-...}` on this one line.

### 1.4 Three bib entries with empty `journal` fields

`cvetkovic-2025-upper`, `zeng-2026-halluguard`, `biau-2026-note` produce bibtex `Warning--empty journal` and will render with no venue. These are 2025/2026 papers; verify whether they're preprints (use `@misc` with `howpublished`) or have venues. Check the entries' `bibsource` — `cvetkovic-2025-upper` has a JFA-style title, likely arXiv-only. **Action:** verify and either fill `journal`/`booktitle` or change entry type to `@misc`.

---

## Severity 2 — substantive concerns the math should address

### 2.1 Stuart-school reduction (Theorem E.2): Step 1 of the proof has a structural gap

**Hypothesis (high confidence after careful reading).** The proof in `E-proofs.md` lines 59–66:

> *Step 1.* The conditional-data-law family $\theta \mapsto P_{\Omega\mid\theta}$ pushes forward $\rho_{\text{noise}}$-concentration on $\theta$ into $T_2(2/\rho_{\text{noise}})$ on the conditional data law (C4 directly).

This phrasing conflates two things. (C4) gives Lipschitz-in-$\theta$ for the conditional-likelihood family; that does *not*, on its own, yield a $T_2$ inequality on the marginal observation law $P_\Omega$. To apply Lemma E.1 (Lipschitz pushforward of $T_2$) we need a measure $\mu$ that already satisfies $T_2$, and a Lipschitz map $T$. Here the candidate $\mu$ is the goal-induced parameter measure $P_\theta$ (i.e., pushforward of $P_G$ under $\theta(\cdot)$), and $T$ is $\theta \mapsto P_{\Omega|\theta}$ followed by $\Omega \mapsto \mu^\Omega$. The argument never establishes that $P_\theta$ satisfies $T_2$.

In the conjugate-Gaussian instance the cascade *does* yield $C_{T_2} = 2 L_{\text{post}}^2 \sigma^2$ — but via a *different* derivation in §C: direct LSI on the post-update parameter law $\mathcal{N}(0, L_{\text{post}}^2\sigma^2)$, with $\rho_{\text{post}} = 1/(L_{\text{post}}^2\sigma^2)$. That route bypasses the Step 1 issue. The general structural reduction would need either:

- *(option a)* an explicit $T_2$ assumption on $P_\theta$ added to (C1)–(C4), with constant matching the canonical cascade form;
- *(option b)* a different proof scaffold — e.g., direct LSI on $P_{M_{\tau^+}|e,M}$ via Bakry-Émery on the post-update density, bypassing the two-step pushforward;
- *(option c)* a Lipschitz-pushforward argument that starts with $T_2$ on the goal measure $P_G$ (which would need to be added as a hypothesis).

This is a strengthen-before-soften candidate per §3.1. The result is *plausibly true* and is needed for the abstract's claim ("*Track 1 generalizes the canonical Stuart-school posterior-stability cascade beyond Class 1*") — softening the theorem to "valid in the conjugate-Gaussian instance" would be a substantial walk-back. **Recommend a focused spike** on closing the proof. The closed-form §C calculation tells me the *result* is right; what's at issue is the *general derivation*.

### 2.2 Two distinct Fisher-Rao conventions used

**Pattern.** Track 2 globally-valid (Theorem D.1) uses the spherical/Amari-Nagaoka FR with $d_{FR} \in [0, \pi]$ via $d_{FR} = 2\arccos(\mathrm{BC})$. The locally-tight FR computation in §C uses the Riemannian convention $d_{FR}(\mathcal{N}(\mu_1, v), \mathcal{N}(\mu_2, v)) = |\mu_1-\mu_2|/\sqrt{v}$, which is unbounded.

These coincide at second order (locally) but differ globally. The paper *is* internally consistent — locally-tight statements use small-$\delta$ where the two conventions agree to leading order, and global statements use the spherical bound. But §D.1.5 explicitly notes the convention choice ("*Throughout we adopt the standard statistician's Hellinger convention... and the Amari-Nagaoka Fisher-Rao convention $d_{FR} = 2\arccos\int\sqrt{pq}$*"). A reviewer may ask why the §C local computation produces $d_{FR}$ values that exceed $\pi$ for large $|\mu_1-\mu_2|/\sqrt{v}$ — the answer is "those values aren't in (H4$'$) so we never compute them", but it's worth a sentence in §C clarifying the regime restriction.

### 2.3 (H1)'s "statistical-manifold sub-case" is mildly conflated with the chain-rule's standard-Borel requirement

**Hypothesis.** (H1) bundles two things: (i) parameter-manifold = statistical-manifold structure (needed for FR), and (ii) standard-Borel regularity (needed for the chain-rule lemma in abstract form). The chain-rule lemma is invoked in *both* tracks (incl. Track 1, which doesn't need FR structure). So (H1) over-requires for Track 1: standard-Borel alone is enough. This is a presentational issue, not a mathematical one. The cleaner factoring would split (H1) into (H1a) standard-Borel and (H1b) statistical-manifold, with Track 1 needing only (H1a). Optional cleanup.

### 2.4 (H4$'$)'s essential-supremum form is stronger than commonly assumed in the literature

(H4$'$): $\mathrm{ess\,sup}_g \mathrm{KL}_g \le \delta_\star$. This is genuinely stronger than the more common "$\mathbb{E}_G[\mathrm{KL}_g]$ small" — and the paper *acknowledges* this on line 24 of `04-main-results.md`. Good. But a reviewer comparing to the in-context-learning literature (where rare-but-high-KL goals are *the* failure mode) may push back. The remark on `04-main-results.md:36` ("*Track 1 outside (H2$'$)*") and the global Track 2 backstop together cover the "rare-high-KL-goal" regime — but this isn't surfaced as an answer to the obvious "what about adversarial goals?" reviewer question. **Suggestion:** add one Remark sentence under (H4$'$) explicitly noting that adversarial / rare-high-KL goals exit the locally-tight regime, and the global $C=2$ bound is the right tool there.

### 2.5 Track 2 global bound's "Tightest form" Jensen step

**Tested.** `D-track2-companions.md:14`: *"Tightest form (Jensen on the concave envelope): $\mathbb{E}\,d_{FR} \le 2\arccos(\exp(-I_M/2)) \le \min(2\sqrt{I_M}, \pi)$."*

The map $\psi(K) := 2\arccos(\exp(-K/2))$ is concave on $[0, \infty)$ (verified: $\psi'(K) = \exp(-K/2)/\sqrt{1-\exp(-K)}$, which is decreasing). So $\mathbb{E}\psi(\mathrm{KL}_g) \le \psi(\mathbb{E}\mathrm{KL}_g) = \psi(I_M)$ by Jensen. ✓ But $\psi'(0) = +\infty$ — derivative is unbounded near zero. The bound is correct but the "concave envelope" framing is informal; a careful reviewer may want to see a brief justification ("$\psi$ is concave on its domain" plus a one-line check). One-sentence add.

---

## Severity 3 — prose, structure, length

### 3.1 Length: paper is ~1 page over the 9-page main-text budget

**Tested.** Main body extends to page 10. Three high-leverage trim opportunities:

- **§1 Introduction (~2 pages → ~1.5).** The "Hallucination size, in this paper, means..." paragraph (lines 11–12) duplicates the abstract's framing. The "Both flow from the same chain-rule move" appears 3× in the intro. The Contributions list (4 items) restates spine content already in prose paragraphs. Cuts of ~20 lines feasible without harming the spine.

- **§3 Setup (~2 pages → ~1.5).** The Coupled-class autoregressive lemma + corollary + paragraph of robustness commentary (lines 60–79 of `03-setup.md`) is the heaviest structural item in the section. This is a *Setup-section* placement of what is essentially a structural theorem. The lemma statement could land in §3 (it's load-bearing for the architectural classification) but the per-architecture corollary and the half-page of robustness discussion can move to §E.6 (proof appendix), with a one-sentence "see Appendix E.6 for instantiations" pointer in §3. Saves ~½ page.

- **§4 Main Results — `(H2')` and `(H4')` definitions inline.** These two hypotheses sit between the umbrella theorem statement and its remarks (lines 20–24, `04-main-results.md`). They could move to §3 Setup alongside (H1)/(PI)/(R)/(K) (where the other regularity hypotheses live), tightening §4 to be theorem-statement-then-remark. Saves ~⅓ page.

If all three are taken, paper lands at ~9 pages comfortably.

### 3.2 Abstract is dense — 4 distinct results in one block

The abstract states the umbrella bound, both universal constants (locally tight and global), the no-go, the architectural reading, the Coupled-class structural claim, and the JSD operational form. This is the contribution surface, but it leaves a reviewer who reads only the abstract no place to land their attention. The Jin-Yang-Wang-Jordan exemplar's abstract (cited in `VISION.md`) names *one* informal result and points to the body. The current abstract may be doing too much. **Suggestion:** keep the umbrella bound + *one* unpacking (either the universal-constant story OR the architectural reading), and let §1 develop the rest.

### 3.3 §F (Extended related work) is comprehensive but possibly too generous

11+ pages of appendix with 6 strands. Strands 1, 2, 6, and "Existing decompositions" are load-bearing. Strands 3 (Fisher-Rao for Bayesian sensitivity), 4 (brittleness), and 5 (adjacent recent work) could each be tightened. Strand 5 in particular reads as a "name-and-distinguish" sweep that doesn't always justify its citations. Optional trim.

### 3.4 Forward-reference patterns in §3 read awkwardly

`03-setup.md:11`: *"Throughout, $d_{\mathcal{M}}(\cdot, \cdot)$ denotes either the Wasserstein distance $W_2$... (Track 1) or the Fisher-Rao geodesic distance $d_{FR}$... (Track 2). Euclidean-on-parameters is the choice [[#^sec-no-go]] rules out."*

A reader at §3 hasn't seen the no-go yet. The forward-reference is fine in principle, but the bald "the choice $\S$X rules out" reads as cryptic at first encounter. One-sentence preview in §3 would help.

---

## Severity 4 — minor / polish

### 4.1 (⋆) glyph rendering verified (NOT an issue)

`pdftotext -layout` extracts the math-mode `$(\star)$` as `(?)` in 8+ places, but the actual PDF rendering (verified by image extraction at p.6) shows the star symbol correctly. No real issue. Don't be alarmed by the apparent broken-cross-ref pattern in `pdftotext` output.

### 4.2 Underfull `\hbox` warnings

Build log has ~30 underfull-box and one overfull-box warning. These are typesetting nits, not correctness issues. Most are unavoidable with NeurIPS's column setup; the overfull at lines 747–757 is in §B's bullet-and-formula block — could absorb a few more characters into the previous paragraph. Optional.

### 4.3 (H$_\kappa$) "convention" in §3 is a side remark in `03-setup.md:31`

*"Convention. When both numerator and denominator vanish... set $\kappa_{\text{processing}} := 0$..."*

This convention is reasonable but appears mid-paragraph between a worst-case witness sentence and another technical note. A reviewer scanning §3 may miss it. It might land more reliably as a small `*Convention.*` paragraph break. Optional.

### 4.4 Two terms used near-synonymously without disambiguation

"Goal-coupling-induced displacement" and "bias quantity" — the abstract uses the former, §3.1 names the latter as $\|\Delta M_{\text{bias}}\|$. They are the same object but a reviewer skimming may not realize. One sentence clarifying that *bias* = *goal-coupling-induced displacement* in §3.1 would help.

---

## Things that hold up well

The math I checked end-to-end:

- **Chain rule on the post-update law (Lemma 5.1).** Standard conditional-MI golden formula; the fixed-$(e_\tau, M_{\tau^-})$ framing is correct under (H1). ✓
- **Two-point witness sharpness (Theorem 5.1(b)).** $G \in \{\pm a\}$, conjugate-Gaussian, leading-order computation gives $\mathbb{E} d_{FR}/\sqrt{I_M} \to \sqrt{2}$. The symmetry argument that makes Jensen tight at first moment is correct. ✓
- **$N$-point witness sharpness (Theorem D.1 sharpness).** $\mathrm{KL} = \log(N/(N-1))$, $\mathrm{BC} = \sqrt{(N-1)/N}$, $d_{FR} = 2\arcsin(1/\sqrt{N})$, ratio $\to 2$ at rate $1 - 1/(12N)$. Verified by direct computation. ✓
- **Chord-arc lemma (Lemma D.2).** $g(h) = 4\arcsin(h/\sqrt{2})$ strictly convex on $(0, \sqrt{2})$, $g(0) = 0$, secant slope monotone increasing → $\phi(h) = g(h)/h \le \pi$. ✓
- **No-go scale-family construction (Theorem 4.4).** Chart rescaling $\phi_a = a\phi$ scales chart-Euclidean $W_2$ linearly while leaving KL/MI/FR/Hellinger invariant. The contradiction $a \to \infty$ at fixed RHS is correct. ✓
- **Hellinger backstop (Theorem D.2).** Tsybakov 2.4 + chain rule + Jensen — correct, though not locally tight (acknowledged). ✓
- **Conjugate-Gaussian Euclidean translation prefactor.** $L_{\text{post}}\sigma = \tau^2\sigma/(\sigma^2+\tau^2) \le \tau/2$ (AM-GM at $\sigma=\tau$). Limits both vanish. ✓
- **Coupled-class autoregressive connectivity (Lemma 3.5).** Per-source non-degeneracy → directed-graph reachability via residual-edge composition. The induction structure is sound; per-architecture verifications in §E.6 cover six architecture families and address the boundary cases (state-collapse, hard-routing MoE, sliding-window) carefully. ✓

The two-axis frame (frequency vs size) is a clean analytical contribution. The explicit acknowledgment that the structural Coupled-class claim is robust *without* the in-context-learning correspondence (`03-setup.md:79`, `E-proofs.md:170`) is the right move and answers an obvious reviewer concern.

Failed-routes appendix (§A) is well-handled — Cramér-Rao inversion and rate-distortion inversion both fail for *structural* reasons (lower-bound machinery doesn't invert to upper-bound machinery without additional assumptions), and recording the failures prevents future re-attempts.

---

## Top-priority action list

1. **Fix `lie-sullivan-teckentrup-2017` bib entry** (Severity 1.1) — hard requirement.
2. **Resolve `Su-Kempe-Ullrich 2024` citation** (Severity 1.2) — cite or remove.
3. **Drop doubled parens around `\eqref` on `03-setup.md:27`** (Severity 1.3).
4. **Fill empty `journal` fields for 3 bib entries** (Severity 1.4).
5. **Spike on Stuart-school reduction Step 1** (Severity 2.1) — strengthen-before-soften per §3.1; if the proof can't be closed in general, narrow Theorem E.2 to the specific cascade structures it actually covers.
6. **Trim §1 + move §3 attention-coupled corollary detail to §E.6 + move (H2$'$)/(H4$'$) to §3** (Severity 3.1) — gets paper under 9-page budget.

Items 1–4 are mechanical and should land before submission. Item 5 is a real strengthening opportunity (the result is plausibly stronger than the current proof shows). Item 6 is the length fix.

— Auditor: Claude Opus 4.7 (1M context), 2026-05-07
