# De novo audit — 03-llm-hallucinate-bound

**Date:** 2026-05-06
**Auditor:** Claude (claude-opus-4-7, 1M context)
**Scope:** Math correctness · argument strength / overclaims · prose & structure · loose citation / prior-art notes
**Method:** First-hand read of all main-body and appendix segments via `OUT.llm-hallucinate-neurips-2026.md` manifest order; PDF used for layout / formatting spot-checks. No prior audits in `audits/` opened.

I verified the load-bearing math: the chain-rule identity, the chord-arc lemma's convexity argument, the Čencov-uniqueness reduction to $C = \sqrt 2$ under (K), the no-go's chart-rescaling, the Hellinger backstop, and the conjugate-Gaussian numerics. All check out. The Track 1 / Track 2 / Hellinger / chord-arc family of bounds is internally consistent and the constants align across the segments where they're cross-referenced.

The findings below are mostly tightening. Two deserve specific attention: M2 (the (H4$'$) hypothesis is uncomfortably strong for the LLM regime the architectural reading targets, and this gap should be more visible in the intro) and S3 ("Track 5.5" appears in the conjugate-Gaussian appendix with no anchor in the main text — looks like leftover from an earlier numbering).

A general note up front: the *failed-routes documentation* (A-failed-routes.md) and the *three-no-gos disambiguation* (Strand 4 in F-related-work-extended.md, Owhadi-Scovel-Sullivan vs. Track 2's no-go vs. Čencov) are model-grade examples of negative-results discipline. I'd protect both from any compression pass.

---

## §1 — Math correctness / load-bearing derivations

### M1 — `(H4$'$)` uniform-locality is essential to the headline $\sqrt 2$ and substantially restrictive

*Primary location:* `src/re/03-setup.md:19–20` (hypothesis statement); `src/re/04-main-results.md:20`; `src/re/05-mechanism.md:31` (where it gates the locally-tight expansion).

The statement of (H4$'$) is honest:

> $\mathrm{ess\,sup}_g\,\mathrm{KL}(P_{M_{\tau^+}\mid e, M, G=g}\,\|\,P_{M_{\tau^+}\mid e, M}) \le \delta_\star$ for some $\delta_\star \in (0, 1)$. Every goal-conditional slice — not merely the average — is uniformly close to the goal-marginal. (H4$'$) is strictly stronger than $\mathbb{E}_G[\mathrm{KL}_g] = I \ll 1$; small mean does not imply small ess-sup.

The "strictly stronger than small mean" caveat is exactly right. But the LLM use case the architectural reading targets — Class 3 (Coupled) transformer — is precisely the regime where goal-conditional slices can be *very* far apart for individual rare goals (jailbreaks, adversarial prompts, persona injection). A single rare $g$ with large $\mathrm{KL}_g$ violates (H4$'$) regardless of the average.

The paper handles this honestly — Track 2 has globally-valid backstops at $\pi/\sqrt{2}$ ([[#^thm-track2-global]]) and Hellinger at $1/\sqrt{2}$ ([[#^thm-hellinger]]) under (H1)+(PI) only, no (H4$'$) — but the headline $\sqrt 2$ constant in Theorem 1's Track 2 statement (`04-main-results.md:14`) and in the contributions paragraph (`01-introduction.md:33`) is *only available under (H4$'$)*. A reviewer will read "universal, dimension-free, no domain-specific parameters" and then encounter (H4$'$) and feel the universality claim was overstated.

**Recommended (strengthening rather than softening):** the headline rate statement in the contributions section and the conclusion should say "$\sqrt 2$ (under uniform-local regime; $\pi/\sqrt 2$ universally without it)" — making the global backstop part of the headline rather than a footnote. The current framing positions the global $\pi/\sqrt 2$ as a fallback, but for the LLM application it's likely the *operating* bound, not a backstop. Strengthening: rebrand as "two universal Fisher-Rao constants — locally-tight $\sqrt 2$ in the uniform-local regime, globally-valid $\pi/\sqrt 2$ throughout — both forced by Čencov."

This is a presentation issue, not a math issue: the math is fine; the rhetorical weight on $\sqrt 2$ relative to $\pi/\sqrt 2$ is currently disproportionate to which one applies in the target regime.

### M2 — The bias quantity notation $\|P, Q\|_{\mathcal M}$ is non-standard

*Primary location:* `src/re/03-setup.md:9` (eq-bias-quantity).

$$\|\Delta M_{\text{bias}}(G)\| := \|P_{M_{\tau^+}|e, M_{\tau^-}, G},\; P_{M_{\tau^+}|e, M_{\tau^-}}\|_{\mathcal{M}}$$

Reads as a norm of two distributions separated by a comma, which isn't standard. The intent is a metric distance: $d_{\mathcal M}(P, Q)$ or $\|P - Q\|_{\mathcal M}$ for the metric/norm reading. A reviewer hits this in §3 and has to pause to figure out what's meant. Replace with $d_{\mathcal{M}}(P, Q)$ throughout — the body text already uses $W_2(P, Q)$ and $d_{FR}(P, Q)$ which compose cleanly with the `d`-notation.

### M3 — `lem-chord-arc` proof is correct; one notational detail worth flagging

*Primary location:* `src/re/D-track2-companions.md:44–45`.

The proof argues $\phi(h) = g(h)/h$ with $g(h) = 4\arcsin(h/\sqrt 2)$, $g(0) = 0$, $g$ strictly convex, hence $\phi$ monotonically increasing on $(0, \sqrt 2)$, with $\phi(0^+) = g'(0) = 4/\sqrt 2 = 2\sqrt 2 \approx 2.83$ and $\phi(1) = g(1) = 4\arcsin(1/\sqrt 2) = 4 \cdot \pi/4 = \pi$.

Verified all four steps. ✓

One detail: the convex-secant-monotonicity is for $\phi(h) = (g(h) - g(0))/(h - 0)$; the standard statement requires $g$ convex with the secant-from-a-fixed-point monotone in the moving point. The version used here (from the origin) needs $g(0) = 0$ to get the slope-monotonicity directly. This is satisfied; just worth one explicit line stating "since $g(0) = 0$, $\phi(h) = g(h)/h$ is the secant slope from the origin, which is monotone increasing for convex $g$." Cleaner for a reviewer.

The limit $\phi(0^+) = 2\sqrt{2}$ is interesting but not load-bearing — the bound $d_{FR} \le \pi \mathrm{Hel}$ is achieved at the antipode $\mathrm{Hel} = 1$, so the small-Hel slope $2\sqrt 2$ is just a loose lower bound on the constant. Worth noting in passing that this means the local-Hellinger-to-Fisher-Rao conversion ratio is $2\sqrt 2$ in the small limit (which is consistent with the local proportionality $\mathrm{Hel} \approx d_{FR}/(2\sqrt 2)$ noted in line 47 of the same segment).

### M4 — The KL-to-Fisher-Rao expansion's remainder bound

*Primary location:* `src/re/E-proofs.md:39` (proof of Track 2):

> Under (H4$'$) the remainder is controlled uniformly: with bounded Amari-Chentsov tensor $|T_{ijk}\delta^i\delta^j\delta^k| \le \mathcal{T}_\star\|\delta\|^3$ on the goal-induced neighborhood and minimum Fisher eigenvalue $\mathbf{I}_{\min} > 0$, the slice-wise inequality $d_{FR}^2(P_{M_{\tau^+}\mid G=g}, P_{M_{\tau^+}}) \le 2\,\mathrm{KL}_g(1 + R_3(\delta_\star))$ holds with $R_3(\delta_\star) = (\mathcal{T}_\star/3)\sqrt{2\delta_\star/\mathbf{I}_{\min}^3} \to 0$ as $\delta_\star \to 0$.

This is the part of the locally-tight Track 2 derivation that converts $(1 + o(1))$ into an explicit bound. The formula for $R_3(\delta_\star)$ is plausible (third-order remainder controlled by the cubic tensor and minimum Fisher eigenvalue) but I want to flag a few things for verification by the per-paper agent:

1. The Amari-Chentsov tensor $T_{ijk}$ doesn't have an explicit reference here. Worth citing Amari-Nagaoka §5 (where the tensor lives) for readers wanting to verify the constant.
2. The $\sqrt{2\delta_\star/\mathbf{I}_{\min}^3}$ scaling: $\delta_\star$ is the ess-sup KL, which by KL-to-Fisher gives $\|\delta\|_{\text{geodesic}} \approx \sqrt{2\delta_\star}$ at second order, so $\|\delta\|^3 \approx (2\delta_\star)^{3/2}$. The cubic remainder is $(\mathcal T_\star/3) \|\delta\|^3 \le (\mathcal T_\star/3)(2\delta_\star)^{3/2}$. Dividing by $\mathrm{KL}_g \approx \delta_\star$ gives $(\mathcal T_\star/3) \cdot \sqrt{2\delta_\star} \cdot 2^{1/2} = (\mathcal T_\star/3) \sqrt{8\delta_\star}$. The $\mathbf{I}_{\min}^{-3/2}$ factor would arise if $\|\delta\|$ in geodesic-distance differs from $\|\delta\|$ in coordinates by $\mathbf{I}_{\min}^{-1/2}$. Plausibly correct, but worth a one-line derivation in the appendix so a reviewer can check.

The headline statement (Track 2 gives $C = \sqrt 2$ in the locally-tight regime) holds; the explicit $R_3$ formula is what makes the $(1+o(1))$ quantitative.

### M5 — Track 2 global backstop's $\pi/\sqrt 2$ proof composes cleanly

*Primary location:* `src/re/D-track2-companions.md:17`.

The proof composes (i) `lem-chord-arc` ($d_{FR} \le \pi \mathrm{Hel}$ globally) with (ii) Tsybakov Lemma 2.4 ($2\mathrm{Hel}^2 \le \mathrm{KL}$) to get $d_{FR}^2 \le (\pi^2/2)\mathrm{KL}$, then chain rule + Jensen → $\mathbb E[d_{FR}] \le (\pi/\sqrt 2)\sqrt{I_M}$. Verified each step. ✓

The "$\pi/2 \approx 1.57$ overhead vs. the locally-tight $\sqrt 2$ is exactly the worst-case arc-chord ratio" observation (line 19) is geometrically correct: at the antipode of the unit $L^2$-sphere, the arc length is $\pi$ and the chord length is $\sqrt 2$ (the diameter is $\sqrt 2$ in the unit-sphere normalization), so the ratio is $\pi/\sqrt 2 \cdot \sqrt 2/\sqrt 2 = \pi/\sqrt 2$. The "$\pi/2$" framing is the *additional* slack vs. $\sqrt 2$ ($\pi/\sqrt 2 / \sqrt 2 = \pi/2$). ✓

### M6 — Conjugate-Gaussian numerics: setup ambiguity around $\Omega | G$

*Primary location:* `src/re/C-conjugate-gaussian-numerics.md:3`:

> latent $\theta \sim \mathcal{N}(0, \tau^2)$, observation channel $\Omega | \theta \sim \mathcal{N}(\theta, \sigma^2)$, goal-conditional likelihood-mean shift $\Omega | G \sim \mathcal{N}(\beta(G), \sigma^2)$.

Two interpretations:

- (a) Direct: $\Omega | G$ is sampled as $\mathcal N(\beta(G), \sigma^2)$, ignoring $\theta$. Then variance $\sigma^2$.
- (b) Marginal-over-$\theta$: $\Omega | G \sim \int_\theta P(\Omega | \theta + \beta(G)) P(\theta) d\theta = \mathcal N(\beta(G), \sigma^2 + \tau^2)$. Then variance $\sigma^2 + \tau^2$.

The variance $L_{\text{post}}^2 \sigma^2$ in line 3 ("post-update parameter law $\mu_+ | G \sim \mathcal{N}(L_{\text{post}}\beta(G),\, L_{\text{post}}^2\sigma^2)$") is consistent with (a): given $G$, the agent observes $\Omega \sim \mathcal N(\beta(G), \sigma^2)$ directly, applies $\mu_+ = L_{\text{post}}\Omega$, gets $\mathrm{Var}(\mu_+|G) = L_{\text{post}}^2 \sigma^2$. ✓

But (a) is a slightly weird setup: it treats $\Omega$ as goal-determined rather than world-determined. The more natural reading would be: the goal *biases* the observation mean (e.g., a sycophantic data source whose biased report depends on what the user asked) on top of $\theta$. Worth a one-line clarification: "for this minimal example we treat $\Omega | G$ as goal-determined directly; the world-state $\theta$ enters only via the agent's prior, not the observation."

The math then checks out; the algebra produces $L_{\text{post}}\sigma$ as the Fisher-Rao-to-Euclidean conversion factor, bounded by $\tau/2$ uniformly with limits to zero in both prior-dominant and likelihood-dominant regimes. Good demo.

### M7 — Track 1's conjugate-Gaussian Stuart-school recovery

*Primary location:* `src/re/C-conjugate-gaussian-numerics.md:9–17`.

The Track 1 cascade gives $C_{T_2} = 2/\rho_{\text{post}} = 2 L_{\text{post}}^2 \sigma^2 = 2\tau^4 \sigma^2/(\sigma^2+\tau^2)^2$, which can be rewritten as $2 L_{\text{post}}^2 / \rho_{\text{LSI}}$ with $\rho_{\text{LSI}} = 1/\sigma^2$. The claim "the canonical Stuart-school cascade constant" matches. I'd ask the per-paper agent to spot-check that Stuart 2010's cascade constant is in fact $2L_{\text{post}}^2/\rho_{\text{LSI}}$ in the form invoked — the connection is plausible from Acta Numerica 2010 §6 but I don't have the exact form in memory.

### M8 — `lem-attention-coupled` proof is graph-reachability and that's exactly the right grade

*Primary location:* `src/re/03-setup.md:63–66`; full proof at `src/re/E-proofs.md:91–112`.

The lemma claims: under non-degenerate attention, every position downstream of the goal positions has a directed-graph path back to a goal position in the input. The proof is induction on layer depth using the residual stream + attention edges. ✓

The honesty in the three caveats (`E-proofs.md:114–118`) is excellent:
- "Graph reachability is not the same as causal-influence magnitude."
- "Causal masking restricts the lemma's scope to downstream positions."
- "Sparse and sliding-window attention require a multi-hop reachability assumption."

This is the right epistemic grade: the lemma is a *structural* claim, not a quantitative one. The "structural Coupled-class claim is robust without the in-context-learning correspondence" disclaimer at line 120 is the right move — it splits the lemma's scope from the bias-bound application's scope.

One thing I'd add: under non-degenerate attention, the *attention weights* are typically learned and can be arbitrarily small in practice. A reviewer could ask "does the lemma cover the case where attention from the goal position is ~0 in practice?" The honest answer is "the structural reachability holds regardless of weight magnitude; the *quantitative* coupling is what $\kappa_{\text{processing}}$ measures." This is implicit in the existing caveats but worth one explicit sentence.

---

## §2 — Argument strength / overclaim risk

### A1 — "Universal, dimension-free, no domain-specific parameters" — propagate the (H4$'$) qualifier

See M1. The intro line 15 / contributions line 33 / conclusion all describe Track 2's $\sqrt 2$ as "universal, dimension-free, no domain-specific parameters." It is — *under (H4$'$)*. For the LLM regime where the architectural reading lives, (H4$'$) likely fails for adversarial / rare goals. The headline phrasing should carry the qualifier or front-load the global $\pi/\sqrt 2$ alternative. Strengthening rather than softening.

### A2 — "Plain decoder-only transformer attention is *Class 3 (Coupled) by construction*"

*Primary location:* `src/re/01-introduction.md:24–25`.

This is a strong, clean claim. The lemma proves it. ✓ One slight overclaim risk in the surrounding text:

> […] every internal computation has a directed-graph path from any input position whenever attention weights are non-degenerate […], by induction on layer depth, robust to RMSNorm / FlashAttention / causal masking / sliding-window.

The "whenever attention weights are non-degenerate" qualifier is in there but quiet. A reviewer skimming the intro might miss it. Consider one explicit sentence: "The structural classification holds at the architectural level — what attention *can* do; the *quantitative* coupling magnitude $\kappa_{\text{processing}}$ requires additional assumptions and is empirically estimated, not analytically derived." That's already in the body but the intro could carry it once.

### A3 — "Composes two literatures that hadn't met" — strong but defensible

*Primary location:* `src/re/01-introduction.md:11`; `src/re/02-related-work.md:9`; `src/re/06-conclusion.md:5`.

The composition claim is real: hallucination-frequency lineage and Bayesian inverse-problems posterior-stability lineage hadn't been bridged before this paper. The bridge is the chain-rule move on the post-update law. Defensible.

The risk: a reviewer in *Bayesian sensitivity analysis* (Strand 3 in the extended related work) might say "Kurtek-Bharath 2015 already used Fisher-Rao for Bayesian sensitivity." The extended related work distinguishes ("Same geometric machinery; different target") but the cite-and-distinguish there is one sentence. Worth a touch more space — Kurtek-Bharath is the closest single existing Fisher-Rao deployment to Track 2.

### A4 — Architectural corollary's "headline factorization"

*Primary location:* `src/re/04-main-results.md:75` ("The factorization is the contribution-headline").

The factorization $C \sqrt{\kappa^* \cdot I(G; \Omega | e, M)}$ requires (H$_\kappa$). The unconditional theorem (Theorem 1) bounds $C \sqrt{I(G; M_+ | e, M)}$ directly, and the substitution $I(G; M_+ | e, M) \leq \kappa^* I(G; \Omega | e, M)$ is what (H$_\kappa$) provides. The "factorization is the contribution-headline" framing slightly overpromises — the unconditional theorem is the actual mathematical content; the factorization is its operational interpretation under one additional commitment.

The body text does this honestly: "The unconditional theorem [[#^thm-umbrella]] is the structural backbone whose math holds without (H$_\kappa$); the corollary is the operational reading." ✓ But "contribution-headline" as a framing leans toward the corollary. Pick one — either the corollary is the headline (and (H$_\kappa$) is part of the headline assumption set), or the unconditional theorem is the headline (and the corollary is a useful operational reading under one additional commitment).

### A5 — The "not in the Stuart school" framing

The paper contrasts its bound with Stuart's lineage and notes that Track 1 *recovers* Stuart's cascade as a special case. The "the composition contains the existing Bayesian-inverse-problems lineage as a strict sub-case" claim (`01-introduction.md:17`; `04-main-results.md:30`) is strong. Verifying this requires showing Stuart's exact cascade form is a specialization of Track 1's framework — the conjugate-Gaussian numerics segment shows this explicitly for one example. For the general claim ("strict sub-case under standard log-Sobolev concentration"), the reduction is more sketched than proved. Worth either an explicit reduction lemma or a softer "recovers in the conjugate-Gaussian Class-1 case (extended in [[#^sec-strand2]])."

### A6 — "the bias quantity captures *one channel* of hallucination"

*Primary location:* `src/re/06-conclusion.md:3, 7`.

> A coupled-architecture model in (PI)-compatible operating regime can simultaneously have an inevitable-frequency hallucination floor [...] *and* a bounded-magnitude goal-coupling displacement on each event (geometric structure). The two together give a more complete picture than either alone.

This is a good framing: the paper is *complementary* to the frequency lineage, not a substitute. The "one channel of hallucination" qualifier in the limitations section is the right scope-naming. ✓

### A7 — "Empirically accessible" attention — load-bearing claim deferred

*Primary location:* `src/re/03-setup.md:82` ("The realized $\kappa_{\text{processing}}$ is empirically accessible. A behavioral two-goal probe — run the architecture on a fixed event set under two goal states […]. Both are out of scope for the present theory paper.").

The architectural-corollary form is operational *given* a $\kappa^*$ bound. The paper says this is "empirically accessible" via two-goal probes or activation-level mediation. But these are out of scope. So a reviewer can ask: "is the bound deployable?" Answer in the paper: in principle yes, via methods we don't analyze.

This is honest scope-naming but the practical-deployability question deserves one paragraph in the conclusion's Future Directions, beyond the existing one-liner. Worth: "First instantiation of $\kappa_{\text{processing}}$ via a two-goal probe on a deployed LLM (in any single domain) would convert the theoretical bound into an operational one, and is the most natural follow-up."

### A8 — "$\pi/\sqrt 2$ overhead is a *geometric maximum*, not a slack"

*Primary location:* `src/re/05-mechanism.md:39`; `src/re/D-track2-companions.md:19`.

This is the right framing — the $\pi/\sqrt 2$ constant is *exact* at the antipode, not a slop in the proof. Reframing it as "geometric maximum" rather than "constant overhead" honors the structure. ✓ Nothing to fix; flagged as good.

---

## §3 — Prose / structure

### S1 — Intro is dense (37 lines)

Threads two literatures, derives the bound, names tracks, names architectural corollary, derives lemma reference, names contributions. Heavy. Two structural moves that would help:

- **Cut paragraph 1's enumeration of hallucination-theory citations** down. Currently five cited works are named in one paragraph (Kalai-2023, Kalai-2025, Karbasi-2025, Wu-Grama-2024, Suzuki-2025). The Strand 1 in the extended related work covers all of them with full attention. Intro paragraph 1 could be: "Recent hallucination theory bounds the *frequency* with which calibrated language models must produce false outputs (refs in §B.1). Hallucination in this lineage is treated as architecture-agnostic." Saves ~3 lines.

- **Cut paragraph 2 similarly** for the Bayesian inverse-problems citation list. Same logic: full citations live in Strand 2; intro can summarize.

### S2 — "Track 1" / "Track 2" / "Track 5.5" / "Track 3 (Hellinger)" — non-monotone numbering

*Primary location:* `src/re/C-conjugate-gaussian-numerics.md:21, 33`.

The numerical-comparison table refers to "Track 5.5 Euclidean" without ever defining a Track 3, 4, or 5. Looks like leftover from an earlier draft where there were more tracks. Either:

- rename to "Track 2 Euclidean translation" (since it's `thm-conjugate-gauss-euclidean`, a Euclidean translation of Track 2);
- or drop the "Track 5.5" naming entirely and call it the "Euclidean translation" — its anchor is `thm-conjugate-gauss-euclidean` which is unambiguous.

Also the same segment refers to "Track 3 — Hellinger backstop" in the heading at line 23, but `D-track2-companions.md:25` calls it just "Hellinger backstop" without a Track number. The table at line 27 then has rows labeled "Track 1 / Track 2 / Track 5.5 Euclidean / Hellinger" — which is *four* labels with an inconsistent track scheme. Pick one numbering and propagate.

The cleanest renaming I can suggest: Track 1 (Talagrand) / Track 2-FR (Fisher-Rao locally-tight) / Track 2-FRG (Fisher-Rao global) / Track 2-Hel (Hellinger) / Track 2-Eucl (Euclidean translation). Then the family becomes "Track 1 transport-inequality, plus the Track 2 family of Fisher-Rao-spine bounds." This restructuring also makes M1's recommendation (front-load the global as part of the headline) easier.

### S3 — The (PI), (R), (K), (H1), (H2$'$), (H4$'$), (H$_\kappa$) namespace

Seven named hypotheses. Each is necessary for some claim but the constellation is heavy. A schematic table early in §3 (axiom name → role) would help readers track which apply to which theorem. Currently the reader has to assemble this from the theorem statements.

### S4 — Setup is ~68 lines and packs a lot

The setup (`03-setup.md`) covers: bias quantity definition, Class 1/2/3 architectural classification, $\kappa_{\text{processing}}$ definition, three axioms (PI/R/K), (H1) statistical-manifold sub-case, attention-coupled lemma. That's ~6 substantive concept introductions in 68 lines. Each is well-organized but the cumulative cognitive load is high. Possible compression:

- Move the (PI)+(R)+(K) axioms to the start of §4 where they're first invoked — they're orthogonal to setup and only matter for Track 2.
- Or: keep them in setup but tag them clearly as "Track 2-only axioms" so a reader who only cares about Track 1 can skip.

### S5 — `\citet` / `\citealt` / `\citep` mixing

*Primary locations:* throughout. `\citealt` appears in proof environments (e.g., `E-proofs.md:14`); `\citet` in body text; `\citep` rare. Probably the build pipeline normalizes these but worth checking against AUTHORING §2.3.

### S6 — `(H2')` vs `(H_2^\prime)` typesetting

*Primary location:* `03-setup.md:35`; `04-main-results.md:16`. The hypothesis name appears as `(H2$'$)` in markdown — the prime is inside math mode. Some uses elsewhere have it outside. Pick one form. Cosmetic.

### S7 — Conclusion's "Future directions" paragraph is dense

*Primary location:* `src/re/06-conclusion.md:9`.

Single 6-sentence paragraph naming five distinct future directions. Each is interesting; the dense list is hard to absorb. Either bullet them or pick the highest-leverage two and expand. A reviewer rewarding "real future-work clarity" would prefer the focused version.

### S8 — `lem-attention-coupled`'s scope qualifiers placement

*Primary location:* `src/re/E-proofs.md:114–120` (three caveats listed after the proof).

The three caveats — graph reachability ≠ causal magnitude, causal masking restricts to downstream, sparse attention needs multi-hop — are exactly the right things to say. Their placement at the end of the appendix proof means a reader of the main text (where the lemma is invoked at `03-setup.md:64`) has to trust the lemma's headline without seeing the caveats. Either move the caveats up to the lemma statement in `03-setup.md`, or carry one summary line: "(Three explicit caveats — magnitude vs. reachability, causal-mask scope, sparse-attention multi-hop — are documented at the proof in [[#^sec-attention-coupled-proof]].)"

---

## §4 — Citation / prior-art notes (loose, training-data-only)

### C1 — Sycophancy / instruction-following bias literature absent

The paper bounds *goal-coupling-induced displacement* in LLMs. There's a substantial empirical literature on LLM *sycophancy* — models adjusting outputs to match user-implied preferences — that is operationally exactly what the paper bounds theoretically. Some keys to consider:

- Sharma et al. *Towards Understanding Sycophancy in Language Models* (2023, Anthropic).
- Perez et al. *Discovering Language Model Behaviors with Model-Written Evaluations* (2022).
- Wei et al. *Simple Synthetic Data Reduces Sycophancy in LLMs* (2023).

These are empirical demonstrations of the bound's quantity; even one citation in the conclusion's "future directions" or in the intro framing would link the theory to its operational referent and defuse a reviewer's "where's the empirical motivation?" pushback.

### C2 — Steering vector / activation-engineering literature for $\kappa$ probes

The paper notes activation-level mediation analyses as one way to estimate $\kappa_{\text{processing}}$ (`03-setup.md:82`). Relevant literature:

- Zou et al. *Representation Engineering* (2023).
- Turner et al. *Activation Addition* / steering vector papers.

Worth a citation when the activation-mediation idea is introduced.

### C3 — Recent transformer interpretability work on attention magnitude

Olsson et al. *In-context Learning and Induction Heads* (Anthropic 2022) and the broader mechanistic interpretability line on attention pattern analysis would be relevant for grounding the lem-attention-coupled framework in empirical attention-pattern observations.

### C4 — Stuart 2010 cascade constant verification

See M7. Per-paper-agent should spot-check that Stuart 2010 §6 (or wherever the cascade lives in the canonical lineage) gives $C = 2 L_{\text{post}}^2 / \rho_{\text{LSI}}$ in the form Track 1 recovers.

### C5 — Cover-Thomas Theorem 2.5.3 cite for chain rule

*Primary location:* `src/re/E-proofs.md:10`. Cover-Thomas Theorem 2.5.3 is the chain rule of relative entropy. ✓

### C6 — Tsybakov Lemma 2.4 cite for $2\mathrm{Hel}^2 \leq \mathrm{KL}$

*Primary location:* `src/re/D-track2-companions.md:17` and `:33`. Tsybakov 2009 Lemma 2.4 gives this inequality. ✓ Standard.

### C7 — Polyanskiy-Wu 2024 / Gray 2011 for abstract-spaces chain rule

*Primary locations:* multiple. Both are appropriate references for the standard-Borel chain rule.

### C8 — Anonymization spot-check

I scanned the segments for AUTHORING §3.5 forbidden categories. Nothing flagged. The bias-bound framing carries no Joseph/Wecker/ASF/ELI references. Run `bin/refs lint 03-llm-hallucinate-bound` for confirmation.

### C9 — Bareinboim 2022 cite usage

The paper invokes Bareinboim 2022 for the causal hierarchy structure (`03-setup.md:25` via the Pearl-blanket). Cleaner than paper 02's heavier use; here it's just an attribution for the Markov-blanket reading. ✓

### C10 — `chlon-2025-predictable` and `zeng-2026-halluguard` framings

*Primary location:* `F-related-work-extended.md:39, 41`.

Both are recent (2026) papers used as adjacent decompositions. The cite-and-distinguish in §F is good (one paragraph each). Worth confirming the cite keys exist in `refs/entries/` via `bin/refs lint`.

---

## §5 — Empirical / experiment-design

The paper is theory-only. The conclusion's limitations explicitly state "we do not instrument a deployed LLM's belief-update dynamics" (`06-conclusion.md:7`). Honest.

The closest empirical anchor is the conjugate-Gaussian numerical comparison (`C-conjugate-gaussian-numerics.md`). It's a worked example, not an experiment — the bound is *evaluated* on a known case to verify the constants align across tracks. Adequate for a theory paper.

For the review's "empirical motivation" question, see C1: the sycophancy literature is the empirical referent for what the bound captures.

---

## §6 — Page-pressure suggestions (if you want to trim)

### P1 — Cut detailed citation enumeration in intro paragraphs 1 and 2 (S1)

Save ~6 lines.

### P2 — Compress "Track 5.5" / Track-numbering inconsistencies (S2)

The renaming itself doesn't save lines but enables compression of the conjugate-Gaussian numerics table by removing redundant explanatory text. ~3 lines.

### P3 — Move (PI)+(R)+(K) axioms out of setup (S4)

Or tag them as "Track 2-only." Saves nothing directly but reduces setup density, allowing other compression.

### P4 — Bullet the conclusion's Future Directions paragraph (S7)

Saves nothing in line count but improves readability. Skip if not bullet-friendly in NeurIPS template.

### P5 — `D-track2-companions.md` is 81 lines

The exponential-family Euclidean generalization (`D-track2-companions.md:65–81`) with worked examples (Bernoulli, multinomial, Gaussian-mean, Gaussian-scale) is detailed. Each example takes 2–3 lines. If page-pressured, the worked examples can compress to a one-line summary: "the natural-parameter chart on simplex / discrete-outcome models gives finite dimension-free bounds; scale-family parameterizations off the natural chart recover the no-go's pathology." Saves ~10 lines.

### P6 — `E-proofs.md` is 120 lines

Contains the chord-arc proof, the Track 1 proof, the Track 2 proof, the no-go proof, the Čencov proof, the attention-coupled proof. Each proof is appropriately concise. The robustness-to-architectural-variants list at the end of the attention proof (`E-proofs.md:108–112`) is itemized — could go to a one-paragraph summary. Saves ~5 lines.

---

## §7 — Minor / nits

### N1 — Greek letter used for both LSI constant and another quantity

*Primary location:* `src/re/C-conjugate-gaussian-numerics.md:13`: "$\rho_{\text{LSI}} := 1/\sigma^2$" introduces $\rho_{\text{LSI}}$ to align with Stuart's notation. The notation $\rho$ is not used elsewhere as far as I can see, so no clash. ✓ Just a heads-up: $\rho$ is heavily used in paper 01 for drift rate, so a consistent-across-papers convention might want $\kappa_{\text{LSI}}$ or similar — though within paper 03 alone it's fine.

### N2 — `\kappa^*` vs `\kappa_{\text{processing}}^*` 

*Primary locations:* `(H_κ)` hypothesis statement uses both. The hypothesis says "$\kappa_{\text{processing}} \le \kappa^* < \infty$" — naming $\kappa^*$ as a separate constant from $\kappa_{\text{processing}}$. Then the corollary statement uses both interchangeably. Minor; ensure consistent.

### N3 — `\citealt` inside `> [!proof]` blocks

*Primary location:* `src/re/E-proofs.md` proof environments. `\citealt` is "citation as part of sentence with no parens." Used several times inside proof callouts. Fine if the build supports it inside theorem-shape callouts; check.

### N4 — `(H4')` — single-quote vs prime

*Primary locations:* the hypothesis name uses `(H2$'$)` in the markdown (prime in math mode) — `4$'$` and `4^\prime` would render the same. Pick one and grep-replace. Cosmetic.

### N5 — In `C-conjugate-gaussian-numerics.md:7`, "$\kappa_{\text{processing}}^{\text{realized}} = 1$"

The notation $\kappa^{\text{realized}}$ vs $\kappa^*$ vs $\kappa_{\text{processing}}$ is a bit much. The "realized" version is the actual measured value; $\kappa^*$ is the bound; $\kappa_{\text{processing}}$ is the random-variable / general quantity. Worth a one-line table near the first introduction.

### N6 — `\succeq` vs `\preceq` vs $\ge$ on PSD matrices

*Primary location:* `src/re/B-hypothesis-verification.md:17` ($\succeq 0$ for likelihood log-concave Hessian). Standard. ✓ Not a finding.

### N7 — `0 \log 0 = 0` convention

*Primary location:* `src/re/05-mechanism.md:8` (proof of `lem-chain-rule`). Standard convention; named explicitly. ✓ Good. Echoes paper 02's identical use.

### N8 — Some equation labels and `^sec-...` anchors

The anchor convention `[[#^lem-...]]`, `[[#^sec-...]]`, `[[#^thm-...]]`, `[[#^eq-...]]` is consistent across the paper. ✓ Build pipeline should resolve all of these — worth running `bin/build` and checking the build log for unresolved anchors.

### N9 — `src/re/05-mechanism.md:8`, "(\citealt[Theorem 3.4]{polyanskiy-wu-2024-info-theory}; \citealt[Theorem 5.4]{gray-2011-entropy})"

The double citation for the chain rule on abstract spaces is good — covers both common reference points. ✓

### N10 — Failed-routes section heading

*Primary location:* `src/re/A-failed-routes.md`. The two failed routes (F1 Cramér-Rao, F2 Rate-distortion) plus the "pattern" recap are well-organized. The "lesson" sentences are exactly what makes negative-results documentation useful. ✓ Flagged as good.

---

## Closing

Two priorities for the per-paper agent before submission:

1. **M1 / A1** (the (H4$'$) vs. global $\pi/\sqrt 2$ relative weight) — propagating the "$\sqrt 2$ in uniform-local; $\pi/\sqrt 2$ globally" framing into the headline statements turns a potential reviewer "you said universal but it requires (H4$'$)" pushback into a "they're upfront about the regime" win. Strengthening rather than softening.

2. **S2** ("Track 5.5" naming inconsistency in the conjugate-Gaussian appendix) — quick fix, prevents a reviewer "what is Track 5.5?" comment from landing.

Beyond those, M2 (notation `\|P, Q\|_{\mathcal M}`) is a 5-minute fix that prevents a reader from pausing at the bias-quantity definition. C1 (sycophancy literature anchor) is a one-citation win that connects the theory to its empirical referent.

The math is solid; the failed-routes documentation and the no-go disambiguation are model practices worth protecting through any compression.

— end audit —
