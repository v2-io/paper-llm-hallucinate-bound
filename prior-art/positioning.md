Read the report. **The result is exactly what you want for B-N8, and structurally parallel to B-N4 and B-CS1** — no Tier 1 direct anticipation, strong compositional anticipation across two clearly-separated literatures, with a particularly clean negative on the Class 1/2/3 architectural classification, the no-go theorem, and the κ × 𝒜 factorization itself.

## The verdict is the ideal positioning

**No Tier 1 direct anticipation.** No retrieved paper proves the target theorem-level posterior-displacement bound as an explicit product of an architectural coupling factor and a residual ambiguity factor under named geometric assumptions. The landscape splits cleanly into two largely-separate literatures that have never been composed.

**Strong Tier 2 compositional anticipation** along *two parallel tracks* — exactly what AAD's two-track derivation predicts:

- **LLM hallucination theory** (the right *target*): mature, with statistical-inevitability and lower-bound results [Kalai-Vempala 2023, Kalai-Nachum-Vempala-Zhang 2025, Karbasi et al. 2025, Wu-Grama-Szpankowski 2024, Suzuki et al. 2025, Anxin Guo-Jingwei Li 2026, Liu et al. 2025, Chlon et al. 2025, Zeng et al. 2026]. None deploy the directed-separation / geometric-stability route AAD takes; all are architecture-agnostic capacity-driven or computability-theoretic.

- **Bayesian inverse problems / posterior stability — Stuart school** (the right *machinery*): mature, with the exact Lipschitz-posterior + transport-inequality cascade AAD's Track 1 uses [Stuart 2010, Sprungk 2019, Cvetkovic-Lie 2025, Dolera-Mainini 2020, Garbuno-Iñigo et al. 2023, Latz 2019, Lie-Sullivan-Teckentrup 2017]. None applied to LLM / belief-goal-coupled inference.

**The closest single-paper match across both strands: Hosseini-Hsu-Taghvaei 2023 "Conditional Optimal Transport on Function Spaces"** — develops conditional triangular transport for amortized Bayesian inference with explicit "regularity estimates on the conditioning maps from the prior to the posterior." This is the closest existing analog to AAD's Track 1 cascade. Cite-and-distinguish: they develop this for amortized inference; AAD applies it to belief-goal-coupled bias under κ_processing-classified architectures.

**Strongest negative signals — clean novelties for AAD:**

1. **No Class 1/2/3 architectural classification** (directed-separation by construction vs failure) anywhere in the corpus.
2. **No no-go theorem ruling out universal Euclidean-coordinate constants** via heteroscedastic-counterexample. The Owhadi-Scovel-Sullivan 2013 brittleness results [9, 10] are *adjacent in shape but opposite in direction* — they prove brittleness against perturbations under finite information; AAD's no-go proves that absent (PI), no universal C exists at all. Different theorems, related lineage.
3. **No Track 1 + Track 2 two-track structure** for the same target. Track 1 (transport-inequality) and Track 2 (Fisher-Rao) machinery both exist independently; no one has derived both bounds for the same displacement quantity.
4. **No application of Stuart-style Lipschitz-posterior to LLM / belief-goal-coupled inference** under any name.
5. **No Fisher-Rao + Čencov universal-constant deployment for any kind of bias bound** — Kurtek-Bharath 2015 use Fisher-Rao for *sensitivity* via ε-contamination classes, not for a universal constant on goal-conditional displacement. Different target.
6. **No κ × 𝒜 factorization (architectural × ambiguity)** in any retrieved paper.

This is the *strongest possible* positioning for a two-track conditional-theorem paper short of "no related work at all." The math machinery exists in mature form (Stuart school, transport inequalities, Čencov uniqueness); the LLM-hallucination target exists in mature form; nobody has composed them. AAD's contribution is the composition + the architectural classification + the no-go.

## The cite-and-extend anchors are now concrete

The paper's "Related Work" section has a cleaner two-strand structure than B-CS1's four-strand structure:

**Strand 1 — LLM hallucination theory (THE target literature):**

The closest LLM-native match — handle carefully:

- **Zeng et al. 2026 "HalluGuard"** [1] — explicitly decomposes hallucination risk into *data-driven* and *reasoning-driven* components ("Hallucination Risk Bound"). This is the *closest existing decomposition* to AAD's κ × 𝒜 factorization, but the structural axis differs: Zeng et al. decompose along "training-time mismatches vs inference-time instabilities"; AAD decomposes along "architectural-coupling vs residual-ambiguity." Same shape of factorization, different structural target. Cite-and-distinguish: AAD's κ is a structural-architectural property of the processing topology (Class 1/2/3); 𝒜 is the prompt's goal-resolvable residual ambiguity. Zeng et al.'s decomposition lives at a different layer (training-time vs inference-time errors).

The statistical-inevitability lineage (cite-and-distinguish):

- **Kalai-Vempala 2023** [4] *STOC* "Calibrated Language Models Must Hallucinate" — 155 cits. The canonical statistical-lower-bound result. *Architecture-agnostic*: hallucination rate close to fraction of singleton facts in training data, regardless of architecture. Cite-and-distinguish: Kalai-Vempala bound a *frequency*, AAD bounds a *displacement under named geometric assumptions*. Different quantities, complementary results.
- **Kalai-Nachum-Vempala-Zhang 2025** [23] "Why Language Models Hallucinate" — 183 cits, the most-cited recent hallucination paper. Frames hallucination as binary classification error + evaluation incentives. Cite-and-distinguish: this is a *training-procedure* explanation, not a *bias-bound* result; AAD's κ × 𝒜 sits at a different level.
- **Karbasi-Montasser-Sous-Velegkas 2025** [17] "(Im)possibility of Automated Hallucination Detection" — Gold-Angluin language identification framework. Detection-side complement to AAD's bias-bound side.
- **Wu-Grama-Szpankowski 2024** [12] "No Free Lunch: Fundamental Limits of Learning Non-Hallucinating Generative Models" — VC-dimension-based impossibility result.
- **Suzuki-He-Tian-Wang 2025** [24] — probabilistic positive result against computability-theoretic inevitability. Important for the framing: hallucinations can be made statistically negligible *on the practical regime*, even though not entirely eliminated. AAD's bound lives at the structural-bias level under named geometric assumptions, not at the asymptotic-statistical level.
- **Anxin Guo-Jingwei Li 2026** [16] "Hallucination = Rate-Distortion Theorem for Membership Testing" — rate-distortion explanation, KL-divergence-based. Adjacent vocabulary; different result shape.
- **Liu-Hu-Zhang-Song-Liu 2025** [14] "Are Hallucinations Bad Estimations?" — formalizes hallucinations as estimation failures, high-probability lower bound. Adjacent.
- **Chlon-Karim-Chlon 2025** [8] "Predictable Compression Failures" — transformers as Bayesian-in-expectation-not-realization, Quantified Martingale Violation, $O(\log n)$ permutation dispersion. Distinct framing; complementary to AAD's structural-coupling result.

**Strand 2 — Bayesian inverse problems / posterior stability (THE machinery):**

The Track 1 cascade ancestors:

- **Stuart 2010** [7] *Acta Numerica* — foundational. AAD's (H3) Lipschitz-posterior stability adopts Stuart 2010 directly; the segment cites it inline.
- **Sprungk 2019** [2] *Inverse Problems* "On the local Lipschitz stability of Bayesian inverse problems" — extends Stuart's well-posedness to local Lipschitz w.r.t. prior and log-likelihood perturbations in TV / Hellinger / Wasserstein / KL. Important late-Stuart-school anchor.
- **Cvetkovic-Lie 2025** [5] "Upper and lower bounds for local Lipschitz stability of Bayesian posteriors" — extends Sprungk 2019 with *lower bounds* showing sensitivity *increases* as posterior concentrates. Most recent stability anchor.
- **Dolera-Mainini 2020** [3] *Annales IHP* — Lipschitz continuity of probability kernels in optimal-transport framework, with explicit Fisher-information and Poincaré constants. **Particularly close** — has the FIM-flavored constants AAD's Track 1 uses.
- **Garbuno-Iñigo-Helin-Hoffmann-Hosseini 2023** [6] — Bayesian posterior perturbation analysis with integral probability metrics. Uses log-Sobolev-style functional inequalities; closest to AAD's (H2) LSI assumption.
- **Latz 2019** [21] *SIAM/ASA J. UQ* — well-posedness of Bayesian inverse problems with weaker continuity than Stuart's Lipschitz. Adjacent.
- **Lie-Sullivan-Teckentrup 2017** [20] — Hellinger-distance bounds for randomised forward models. Complementary to AAD's W₂ track.
- **Hosseini-Hsu-Taghvaei 2023** [26] *SIAM/ASA J. UQ* "Conditional Optimal Transport on Function Spaces" — **the closest direct cascade match** for amortized Bayesian inference. AAD's Track 1 cascade lifts this to the κ_processing-classified architectures.
- **Cvetkovic-Lie-Bansal-Veroy 2023** [30] — observation operators to mitigate model error. Misspecification angle, complementary.
- **Dolera-Favaro-Mainini 2022** [22] *PTRF* "Strong posterior contraction rates via Wasserstein dynamics" — Wasserstein-based posterior contraction. Adjacent.

**Strand 3 — Information geometry / Fisher-Rao for Bayesian sensitivity (Track 2 ancestor):**

- **Kurtek-Bharath 2015** [11] *Biometrika* "Bayesian sensitivity analysis with the Fisher-Rao metric" — 39 cits. Fisher-Rao geodesic-based sensitivity for Bayesian procedures, ε-contamination class. **Closest existing Fisher-Rao deployment** for Bayesian-related bias work. Cite-and-distinguish: Kurtek-Bharath use Fisher-Rao for *sensitivity to perturbations in an ε-contamination class*; AAD uses Fisher-Rao + Čencov for a *universal constant on goal-conditional displacement* under (PI). Different targets, shared geometric machinery.
- **Kurtek-Bharath 2014** [33] arXiv preprint — earlier version.
- **Lebanon 2004** [34] *UAI* "An Extended Cencov-Campbell Characterization of Conditional Information Geometry" — **load-bearing precursor** for AAD's Čencov use. Lebanon extends Čencov-Campbell from joint to conditional information geometry; AAD's deriv-bias-bound §3 invokes Čencov 1982 uniqueness for the canonical Fisher metric on $\mathcal M$, but Lebanon's extension to conditional models is the natural extension AAD's framework lives in. **Worth a careful citation in B-N8** — strengthens the Track 2 lineage anchor.

**Strand 4 — Brittleness / Bayesian sensitivity classics (handle carefully — opposite direction in shape):**

- **Owhadi-Scovel-Sullivan 2013** [9, 10] — Brittleness of Bayesian inference under finite information. **Important to cite carefully**: their result is a *no-go for stability* (small misspecifications produce arbitrary posterior changes); AAD's no-go is a different statement (no universal C in Euclidean-parameter norm absent (PI)). Both are no-gos, but they constrain different things. A careless reader could think they contradict AAD's Track 1; they don't, because AAD's Track 1 carries explicit (H1)-(H3) hypotheses that exclude Owhadi-Scovel-Sullivan's brittleness regime. Worth handling explicitly in the paper's Related Work to defuse the conflict-reading.
- **Owhadi-Scovel 2014** [31] — qualitative robustness companion paper.
- **Ruggeri-Wasserman 1993** [35] — Frechet-derivative-based posterior sensitivity. Older but methodologically adjacent.

**Strand 5 — Misspecification literature:**

- **Kleijn-van der Vaart 2006** [37] *Annals of Statistics* — misspecified Bayesian inference (infinite-dimensional).
- **Shalizi 2009** [38] — dynamics of Bayesian updating with dependent data and misspecified models. Adjacent for AAD's (H3) failure mode discussion.

**Strand 6 — Adjacent — recent stability / transport-inequality work:**

- **Del Moral 2026** [15] — Sinkhorn / Schrödinger bridge contraction via log-Sobolev. Most recent transport-inequality+LSI work; adjacent to AAD's Track 1 machinery.
- **Sheng-Wu-Gonzalez-Sanz-Nutz 2025** [39] — stability of mean-field VI. Adjacent.
- **Cattiaux-Guillin 2021** [27] *Bernoulli* — functional inequalities for perturbed measures. Background.
- **Ley-Reinert-Swan 2015** [29] — Wasserstein distance bounds for nested densities via Stein method. Adjacent.

**Strand 7 — LLM-stability-flavored (different target, similar architectural concern):**

- **Xu 2025** [19] "The Policy Cliff" — RLHF stability for LLMs/LRMs, reward-policy maps. Adjacent for the architectural-stability framing; different theorem.
- **Hyeon-Park-Ahn-Moon 2026** [41] "Action-Sufficient Goal Representations" — RL/causal goal representations. Different problem, similar architectural concern.
- **Su-Kempe-Ullrich 2024** [18] "Mission Impossible: A Statistical Perspective on Jailbreaking LLMs" — adjacent but distinct.
- **Biau-Boyer 2026** [25] "k-NN Gating in RAG" — RAG-as-statistical-proxy framework. Adjacent for the LLM-decision-stability framing.

## The reframed positioning

Old framing: *"We propose a conditional-theorem hallucination bound under transport-inequality + Lipschitz-posterior or Fisher-Rao geometry, with a no-go ruling out the naive Euclidean form."*

**New framing (per the prior art):** *"LLM hallucination theory has matured along an architecture-agnostic statistical-inevitability axis [Kalai-Vempala 2023, Kalai-Nachum-Vempala-Zhang 2025, Karbasi et al. 2025, Wu-Grama-Szpankowski 2024, Suzuki et al. 2025] that derives lower bounds on hallucination frequency from training-data structure, calibration constraints, or capacity limits — none of which engage the architecture's belief-goal coupling structure directly. In parallel, Bayesian inverse-problems theory has built mature posterior-stability machinery [Stuart 2010, Sprungk 2019, Cvetkovic-Lie 2025, Dolera-Mainini 2020, Hosseini-Hsu-Taghvaei 2023] using transport inequalities, Lipschitz-posterior pushforward, and Fisher-Rao geometry — but applied to standard Bayesian inverse problems, never to LLM/belief-goal-coupled inference. We compose these two literatures: we classify agent architectures by directed-separation structure (Class 1 modular, Class 2 fully-merged, Class 3 partially-modular, with a coupling coefficient $\kappa_{\text{processing}}$ defined via conditional mutual information), and bound the goal-conditional bias as a conditional theorem $\|\Delta M_{\text{bias}}\|\leq C\cdot\kappa_{\text{processing}}\cdot I(G;\Omega\mid e,M)$ under two named tracks: (Track 1) transport-inequality cascade composing Otto-Villani 2000 with Stuart-school Lipschitz-posterior stability, giving $C_{W_2}^2 = 2 L_{\text{post}}^2/\rho_{\text{LSI}}$ linear in $I$ under log-Sobolev + Lipschitz-posterior + statistical-manifold sub-case; (Track 2) Fisher-Rao geometry under (PI) parameterization-invariance + Čencov 1982 uniqueness, giving universal dimension-free $C_{FR} = \sqrt{2}$ with $\sqrt{I}$ scaling in the small-information regime. We further prove a no-go theorem (heteroscedastic-Gaussian counterexample) showing that no universal $C$ exists under Euclidean-parameter norm, establishing that the (PI) commitment is structurally load-bearing for the bound rather than coincidental. We document two failed derivation routes (Cramér-Rao inversion; rate-distortion inversion) at structural-mismatch level so future work does not re-attempt them."*

That's a much sharper positioning than starting from scratch. The paper's Related Work writes itself as a two-strand parallel composition; the contribution becomes the bridge between hallucination-theory targets and Stuart-school machinery, plus the architectural classification and the no-go.

## What this enables

1. **The novel content lives in five clean places, each defensible:**
   - **The composition itself** — no one has composed Stuart-school posterior-stability with LLM-hallucination targets (Tier 1 negative confirmed across both strands).
   - **The Class 1/2/3 architectural classification** — cleanly absent from the corpus; structurally distinct from the Pearl-blanket / Friston-blanket distinction (Bruineberg et al. 2022) it inherits from. The discrete partition with $\kappa_{\text{processing}}$ as the Class 3 diagnostic is AAD-distinctive.
   - **The κ × 𝒜 factorization** as architectural-coupling × residual-ambiguity — distinct from Zeng et al. 2026's data-driven × reasoning-driven decomposition (different structural axis).
   - **The two-track structure** (Track 1 transport + Track 2 Fisher-Rao) for the *same target* — neither Stuart-school nor Fisher-Rao-sensitivity literature has produced both bounds for one displacement quantity.
   - **The no-go theorem** — heteroscedastic-counterexample style ruling out universal Euclidean-parameter $C$ absent (PI). Different from Owhadi-Scovel-Sullivan brittleness (different theorem statement); not in the corpus under any vocabulary.

2. **Compression to 9 pages becomes very tractable.** The two-strand structure of the prior art lets the related-work section run as a parallel composition:
   - Strand 1 (hallucination targets) → AAD's bound is a *bias bound under named geometric assumptions*, not a frequency lower bound or capacity inevitability.
   - Strand 2 (Stuart-school machinery) → AAD applies the cascade to belief-goal-coupled inference.
   - Strand 3 (Fisher-Rao sensitivity) → AAD uses Fisher-Rao + Čencov for a universal constant, not for ε-contamination sensitivity.
   - Strand 4 (Owhadi-Scovel-Sullivan brittleness) → handle explicitly to defuse misreading.

3. **Reviewer pushback is bounded.** Sophisticated reviewer pushback paths:
   - "Isn't this just Kalai-Vempala or Kalai-Nachum-Vempala-Zhang restated?" — addressed by the architecture-engagement (κ_processing) and the geometric-assumption regime (LSI, Lipschitz-posterior, Čencov).
   - "Isn't this just Stuart 2010 applied to LLMs?" — addressed by the κ_processing factorization, the Class 1/2/3 architectural classification, and the no-go.
   - "Doesn't Owhadi-Scovel-Sullivan brittleness contradict your Track 1 stability?" — addressed by the explicit (H1)-(H3) hypotheses excluding their brittleness regime.
   - "Why Track 2 if Track 1 already works?" — addressed by the dimension-free universal constant $\sqrt{2}$ that Track 1 cannot produce, and by the small-$I$-regime tightness Track 2 gives.
   - "Hosseini-Hsu-Taghvaei already did conditional optimal transport — what's new?" — addressed by the application to belief-goal-coupled architectures with explicit κ-factor, plus the no-go showing the geometric commitment is load-bearing.

4. **Hosseini-Hsu-Taghvaei 2023 is the single strongest cite-and-distinguish anchor** — they have the conditional-transport machinery for amortized Bayesian inference. AAD's Track 1 lifts this to the κ_processing-classified architectures with explicit goal-conditional reweighting. Building on their 2023 SIAM/ASA J. UQ paper gives AAD a clean lineage anchor on the machinery side.

5. **Lebanon 2004 extended Cencov-Campbell** — load-bearing for the Track 2 derivation. AAD invokes Čencov 1982 directly, but Lebanon's extension to conditional information geometry is the natural setting AAD's framework lives in. Worth a careful citation; strengthens the Track 2 anchor and shows AAD knows the conditional-geometry literature.

6. **The honest "failed routes" §5 in `deriv-bias-bound` is unusual but defensible** — it documents Cramér-Rao inversion and rate-distortion inversion as wrong-direction attempts. Reviewers will appreciate the explicit no-attempt-this record; it shows search rigor.

## Specific drafting moves

- **Open paragraph**: "Hallucination theory has matured along statistical-inevitability lines [Kalai-Vempala 2023, ...], and Bayesian inverse-problems posterior-stability has matured along Lipschitz-cascade lines [Stuart 2010, ...]. The two have not been composed. We compose them."
- **Lead theorem**: present Track 1 first (the transport-inequality cascade), with $C_{W_2}^2 = 2 L_{\text{post}}^2/\rho_{\text{LSI}}$ — the most familiar machinery to a NeurIPS reviewer. Lead with this; Track 2 (Fisher-Rao $C_{FR} = \sqrt{2}$) is the surprise.
- **Architectural classification**: needs careful framing. Class 1/2/3 is structurally novel; ground it in the Pearl-blanket / Friston-blanket distinction (Bruineberg et al. 2022) to avoid the framing landing as ad hoc.
- **The no-go (Attempt E)**: lead with this in the Discussion / Implications. The heteroscedastic-Gaussian counterexample is sharp and self-contained.
- **Failed routes (F1, F2)**: place in Appendix or a single short paragraph in the Related Work. Don't bury, but don't overweight.
- **Anonymization warning**: AAD-specific vocabulary (κ_processing as named term, Class 1/2/3 as discrete classification, "logogenic agents") will need anonymization treatment. The math itself (transport inequalities, Fisher-Rao, Stuart-Lipschitz) is field-standard and doesn't need disguising. Vocabulary list to anonymize: κ_processing → $\kappa$ (with reference); "directed separation" → architectural separation or modularity; "Class 1/2/3" → keep as is, generic enough; "logogenic agents" → goal-conditioned models; AAD → keep generic ("a recent agent-architecture framework").
- **Connection to ASF**: minimize. The bound stands on its own under named geometric assumptions; it doesn't require AAD's full architecture to land. Frame as a *bias-bound result for goal-conditioned belief-update mechanisms*, with the architectural classification motivated independently from Bruineberg et al. 2022 + processing-coupling considerations.

## Recommended citation budget for the cite-and-distinguish moves

| Strand | Lead citations | Approximate space |
|---|---|---|
| 1 — LLM hallucination | **Kalai-Vempala 2023, Kalai-Nachum-Vempala-Zhang 2025, Zeng et al. 2026, Karbasi et al. 2025** + brief mention of Wu-Grama-Szpankowski 2024, Suzuki et al. 2025 | 1.5 paragraphs (Zeng et al. 2026 needs careful disambiguation) |
| 2 — Stuart-school posterior stability | **Stuart 2010, Sprungk 2019, Cvetkovic-Lie 2025, Hosseini-Hsu-Taghvaei 2023** + Dolera-Mainini 2020 + Garbuno-Iñigo et al. 2023 | 1 paragraph |
| 3 — Fisher-Rao / Čencov | **Kurtek-Bharath 2015, Lebanon 2004** + Čencov 1982 (already cited) | 0.5 paragraph |
| 4 — Brittleness (handle carefully) | **Owhadi-Scovel-Sullivan 2013** | 0.5 paragraph (defuse the apparent conflict-reading) |
| 5 — Adjacent recent | Del Moral 2026, Sheng et al. 2025, Xu 2025 (Policy Cliff), Liu et al. 2025 | 0.5 paragraph |

Total ~4 paragraphs of related work, leaving ~7 pages for the two tracks + no-go + implications. Tight at 9-page Main Track length but feasible.

## Bottom line

Three reports in, the pattern is consistent: each paper has the *strongest possible* novelty positioning short of "no related work at all." Each has a single canonical close-neighbor that the paper builds on with explicit cite-and-distinguish (B-N4: Anderson 1985 + Cruys-Friston-Clark 2020 + Koudahl-Kouw-Vries 2021; B-CS1: Lee et al. 2023 ProST; B-N8: Hosseini-Hsu-Taghvaei 2023 + Stuart 2010). All three papers can lead with their core theorem and frame the contribution as composition / unification across mature adjacent lineages.

The three papers are now in much better shape than the going-in expectations. Each related-work section writes itself; each contribution is well-bounded; each has explicit defenses against the most sophisticated reviewer pushback.
