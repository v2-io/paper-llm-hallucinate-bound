# J-01 — the vacuity ceiling, and whether the bound can be restated so it doesn't saturate

**Status: the problem is CONFIRMED; the fix is OPEN.** Nothing below the "confirmed" section is proved.

## Confirmed (arithmetic, checked)

Ambient Amari–Nagaoka spherical-arc convention: `d_FR(P,Q) = 2 arccos ∫√(pq)`. Since `∫√(pq) ∈ [0,1]`, `arccos(·) ∈ [0, π/2]`, so

    d_FR ∈ [0, π],    max d_FR = π  (attained at disjoint support).

Global Track-2 bound: `E d_FR ≤ 2√I` where `I = I(G; M_τ+ | e_τ, M_τ−)` in nats. This constrains nothing once

    2√I ≥ π  ⟺  I ≥ (π/2)² ≈ 2.4674 nats  (≈ 3.56 bits).

Hellinger companion: `H ≤ √2`, bound `≤ √(2I)` (or as stated in the paper), vacuous around `I ≈ 2` nats — reviewer's "roughly 2 nats" is right.

**So the objection stands as stated.** And the framing problem is worse than the arithmetic: the abstract names `C = 2` as the operating constant for jailbreaks and persona injection — the large-`I` regime — which is exactly where the statement is empty. Any response that does not concede this plainly will read as evasive.

## Why saturation is structural, not incidental

Bounding a **bounded** metric by an **unbounded** function of information must go vacuous somewhere. The only questions are *where* and whether a different left-hand or right-hand coordinate avoids it. So "tighten `C`" cannot fix this in general — halving `C` merely doubles the reachable `I` (`C = 1` buys `I < π² ≈ 9.87`, still finite). Worth stating explicitly in the response, because it shows we understand the shape of the problem rather than patching a constant.

## The route worth trying: bound the affinity, not the arc

The geometry lives in the Bhattacharyya affinity `ρ(P,Q) := ∫√(pq) = cos(d_FR/2)`, which is naturally multiplicative and bounded in `[0,1]` with an *information* interpretation — `−log ρ` is the Rényi-1/2 divergence up to constants, and Rényi-1/2 monotonicity is already a tool the paper uses for the global constant.

Conjecture to test: a bound of the form

    E[ −log ρ(P_{M|G}, P_M) ]  ≤  c · I        (or with a Rényi-order correction)

would be **non-saturating** — the left side is unbounded, so the inequality retains content at every `I`. Converting back gives `E d_FR ≤ 2 E arccos(ρ)`, which degrades gracefully rather than dying at a threshold. This is plausibly *the same content* the paper already has, restated on the coordinate where it doesn't hit a ceiling: Rényi-1/2 monotonicity relates `−log ρ` to KL directly, and the goal-averaged KL is exactly `I` by the chain-rule lemma. If the inequality falls out with `c` small and universal, this is a strict strengthening and turns the reviewer's objection into an improvement.

Things to check before believing it:
- The direction of Rényi-order monotonicity — `D_{1/2} ≤ D_1 = KL`, so `E[−log ρ] ≤ (1/2)·I`-ish is the *promising* direction. Verify constants and whether the factor is `1/2` or `2`; do not guess.
- Whether Jensen bites when pushing the expectation over `G` through `arccos` (concave/convex on the relevant range?). The existing `√2` witness uses symmetry to make Jensen tight; check whether the same witness applies here.
- Whether the resulting statement is genuinely new or is a known Rényi-divergence bound wearing different notation. Given J-02 ("what's new beyond known inequalities"), landing a bound that turns out to be textbook would make J-02 *worse*. Search before claiming.

## Fallback, which is honest and still worth having

If the affinity route fails: state the informative range explicitly as part of the result rather than as a limitation buried in an appendix. *"The bound is quantitative for `I ≲ 2.5` nats and vacuous beyond; measured `I` on adversarial prompts is expected to exceed this, so the adversarial regime is open."* That is a real scope statement and it inverts the abstract's current claim — which needs to change at revision time regardless of how the math goes.

Also worth flagging as a genuine (small) result in the fallback: *no* `√I`-shaped bound on a bounded metric can be informative at high coupling. That is a one-line no-go and it explains why the adversarial regime needs a different object entirely. Small, but it is present truth rather than an apology.

## Next actions

1. Check the Rényi-1/2 ↔ KL constant and direction. Half an hour, decisive.
2. If direction is favourable, derive `E[−log ρ] ≤ c·I` and check `c`.
3. Search whether that bound is already known (this matters as much as deriving it — see J-02).
4. Draft response language only after 1–3.
