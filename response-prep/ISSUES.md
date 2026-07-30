# ISSUES — submission 33977

Ratings 3 / 1 / 2 (confidences 2 / 2 / 4). Meta-review is negative on three axes — theoretical novelty beyond composition, LLM relevance, accessibility — but closes constructively by naming what would substantially strengthen the work. Reviewers are R-A (3), R-B (1), R-C (2) — our labels, not venue identifiers.

> **Tracked in a public repo.** Paraphrase only; no reviewer pseudonyms or verbatim text. Reviews at `~/src/neurips/reviews/neurips-2026/03-llm-hallucinate-bound/` (gitignored).

Status codes as in paper 01: `POINT` / `MATH` / `CITE` / `CONCEDE` / `REVISION`.

| ID | Issue | Raised by | Disposition | Status |
|---|---|---|---|---|
| **J-01** | **Bound is vacuous in the motivating regime — `2√I > π ≥ d_FR` once `I ≳ 2.47` nats, and adversarial/jailbreak prompts are exactly the high-`I` regime the global `C=2` form is advertised for** | R-A | **`MATH`** | **open — the real finding** |
| J-02 | Unclear what is proved beyond composing known results (chain rule = definition of conditional MI; Talagrand, Čencov, Rényi monotonicity all textbook) | R-A, R-C, meta | `MATH` + framing | open |
| J-03 | LLM connection not established: `κ_processing` neither bounded nor estimated for transformers, so the architectural corollary doesn't apply to the architectures motivating the paper | R-A, R-C, meta | `CONCEDE` | open |
| J-04 | No empirical instantiation; asked to compute the JSD estimator on a sycophancy benchmark and report whether the bound is non-vacuous | R-A, R-C, meta | `CONCEDE` + plan | open |
| J-05 | Belief-state reading depends on the ICL correspondence, which the paper itself restricts | R-A | `POINT` | open |
| J-06 | Assumptions ((PI), (R), (K), (H4′), manifold structure) may be mathematical convenience rather than properties of real LLMs; sensitivity to violations unclear | R-C | partly `POINT` | open |
| J-07 | Invented/unexplained terminology: goal-coupling-induced displacement, belief-goal-coupling structure, frequency lineage, operational shape, empirical referent, cascade, load-bearing | R-B, meta | `REVISION` | open |
| J-08 | **Terminology error:** "probabilistic-negligibility" — the literature's term is *statistical* negligibility | R-B | fix, and concede | open |
| J-09 | Abstract is too technical; notation used before definition; sets to which symbols belong never specified | R-B, meta | `REVISION` | open |
| J-10 | Displacement is an abstract belief-state quantity, not factual correctness — hallucination link is indirect | R-C, meta | `POINT` (abstract says this) | open |
| J-11 | No practical mitigation follows from the bound; unclear how to operationalize at scale | R-C | `CONCEDE` | open |

---

## J-01 — the vacuity ceiling  ← work this first

**The objection, and it is arithmetically correct.** I checked it. On the ambient Amari–Nagaoka spherical-arc convention `d_FR(P,Q) = 2·arccos ∫√(pq)`, the metric is bounded: `d_FR ≤ π`. The global Track-2 bound is `E d_FR ≤ 2√I`. So the bound is informative only while `2√I < π`, i.e. `I < (π/2)² ≈ 2.467` nats. The Hellinger companion saturates near 2 nats similarly.

**Why it stings rather than merely being noted.** The abstract sells `C = 2` as *the operating constant for adversarial / rare-high-KL prompts including jailbreaks and persona injection* — precisely the regime where transferred goal-information is large and the bound is therefore empty. So the paper's advertised operational value sits exactly where its mathematics says nothing. That is a structural problem with the framing, not a presentation issue, and the reviewer is right to lead with it.

**Do not concede first.** Strengthening routes to try, roughly in order of promise:

1. **Reformulate on an unbounded or slowly-saturating quantity.** The saturation is an artifact of bounding a *bounded* metric by an *unbounded* `√I`. Any `√I`-shaped bound on a bounded metric must go vacuous — so the interesting object may be a bound with the right asymptotic shape, e.g. something of the form `E d_FR ≤ π·f(I)` with `f(I) → 1` slowly, or a bound on `arccos`-argument / Bhattacharyya affinity `∫√(pq)` directly, which is where the geometry actually lives. A multiplicative-affinity bound (`E ∫√(pq) ≥ g(I)`) would remain informative at large `I` if `g` decays gracefully. **This is the route I'd spend the time on** — it is the same content, stated on a coordinate that doesn't saturate.
2. **Sharpen `C` in the high-`I` regime.** `C = 2` is proved sharp via a symmetric `N`-point witness as `N → ∞`. But sharpness *of the constant in the limit* does not mean the bound is tight at every `I` — the witness may live at small per-slice KL with large `N`. If the sharp constant degrades in a controlled way as a function of `I`, the useful statement is a two-parameter family `C(I)` rather than one constant. Check what the `N`-point witness's `I` actually is.
3. **Accept the ceiling and reframe what the bound is for.** If the metric is bounded, then "displacement is bounded" is trivially true at high coupling, and the *content* is at low-to-moderate `I` — where it is a genuine quantitative statement. Then the honest framing is the reverse of the abstract's: the bound is informative for ordinary goal-conditioning, and jailbreak regimes are where it provably *cannot* say anything, which is itself a limitation worth stating as a result. This is the concession, and it requires editing the abstract's claim at revision time.

Note (1) and (3) are not exclusive: (3) is the honest fallback if (1) fails, and (1) would make (3) unnecessary.

**In the response**, whichever way it goes: acknowledge the arithmetic without hedging. The reviewer computed something real and getting this wrong destroys credibility on everything else. If (1) is not settled by the deadline, say plainly that the bound's informative range is `I ≲ 2.5` nats, that the abstract oversells the adversarial regime, and that the correct statement of the adversarial case is a separate question we now consider open.

Working notes → `math/J-01-vacuity-ceiling.md`.

---

## J-02 — "what is proved beyond composing known inequalities?"

Raised independently by two reviewers and led the meta-review, so it is the *decision-relevant* one even though J-01 is the sharper catch.

**The critique has real force and should not be brushed off.** Lemma 5.1 genuinely *is* the chain rule / definition of conditional mutual information — the paper says so. Track 1 applies Talagrand `T₂`; Track 2 applies a KL-to-Fisher-Rao expansion plus Čencov. Each step is standard. So "what is new?" is a fair question, and answering it with a list of the components restates the objection.

**Candidate honest answers, in descending strength:**

1. **The no-go is the novel content.** That no coordinate-independent universal constant exists for Euclidean chart norms — and therefore that a parameterization-invariance commitment is *forced* if one wants a universal constant at all — is not a composition of known inequalities. It is a negative result about the space of possible bounds. The `C = 2` / `√2` constants then follow from Čencov *given* that commitment, and the interesting claim is the conditional structure: invariance commitment ⟹ Fisher–Rao ⟹ a specific dimension-free constant, with no remaining freedom. Lead with this.
2. **The architectural classification.** The Class 1/2/3 ladder and the derivation that plain attention is Class 3 by graph reachability alone is not a repackaging of an inequality. It is weak (path existence, not magnitude — see J-03) but it is ours.
3. Sharpness witnesses for both constants — mild, but they mean the constants are not slack artifacts.

**What not to claim.** Don't argue the `√I` conversion is novel. It isn't. The composition-as-contribution framing is what drew the objection, and defending it directly loses.

---

## J-03 / J-04 — the LLM gap

These are the same gap seen twice, and it is real: `κ_processing` is unbounded for Coupled architectures (the parrot witness gives `∞`), transformers are Coupled, therefore the `κ × A` factorization — the paper's stated headline reading — does not quantitatively apply to transformers. The unconditional theorem still bounds transferred information directly, which is the honest fallback, and the paper does say this in places. But the abstract's operational promise outruns it.

Concede cleanly. Then note the concrete thing that *is* doable and would answer J-04: the binary-uniform two-goal JSD estimator is directly computable from per-goal response samples on an existing sycophancy benchmark, needs no model internals, and would settle non-vacuity empirically. We cannot run it during the response period (no revisions), but committing to it — and stating the prediction that measured `I` will often exceed the ~2.5-nat ceiling, connecting to J-01 — is a credible answer. **Only state that prediction if we believe it; my read is that it is likely true and that saying so is more honest than promising a favourable result.**

---

## J-07 / J-08 / J-09 — terminology and accessibility

This is the harshest review and also the cheapest to learn from. One reviewer stated plainly they could parse only a handful of sentences in the paper — at confidence 2, with an admission of non-comprehension, so the AC may discount the rating, but **the diagnosis should not be discounted**: it is the same clarity finding all three papers received.

The specific substitutions asked for are all improvements and cost nothing: *operational shape* → manifestation; *empirical referent* → real-world example; *load-bearing* → crucial/essential; *cascade* → name the actual chain of results. And **J-08 is a genuine error to own**: the literature's term is *statistical* negligibility. Fix it and say so — conceding a real mistake buys credibility for the places where we push back.

For revision: the abstract needs to stop being a compressed technical summary. Notation before definition, and symbol domains left unstated, are fixable mechanically.

Drafts → `segments/`.
