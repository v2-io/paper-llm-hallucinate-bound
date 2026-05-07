# De novo audit, 2026-05-07

Scope note: I read the current manuscript segments in `src/re/*.md`, `meta.md`,
`README.md`, and `llm-hallucinate-neurips-2026.extracted.bib`. I did not read
the existing files under `audits/`, and I did not read the archived peer reviews
or project planning/prior-art reports. I did a limited web spot-check of recent
and high-risk citations.

## Executive verdict

The paper has a real, clean mathematical core:

1. The chain-rule identity
   `E_G KL(P_{M+|G,e,M-} || P_{M+|e,M-}) = I(G;M+|e,M-)`.
2. The immediate `T_2` consequence
   `E W_2 <= sqrt(C_T2 I(G;M+|e,M-))`.
3. The local Fisher-Rao consequence
   `E d_FR <= sqrt(2 I(G;M+|e,M-))` in a genuinely local regime.

Those pieces are correct in spirit and worth preserving. The current manuscript
is not submission-ready as a NeurIPS theory paper, mainly because several
headline claims outrun the hypotheses actually proved. The most important risks
are mathematical, not stylistic:

1. The object whose distance is being measured is not kept at one type level.
   The text alternates between model states as points in a statistical
   manifold, laws over model states, and belief distributions over latent
   world-states.
2. The global Fisher-Rao `C=2` claim uses the Hellinger/Bhattacharyya spherical
   arc identity as if it were the intrinsic Fisher-Rao geodesic on an arbitrary
   statistical manifold. That identity is valid for the ambient full
   distribution space/simplex, not for arbitrary parametric submanifolds.
3. The Cencov uniqueness claim is overgeneralized from the appropriate
   categorical setting to an arbitrary `M`.
4. The architectural factorization is driven by the assumed bounded
   attenuation ratio `H_kappa`; for Class 3 architectures it is not derived.
5. The LLM/hallucination framing is much stronger than the paper's actual
   theorem, which is a conditional bound on distributional displacement by
   transferred goal information.

My recommendation is to revise toward a more modest and defensible claim:

> A conditional information-geometric bound on goal-conditioned post-update
> displacement, with an LLM/sycophancy application through observable
> goal-conditioned response distributions.

That version could be publishable if the type-level geometry is fixed and the
framing is made less sweeping. In the current form, a theory reviewer is likely
to see the main inequalities as standard once the definitions are unwrapped,
then attack the LLM connection and the global Fisher-Rao/Cencov claims.

## Major mathematical findings

### 1. The paper has a type-level ambiguity in its central object

Relevant lines:

- `src/re/03-setup.md:3`: `M_{tau+}` is a random element of a parameter manifold.
- `src/re/03-setup.md:9`: the bias is defined as a distance between laws
  `P_{M+|G,e,M-}` and `P_{M+|e,M-}`.
- `src/re/03-setup.md:11`: the same symbol `d_M` is said to mean either `W_2`
  on an induced model-distribution or Fisher-Rao on a statistical manifold.
- `src/re/03-setup.md:55`: H1 says each model state `M_t` corresponds to a
  probability distribution over latent world-states.
- `src/re/E-proofs.md:77`: the Track 2 proof applies Fisher-Rao directly to
  `P_{M+|G}` and `P_{M+}`.

These are different kinds of objects:

1. `M_t` as a point in a parameter/statistical manifold.
2. `P_{M_t}` as the belief distribution represented by that point.
3. `P_{M+|G}` as a law over random model states.
4. `P_{M+}` as a mixture law over random model states.

Fisher-Rao geometry naturally applies to probability distributions in a
statistical model. Wasserstein naturally applies to laws over a metric state
space. The manuscript currently moves between these without a single formal
construction tying them together. This is the highest-priority fix because it
affects every Track 2 theorem.

Concrete fix options:

1. Make Track 1 the theorem about laws over model states:
   `P_{M+|G}` and `P_{M+}` live in `P(M)`, with a ground metric on `M`.
2. Make Track 2 a theorem about distributions themselves:
   for each goal `g`, the post-update belief distribution is a point
   `Q_g` in a statistical manifold, the baseline is a point `Q_0`, and the
   random variable is `d_FR(Q_G,Q_0)`. Then separately define what `Q_0` is.
3. Or make Track 2 a theorem about the family of laws over random model states,
   but then H1 and all Cencov/Fisher-Rao statements must be about that
   higher-order family, not about beliefs over latent world-states.

Do not keep all three interpretations active.

### 2. The global Fisher-Rao backstop is overclaimed

Relevant lines:

- `src/re/04-main-results.md:18`: global `C=2` under `(PI)` alone.
- `src/re/D-track2-companions.md:9-17`: theorem and proof.
- `src/re/D-track2-companions.md:39-41`: convention and claim that the regimes
  share the same intrinsic geometry.
- `src/re/D-track2-companions.md:45-49`: chord-arc lemma.

The proof uses

`d_FR(P,Q) = 2 arccos int sqrt(pq)`.

That is the spherical arc distance under the square-root embedding for the
ambient full space of probability distributions, or for the full simplex with
the standard Fisher metric. It is not, in general, the intrinsic Fisher-Rao
geodesic distance on an arbitrary parametric statistical manifold or curved
submanifold. On a submanifold, the intrinsic geodesic constrained to the model
can be strictly longer than the ambient spherical arc, or may fail to exist
within the submanifold between the two endpoints.

This matters because the theorem is stated under H1 and PI for general
statistical-manifold sub-cases. H1 does not say the manifold is the full simplex
or full nonparametric distribution space.

Concrete fix:

1. Restate the global theorem as a bound for the ambient Hellinger/Bhattacharyya
   arc metric, not the intrinsic Fisher-Rao geodesic on arbitrary `M`; or
2. Add a strong hypothesis that `M` is geodesically convex/full under the
   square-root embedding, so the spherical arc is the relevant distance; or
3. Demote the global `C=2` result to an appendix as a companion metric result,
   not part of the main Fisher-Rao theorem.

Do not claim "under PI alone" that Fisher-Rao is forced globally. PI alone does
not define a Riemannian metric, and the current proof is really a
Hellinger/Bhattacharyya arc argument.

### 3. Cencov uniqueness is applied too broadly

Relevant lines:

- `src/re/03-setup.md:37-40`: PI definition.
- `src/re/04-main-results.md:53-60`: uniqueness theorem.
- `src/re/E-proofs.md:121-122`: proof invokes Cencov on `M`.

Cencov's theorem is a uniqueness theorem for monotone Riemannian metrics under
congruent Markov embeddings/sufficient statistics in the appropriate category
of statistical models. It does not automatically say that, for any arbitrary
statistical submanifold `M` appearing in H1, the metric on that fixed `M` is
uniquely Fisher-Rao merely because the paper asks for PI.

The manuscript tries to patch this by saying "full Markov-morphism strength,"
but the formal H1 theorem statement still reads as if the result holds on any
local statistical manifold. A reviewer familiar with information geometry will
likely object.

Concrete fix:

1. Strengthen the formal assumption: the metric assignment is a natural
   monotone Riemannian metric over the relevant category of finite or standard
   statistical models, not just a metric on one fixed `M`.
2. Then say the induced metric on the manuscript's model family is Fisher-Rao.
3. Stop saying "no further freedom" unless the categorical assumption is fully
   explicit.

### 4. The local Fisher-Rao proof requires both endpoints to lie in one smooth model

Relevant lines:

- `src/re/04-main-results.md:23-24`: H4 prime.
- `src/re/05-mechanism.md:28-35`: local expansion.
- `src/re/E-proofs.md:75-83`: full proof.
- `src/re/E-proofs.md:125`: sharpness witness uses a Gaussian mixture as the
  goal-marginal baseline.

The KL-to-Fisher-Rao expansion applies to nearby points in a smooth statistical
model. But the baseline `P_{M+|e,M-}` is a goal mixture of the conditional laws.
Even if every `P_{M+|G=g}` is in a parametric family, the mixture generally is
not in the same family.

The conjugate-Gaussian sharpness witness makes this visible: two equal-variance
Gaussian slices mix to a two-component Gaussian mixture, not to an
equal-variance Gaussian. The text says the mixture is approximately Gaussian to
leading order, which is fine for an asymptotic witness, but it is not the exact
manifold statement used in the theorem.

Concrete fix:

1. Add a hypothesis that the goal-marginal baseline also lies in the same
   statistical manifold and that all slices are connected to it by a local
   chart/geodesic.
2. Or define the baseline as a Fisher-Rao barycenter/projection in the manifold,
   then separately bound the projection error.
3. Or make the local Track 2 theorem explicitly an asymptotic/tangent-space
   statement, not a finite-distance theorem between arbitrary mixture laws.

### 5. The Stuart-school reduction does not prove H2 prime as stated

Relevant lines:

- `src/re/E-proofs.md:40-57`: Stuart-school reduction theorem.
- `src/re/E-proofs.md:49`: C4 assumes pairwise W2 control of conditional data
  laws.
- `src/re/E-proofs.md:62-64`: proof asserts this gives `T_2` for the conditional
  data law and then for the post-update law.

The pushforward lemma is fine: if `mu` satisfies `T_2(C)` and `T` is
Lipschitz, then `T_* mu` satisfies `T_2(L^2 C)`.

The problem is Step 1. C4 gives a pairwise Wasserstein bound between
`P_{Omega|theta1}` and `P_{Omega|theta2}`. That is not the same as saying the
goal-marginal law `P_Omega` satisfies a Talagrand `T_2` inequality. Mixtures of
nice `T_2` distributions can have much worse concentration constants, and
multimodality can break the advertised constant.

Concrete fix:

1. Replace C4 with a direct assumption that the actual conditional/marginal data
   law used in the cascade satisfies `T_2(2/rho_noise)`.
2. Or prove a mixture/convolution/tensorization lemma with explicit constants
   for the specific generative setup.
3. Rephrase "recovers the canonical Stuart-school cascade generically" to
   "recovers it in the cases where the post-update law inherits the required
   `T_2` concentration."

### 6. The `T_1` fallback constant is inconsistent with the displayed inequality

Relevant lines:

- `src/re/B-hypothesis-verification.md:24-28`.

The text derives

`W_1 <= D sqrt(KL/2)`.

If using the same squared convention as H2 prime, this is

`W_1^2 <= (D^2/2) KL`.

The line then says `C_T1 = D^2/4`. That value corresponds to the alternate
Bobkov-Goetze convention `W_1 <= sqrt(2 C KL)` with `C = D^2/4`. Both
conventions are common, but the manuscript mixes them. Since the main theorem
uses `W_2^2 <= C_T2 KL`, the analogous `T_1` constant should be `D^2/2`, or the
convention should be explicitly changed.

### 7. The architectural factorization is not yet a theorem about LLMs

Relevant lines:

- `src/re/01-introduction.md:21-25`: headline factorization.
- `src/re/03-setup.md:27-31`: definition of `kappa_processing`.
- `src/re/04-main-results.md:68-86`: H_kappa and corollary.
- `src/re/B-hypothesis-verification.md:42-60`: sufficient conditions and parrot
  witness.

The factorization is mathematically immediate once

`kappa_processing = I(G;M+|e,M-) / I(G;Omega|e,M-)`

is defined and bounded. For Class 3 architectures, the boundedness is assumed
via H_kappa, not derived from transformer structure. The paper correctly admits
this in places, but the abstract and introduction still sell the factorization
as the operational headline.

There is also a conceptual risk: the empirical referent is sycophancy, but in
many sycophancy cases the user's goal or preferred answer is not information
about the latent truth `Omega`. The paper's own parrot witness is exactly the
case `I(G;Omega|e,M-) = 0` and `I(G;M+|e,M-) > 0`. That means the factorized
bound fails for an important class of sycophancy-like behavior unless additional
modeling makes `G` informative about `Omega`.

Concrete fix:

1. Make the unconditional transferred-information bound the main operational
   theorem.
2. Present the `kappa x ambiguity` form as a corollary for regimes where goals
   are truth-informative or where a separate model proves H_kappa.
3. For sycophancy, lead with the binary-uniform JSD estimator of
   `I(G;M+|e,M-)`, not with `I(G;Omega|e,M-)`.

### 8. The Class 1 data-processing claim needs a formal conditional DAG

Relevant lines:

- `src/re/03-setup.md:31`.
- `src/re/04-main-results.md:82`.
- `src/re/B-hypothesis-verification.md:44`.

The text says Class 1 gives the Markov chain

`G -> Omega_tau -> M_{tau+}` conditional on `(e_tau,M_{tau-})`.

But a separated Bayesian update usually maps `(e_tau,M_{tau-})` to `M_{tau+}`.
After conditioning on `e_tau` and `M_{tau-}`, there may be no remaining
dependence on `Omega_tau`, and `M_{tau+}` may be deterministic or independent
of `G`. If `M_{tau+}` instead depends on the latent `Omega_tau` directly, that
is a different generative model from the usual inverse-problem update from
observations.

This may be fixable, but the manuscript needs an explicit conditional DAG and a
clear statement of whether `e_tau` is fixed data, a random observation, or part
of the update kernel. Otherwise the DPI step will look hand-waved.

### 9. The architecture lemma proves graph reachability, not influence magnitude or belief coupling

Relevant lines:

- `src/re/01-introduction.md:27`.
- `src/re/03-setup.md:63-79`.
- `src/re/E-proofs.md:146-170`.

The graph-reachability claim for transformers is essentially true under
nondegenerate attention, but it is weak: it establishes a possible directed path
from goal tokens to downstream activations. It does not establish meaningful
causal effect, mutual information transfer, belief-state interpretation, or a
finite `kappa_processing`.

The appendix caveats acknowledge this, but the main-text rhetoric still says
"belief-goal-coupling structure" and "Coupled by construction" as if the lemma
does more than it does. In a NeurIPS review, this is likely to be seen as a
trivial observation about causal attention unless it is tied to a measurable
quantity.

Concrete fix:

1. Keep the transformer reachability lemma, but lower its status.
2. Move the Mamba/RWKV/RetNet/Hyena instantiations to appendix unless all
   architecture papers are cited and the assumptions are exact.
3. State plainly: "This proves structural reachability only; all quantitative
   coupling is represented by `I(G;M+)` or by the additional H_kappa assumption."

### 10. Track 1 "generalizes Stuart-school beyond Class 1" is too strong

Relevant lines:

- `src/re/01-introduction.md:19`.
- `src/re/04-main-results.md:34`.
- `meta.md:15`.

The unconditional Track 1 theorem holds for any architecture whose post-update
law satisfies H2 prime. That is true but mostly tautological: H2 prime is the
hard regularity condition. The manuscript only gives a Stuart-school
verification path in the Class 1/separated setting. It does not prove that
goal-coupled architectures inherit H2 prime from the Stuart-school hypotheses.

Concrete fix:

Say:

> Track 1 uses the same transport cascade and applies to goal-coupled
> post-update laws whenever their concentration can be verified. The standard
> Stuart-school hypotheses verify this in the separated case.

Do not say it "generalizes the canonical Stuart-school cascade beyond Class 1"
unless you add a coupled-architecture concentration theorem.

### 11. The no-go is valid but rhetorically overused

Relevant lines:

- `src/re/04-main-results.md:38-45`.
- `src/re/05-mechanism.md:41-50`.
- `src/re/E-proofs.md:91-115`.

The chart-rescaling no-go is correct and useful. It proves that no
coordinate-independent universal constant can hold for arbitrary Euclidean chart
norms. It does not, by itself, force Fisher-Rao. It only forces some intrinsic
commitment. Fisher-Rao follows only after adding the Cencov/Riemannian/KL
normalization assumptions.

Concrete fix:

Replace phrases like "the no-go tells us exactly what to commit to" with:

> The no-go rules out arbitrary Euclidean chart norms. Under the additional
> PI+R+K commitment, Cencov then selects Fisher-Rao.

This is both accurate and harder to attack.

## Framing and publishability

### Current title and abstract overpromise

Relevant lines:

- `meta.md:2`: title.
- `meta.md:9-15`: abstract.

"How Much Can LLMs Hallucinate?" strongly suggests a semantic or behavioral
upper bound on hallucination severity in deployed LLMs. The paper actually
proves conditional bounds on distributional displacement under a particular
goal-conditioned update model. The current title invites reviewers to reject
the paper for not measuring semantic hallucination, truth distance, deployed
LLM behavior, or actual hidden belief updates.

Safer title options:

1. "Bounding Goal-Conditional Belief Displacement by Transferred Information"
2. "Information-Geometric Bounds for Goal-Coupled Bayesian Updates"
3. "Goal Coupling, Ambiguity, and Post-Update Displacement in Probabilistic
   Models"

If "LLM hallucination" must remain in the title, use a subtitle that makes the
scope explicit:

> A conditional information-geometric bound for goal-induced response
> displacement

### The abstract is too dense and too absolute

The abstract currently stacks Cencov, two Fisher-Rao constants, a no-go theorem,
Stuart-school transport, architecture classes, transformer reachability, and a
JSD estimator. It reads like a proof inventory rather than a NeurIPS abstract.
It also foregrounds the most vulnerable claims.

Suggested abstract shape:

1. One sentence: frequency lower bounds do not quantify goal-induced response
   displacement.
2. One sentence: define the quantity and the transferred-information identity.
3. One sentence: state the two conditional metric bounds with hypotheses.
4. One sentence: state the architecture corollary as conditional on H_kappa.
5. One sentence: state the transformer reachability and binary JSD diagnostic.
6. One sentence: limitations: theory-only, belief-state interpretation
   conditional.

Draft:

> We study goal-conditioned update mechanisms and ask how far the post-update
> model state can move from its goal-marginal baseline. For a fixed event and
> prior state, the chain rule identifies the average slice KL with transferred
> goal information, `I(G;M+|e,M-)`. Consequently, any post-update law satisfying
> a Talagrand `T_2` inequality obeys a `W_2` displacement bound, and any local
> Fisher-Rao statistical-manifold regime obeys a `sqrt(2)` small-information
> bound. Under an additional bounded-attenuation assumption, the bound factors
> into an architectural transfer coefficient and a residual ambiguity term.
> We use a graph-reachability lemma to classify decoder-only attention as
> structurally goal-coupled, and note that binary goal probes estimate the
> transferred-information term by Jensen-Shannon divergence. The result is a
> conditional theory of goal-induced distributional displacement, not a semantic
> metric on false outputs.

### Novelty risk

Reviewers may see the central theorem as a direct consequence of:

1. Chain rule for mutual information.
2. Talagrand transportation inequality.
3. Local KL/Fisher expansion.
4. Jensen.

That does not make the paper worthless, but it means the novelty must be framed
as:

1. Defining the right goal-conditioned bias quantity.
2. Connecting it to transferred goal information.
3. Separating transferred-information bounds from architectural factorization.
4. Providing a careful LLM/sycophancy diagnostic interpretation.

Avoid presenting the inequality itself as the main mathematical novelty.

### LLM connection risk

The paper says the LLM connection is via in-context-learning correspondence and
structural attention reachability. That is not enough to claim an upper bound on
"LLM hallucination" in the ordinary semantic sense. It is enough to claim an
upper bound on a modeled response-distribution displacement, conditional on an
implicit-posterior reading.

The limitation in `src/re/01-introduction.md:11` is good and should be moved
earlier, perhaps into the abstract. The conclusion's phrase "mathematically
airtight via Cencov" (`src/re/06-conclusion.md:7`) should be softened until the
Cencov/global issues are fixed.

## Citation audit

### Mechanical citation check

Every LaTeX citation key used in `src/re/*.md` appears in
`llm-hallucinate-neurips-2026.extracted.bib`. I did not find missing citation
keys from `\cite{...}` commands.

### Non-mechanical citation problems

1. `src/re/F-related-work-extended.md:33` names "Su-Kempe-Ullrich 2024" in
   plain text with no citation command and no BibTeX entry.
2. `src/re/D-track2-companions.md:39` names "Csiszar 1967; Liese-Vajda 1987"
   with no citation commands and no BibTeX entries.
3. The architecture claims cite only linear attention. Mamba, RWKV, RetNet,
   Hyena/long-convolution, FlashAttention, RMSNorm, and GroupNorm should be
   cited if they remain in the main theorem/corollary.
4. Several BibTeX entries are low-quality or stale:
   - `kalai-2023-calibrated` has year 2023 but the STOC proceedings are STOC
     2024, pages 160-171, DOI `10.1145/3618260.3649777`.
   - `wu-grama-szpankowski-2024` is listed as ICLR with year 2024, but the
     conference version is ICLR 2025. The arXiv date is 2024.
   - `suzuki-2025-hallucinations` appears to have the exact arXiv title
     "Hallucinations are inevitable but statistically negligible" and arXiv
     `2502.12187`; update the title/key/note.
   - `biau-2026-note`, `guo-2026-hallucination`, `hyeon-2026-actionsufficient`,
     `seo-lee-sim-2026-tangent`, and similar entries should include arXiv IDs
     or venue status.
   - `bakry-1985-diffusions` is not a book entry as currently formatted.
   - `cattiaux-2021-functional` has journal metadata embedded in a partial
     string; fix volume/pages/year.
   - `liu-2025-hallucinations` has malformed author formatting and the arXiv ID
     in the title field.

### Web spot-checks

I verified the existence/status of a subset of recent and high-risk references:

1. Kalai and Vempala, "Calibrated Language Models Must Hallucinate", STOC 2024:
   https://doi.org/10.1145/3618260.3649777
2. Kalai/Nachum/Vempala/Zhang, "Evaluating large language models for accuracy
   incentivizes hallucinations", Nature 2026 DOI:
   https://doi.org/10.1038/s41586-026-10549-w
3. Wu/Grama/Szpankowski, "No Free Lunch...", ICLR 2025:
   https://proceedings.iclr.cc/paper_files/paper/2025/hash/f2a11632520f4b7473d7838f074a7d25-Abstract-Conference.html
4. Sharma et al., sycophancy paper, arXiv `2310.13548`:
   https://arxiv.org/abs/2310.13548
5. Guo/Li, rate-distortion membership-testing paper, arXiv `2602.00906`:
   https://arxiv.org/abs/2602.00906
6. Zeng et al., HalluGuard, arXiv `2601.18753`, apparently ICLR 2026:
   https://arxiv.org/abs/2601.18753
7. Biau/Boyer, k-NN gating in RAG, arXiv `2601.13744`:
   https://arxiv.org/abs/2601.13744
8. Seo/Lee/Sim, tangent-linearized Gaussian inference, arXiv `2602.19179`:
   https://arxiv.org/abs/2602.19179
9. Sheng et al., mean-field VI stability, arXiv `2506.07856`:
   https://arxiv.org/abs/2506.07856
10. Del Moral, Sinkhorn/Schrodinger bridges via LSI, Stochastic Analysis and
    Applications 2026:
    https://doi.org/10.1080/07362994.2026.2619443

Recommendation: make the related-work section explicitly distinguish
peer-reviewed work from arXiv/preprint work. For a NeurIPS theory submission,
stale or malformed citations will damage trust quickly.

## Page-limit triage

The fastest cuts that preserve the paper's best version:

1. Move almost all of `src/re/D-track2-companions.md` to appendix/supplement.
   In main, keep only one sentence: global Hellinger/BC-arc companion bounds are
   available outside H4 prime. Do not foreground the global FR `C=2` until fixed.
2. Move all named architecture instantiations beyond plain transformer
   attention to appendix. In main, keep only the transformer graph-reachability
   lemma and the caveat that it is reachability, not magnitude.
3. Move the no-go proof fully to appendix. Main text needs only the statement
   and one sentence explaining chart rescaling.
4. Cut most theorem remarks in `src/re/04-main-results.md:26-36` and
   `src/re/04-main-results.md:78-86`. Keep only hypothesis-critical remarks.
5. Move `src/re/C-conjugate-gaussian-numerics.md` entirely to appendix.
6. Consider dropping `src/re/A-failed-routes.md` from the submitted supplement
   unless page/supplement budget is generous. It is useful internally, but it
   advertises exploratory dead ends.
7. Keep `src/re/F-related-work-extended.md` as supplement only. The main related
   work should be 4-6 paragraphs with one precise gap statement.
8. Shorten the introduction by removing repeated claims that "the two
   literatures do not engage"; say it once, then state the theorem.

Best main-paper structure:

1. Introduction and scope limitation.
2. Setup and bias quantity.
3. Chain-rule lemma and umbrella theorem.
4. Track 1 and local Track 2 theorem statements.
5. Architectural corollary and binary JSD diagnostic.
6. Transformer reachability lemma, stated modestly.
7. Related work.
8. Limitations/conclusion.

## Specific rewrite priorities

1. Define the mathematical object exactly once. Is the metric between random
   parameter laws, between belief distributions, or between points in a
   statistical manifold?
2. Fix Track 2 before editing prose. In particular, decide whether the global
   result is intrinsic Fisher-Rao or extrinsic Hellinger/BC arc.
3. Reframe `H_kappa` as an additional modeling assumption, not as an
   architecture-derived result for transformers.
4. Make the binary JSD estimator central. It is the most operational and least
   overclaimed bridge to empirical LLM work.
5. Replace "hallucination size" with "goal-induced response/belief
   displacement" throughout the theorem statements. Keep "hallucination" in the
   motivation, not in the formal object.
6. Add a table of hypotheses with "what it buys" and "where it is verified".
   Reviewers need to see immediately which results are unconditional, which are
   local, and which are assumptions.
7. Update the bibliography from authoritative sources before submission.

## Likely reviewer objections and preemptive fixes

1. "This is not an LLM hallucination bound."  
   Fix by saying it is a bound on one modeled channel: goal-induced
   distributional displacement.

2. "The main theorem is a standard consequence of T2/KL/Jensen."  
   Fix by making the contribution the modeling decomposition and diagnostic,
   not the inequality alone.

3. "Cencov is being overapplied."  
   Fix the formal categorical assumption or narrow the claim.

4. "The global Fisher-Rao identity is false on arbitrary submanifolds."  
   Fix by using ambient Hellinger/BC arc or adding a full-simplex/geodesic
   convexity assumption.

5. "The transformer lemma is trivial and does not prove influence."  
   Fix by explicitly calling it graph reachability and making quantitative
   influence entirely an information term to be measured/assumed.

6. "No experiments."  
   For NeurIPS, either include a small binary-goal JSD probe on a sycophancy
   benchmark, or be very clear that this is a theory paper whose empirical
   contribution is a diagnostic formula. A small experiment would materially
   improve publishability.

## Bottom line

The promising paper is inside the current one, but it is narrower:

> Transferred goal information controls goal-conditional post-update
> displacement under standard metric/concentration assumptions; architectural
> structure determines whether and how much goal information can enter the
> update, but the quantitative transfer must be measured or assumed.

That is a defensible NeurIPS theory story. The current story says "how much can
LLMs hallucinate?" and "Cencov forces universal constants globally"; those are
the claims most likely to draw rejection unless narrowed or repaired.
