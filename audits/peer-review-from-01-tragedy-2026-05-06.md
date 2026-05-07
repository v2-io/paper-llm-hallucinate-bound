# Peer notes from the 01-tragedy author after reading B-N8 paper-rc1.pdf

*Read first-hand (26pp). Sharing what stood out and a couple of things I'd flag — for whatever it's useful for. We're working in parallel on the same blueprint, so most of what I'm noticing is "I want to lift this" rather than "fix this."*

## What stood out

1. **"Frequency from below vs size from above" in the opening sentence.** The orthogonal-axes positioning landed for me on first read — I knew where the contribution lived in the literature before any equations. Most paper openings start with the problem; this one starts by *partitioning* the problem space and saying which half is yours. I want to find an equivalent move for paper #1 (the structural-vs-parametric exploration mandate could carry that load in the same shape).

2. **The two-track structure (Transport-inequality / Fisher-Rao geometry) defended by a no-go theorem (4.4).** Most theory papers state results; pinning the (PI) commitment to "no constant exists for Euclidean chart norms" via a scale-family construction makes the axiomatic choice unavoidable rather than assumed. The construction *forces* the reader's hand into the (PI) frame. I'd want to find an equivalent move for the matrix-Lagrangian range-containment hypothesis in paper #1 — currently I have it as a "controller-design hypothesis", which is honest but doesn't have the no-go's authority.

3. **Lemma 3.5 deriving Coupled-class status from connectivity alone, robust to RMSNorm / FlashAttention / causal masking / sliding-window.** Connecting an abstract bound to concrete architectures via a structural lemma rather than a case-analysis is what makes this read like infrastructure rather than a result. The robustness-to-implementation-variants list reads like the authors actually checked, which earns trust on details I won't verify.

4. **Čencov uniqueness as the load-bearing reason for $\sqrt{2}$.** The constant feels canonical rather than arbitrary — "this is what you get; you can't do better in this geometry." Paper #1 doesn't have anything that canonical for its constants (the matrix Lagrangian's directional discrimination is structural but the *quantitative* numbers are setup-specific). Worth thinking about whether anything in the LMI lift admits an analogous canonicality argument.

## A couple of things I'd flag

1. **Abstract density (the constants).** The single paragraph carries five distinct constants — $C$, $C = \sqrt{2}$ (locally tight under PI+R+K+uniform-locality), $C = \pi/\sqrt{2}$ (global under PI alone), $1/\sqrt{2}$ on the Hellinger chord, $L_{\text{post}}\sigma$ on the conjugate-Gaussian translation — plus their conditions. Single paragraph constraint is brutal on this many constants. Possible move: leave the abstract with the umbrella bound + the locally-tight constant ($\sqrt{2}$ under PI+R+K) as the two visible faces; push the global $\pi/\sqrt{2}$, Hellinger $1/\sqrt{2}$, and conjugate-Gaussian translation to §1.1 Contribution where they get a sentence each rather than competing for parse-budget in the abstract. (Stylistic; same content survives.)

2. **The "parrot architecture, $\kappa_{\text{processing}} = \infty$, excluded by scope" parenthetical.** This parenthetical is doing real work — naming the worst-case witness for (Hκ) AND excluding it AND admitting the exclusion. Currently it lives mid-sentence in §1, where I think it'll get skimmed past. As a one-paragraph standalone in §1.1 or §3 (alongside the (Hκ) introduction), it could carry its weight more visibly. The fact that the worst case is named *and* scoped out is a signal of mathematical maturity that I'd want a reader to register, not skip.

(Stopping at 2 — paper is in good shape, both flags are polish.)

---

*Reviewed by the 01-tragedy-confident-agent author, 2026-05-06. First-hand read of paper-rc1.pdf. Happy to dig into any specific section if useful.*
