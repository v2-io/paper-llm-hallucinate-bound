# De Novo Audit - 2026-05-07

Paper: `How Much Can LLMs Hallucinate? An Upper Bound via Coupling and Ambiguity`

Scope: first-hand read of the built PDF plus source markdown in `src/re/`. I did not do external bibliographic verification. I focused on theorem-object clarity, constant claims, and the translation from architecture classification to LLM hallucination language.

## Overall Read

The chain-rule move is clean: average slice-wise KL from goal-conditional post-update laws to the goal-marginal equals transferred goal information. The Track 1 transport bound is straightforward under the stated `T_2` hypothesis. The main audit risk is Track 2's constant language: the source proof gives a local `(1+o(1))` result, while the main theorem states a finite-regime constant `sqrt(2)`. The second risk is semantic: the theorem bounds goal-coupling displacement of an implicit belief/model state, not hallucination truth error directly.

## Findings

### H1 - Track 2 states `C = sqrt(2)` as a theorem, but the proof gives `sqrt(2)(1+o(1))`

Source: theorem at `src/re/04-main-results.md:5-20`; mechanism at `src/re/05-mechanism.md:28-37`; appendix proof at `src/re/E-proofs.md:34-49`.

The main theorem says that under H4' the Fisher-Rao route supplies `C = sqrt(2)` with no domain-specific parameters. The proof applies a second-order KL-to-Fisher-Rao expansion and explicitly carries a remainder:

`E d_FR <= sqrt(2) sqrt(I_M) (1+o(1))`.

The appendix even gives a finite remainder form `1 + R_3(delta_star)` at `src/re/E-proofs.md:39`. For any fixed `delta_star in (0,1)`, the constant should be `sqrt(2(1+R_3(delta_star)))` or similar, unless an independent global inequality gives the exact `sqrt(2)` constant on the whole H4' regime.

Suggested fix: choose one of these defensible statements:

- Local asymptotic theorem: `E d_FR <= sqrt(2 I_M)(1+o(1))` as `delta_star -> 0`, with `sqrt(2)` locally tight.
- Finite-local theorem: `E d_FR <= sqrt{2(1+R_3(delta_star)) I_M}` with the explicit remainder.
- Global theorem: use the existing `pi/sqrt(2)` backstop for nonlocal regimes.

As written, the exact finite-regime `sqrt(2)` claim is stronger than the proof.

### H2 - The sharpness proof proves a second-moment witness, not the stated `E d_FR` sharpness

Source: theorem statement at `src/re/04-main-results.md:49-56`; proof at `src/re/E-proofs.md:84-87`; conjugate-Gaussian appendix at `src/re/C-conjugate-gaussian-numerics.md`.

Theorem 4.5(b) states no constant `C < sqrt(2)` uniformly bounds `E d_FR / sqrt(I_M)`. The proof shows `E[d_FR^2] / I_M -> 2`. That does not by itself imply `E[d_FR] / sqrt(I_M) -> sqrt(2)`, because Jensen goes the other direction.

This looks strengthen-able rather than fatal. A two-point symmetric goal perturbation in the small-variation Gaussian family should make `d_FR` essentially constant across the two goal slices, giving `E d_FR / sqrt(I_M) -> sqrt(2)` directly. The report should use that witness, or else restate the sharpness theorem for the squared-distance bound.

Suggested fix: replace the proof witness with an explicit two-point goal construction and compute `E d_FR`, not only `E d_FR^2`. If the authors prefer the current Gaussian variance calculation, change the theorem to sharpness of the squared-distance inequality.

### H3 - The title and opening question overstate the theorem object unless "hallucination size" is defined narrowly

Source: title; intro at `src/re/01-introduction.md:3-13`; bias definition at `src/re/03-setup.md:7-11`; limitations at `src/re/06-conclusion.md:7`; caveat at `src/re/E-proofs.md:120`.

The theorem bounds displacement between goal-conditional and goal-marginal post-update model-state laws. That is not automatically "how much an LLM hallucinates" in the truth-conditional sense. The paper does acknowledge this in limitations and in the proof caveat: the bias-bound application requires an in-context-learning/implicit-posterior correspondence, and out-of-distribution or jailbreak regimes degrade to an output-distribution displacement bound.

Suggested fix: add a crisp definition near the end of the intro:

"In this paper, hallucination size means the goal-coupling-induced displacement of the model's evidence-conditioned belief state, not the semantic distance from a false output to truth."

Alternatively, retitle/subtitle around "goal-coupling displacement" and keep hallucination as the motivating application. This would protect the paper from a reviewer saying the theorem bounds a proxy but the title claims the target.

### H4 - `kappa_processing` needs a zero-denominator convention

Source: definition at `src/re/03-setup.md:27-31`; corollary at `src/re/04-main-results.md:64-80`; proof note at `src/re/E-proofs.md:28`; parrot witness in `src/re/B-hypothesis-verification.md` under `(H_kappa) sufficient conditions`.

The ratio

`kappa_processing = I(G; M_{tau+} | e, M_{tau-}) / I(G; Omega_tau | e, M_{tau-})`

is undefined when the residual ambiguity denominator is zero. The parrot witness treats positive numerator over zero as infinity, which is right. But Class 1/separated cases can also produce `0/0`: no residual ambiguity and no transferred goal information. The corollary should define this case rather than rely on informal ratio reading.

Suggested fix: state the corollary with either `I(G; Omega | e,M) > 0`, or define the convention:

- denominator zero and numerator zero: `kappa_processing = 0` and the factorized bound is zero;
- denominator zero and numerator positive: `kappa_processing = +infty`, so H_kappa fails.

### H5 - The transformer Class 3 claim is stronger in prose/table than in the lemma

Source: intro at `src/re/01-introduction.md:25`; table at `src/re/03-setup.md:17-24`; lemma at `src/re/03-setup.md:63-68`; proof/caveats at `src/re/E-proofs.md:102-120`.

The intro says "every internal computation has a directed-graph path from any input position." The table says `G` is "causally upstream of every computation." The formal lemma is narrower: downstream positions `j >= max(i_G union i_E)`, non-degenerate attention, and sparse/sliding-window attention only when a multi-hop path exists. The proof caveats are good, but the reader-facing prose should match them.

Suggested fix: replace the broad Class 3 prose with "every downstream output computation used to read the post-update state has a graph path from goal tokens under non-degenerate reachable attention." That preserves the useful structural claim without overclaiming upstream positions or masked-out paths.

### H6 - "Empirically accessible kappa" is underdefined

Source: `src/re/04-main-results.md:82`; related future direction at `src/re/06-conclusion.md:9`.

The paper says a behavioral two-goal probe gives a lower bound on `kappa_processing` by measuring divergence of "epistemic content" of the response. No metric or estimator is defined in the theorem layer, and lower-bounding a mutual-information ratio from two-goal probes is nontrivial. This is fine as future work, but too strong as a main-text remark.

Suggested fix: move the sentence fully into future directions, or restate it as "may be empirically probed" rather than "is empirically accessible." If kept in main text, define the observable divergence and the assumptions under which it lower-bounds transferred MI.

### M1 - H1's LLM applicability is narrow and should be attached to headline claims

Source: H1 at `src/re/03-setup.md:54-57`; intro claim at `src/re/01-introduction.md:7-9`; limitations at `src/re/06-conclusion.md:7`.

H1 requires the model state to correspond to a probability distribution on latent world-states and the model class to be locally a statistical manifold. That is natural for Bayesian inverse problems and parametric posterior families, but only a subclass/idealization for deployed LLMs. The paper knows this, but the title and intro can read architecture-general.

Suggested fix: in the abstract or intro, say the bound applies to "LLM belief-state idealizations satisfying H1" or "the parametric/implicit-posterior subclass of LLM behavior." Keep Lemma 3.5 as a structural attention result, but do not let it imply H1 for arbitrary transformer operation.

### M2 - Track 1's "strict sub-case" claim may need a softer mapping

Source: `src/re/01-introduction.md:17`, `src/re/04-main-results.md:30`, `src/re/C-conjugate-gaussian-numerics.md`.

Track 1 clearly uses the same transport-inequality machinery as Bayesian inverse-problems posterior stability. The phrase "contains the existing lineage as a strict sub-case" is stronger: existing posterior-stability results often bound perturbations of data/prior/likelihood maps, while this paper bounds goal-conditional displacement on a post-update law after a chain-rule step. The conjugate-Gaussian example is a strong witness, but not necessarily a containment of the whole lineage.

Suggested fix: say "recovers the canonical Stuart-school cascade constant in the conjugate-Gaussian/log-Sobolev case" instead of "contains the lineage as a strict sub-case," unless a broader mapping theorem is added.

## Trim-Adjacent Opportunities

- The paper repeats the frequency-vs-size contrast in abstract, intro, related work, and conclusion. Once the proxy definition of hallucination size is explicit, later repetitions can be shortened.
- The no-go proof is short enough that the main text can state the result and leave most commentary to Appendix E. The "exactly what to commit to" prose is rhetorically strong but not necessary in every location.
- The Hellinger/Fisher-Rao companion taxonomy is useful, but much of it can stay appendix-side unless the main theorem is changed to explicitly use the global backstop.

## Suggested Triage

1. Fix Track 2 theorem statement to carry either `(1+o(1))` or an explicit finite-local remainder.
2. Repair Theorem 4.5 sharpness using an `E d_FR` witness, or restate it for squared distance.
3. Define hallucination-size proxy in the intro and attach H1/implicit-posterior scope.
4. Add the zero-denominator convention for `kappa_processing`.
5. Narrow the transformer Class 3 prose to the formal downstream/reachable-attention claim.
